# Drift Zone v2.9.26

## What's in this release (2025-02-28)

### 1. Receipts for Snacks & Tabs
- **NEW:** Print receipt for standalone Snack orders and Tab checkouts — same clean receipt style as sessions
- Available from the Orders tab — a 🖨 button now sits next to each order/tab entry

### 2. Move Session Between Stations
- **NEW:** A "🔀 MOVE" button appears alongside Extend on busy station cards (hover to reveal, same as Extend)
- Tapping it shows a list of currently-free stations to move the session to
- Elapsed time, player name, and snacks all carry over unchanged
- **Original hourly rate is kept for the whole session** — no split-billing across two rates. If a rare case needs correcting, use the existing Adjustment field at close time
- Device type shown/logged for the session automatically follows the new station
- Every move is logged to the Activity Log

## Upload instructions

1. Create `releases/v2.9.26/` in your GitHub repo
2. Add `drift-zone.html` into that folder (and update the root `drift-zone.html` too)
3. Commit: `Release v2.9.26 — add receipts for snacks/tabs, move session between stations`
