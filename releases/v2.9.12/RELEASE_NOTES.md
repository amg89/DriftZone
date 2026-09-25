# Drift Zone v2.9.12

## What's in this release (2025-02-14)

- **NEW: Returnable Bottle tracking** — for items like glass Cola bottles where you buy empties once, then exchange them with your supplier for full ones on every restock.
- In the item edit form, a sellable item (e.g. "Cola") can now be linked to a separate "empty" item (e.g. "Empty Cola Bottles") via **🍾 Returnable Bottle → "When sold, add an empty to..."**
- Every sale of a linked item automatically adds 1 to the linked empty item's stock — mirrors what happens physically.
- Logging a **Purchase** against a returnable-bottle item now asks how many empties you handed back to the supplier, and reduces the empty item's stock accordingly. Defaults to match the quantity purchased (the common 1-for-1 swap case), but you can lower it if some bottles broke or were lost.
- Removing/undoing a linked item from a client tab correctly reverses the empty-bottle side effect too.

## How to set it up (Cola example)

1. Create an item **"Empty Cola Bottles"** — no recipe, stock = however many empties you're currently holding (0 if starting fresh)
2. Create/edit your **"Cola"** item — under Returnable Bottle, link it to "Empty Cola Bottles"
3. The **first-ever** empty-bottle purchase (buying the bottles themselves) is a one-time capital cost — log it as an **Expense**, not a Purchase
4. Every supplier visit after that = a normal **Purchase** of Cola — the form will now also ask how many empties you gave back

## Upload instructions

1. Create `releases/v2.9.12/` in your GitHub repo
2. Add `drift-zone.html` into that folder
3. Commit: `Release v2.9.12 — add returnable bottle (empties) tracking`
