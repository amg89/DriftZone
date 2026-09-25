# Drift Zone v2.9.22

## What's in this release (2025-02-24)

- **NEW: Search box** added to the Snacks Order menu — type to filter items by name, works alongside the existing category filter buttons (All/Snacks/Drinks/Bar/Indomie/etc).
- **BUG FIX (re-applied):** out-of-stock graying in the Snacks menu was broken again — the v2.9.17 rollback also reverted this fix (originally made in the abandoned v2.9.19). Same root cause as before: a `style="..."` attribute was getting smashed as literal text inside the `class` attribute instead of being its own real attribute. Fixed properly this time, verified in the same pass as the search feature.

## Upload instructions

1. Create `releases/v2.9.22/` in your GitHub repo
2. Add `drift-zone.html` into that folder
3. Commit: `Release v2.9.22 — add search to Snacks menu, re-fix out-of-stock graying`
