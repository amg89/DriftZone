# Drift Zone v2.9.21

## What's in this release (2025-02-23)

Good catch asking about this — rolling back to v2.9.17 in the last release also silently undid two empty-bottle bug fixes that had been made in v2.9.19 (the version abandoned along with the sync feature). Re-applied both here:

- **BUG FIX:** Purchase form's "Empties returned" field only matched Quantity at the moment an item was selected — changing Quantity afterward (e.g. to 24 for a crate) never updated it, silently recording the wrong empties count on nearly every purchase.
- **BUG FIX:** Deleting an open tab returned items to stock but did not reverse the empty-bottle credit for returnable-bottle items, inflating empty counts.

Also verified (not just assumed) that every other empty-bottle hook point is intact: checkout, tab quantity +/-, adding new items to a tab, and removing individual tab items. This version has been checked against every empty-bottle bug found so far.

## Upload instructions

1. Create `releases/v2.9.21/` in your GitHub repo
2. Add `drift-zone.html` into that folder
3. Commit: `Release v2.9.21 — re-apply empty bottle fixes lost in the v2.9.17 rollback`
