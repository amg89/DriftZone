# Drift Zone v2.9.16

## What's in this release (2025-02-18)

- **NEW: Undo Close Shift** — same-day closed shifts now have an "↩ Undo Close" button in shift history, reopening the shift. Same pattern as the existing Undo Tab Checkout.
- Undoing a close clears its cash reconciliation (expected/actual/variance) — you'll need to re-count and re-close when actually finishing the shift.
- Undo is blocked if another shift is currently open (only one active shift allowed at a time) — shows a hint explaining why instead of just silently hiding the button.

## Upload instructions

1. Create `releases/v2.9.16/` in your GitHub repo
2. Add `drift-zone.html` into that folder
3. Commit: `Release v2.9.16 — add Undo Close Shift`
