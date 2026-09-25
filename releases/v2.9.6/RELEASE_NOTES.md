# Drift Zone v2.9.6

## What's in this release (2025-02-08)

- **BUG FIX:** Stock Evaluation was double-counting value — recipe-based items (e.g. "Indomi Ready", "Indomi Double") were valued on top of the raw ingredient ("Indomi") they're made from, so the same physical stock got counted twice (or more, once per recipe variant sharing that ingredient).
- Cost Value / Retail Value / By-Category breakdown now only count items **without** a recipe — a recipe item's value already lives in its ingredients, which are counted once.
- Added a clarifying note in the Evaluation tab showing how many recipe-based items are excluded and why, so this doesn't look like items are missing.
- Excel export (Stock Value sheet) fixed to match — recipe items are still listed for reference (with their "can make" quantity) but show 0 in the value columns instead of inflating the total.

## Why this happened

The Stock Evaluation summed **every** inventory item's `quantity × cost`, including recipe items — but a recipe item's stock is never really "its own," it's just a computed view of the raw ingredient(s) it draws from (effectiveStock = how many can be made from what's left). Since the raw ingredient was *also* being counted in the same total, every recipe variant built from it added its value again on top.

## Upload instructions

1. Create `releases/v2.9.6/` in your GitHub repo
2. Add `drift-zone.html` into that folder
3. Commit: `Release v2.9.6 — fix stock evaluation double-counting recipe items`
