# Drift Zone v2.9.4

## What's in this release

### v2.9.4 — Station Alarm (2025-02-06)
- **NEW:** Station alarm — plays an audible beep + shows a flashing "TIME UP" button when a timed session (15 min / 1 hour / etc package) runs out, so staff notice even without watching the screen
- Alarm repeats every 15 seconds until dismissed, the session is extended, or it's closed out — tap the red button on the station card to silence it
- New Settings toggle: "🔔 Alarm when station time runs out" — ON by default, can be turned off per café preference
- No external sound file needed — alarm is generated in-browser (Web Audio), keeping the app a single self-contained file

### v2.9.3 — Automatic Recipe Costing (2025-02-05)
*(bundled into this same release — see note below)*
- Recipe-based items now auto-calculate their Cost Price from ingredient costs — no more manually re-typing cup-level cost every time a drink's recipe changes
- Cost Price field locks and shows "🧮 auto from recipe" whenever an item has recipe ingredients — recalculates live as you edit the recipe
- Logging a Purchase (which updates an ingredient's cost) now automatically cascades into every recipe item that uses it
- Extra costs like cups/lids/sugar can be added as their own recipe ingredient — no separate manual cost concept needed

> **Note:** v2.9.3 and v2.9.4 were built back-to-back in the same working
> session without a separate saved snapshot in between, so there is no
> standalone `releases/v2.9.3/` folder — this release folder represents
> both sets of changes on top of v2.9.2. Going forward, each version will
> get its own snapshot folder as requested.

## Upload instructions

1. In your GitHub repo, create the folder `releases/v2.9.4/`
2. Add `drift-zone.html` (in this same delivery) into that folder
3. Commit with a message like `Release v2.9.4 — Station alarm + auto recipe costing`

Full in-app changelog is also visible directly in the app under the 📝 Log tab.
