# Drift Zone v2.9.19

## What's in this release (2025-02-21)

### Bug fix — Snacks Order menu graying
Out-of-stock items in the Snacks Order menu were not actually graying out. The code's intent was right, but the HTML was malformed — a `style="..."` attribute got smashed as literal text inside the `class` attribute instead of being its own attribute, so the browser never applied it. Fixed to build the element the same clean way the Tab menu already did (which was working correctly).

### Bug fix — Empty bottle count drift (the "difference every time" issue)
Found the actual cause: the Purchase form's **"Empties returned"** field only ever matched **Quantity** at the exact moment you selected the item — usually defaulting to 1. If you then changed Quantity afterward (e.g. bumped it to 24 for a full crate), the empties field silently stayed at 1. Every purchase where quantity was adjusted after selecting the item recorded the wrong number of empties handed back — which explains a difference appearing basically every time.

**Fixed:** the empties field now stays in sync with Quantity as you type. If fewer empties were actually returned than purchased (some broke, some are still in your possession), adjust the empties number manually **after** you've finished setting the final quantity — that order matters now.

### Bug fix — deleting a tab didn't reverse empty-bottle credit
Deleting an entire open tab correctly returned items to stock, but for returnable-bottle items it never reversed the empty-bottle count that was added when those items were sold onto the tab — inflating your empties total. Now correctly reversed, matching the fix already in place for removing individual tab items.

## What to do next
Your empty-bottle counts have likely drifted from these bugs. Worth doing a physical recount and manually correcting the "Empty [X] Bottles" item's stock in Inventory once, as a fresh baseline — going forward it should track accurately.

## Upload instructions

1. Create `releases/v2.9.19/` in your GitHub repo
2. Add `drift-zone.html` into that folder
3. Commit: `Release v2.9.19 — fix menu graying + empty bottle count drift`
