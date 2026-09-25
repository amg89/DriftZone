# Drift Zone v2.9.18

## What's in this release (2025-02-20)

### NEW: Remote Dashboard (read-only monitoring from your phone)

- Settings → 📡 Remote Dashboard: enable, connect a free Firebase project (Firestore only — no billing plan needed), and set an Access Code that protects it.
- The main app stays 100% localStorage, exactly as before — this only **adds** a small one-way sync (local → cloud) that fires at key moments (session open/close, checkout, shift open/close) plus every 90 seconds as a safety net while the app is open.
- **`dashboard.html`** — a separate, mobile-friendly page. Open it on your phone, enter the same API Key / Project ID / Access Code once (remembered after that), and it updates live: today's revenue, shift status, active stations with time remaining, low stock, and the last shift's cash reconciliation result.
- **View-only by design** — there is no way to take any action from the dashboard page. It cannot open a session, edit stock, or touch anything in the café.

### Important — read before setting this up

- This is **not** the full cloud migration discussed separately. It's a lightweight monitoring add-on. Full remote *operation* (opening sessions, managing staff from anywhere) is still the bigger Firebase migration for later.
- **Setup you need to do:**
  1. Create a free Firebase project at console.firebase.google.com (Spark/free plan, no billing needed — Firestore only)
  2. In the Firebase Console → Firestore Database → create a database
  3. Firestore → Rules tab → paste the contents of `firestore-dashboard.rules` → Publish
  4. In Drift Zone → Settings → Remote Dashboard: paste your Firebase Web API Key and Project ID (found in Firebase Console → Project Settings), generate an Access Code, save, then hit "Test Connection & Sync Now"
  5. Open `dashboard.html` on your phone (host it anywhere — GitHub Pages, or just email yourself the file and open it in a mobile browser), enter the same three values

### Security note (read this)

There's no login on the dashboard — the **Access Code is the security**. It's used as the Firestore document ID, so treat it like a password: use the "🎲 Generate" button for a long random one, and don't share it publicly. Anyone with that exact code can read your café's live status (not edit anything, per the rules provided).

## Upload instructions

1. Create `releases/v2.9.18/` in your GitHub repo
2. Add `drift-zone.html`, `dashboard.html`, and `firestore-dashboard.rules` into that folder
3. Commit: `Release v2.9.18 — add read-only remote dashboard monitoring`
