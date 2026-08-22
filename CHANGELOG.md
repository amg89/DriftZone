# Changelog

All notable changes to Drift Zone are documented here.

| Version | Date | Highlight |
| --- | --- | --- |
| v2.9.25 | 2025-02-27 | **Urgent fix** — persist() now handles storage failures instead of failing silently; added Storage Health diagnostics |
| v2.9.24 | 2025-02-26 | "Hide out of stock" toggle added to Inventory tab |
| v2.9.23 | 2025-02-25 | "Hide out of stock" toggle added to Snacks Order menu |
| v2.9.22 | 2025-02-24 | Search box added to Snacks menu; re-fixed out-of-stock graying |
| v2.9.21 | 2025-02-23 | Re-applied empty-bottle fixes lost in the v2.9.17 rollback |
| v2.9.20 | 2025-02-22 | **Rolled back** Remote Dashboard sync (caused bugs); fixed restore not refreshing all panels |
| v2.9.19 | 2025-02-21 | ⚠️ Abandoned — bundled with the sync feature removed in v2.9.20 |
| v2.9.18 | 2025-02-20 | ⚠️ Abandoned — Remote Dashboard sync, later found to cause UI/checkout bugs |
| v2.9.17 | 2025-02-19 | Fixed empty-bottle tracking on tabs; require open shift for any sale |
| v2.9.16 | 2025-02-18 | Undo Close Shift |
| v2.9.15 | 2025-02-17 | Cash Reconciliation per shift; Item Sales Summary report |
| v2.9.14 | 2025-02-16 | Free-text Device Type; Gaming-by-Device shift breakdown |
| v2.9.13 | 2025-02-15 | Device Type filter in Sessions tab |
| v2.9.12 | 2025-02-14 | Returnable Bottle (empties) tracking |
| v2.9.11 | 2025-02-13 | Fixed Purchase not updating stock for recipe items |
| v2.9.10 | 2025-02-12 | Staff PIN system + Activity Log |
| v2.9.9 | 2025-02-11 | Fixed Retail Value double-counting (final correction) |
| v2.9.8 | 2025-02-10 | Retail Value column added to Inventory tab |
| v2.9.7 | 2025-02-09 | Fixed Retail Value regression from v2.9.6 |
| v2.9.6 | 2025-02-08 | Fixed Stock Evaluation double-counting recipe items |
| v2.9.5 | 2025-02-07 | Fixed restore bug; alarm heads-up + escalation; auto snapshots; backup reminder |
| v2.9.4 | 2025-02-06 | Station Alarm (bundled with v2.9.3's recipe costing) |
| v2.9.3 | 2025-02-05 | Automatic recipe costing — *no standalone file; merged into v2.9.4* |
| v2.9.2 | 2025-02-04 | **Real fix** — Gaming Revenue reflects actual charge (markup + discount) |
| v2.9.1 | 2025-02-03 | First attempt at discount fix (incomplete — see v2.9.2) |
| v2.9.0 | 2025-01-31 | Live tab updates, unpaid/waived tab tracking |
| v2.8.1 | 2025-01-30 | Top items + reorder suggestions |
| v2.8.0 | 2025-01-30 | Inventory Evaluation tab |
| v2.7.2 | 2025-01-29 | Critical hotfix — broken script crash |
| v2.7.1 | 2025-01-29 | Recipe stock calculation fix (⚠ broken, see v2.7.2) |
| v2.7.0 | 2025-01-28 | Client Tabs (running tab per customer) |
| v2.6.0 | 2025-01-27 | Purchases tab, time package editor, factory reset |
| v2.5.1 | 2025-01-26 | Inventory filter, sort, search |
| v2.5.0 | 2025-01-25 | Recipe/ingredient system |
| v2.4.2 | — | Cart unit price ↔ line total sync |
| v2.4.1 | — | Custom price per snack item |
| v2.4.0 | — | PWA install, peak hours heatmap, receipts, shifts |

> **v3.0.0 / v3.1.0 (Firebase multi-branch line): discontinued.** After
> extended work, this branch was set aside to focus on maturing the
> localStorage version instead. **Production runs on v2.9.25** (the
> version at repo root). If cloud/multi-tenant work resumes later, it
> will likely be rebuilt fresh rather than resumed from v3.1.0.

> **⚠️ Do not roll back to v2.9.18 or v2.9.19.** Both contain a Remote
> Dashboard sync feature that caused real bugs (tab items not updating
> without a manual refresh, snack checkout incorrectly reporting an
> empty cart). The feature was fully removed in v2.9.20. Kept in
> `releases/` for historical reference only.

---

## v2.9.25 — 2025-02-27 (urgent)

**Likely root cause found for "needs refresh everywhere" bugs:** `persist()` — the function that saves every change — had no error handling at all. If browser storage was full or failing, a save could break silently partway through, halting whatever screen updates were supposed to run right after it, with zero visible error.

- `persist()` now saves each piece of data independently — one failure no longer blocks the rest
- Real, visible warning now appears if a save fails, instead of silent failure
- **NEW:** Settings → 📊 Storage Health — shows browser storage usage broken down by data type, with a warning bar before things actually fail
- **NEW:** "Clear Old Auto-Snapshots" button — frees space without touching café data
- Daily auto-snapshot retention reduced from 10 days to 5 — halves this feature's storage footprint
- App proactively warns at startup if storage is already critically full

## v2.9.24 — 2025-02-26

- "Hide out of stock" toggle added to the Inventory tab, next to Search and Sort
- Correctly accounts for recipe-based items (uses "can make" quantity)

## v2.9.23 — 2025-02-25

- "Hide out of stock" toggle added to the Snacks Order menu, next to the search box
- Works together with search and category filters

## v2.9.22 — 2025-02-24

- Search box added to the Snacks Order menu — filter items by name
- BUG FIX (re-applied): out-of-stock graying in the Snacks menu was broken again after the v2.9.17 rollback — fixed properly

## v2.9.21 — 2025-02-23

- Re-applied two empty-bottle bug fixes lost when v2.9.20 rebuilt on the v2.9.17 base:
  - Purchase form's "Empties returned" field now stays synced to Quantity as it changes
  - Deleting an open tab now correctly reverses the empty-bottle credit for returnable-bottle items

## v2.9.20 — 2025-02-22

- **Rolled back** Remote Dashboard sync (v2.9.18) — caused tab items not updating without a manual refresh, and snack checkout incorrectly reporting an empty cart. Feature fully removed; this version rebuilds on the confirmed-stable v2.9.17 base.
- BUG FIX: found the actual cause of "restore brings the bug back" — Restore Backup only ever refreshed 6 of the app's 18+ view panels. Now automatically reloads the page after restoring, guaranteeing every panel shows fresh data.

## v2.9.19 — 2025-02-21 ⚠️ Abandoned

- Bundled with the Remote Dashboard sync feature, later identified as the cause of real bugs and fully removed in v2.9.20. Kept for historical reference only — do not use.

## v2.9.18 — 2025-02-20 ⚠️ Abandoned

- Remote Dashboard sync — read-only monitoring of café status from a phone via Firebase. Later found to cause tab/checkout UI bugs and was fully removed in v2.9.20. Kept for historical reference only — do not use.

## v2.9.17 — 2025-02-19

- BUG FIX: adding a returnable-bottle item directly to a client tab did not add an empty to the linked item — fixed for every path (new item, +1 existing, remove)
- NEW: orders, tabs, and sessions can no longer be started or checked out without an open shift
- Closing/extending an already-open session is not blocked, even without a shift open

## v2.9.16 — 2025-02-18

- NEW: Undo Close Shift — same-day closed shifts can be reopened, same pattern as Undo Tab Checkout
- Clears cash reconciliation on undo; blocked if another shift is already open

## v2.9.15 — 2025-02-17

- NEW: Cash Reconciliation per shift — starting float, expected vs actual cash, variance tracking
- NEW: Item Sales Summary in Reports — units sold and revenue per item, sorted by best-sellers

## v2.9.14 — 2025-02-16

- Device Type per station is now free text instead of a fixed dropdown
- NEW: Shift breakdown expands Gaming revenue into a per-device breakdown

## v2.9.13 — 2025-02-15

- NEW: Device Type per station (PS5/PS4/SIM/etc)
- NEW: Device filter in Sessions tab

## v2.9.12 — 2025-02-14

- NEW: Returnable Bottle tracking — link a sellable item to an "empty" item; sales add empties, purchases ask how many were handed back

## v2.9.11 — 2025-02-13

- BUG FIX: logging a Purchase against a recipe-based item silently updated a stock field that's never displayed. Purchase form now only lists non-recipe items.

## v2.9.10 — 2025-02-12

- NEW: Staff PIN system — "Who's working?" sign-in, Owner/Staff accounts, per-staff PINs
- NEW: Activity Log (Owner-only) — records sign-ins, closes, discounts, expenses, staff/inventory changes

## v2.9.9 — 2025-02-11

- BUG FIX: Retail Value now correctly excludes recipe items everywhere (Evaluation, Inventory tab, Excel export), avoiding double-counting when multiple recipe items share a limited raw ingredient

## v2.9.8 — 2025-02-10

- NEW: Retail Value column added to the Inventory tab, with a running total for the current filter

## v2.9.7 — 2025-02-09

- BUG FIX: v2.9.6 excluded recipe items from Retail Value too aggressively, understating revenue potential. Cost Value and Retail Value now correctly use different rules.

## v2.9.6 — 2025-02-08

- BUG FIX: Stock Evaluation was double-counting value — recipe items were valued on top of their raw ingredients, the same physical stock counted multiple times

## v2.9.5 — 2025-02-07

- BUG FIX: Restore-from-backup was silently dropping Shifts, Purchases, and Client Tabs
- Alarm: added heads-up beep at 5 min remaining, separate from the time-up alarm; escalation banner if ignored 5+ minutes
- NEW: Automatic daily snapshots + backup reminder banner

## v2.9.4 — 2025-02-06

- NEW: Station Alarm — audible + visual alert when a timed session expires, repeats until dismissed
- Settings toggle to disable the alarm

## v2.9.3 — 2025-02-05 *(no standalone file — merged into v2.9.4)*

- NEW: Recipe-based items auto-calculate their Cost Price from ingredient costs
- Logging a Purchase cascades cost updates into every recipe item using that ingredient

## v2.9.2 — 2025-02-04

- REAL FIX: Gaming Revenue now shows exactly what you actually charged — e.g. 15 min @ 50/hr with custom amount 15 now correctly shows 15, not the calculated 12.5
- Previous v2.9.1 "discount" fix only handled discounts (charging less) — broke when charging MORE than calculated (markup). Now both directions work correctly.
- Gaming/Snack figures in Shifts, Reports, and Profit are now always the actual amount charged
- Discounts and Markups now shown as separate transparency lines when they occur
- Removed confusing duplicate "Total Revenue" vs "Actual Cash" labels

## v2.9.1 — 2025-02-03

- BUG FIX: Discounts/adjustments no longer silently mixed into Gaming or Snack revenue
- Gaming Revenue and Snack Revenue now always show full, undiscounted values
- New "💵 Actual Cash Collected" figure
- Payment Method breakdown in Shifts now correctly reflects actual cash per method
- 🗂 Tabs: Undo Checkout and Undo Mark Unpaid

## v2.9.0 — 2025-01-31

- BUG FIX: Client Tab card now updates live
- New: "On Credit" payment option, Unpaid Tabs section, Collect Payment, Waive

## v2.8.1 — 2025-01-30

- 🏆 Top Items — Top 5 by Revenue and Units Sold
- 🔄 Reorder Suggestions based on usage rate

## v2.8.0 — 2025-01-30

- 💎 Inventory Evaluation tab — Stock Value Summary, Sales Performance, Stock Health

## v2.7.2 — 2025-01-29

- 🔴 CRITICAL HOTFIX: fixed broken JavaScript causing the entire app to fail to load

## v2.7.1 — 2025-01-29

- BUG FIX: Recipe items no longer blocked by own stock = 0

## v2.7.0 — 2025-01-28

- 🗂 Client Tabs — running tab per customer

## v2.6.0 — 2025-01-27

- 🛒 Purchases tab, time package editor, factory reset

## v2.5.1 — 2025-01-26

- Inventory filter, sort, search

## v2.5.0 — 2025-01-25

- Recipe/ingredient system

## v2.4.2 — 2025-01-24

- Cart unit price ↔ line total sync

## v2.4.1 — 2025-01-23

- Custom sale price per item in cart, Indomie category added

## v2.4.0 — 2025-01-22

- PWA install, Peak Hours Heatmap, Print Receipt, Shift Management, Low Stock Badge

## v2.3.1 — 2025-01-21

- BUG FIX: date/time handling around midnight, session modal, payment method display

## v2.3.0 — 2025-01-20

- BUG FIX: open package duplication, theme switcher on desktop Chrome
- Filter bars added across Orders, Sessions, Expenses, Profit tabs

## v2.2.0 — 2025-01-15

- Time package shown in Close Session popup, payment methods, custom/daily/weekly/monthly reports

## v2.1.0 — 2025-01-01

- Extend Time, Adjusted Amount override, theme switcher, renamed to Drift Zone

## v2.0.0 — 2024-12-15

- Backup & Restore (JSON), Excel import/export, Profit Overview, Time Packages

## v1.0.0 — 2024-11-01

- Initial release
