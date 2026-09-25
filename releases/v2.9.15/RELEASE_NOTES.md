# Drift Zone v2.9.15

## What's in this release (2025-02-17)

### 1. Cash Reconciliation per Shift
- **Open Shift** now asks for a **Starting Cash Float** (cash already in the drawer before the shift begins).
- **Close Shift** shows Expected Cash (float + cash sales this shift) and asks you to count the drawer and enter **Actual Cash Counted**.
- Shows the variance immediately — matched exactly, short, or over — with a toast on close and a badge in shift history.
- Shift history detail expands into a full reconciliation breakdown: Starting Float → + Cash Sales → = Expected → Actual Counted → Variance.
- Shifts closed before this update show "No cash count recorded" rather than a broken number — old data isn't touched.

### 2. Item Sales Summary (Reports)
- New table in the Reports tab: **units sold** and **revenue** per item, sorted by units sold (best-sellers first), aggregated across standalone snack orders, session-attached snacks, and closed tabs.
- Added as its own sheet ("Item Sales") in the Excel export.

## Upload instructions

1. Create `releases/v2.9.15/` in your GitHub repo
2. Add `drift-zone.html` into that folder
3. Commit: `Release v2.9.15 — cash reconciliation + item sales report`
