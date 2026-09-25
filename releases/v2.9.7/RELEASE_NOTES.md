# Drift Zone v2.9.7

## What's in this release (2025-02-09)

- **BUG FIX:** v2.9.6 fixed Cost Value double-counting but went too far and also excluded recipe items from Retail Value — understating revenue potential, since dishes like "Indomi Ready" are the actual sellable menu items.
- Cost Value and Retail Value now correctly use **different** rules:
  - **Cost Value** excludes recipe items — that capital is already counted via the raw ingredients
  - **Retail Value** includes recipe items — they're what's actually sold, at their actual price
- Added a note explaining that Retail Value shows each recipe item's full potential *separately* — if two dishes share a limited ingredient (e.g. both draw from the same Indomi stock), you can't realize both totals from the same shared stock at once. This is a known, documented limitation rather than a bug — a true "max realizable revenue" calculation would need constraint-solving across shared ingredients, which is more complexity than this figure needs to earn its keep.
- Excel export Stock Value sheet updated to match.

## Quick mental model going forward

| | Cost Value | Retail Value |
|---|---|---|
| Non-recipe item (raw ingredient) | ✅ stock × cost | stock × price (usually 0 if never sold raw) |
| Recipe item (sellable dish) | ❌ excluded (already counted above) | ✅ effectiveStock × price |

## Upload instructions

1. Create `releases/v2.9.7/` in your GitHub repo
2. Add `drift-zone.html` into that folder
3. Commit: `Release v2.9.7 — fix retail value regression from v2.9.6`
