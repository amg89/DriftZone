# Drift Zone v2.9.25

## What's in this release (2025-02-27) — urgent

### Likely root cause found for the "needs refresh everywhere" bugs

`persist()` — the function that saves every single change in the app — had **no error handling at all**. If browser storage was full or failing on that PC, a save could break silently partway through, halting whatever screen updates were supposed to happen right after it, with zero visible error. This matches every symptom you described: stale UI across nearly every tab, and a checkout that appeared to fail but had actually already gone through.

### What changed

- `persist()` now saves each piece of data independently — one failure no longer blocks the rest from saving.
- A **real, visible warning** now appears if a save fails, instead of failing silently.
- **NEW: Settings → 📊 Storage Health** — shows exactly how much browser storage is used, broken down by data type, with a warning bar before things actually start failing.
- **NEW: "Clear Old Auto-Snapshots" button** — frees up space immediately. Your actual café data (sessions, inventory, staff, etc.) is completely untouched by this.
- Daily auto-snapshot retention reduced from 10 days to 5 — this feature alone was likely a real contributor to filling up storage over months of daily use.
- The app now proactively warns at startup if storage is already critically full, instead of only surfacing the problem if you happen to open Settings.

## What to do on the affected PC

1. Update to this version
2. Open **Settings → Storage Health** and check the usage bar
3. If it's high, tap **"Clear Old Auto-Snapshots"**
4. Download a fresh manual backup while you're in there, for good measure
5. Test the actions that were breaking (tab items, snack checkout)

If storage does turn out to have been the cause, this should resolve it going forward — and now you'll get a clear warning before it becomes a problem again, on any PC.

## Upload instructions

1. Create `releases/v2.9.25/` in your GitHub repo
2. Add `drift-zone.html` into that folder
3. Commit: `Release v2.9.25 — harden persist() against storage failures, add Storage Health diagnostics`
