# Drift Zone v2.9.9

## What's in this release (2025-02-11)

- **BUG FIX:** Retail Value was still overstated after v2.9.7 — when multiple recipe items share the same raw ingredient (e.g. "Indomi Ready" and "Indomi Double" both drawing from the same Indomi stock), each one's full potential was counted separately, overstating what could actually be sold from limited shared stock.
- Retail Value now excludes recipe items **everywhere** — Evaluation tab, Inventory tab, and Excel export — same rule as Cost Value. A recipe item's value is fully represented by its raw ingredients, counted once.
- Inventory tab's Retail Value column shows "—" for recipe items instead of a number, so it's clear they're intentionally excluded rather than showing 0 by mistake.

## ⚠️ Action needed on your end

For this to be accurate, go through your **raw ingredients** (things only ever used inside a recipe, never sold as-is — like loose Indomi packets) and make sure their **Sale Price is set to 0**. If a raw ingredient still has a nonzero sale price left over from before, it'll inflate Retail Value on its own row even with this fix.

## Final mental model (as of this release)

| | Cost Value | Retail Value |
|---|---|---|
| Raw ingredient (no recipe) | ✅ stock × cost | ✅ stock × price *(should be 0 if never sold raw)* |
| Recipe item (e.g. Indomi Ready) | ❌ excluded | ❌ excluded |

Both values now follow the same rule: only items without a recipe count, full stop. No more asymmetry between the two.

## Upload instructions

1. Create `releases/v2.9.9/` in your GitHub repo
2. Add `drift-zone.html` into that folder
3. Commit: `Release v2.9.9 — exclude recipe items from Retail Value everywhere`
