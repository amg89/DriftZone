# Drift Zone — Gaming Café Manager

A single-file web app for running a PlayStation/gaming café: station sessions, snacks & drinks, client tabs, inventory with recipes, expenses, purchases, shifts, and profit reporting.

**Current version: v2.9.25** (production — localStorage based)

> **Note:** the earlier v3.0.0/v3.1.0 Firebase multi-branch experiment has been **discontinued** in favor of continuing to mature this localStorage version. It's kept in `releases/` for reference only — do not build on top of it.

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
    ├── ...
    ├── v2.9.25/
    └── v3.1.0/                ← discontinued, kept for reference only
```

Each folder under `releases/` is a complete, working snapshot of the app at that version — fully self-contained.

**⚠️ Do not roll back to `v2.9.18` or `v2.9.19`** — both contain a Remote Dashboard sync feature that caused real bugs (see CHANGELOG). Fully removed in v2.9.20.

---

## ⏪ How to Roll Back to a Previous Version

**If something breaks in the current version:**

1. Go to `releases/` and find the last version you know worked (check `CHANGELOG.md` for what changed in each)
2. Copy that folder's `drift-zone.html` to the repo root, replacing the current one
3. Commit with a message like `"Rollback to v2.9.17 — v2.9.18 introduced sync bugs"`

**Using GitHub's web interface (no command line needed):**

1. Click **Code** tab → navigate to `releases/vX.X.X/drift-zone.html` → click **Raw** → copy all the content
2. Go to the root `drift-zone.html` → click pencil to edit → paste over everything → commit

**Using Git (if you have it installed):**

```bash
git checkout main -- releases/v2.9.17/drift-zone.html
cp releases/v2.9.17/drift-zone.html drift-zone.html
git add drift-zone.html
git commit -m "Rollback to v2.9.17"
git push
```

---

## 🩺 If things stop updating without a manual refresh

As of v2.9.25, the app has real diagnostics for this. Go to **Settings → 📊 Storage Health**. If usage is high, tap **Clear Old Auto-Snapshots**. This was the root cause of a real incident — see the v2.9.25 changelog entry for details.

---

## 🧩 Tech Stack

- Single HTML file — vanilla JS, no build step, no framework
- [SheetJS (xlsx)](https://github.com/SheetJS/sheetjs) — Excel export, loaded via CDN
- PWA manifest + service worker — installable, offline-capable
- 100% localStorage — no server, no account required, no internet dependency for daily use

---

## 📝 Changelog

See [CHANGELOG.md](./CHANGELOG.md) for full version history.
