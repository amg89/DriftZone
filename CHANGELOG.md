# Changelog

All notable changes to Drift Zone are documented here.

| Version | Date | Highlight |
|---|---|---|
| v2.9.2 | 2025-02-04 | **Real fix** — Gaming Revenue reflects actual charge (markup + discount) |
| v2.9.1 | 2025-02-03 | First attempt at discount fix (incomplete — see v2.9.2) |
| v2.9.0 | 2025-01-31 | Live tab updates, unpaid/waived tab tracking |
| v2.8.1 | 2025-01-30 | Top items + reorder suggestions |
| v2.8.0 | 2025-01-30 | Inventory Evaluation tab |
| v2.7.2 | 2025-01-29 | Critical hotfix — broken script crash |
| v2.7.1 | 2025-01-29 | Recipe stock calculation fix (⚠ broken, see v2.7.2) |
| v2.7.0 | 2025-01-28 | Client Tabs (running tab per customer) |
| v2.6.0 | 2025-01-27 | Purchases tab, time package editor, factory reset |
| v2.5.1 | 2025-01-26 | Inventory filter, sort, search |
| v2.5.0 | 2025-01-25 | Recipe/ingredient system |
| v2.4.2 | — | Cart unit price ↔ line total sync |
| v2.4.1 | — | Custom price per snack item |
| v2.4.0 | — | PWA install, peak hours heatmap, receipts, shifts |

> **Note:** v3.0.0 and v3.1.0 are an experimental Firebase/multi-branch
> line, kept separate and not yet tested in production.
> **Production currently runs on v2.9.2** (this is the version at repo root).

## v2.9.2 — 2025-02-04

- REAL FIX: Gaming Revenue now shows exactly what you actually charged — e.g. 15 min @ 50/hr with custom amount 15 now correctly shows 15, not the calculated 12.5 🆕
- Previous v2.9.1 "discount" fix only handled discounts (charging less) — broke when charging MORE than calculated (markup). Now both directions work correctly. 🆕
- Gaming/Snack figures in Shifts, Reports, and Profit are now always the actual amount charged — no separate math needed to find real cash 🆕
- Discounts and Markups now shown as separate transparency lines when they occur, alongside the actual totals 🆕
- Removed confusing duplicate "Total Revenue" vs "Actual Cash" labels — there is now one true cash figure throughout 🆕

## v2.9.1 — 2025-02-03

- BUG FIX: Discounts/adjustments no longer silently mixed into Gaming or Snack revenue — now shown as a separate "Discounts" line everywhere (Shifts, Reports, Profit) 🆕
- Gaming Revenue and Snack Revenue now always show full, undiscounted values for accurate breakdown 🆕
- New "💵 Actual Cash Collected" figure — what really came in after discounts, separate from gross revenue 🆕
- Payment Method breakdown in Shifts now correctly reflects actual cash per method, unaffected by how a session splits between gaming/snacks 🆕
- 🗂 Tabs: Undo Checkout — reopen an accidentally-closed tab (same-day only), removes the order from revenue, items stay on the tab 🆕
- 🗂 Tabs: Undo Mark Unpaid — reopen a tab accidentally marked as unpaid/on-credit 🆕

## v2.9.0 — 2025-01-31

- BUG FIX: Client Tab card now updates live — adding/removing items, editing line totals, and adjusting amounts instantly reflect on the tab card without switching tabs 🆕
- New: "On Credit" payment option — close a tab as unpaid and track it as a debt 🆕
- New: Unpaid Tabs section — see everyone who owes money with a running total 🆕
- 💰 Collect Payment — pay off an unpaid tab later, counted as revenue on the day collected 🆕
- 🤝 Waive — forgive a debt completely, optionally logged as a "Waived Tab" expense for accurate books 🆕
- Closed tab history shows WAIVED and "collected debt" badges for full traceability 🆕

## v2.8.1 — 2025-01-30

