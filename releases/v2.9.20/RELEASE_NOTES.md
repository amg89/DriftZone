# Drift Zone v2.9.20

## What's in this release (2025-02-22)

### Rolled back: Remote Dashboard sync
The Firebase remote dashboard sync feature (added in v2.9.18) caused real problems — tab items not updating without a manual refresh, and snack checkout incorrectly saying the cart was empty. **That entire feature has been fully removed.** This version is built directly on the confirmed-stable v2.9.17 base — zero Firebase or sync code remains anywhere in the file (verified).

### Bug fix — the actual "restore brings the bug back" cause
Found it: **Restore Backup only ever refreshed 6 of the app's 18+ view panels** (Sessions, Expenses, Inventory, Report, Orders, Stations). Everything else — Shifts, Tabs, Purchases, Evaluation, Staff, Activity Log, low-stock badge — stayed stale until a manual page refresh. This is a separate, older bug that happened to look exactly like the sync issue, which is why restoring seemed to "bring the bug back" even on a clean version.

**Fixed properly:** Restore Backup and Restore Auto-Snapshot now automatically reload the page right after restoring. This guarantees every single panel shows fresh data — the same reliable path as a normal app launch — instead of relying on a manually-maintained list of refresh calls (which is exactly how this bug happened, and would keep happening as more panels get added).

## What to do

1. Use this version (v2.9.20) going forward — do not use v2.9.18 or v2.9.19, both contain the sync bug
2. Your data is untouched by any of this — the bug was in *rendering*, not in your actual saved data
3. Test a restore once to confirm: the app will show a "Restored — reloading…" toast and refresh itself automatically

## Upload instructions

1. Create `releases/v2.9.20/` in your GitHub repo
2. Add `drift-zone.html` into that folder
3. Commit: `Release v2.9.20 — remove Firebase sync (caused bugs), fix restore not refreshing all panels`
