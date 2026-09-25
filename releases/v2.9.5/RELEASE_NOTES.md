# Drift Zone v2.9.5

## What's in this release (2025-02-07)

- **BUG FIX:** Restore-from-backup was silently dropping Shifts, Purchases, and Client Tabs even though Backup saves them — a real disaster-recovery gap. Restore now brings back everything Backup writes.
- **Alarm:** added a single soft heads-up beep at 5 minutes remaining, separate from the repeating time-up alarm — lets staff offer an extension before time actually runs out.
- **Alarm:** if a time-up alarm goes unaddressed for 5+ minutes, a red banner now appears across the whole app (not just the station card) so it isn't missed while staff are on another tab.
- **NEW — Automatic daily snapshots:** a local backup is taken once a day with no action needed, restorable from Settings → Backup & Restore. This protects against mistakes/corruption, **not** device loss.
- **NEW — Backup reminder banner:** appears if it's been 7+ days since your last manual backup download, with a one-tap "Backup Now" button and a "remind me tomorrow" dismiss.

## Important distinction (worth remembering)

Two separate safety nets now exist, and they protect against different things:
| | Automatic Daily Snapshot | Manual Backup (JSON download) |
|---|---|---|
| Needs action? | No — fully automatic | Yes — you click Backup |
| Protects against | Accidental changes / data corruption | Device loss, theft, browser data cleared |
| Where it lives | Same browser/device (localStorage) | Wherever you save the downloaded file |

Keep downloading manual backups periodically (the reminder banner will nudge you) — the daily snapshot is a convenience, not a substitute for a real off-device copy.

## Upload instructions

1. Create `releases/v2.9.5/` in your GitHub repo
2. Add `drift-zone.html` into that folder
3. Commit: `Release v2.9.5 — restore bug fix, alarm heads-up + escalation, auto snapshots, backup reminder`