- 🏆 Top Items — Top 5 by Revenue and Top 5 by Units Sold, with medal ranking 🆕
- 🔄 Reorder Suggestions — flags items with ≤3 days of supply left based on usage rate 🆕
- Suggested reorder quantity tops up to ~14 days of supply automatically 🆕
- URGENT badge shown for items with 1 day or less remaining 🆕
- Recipe items show ingredient-level reorder suggestions, not the meal itself 🆕
- Excel export now includes Top Items and Reorder Suggestions sheets 🆕

## v2.8.0 — 2025-01-30

- 💎 New Inventory Evaluation tab 🆕
- Stock Value Summary — total cost value, retail value, potential profit, broken down by category 🆕
- Sales Performance — units sold, revenue, COGS, gross profit, margin % per item over any date range 🆕
- Stock Health — Out of Stock, Low Stock, and Dead Stock (no sales in period) all flagged automatically 🆕
- Same date filters as Reports — Custom, Today, This Week, This Month 🆕
- Recipe items use ingredient-based "Can make" quantity for accurate stock valuation 🆕
- Export full Evaluation to Excel — Stock Value, Sales Performance, Stock Health sheets 🆕

## v2.7.2 — 2025-01-29

- 🔴 CRITICAL HOTFIX: Fixed broken JavaScript that caused the entire app to fail to load (blank tabs, nothing clickable) 🆕
- Root cause: a nested backtick inside a template string broke the script — now fixed and verified 🆕
- Removed accidental duplicated code block in Inventory rendering 🆕
- All previous v2.7.1 features (recipe stock fix) confirmed working

## v2.7.1 — 2025-01-29

- BUG FIX: Recipe items (Indomie Meal, Tea etc.) no longer blocked by own stock = 0 🆕
- Recipe items use ingredient stock to determine availability — "Can make: 45" shown 🆕
- Own stock of recipe items never deducted on sale — only ingredients are deducted 🆕
- Menu shows "Can make: N" for recipe items, "❌ Ingredients low" when unavailable 🆕
- Inventory table shows "🧾 Can make: N" for recipe items instead of own stock 🆕
- +Stock button hidden for recipe items (not needed — stock is ingredient-based)
- Tab remove / delete correctly returns ingredient stock, not own stock
- Tab qty adjust correctly deducts/returns ingredient stock for recipe items

## v2.7.0 — 2025-01-28

- 🗂 Client Tabs — open a running tab per client, add items throughout their visit, checkout at the end 🆕
- Tabs can be linked to a gaming station or standalone 🆕
- Add items to tab from menu, adjust qty, edit line total directly 🆕
- Recipe ingredients auto-deducted when adding to tab 🆕
- Stock returned to inventory if tab is deleted 🆕
- Custom amount + payment method at checkout 🆕
- Closed tabs shown in history with date filter 🆕
- 🛒 Purchase tab: Qty × Unit Cost = Line Total — all three fields editable and synced 🆕
- Tab badge shows count of open client tabs

## v2.6.0 — 2025-01-27

- 🛒 Purchases tab — record vendor purchases, auto-update stock + cost, auto-log as expense 🆕
- Purchase history with vendor filter, item breakdown, previous cost shown 🆕
- ⚙️ Settings — Time Packages editor: add, edit, delete packages with custom labels and durations 🆕
- ☠ Settings — Factory Reset: wipe all data and start from scratch (double-confirm) 🆕
- 📊 Revenue by Category in Reports: Gaming, Indomie, Indomie Double, Ready, Drinks, Bar, etc. 🆕
- 👥 Shift details: Category breakdown + Payment breakdown per closed shift (tap ▸ Details) 🆕
- Clear Sessions now also clears purchases and shifts (inventory kept)

## v2.5.1 — 2025-01-26

