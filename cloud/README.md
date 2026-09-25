# Drift Zone Cloud

Multi-device, multi-tenant rebuild of Drift Zone on Firebase Firestore.
See [`DATA_MODEL.md`](./DATA_MODEL.md) for the full schema and design
reasoning; this file is just setup steps.

## What you need

- A free Firebase project (the **Spark** plan — this app deliberately
  needs no Cloud Functions, so it never requires upgrading to Blaze)
- Firestore **Database** enabled, in **Native mode**
- Firestore **Authentication** enabled, with the **Email/Password**
  sign-in method turned on

## First-time setup

1. Go to [console.firebase.google.com](https://console.firebase.google.com) → create a project (or use an existing one)
2. **Build → Firestore Database → Create database** → start in production mode, pick a region
3. **Build → Authentication → Get started → Sign-in method → Email/Password → Enable**
4. **Build → Firestore Database → Rules tab** → paste in the entire contents of [`firestore.rules`](./firestore.rules) → **Publish**
5. In **Project settings → General → Your apps**, add a Web app (if you haven't) and copy its **API Key** and **Project ID**
6. Open `driftzone-cloud.html` in a browser — it will ask for those two values on first run and remember them (stored in that browser's `localStorage` as `dzc_config`)
7. Sign up as the business owner (first account created for a business becomes `owner`)

## Updating the rules later

Any time `firestore.rules` changes in this repo, **paste the new file's
entire contents** into Firebase Console → Firestore Database → Rules →
Publish. The app doesn't push rules itself — Firestore rules are only
ever set from the console (or the Firebase CLI, not used here).

## Permission model, in short

Every staff account gets a **default** bundle of permissions based on
role (staff / manager / owner) at invite time, but every individual
permission key can be freely overridden per person afterward from the
Staff tab — it's not a fixed role table. The actual enforcement lives
in `firestore.rules`, not in the app's UI — the UI only hides buttons
for convenience; a person without a permission genuinely cannot write
that data, even from the browser console. See `DATA_MODEL.md` →
"Permissions" for the full key list and what each one gates.

## Known limitations (by design, for now)

- **One branch per account** — `branchIds[0]` is used directly; there's
  no branch switcher yet even though the schema supports multiple
  branches per tenant.
- **No Cloud Functions** — a few things that would normally be
  server-triggered (e.g. custom auth claims) are instead done via
  documents the rules read directly (see `DATA_MODEL.md`). This keeps
  the whole app on Firebase's free plan.
- **Reports pull unfiltered-by-date, filter client-side** — every
  report/history query filters only by `branchId` (an equality match)
  and applies the date range in JavaScript afterward, specifically to
  avoid needing a manual Firestore composite index for this repo to
  work out of the box. Fine at café data volumes; revisit if it ever
  gets slow.
