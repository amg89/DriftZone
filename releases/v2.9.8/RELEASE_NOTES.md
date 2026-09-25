# Drift Zone v2.9.8

## What's in this release (2025-02-10)

- **NEW:** Retail Value column added to the Inventory tab — shows `qty × price` per item, using the same rule as the Evaluation tab: recipe items use their "can make" quantity (effectiveStock), so a dish's retail value reflects real sellable potential, not a meaningless number on an item with zero stock of its own.
- The Inventory tab now also shows a running **Retail Value total** for whatever's currently filtered/searched, right above the table — so filtering to just "Drinks" or searching "Indomi" gives you a relevant subtotal, not just the grand total.

## Upload instructions

1. Create `releases/v2.9.8/` in your GitHub repo
2. Add `drift-zone.html` into that folder
3. Commit: `Release v2.9.8 — add Retail Value to Inventory tab`
