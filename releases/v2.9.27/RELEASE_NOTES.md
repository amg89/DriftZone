# Drift Zone v2.9.27

## What's in this release (2025-03-01)

### 1. Shift label on Sessions & Orders history
- Every closed session and every order (standalone, session-attached, or from a tab) now shows a **🕐 [Staff Name]** badge indicating which shift it happened during.
- Works **retroactively** on all your existing history — no data migration, since it's computed from timestamps you already have, using the exact same shift-matching logic already used for cash reconciliation.
- Entries that happened with no shift open show a clear **"No shift"** badge instead of silently leaving it blank.

### 2. Hide Out of Stock in Tabs
- The item-adding menu inside a client tab now has the same **"Hide out of stock"** toggle already in the Snacks Order menu and Inventory tab.

## Upload instructions

1. Create `releases/v2.9.27/` in your GitHub repo
2. Add `drift-zone.html` into that folder (and update root `drift-zone.html`)
3. Commit: `Release v2.9.27 — add shift label to history, Hide Out of Stock in Tabs`