- Inventory filter bar — All, Drink, Snack, Bar, Indomie, Double, Ready, Other, ⚠ Low Stock 🆕
- Inventory search — type to filter by name or category instantly 🆕
- Inventory sort — Name, Stock, Price, Margin, Category 🆕
- Indomie Double and Indomie Ready added as separate categories 🆕
- Inventory table shows full category labels (Indomie Double, ⚡ Ready, etc.)
- Item count shown (e.g. "12 of 20 items") when filtering

## v2.5.0 — 2025-01-25

- Recipe system — link ingredients to any sellable item (Tea → Tea Bag ×1 + Paper Cup ×1) 🆕
- Works for Indomie Meal → Indomie Packet ×1 + Cup ×1 + Fork ×1 🆕
- Stock auto-deducts all linked ingredients on every sale (soft mode — warns, never blocks) 🆕
- Recipe shown as a column in inventory table 🆕
- Shift: now includes snack revenue + standalone orders, not just gaming sessions 🆕
- Shift: payment breakdown shows Cash / Vodafone Cash / Instapay with count + total 🆕
- Shift history cards show gaming vs snack split and full payment breakdown 🆕

## v2.4.2 — 2025-01-24

- Removed up/down arrows from all number inputs — type directly 🆕
- Cart: Unit Price and Line Total are both editable and stay in sync 🆕
- Edit unit price → line total recalculates automatically 🆕
- Edit line total → unit price back-calculates (e.g. 2 Indomie for 8 = 4/unit) 🆕
- Grand total updates live as you type without losing focus
- Default price shown as reference when you override

## v2.4.1 — 2025-01-23

- Custom sale price per item in cart — edit the price on any item before confirming order 🆕
- Indomie category added to Snacks, Inventory, and filter bar 🆕
- Custom prices are used in order totals, reports, and session billing
- Cart resets custom prices when cleared or item removed

## v2.4.0 — 2025-01-22

- PWA — install Drift Zone on phone/tablet home screen, works offline 🆕
- Peak Hours Heatmap — see busiest hours and days of the week 🆕
- Print Receipt — formatted customer receipt per session 🆕
- Shift Management — open/close shifts, track revenue per shift 🆕
- Low Stock Badge — inventory tab shows ⚠ count when items are low or out 🆕
- Install banner appears automatically in Chrome when criteria are met

## v2.3.1 — 2025-01-21

- BUG FIX: Date now always reads local device date — no more "yesterday" after midnight 🆕
- BUG FIX: Session start date/time always shows correct local time when modal opens 🆕
- BUG FIX: Payment method in Snacks hidden when attaching order to a station (no duplication) 🆕
- Toast message now correctly says "added to session" vs "via Cash" depending on order type

## v2.3.0 — 2025-01-20

- BUG FIX: Open package no longer duplicated in session modal 🆕
- BUG FIX: Theme switcher now works on Chrome desktop (fixed hover/click detection) 🆕
- Light theme is now the default 🆕
- Payment method added to standalone snack orders 🆕
- Filter bar in Orders tab — Custom, Today, This Week, This Month 🆕
- Filter bar in Sessions tab — Custom, Today, This Week, This Month 🆕
- Filter bar in Expenses tab — Custom, Today, This Week, This Month 🆕
- Filter bar in Profit tab — Custom, Today, This Week, This Month, All Time 🆕
- Bar category added to snack inventory and filter
- Payment method shown in snack order list and session list

## v2.2.0 — 2025-01-15

- Time package shown in Close Session popup — change package at close
- Default time package is Open
- Payment method: Cash, Vodafone Cash, Instapay
- Bar filter in snacks section
- Custom / Daily / Weekly / Monthly reports
- All snack orders shown in reports and Orders tab

## v2.1.0 — 2025-01-01

- Extend Time for active sessions
- Adjusted Amount override with reason
- Dark / Light / Neon theme switcher
- App renamed to Drift Zone

## v2.0.0 — 2024-12-15

- Backup & Restore (JSON)
- Import/Export inventory and expenses as Excel
- Profit Overview tab
- Time Packages
- Timed session countdown

## v1.0.0 — 2024-11-01

- Initial release

