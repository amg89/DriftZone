# Drift Zone v2.9.17

## What's in this release (2025-02-19)

### Bug fix — empty bottles not counted on tabs
Adding a returnable-bottle item (e.g. Cola) directly to a client tab didn't add an empty to the linked item — only the main cart checkout and the tab quantity +/- buttons were wired up. Now covered everywhere:
- Adding a brand new item to a tab
- Tapping +1 on an item already on a tab
- Removing an item from a tab (correctly reverses the empty too)

### New — shift required before any sale
Orders, tabs, and sessions can no longer be started or checked out without an open shift:
- Starting a new gaming session
- Checking out the cart (walk-in snack/drink sale)
- Opening a new client tab
- Adding an item to a tab
- Checking out a tab

If no shift is open, you'll get a clear warning pointing to the Shifts tab instead of the action silently succeeding with no shift to attribute it to.

**Not blocked:** closing or extending a session that's *already* open — so nobody gets stuck unable to close out a station just because shift bookkeeping fell out of sync.

## Upload instructions

1. Create `releases/v2.9.17/` in your GitHub repo
2. Add `drift-zone.html` into that folder
3. Commit: `Release v2.9.17 — fix empty bottle tracking on tabs, require open shift for sales`
