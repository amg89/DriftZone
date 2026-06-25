# Drift Zone — Gaming Café Manager

A single-file web app for running a PlayStation/gaming café: station sessions, snacks & drinks, client tabs, inventory with recipes, expenses, purchases, shifts, and profit reporting.

**Current version: v3.1.0** (Phase 2, Stage 1 — Firebase cloud foundation + per-staff permissions)

---

## 🚀 Quick Start

### Option A — Just open it (no install)
Open `drift-zone.html` directly in any modern browser (Chrome, Safari, Edge). Works immediately.

### Option B — Install as an app (PWA)
1. Download `drift-zone.html`, `manifest.json`, `sw.js`, `icon-192.png`, `icon-512.png` into **one folder**
2. Open `drift-zone.html` in Chrome
3. Tap the **Install** banner that appears (or browser menu → "Install app")
4. It now lives on your home screen like a native app, works offline

---

## 📁 Repository Structure

```
drift-zone-app/
├── drift-zone.html          ← CURRENT live version (always latest release)
├── manifest.json             ← PWA config
├── sw.js                     ← Service worker (offline support)
├── icon-192.png / icon-512.png
├── CHANGELOG.md              ← Full version history with details
├── README.md                 ← This file
└── releases/                 ← Every past version, frozen, for rollback
    ├── v2.4.0/
    ├── v2.4.1/
    ├── ...
    └── v3.1.0/
```

Each folder under `releases/` is a complete, working snapshot of the app at that version — fully self-contained with its own HTML/manifest/icons.

---

## ⏪ How to Roll Back to a Previous Version

**If something breaks in the current version:**

1. Go to `releases/` and find the last version you know worked (check `CHANGELOG.md` for what changed in each)
2. Copy that folder's `drift-zone.html` (and other files) to the repo root, replacing the current ones
3. Commit with a message like `"Rollback to v2.9.0 — v3.0.0 introduced login issue"`

**Using GitHub's web interface (no command line needed):**
1. Open the `releases/vX.X.X/drift-zone.html` file you want to roll back to
2. Click the file → click the **pencil (edit)** icon... actually easier:
3. Click **Code** tab → navigate to `releases/vX.X.X/drift-zone.html` → click **Raw** → copy all the content
4. Go to the root `drift-zone.html` → click pencil to edit → paste over everything → commit

**Using Git (if you have it installed):**
```bash
git checkout main -- releases/v2.9.0/drift-zone.html
cp releases/v2.9.0/drift-zone.html drift-zone.html
git add drift-zone.html
git commit -m "Rollback to v2.9.0"
git push
```

---

## 🔥 Firebase Setup (Phase 2 — Cloud Sync)

Starting at v3.0.0, the app connects to Firebase for multi-branch, multi-device support.

**Firebase project:** `drift-zone-cafe`

If you need to recreate or check the Firebase project:
1. Go to https://console.firebase.google.com
2. Project: `drift-zone-cafe`
3. **Firestore Database** — where all branch/staff/session data lives
4. **Firestore Rules** — currently set to development mode (`allow read, write: if true`). **This needs to be locked down before going fully live** — see "Known Issues" below.

The Firebase config is embedded directly in `drift-zone.html` (it's safe to be public — Firebase security relies on Firestore Rules, not hiding the API key).

---

## ⚠️ Known Issues / Next Steps

- [ ] **Firestore security rules are currently open** (`if true`) for development. Needs proper rules tied to authenticated branch/staff access before relying on this in production with sensitive data.
- [ ] **Stage 2 of Phase 2 not yet built**: Stations, Sessions, Inventory, Snacks, Tabs still save to `localStorage` on each device — not yet synced live across devices. Only login/branch/staff/permissions are cloud-based so far.
- [ ] Once Stage 2 ships, the **"Import Local Data"** button in Settings should be used once per device to push existing local data into the cloud branch.

---

## 🧩 Tech Stack

- Single HTML file — vanilla JS, no build step, no framework
- [SheetJS (xlsx)](https://github.com/SheetJS/sheetjs) — Excel export, loaded via CDN
- Firebase Firestore — cloud data (v3.0.0+)
- PWA manifest + service worker — installable, offline-capable

---

## 📝 Changelog

See [CHANGELOG.md](./CHANGELOG.md) for full version history.
