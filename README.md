# Drift Zone — Gaming Café Manager

Two apps live in this repo, for two different stages of the same café
management system:

| | Local App | Cloud App |
|---|---|---|
| **Where** | repo root — [`drift-zone.html`](./drift-zone.html) | [`cloud/driftzone-cloud.html`](./cloud/driftzone-cloud.html) |
| **Storage** | Browser `localStorage`, one device | Firebase Firestore, multi-device, multi-tenant |
| **Status** | Mature, production, actively used | Newer — most features ported, real-time, multi-branch not yet built |
| **Accounts / roles** | Staff PIN (soft — client-side only) | Firebase Auth + real server-side permission rules |
| **Setup** | None — open the HTML file | Needs a free Firebase project (see [`cloud/README.md`](./cloud/README.md)) |

They are **independent** — not two versions of the same file, not a
migration path you switch over on. The local app keeps running exactly
as it does today; the cloud app is a fresh rebuild aimed at multi-device
sync, real permissions, and eventually a mobile app + SaaS layer. Fixes
and features are tracked separately for each.

---

## 📱 Local App

A single-file web app for running a PlayStation/gaming café: station
sessions, snacks & drinks, client tabs, inventory with recipes,
expenses, purchases, shifts, and profit reporting. No install, no
server, no internet dependency for daily use.

**Current version: v2.9.29**

- Open `drift-zone.html` directly in any modern browser, or install it
  as a PWA (see below).
- Full version history: [`CHANGELOG.md`](./CHANGELOG.md)
- Every past version, frozen and working, under [`releases/`](./releases/)
- ⚠️ Do not roll back to `v2.9.18` or `v2.9.19` — see CHANGELOG.

### Installing as a PWA

The app references `manifest.json`, `sw.js`, and icon files for
installable/offline support. **Those support files aren't included in
this delivery** (they weren't in this session's file store) — the app
works perfectly fine as a plain web page without them, you'd just be
re-adding those three small files to get the "Install as app" /
offline banner back. Ask if you'd like them regenerated.

### Rolling back a version

1. Find the last known-good version under `releases/`
2. Copy that folder's `drift-zone.html` over the one at repo root
3. Commit: `Rollback to vX.X.X — <reason>`

(Or via GitHub's web UI: open `releases/vX.X.X/drift-zone.html` → Raw →
copy → paste over the root file → commit.)

---

## ☁️ Cloud App

A ground-up rebuild on Firebase — real multi-device sync, real
server-side permission enforcement (not just hidden buttons), and the
foundation for a mobile app and multi-tenant SaaS. Built fresh rather
than migrated from the local app, using what the local app's bug
history taught along the way (atomic writes, direct shift references,
a flexible per-permission-key access model instead of a fixed role
table).

- App: [`cloud/driftzone-cloud.html`](./cloud/driftzone-cloud.html)
- Security rules: [`cloud/firestore.rules`](./cloud/firestore.rules)
- Data model + design notes: [`cloud/DATA_MODEL.md`](./cloud/DATA_MODEL.md)
- Setup instructions: [`cloud/README.md`](./cloud/README.md)

**Ported so far:** Stations/Sessions, Shifts, Inventory, Snacks/Checkout,
Client Tabs, Purchases, Expenses, Staff & flexible permissions, Business
Settings, Reports (sales/profit/item sales/valuation), Activity Log,
real stock-movement history ("stock as of any date").

**Not yet built:** multi-branch switching (currently one branch per
account), the mobile app wrap, and the SaaS commercial layer
(super-admin console, billing).

This app has **no version-number/changelog discipline yet** the way the
local app does — it's tracked as one evolving file for now. That's
worth setting up once it's closer to daily-use-ready.

---

## 🧩 Tech Stack

**Local app:** vanilla JS, single HTML file, no build step, no
framework. [SheetJS](https://github.com/SheetJS/sheetjs) via CDN for
Excel export. 100% `localStorage`.

**Cloud app:** vanilla JS, single HTML file, no build step, no
framework. Firebase Firestore + Firebase Auth (client SDK, ES modules
loaded via CDN) — no Cloud Functions, deliberately free-plan (Spark)
compatible.
