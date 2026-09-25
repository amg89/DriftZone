# Drift Zone Cloud — Data Model v2 (Phase 1 Foundation)

Reflects the FULL feature set of the current local app (v2.9.29), not the
earlier, simpler design from months ago. Built for Firestore, free
(Spark) plan compatible — no Cloud Functions required, same
document-lookup-based security pattern as before.

## Collections

```
/tenants/{tenantId}
  name, status ('trial'|'active'|'suspended'), createdBy, createdAt, trialEndsAt

/branches/{branchId}
  tenantId, name, createdAt
  settings: { cafeName, currency, defaultRate, numStations,
              stationNames[], stationRates[], stationTypes[],
              alarmEnabled, timePackages[] }

/users/{uid}
  tenantId, name, role ('superadmin'|'owner'|'manager'|'staff'),
  branchIds[], createdAt
  permissions: { <key>: true|false, ... }   ← NEW — see Permissions section below

/invites/{code}
  tenantId, role, branchIds, used, createdBy, createdAt

/inventory/{itemId}
  tenantId, branchId, name, cat, icon, price, cost, stock, lowAlert,
  recipe[{ingredientId, qty}], linkedEmptyId

/stockMovements/{id}                    ← enables "stock as of any date" — LIVE
  tenantId, branchId, itemId, delta, reason
  ('sale'|'purchase'|'adjustment'), refId (order/tab/purchase/item id), timestamp
  — written via queueStockMovement() into the SAME writeBatch as every
  stock change (checkout, tab add/remove/void, purchase, manual edit in
  the inventory form), so the ledger can never drift from the actual
  stock field. "Stock as of any date" (Inventory tab → 📜 on any item →
  pick a date) is computed as current stock MINUS every movement after
  that date's cutoff — no need to sum from zero.

/sessions/{id}
  tenantId, branchId, shiftId (direct reference — no more time-window
  guessing), station, deviceType, player, rate, mins, game, calcGame,
  snack, total, payment, adjustment, adjustedReason, closedBy, timestamp

/shifts/{id}
  tenantId, branchId, shiftNumber, staff, startTs, endTs,
  startingCash, actualCashCounted, cashVariance

/clientTabs/{id}
  tenantId, branchId, shiftId, name, stationName,
  items{ [itemId]: {name, icon, price, qty} }, total, status
  ('open'|'closed'|'waived'), payment, openTs, closedTs, closedBy, createdBy
  — stock is deducted per item AS IT'S ADDED to the tab (not at close),
  same as the local app; voiding an open tab restores it. Closing a tab
  also writes a mirror /snackOrders doc (isTab:true, tabId) so it shows
  up in order history/reports alongside walk-up orders.

/snackOrders/{id}
  tenantId, branchId, shiftId, items[], total, payment, isTab, date

/purchases/{id}
  tenantId, branchId, vendor,
  items[{id, name, icon, qty, unitCost, total}], total, date, createdBy
  — recording a purchase increments each item's stock immediately
  (increment(qty), routine "stock"-only write, no special permission
  needed); editing/deleting a saved purchase record afterward is
  manager+-only (opManage), same as expenses.

/expenses/{id}
  tenantId, branchId, desc,
  cat ('rent'|'utilities'|'salaries'|'maintenance'|'supplies'|'marketing'|'other'),
  amount, date, createdBy
  — logging one is open to any branch member (opCreate); editing/
  deleting a saved record is manager+-only (opManage), same as purchases.

/activityLog/{id}                        ← insert-only, same as local version
  tenantId, branchId, uid, actorName, action, detail, timestamp
  — written fire-and-forget (logActivity()) after every real mutation:
  session open/close, shift open/close, inventory add/edit/delete,
  snack checkout, tab open/close/void, purchase, expense, invite
  created, staff permissions changed, settings updated. A logging
  failure never blocks the action it describes. Read access is
  manager+/superadmin only (a role check, not a permission key — see
  firestore.rules), and the app only attempts the read for those roles.
```

## Key improvements over the local (localStorage) version

1. **Real "stock as of any date"** — `stockMovements` is a proper event
   log. Query: sum every movement for an item where `timestamp <= X` to
   get stock as of any historical date. localStorage never could do
   this well; a real database makes it a straightforward query.

2. **Direct shift linkage** — sessions/orders store `shiftId` directly at
   creation time, instead of guessing "which shift was open" from a
   time-window match after the fact (what the local version has to do).
   More reliable, especially around edge cases like overlapping/adjusted
   shift times.

3. **Real permission enforcement** — role checks happen in Firestore
   rules (server-side), not just hidden buttons. A Staff account
   literally cannot write to `/expenses` if rules forbid it — no
   DevTools workaround like the local PIN system.

## Permissions — configurable, not fixed

`role` still exists as a coarse tier — it decides basic structural things
(can this account even create a branch, invite staff, see billing).
But for the day-to-day sensitive actions, **role only sets a starting
default** — the Owner can flip any individual permission for any staff
member, independent of their role. Two Staff accounts can end up with
different permissions if the Owner wants that.

### Permission keys

| Key | What it gates | Default: Staff | Default: Manager |
|---|---|---|---|
| `void_transaction` | Delete/void a session, order, or tab | ❌ | ✅ |
| `apply_discount` | Give a discount/markup on close | ❌ | ✅ |
| `edit_stock` | Restock / adjust stock counts | ✅ | ✅ |
| `edit_prices` | Edit sale price or cost price | ❌ | ✅ |
| `manage_inventory_items` | Add/delete inventory items entirely | ❌ | ✅ |
| `view_reports` | Sales reports beyond their own shift | ❌ | ✅ |
| `view_profit` | Profit/margin figures | ❌ | ❌ |
| `view_evaluation` | Stock valuation (cost/retail value) | ❌ | ❌ |
| `review_cash_recon` | See cash variance details on other shifts | ❌ | ✅ |
| `manage_staff` | Add/edit/remove staff accounts | ❌ | ❌ |
| `edit_settings` | Change business/branch settings | ❌ | ❌ |

`owner` and `superadmin` roles implicitly have every permission — not
worth making those toggleable, since removing them from the Owner's own
account would be self-defeating.

These are **defaults applied at account creation** (when invited via a
role), not hardcoded rules — the Owner can toggle any of them per staff
member afterward from a Staff Management screen. The table above is a
sensible starting point, not a constraint.

### How this gets enforced

Coarse tenant/branch access uses `role` (already in the rules below).
For the specific sensitive actions in the table, Firestore rules check
the individual permission key on the user's own doc — e.g. deleting a
session additionally requires
`myUserDoc().permissions.void_transaction == true` unless the user is
Owner/Manager-by-default-bundle. This is real server-side enforcement,
not a hidden button — a Staff account without `void_transaction` cannot
delete a session even via direct API calls.

## What's NOT decided yet (next conversation)

- Exact permission matrix per role (which of manager/staff can void a
  sale, edit inventory, see the Evaluation report, etc.) — needs your
  input on what's actually sensitive in daily café operation
- Whether the initial migration keeps localStorage as a *fallback* for
  offline café days, or goes fully online-only
- Billing/subscription mechanics for the SaaS side (Phase 4)
