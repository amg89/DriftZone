# Drift Zone v2.9.28

## What's in this release (2025-03-02)

### 1. Shift label on Tab history
Closed and waived tabs now show the same "🕐 Shift Staff" badge already added to Sessions and Orders.

### 2. Shift Number
Every shift now has a permanent, sequential number — Shift #1, #2, #3, and so on.
- Shown in Shift Management, both the current open shift and closed shift history
- Shown in every shift badge across Sessions, Orders, and Tabs history (e.g. "🕐 #12 Ahmed")
- **Existing shifts were automatically numbered** in chronological order when you first open this version — no manual work, no data loss

### 3. Open Shift auto-fills your name
The Staff Name field on Open Shift now pulls automatically from your signed-in account instead of asking you to type it again. If you're opening a shift on behalf of someone else, switch users first via the header badge — the field is read-only to keep shift attribution accurate.

## Upload instructions

1. Create `releases/v2.9.28/` in your GitHub repo
2. Add `drift-zone.html` into that folder (and update root `drift-zone.html`)
3. Commit: `Release v2.9.28 — shift numbers, tab history shift labels, auto-fill staff name`
