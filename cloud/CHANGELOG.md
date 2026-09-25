# Changelog — Cloud App (driftzone-cloud.html + firestore.rules)

Separate from the local app's [`../CHANGELOG.md`](../CHANGELOG.md).
The app and the rules share one version number — **always publish the
matching `firestore.rules`** (Firebase Console → Firestore → Rules →
paste → Publish) when updating the HTML.

| Version | Date | Highlight |
| --- | --- | --- |
| v1.0.1 | 2026-09-25 | **Critical fixes** — queries blocked by rules, staff couldn't close stations/open shifts/join, owner-takeover security hole |
| v1.0.0 | — | Baseline: the unversioned cloud file as of the first review (no changes) |

## v1.0.1 — 2026-09-25

⚠️ **Requires the new `firestore.rules`** — publish it together with the HTML.

### Blocking bugs (app)
- **Every live list/report query now filters on `tenantId`.** The rules check
  `tenantId`, and Firestore rejects any query that doesn't filter on the fields its
  rules check, so stations, shifts, inventory, tabs, purchases, expenses, reports,
  activity log and stock history couldn't load (**● connection issue**).
- **Close Shift cash total** was blocked by the rules, which silently set expected cash
  to 0 and saved a wrong variance. Close Shift now refuses to save until the total has
  actually been calculated.
- **Tabs opened in an earlier shift can now be closed.** The payment is recorded in
  the *current* shift (the shift the tab was opened in is kept as `openShiftId`).
- **Sign-up / join no longer stay stuck on the form** after success. The app opens
  straight away, and the join form no longer jumps to the sign-up form mid-join.
- **New staff can join with an invite code.** The invite was read before sign-in,
  which the rules don't allow.

### Blocking bugs (rules)
- **Staff without `apply_discount` couldn't close any station.** The rule read
  `adjustment`, which new sessions didn't have. The rule now defaults it to 0, and new
  sessions are saved with `adjustment:0`.
- **Staff and default managers couldn't open a shift.** The shift counter bump on the
  branch needed `edit_settings`. Any branch member can now do exactly `+1` on
  `nextShiftNumber` and nothing else.
- **Users can read their own user doc before it exists**, which the sign-up/join
  "already set up?" check needs.

### Security (rules)
- **Owner takeover closed.** A new account could create a user doc as `owner` of *any*
  business, and a branch for any business, using business IDs from the invite list. Now
  only the account that created the business can do that.
- **Invites can only be fetched one at a time by code.** Listing them is limited to that
  business's staff managers. An invite can only be marked used by the person who just
  joined with it.
- **`manage_staff` can change only a person's `permissions`**, never their role,
  business or branches, and can't edit or delete an owner.
- **Inventory permissions now unlock only their own fields:** stock only → anyone;
  price/cost → `edit_prices`; anything else → `manage_inventory_items`. Before, any
  of the three (including `edit_stock`, on for staff by default) allowed editing
  everything. Items can't be moved to another business or branch.
- **`hasPerm()` treats a missing permission key as "no"** instead of throwing an error.

### Security (app)
- **Everything typed by users is escaped before it's shown** (player, item, tab, staff,
  vendor, expense, station names, activity details), closing a script-injection path
  from staff to the owner's screen.

### Correct numbers
- **Close Shift expected cash** now includes cash from snack orders and paid tabs, not
  just sessions. Sessions count in the shift they were **closed** in (new
  `closeShiftId`); sessions closed before v1.0.1 fall back to `shiftId`.
- **Waived tabs are no longer counted as revenue.** They're saved with `total:0` plus
  `waivedAmount`, and reports also ignore waived tabs saved before v1.0.1. They show
  on a separate "Waived tabs (not counted)" line. Their items still count toward COGS,
  because the stock was really used.

### Small
- **Closing a session with a custom amount of 0** is now allowed (a free session).
  An empty box still means "use the calculated price".
- **Closing a session or tab needs an open shift**, so the money always lands in a shift.
- The **`tenant_created` activity entry** now uses a server timestamp, so it sorts
  correctly.
- Version shown in the page title, and as a tooltip on the business name.
