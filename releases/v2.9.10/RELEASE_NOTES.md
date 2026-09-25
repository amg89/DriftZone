# Drift Zone v2.9.10

## What's in this release (2025-02-12)

- **NEW: Staff PIN system** — the app now asks "Who's working?" every time it's opened. First run walks you through creating an Owner account (name + 4-digit PIN). The Owner can then add Staff accounts from Settings → Staff & PINs, each with their own PIN.
- **NEW: Activity Log** (Settings, Owner-only) — records sign-ins/sign-outs, session closes, discounts/markups given, expenses added, and staff/inventory changes. Shows the last 100 entries.
- Session closes, manually-added expenses, and discounts/markups now record **which staff member** performed them.
- Tap the staff badge in the header (👤 Name) anytime to switch users without losing your place in the app.

## Important — read this before relying on it

This is **local-only accountability, not real security**. Anyone with basic browser DevTools access could bypass a PIN check or edit the activity log directly in localStorage. The real value here is:
- Knowing *who* closed a session, gave a discount, or logged an expense — for your own tracking and peace of mind
- Light deterrence against casual staff misuse

It is **not** a defense against a determined bad actor, and it does **not** prevent someone from technically doing anything in the app — PINs only gate the *sign-in* step, not every individual action.

## What's NOT in this release (known gaps, intentional for now)

- PIN does not gate individual actions (e.g. a signed-in Staff member can still open Settings) — only the initial "who's working" sign-in is PIN-protected
- No PIN attempt lockout/rate-limiting (not meaningful to add given it's easily bypassed via DevTools anyway)
- Activity Log is visible to Owner only, with no export/filter yet — worth adding later if it becomes genuinely useful day to day

## Upload instructions

1. Create `releases/v2.9.10/` in your GitHub repo
2. Add `drift-zone.html` into that folder
3. Commit: `Release v2.9.10 — add Staff PIN system + Activity Log`
