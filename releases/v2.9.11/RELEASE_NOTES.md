# Drift Zone v2.9.11

## What's in this release (2025-02-13)

- **BUG FIX:** Logging a Purchase against a recipe-based item (e.g. "Indomi Ready") silently updated a `stock` field that's never actually displayed — recipe items show "Can Make", calculated from their ingredients, not their own stock. The purchase looked successful (toast + log entry) but the visible number never moved.
- The Purchase form now only lists items **without** a recipe. To restock a recipe item, purchase its raw ingredient instead (e.g. buy more Indomi, not "Indomi Ready").
- Added a safety check for old purchase data that might still reference a recipe item — it's now skipped with a warning instead of silently doing nothing.

## Upload instructions

1. Create `releases/v2.9.11/` in your GitHub repo
2. Add `drift-zone.html` into that folder
3. Commit: `Release v2.9.11 — fix purchase not updating stock for recipe items`
