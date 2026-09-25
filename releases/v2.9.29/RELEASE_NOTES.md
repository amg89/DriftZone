# Drift Zone v2.9.29

## What's in this release (2025-03-03)

### Bug fix — deleted orders never restored stock
Confirmed and fixed: `delOrder()` only ever removed the order record — it never restored the stock that `checkout()` deducted when the order was placed. This affected **every** deleted standalone snack order, regardless of payment method (VodafoneCash just happened to be the one that surfaced it — Cash and Instapay orders had the exact same problem).

- Deleting a standalone order now correctly returns stock — raw stock for plain items, ingredients for recipe items
- Also reverses any empty-bottle credit for returnable-bottle items (e.g. Cola), consistent with the fixes already made for tabs
- **Tab-checkout orders are deliberately left alone** by this fix — their stock is handled at add-to-tab time, not at checkout, and "↩ Undo Checkout" is already the correct tool for reversing those. Restoring stock here too would double it up incorrectly.
- Order deletions are now logged to the Activity Log

## Upload instructions

1. Create `releases/v2.9.29/` in your GitHub repo
2. Add `drift-zone.html` into that folder (and update root `drift-zone.html`)
3. Commit: `Release v2.9.29 — fix deleted orders not restoring stock`
