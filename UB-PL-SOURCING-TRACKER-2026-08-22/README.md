# UB / PL Sourcing Tracker — Phase 1 (local save)

One page, two trackers. **Unique Bundles** (the team) and **Private Label** (Jack), side by side under one URL. All data stays in the browser it was typed into — no database, no accounts, nothing leaves the machine. Phase 1 of the rollout plan.

## Files — push all four to the repo root

| File | What it is |
|---|---|
| `index.html` | The shell — tab bar, loads the two apps |
| `ub.html` | Unique Bundle Tracker v52.0 (localStorage, key `ub_tracker_v1`) |
| `pl.html` | PL Sourcing in local mode (localStorage, key `pl_sourcing_v1`) |
| `README.md` | This file |

GitHub Pages serves `index.html` automatically. First deploy: repo → Settings → Pages → Deploy from branch → main → root.

## Pushing an update

1. Replace the changed file(s).
2. **Bump `BUILD` in `index.html`** (one line near the bottom: `var BUILD = '0.1';` → `'0.2'`). This busts the Pages cache and updates the version chip top-right, so anyone can confirm they're on the new build after a refresh.
3. Push. Live in about a minute.

**Updates never touch anyone's data.** Data lives in the browser, keyed to the site address — not in these files. Pushing new HTML changes the app, never the data.

## Rules that keep data safe

- **Never rename** `ub.html` or `pl.html`, and never change the storage keys inside them.
- **The site URL is the anchor.** Moving to a different domain later is fine, but it must be planned: everyone exports a backup, opens the new address, imports. One minute — but it does not happen automatically.
- **No private/incognito windows** — data typed there vanishes when the window closes.
- **Don't clear browsing data** for this site — that is where the tracker lives.
- **Same browser, same profile, every time.** Chrome on the same laptop is a different store than Safari on the same laptop.

## Backups (weekly, minimum)

- **UB tab:** the backup chip in the top bar — the app nags when one is due.
- **PL tab:** Settings → Backup & migration → **Download full backup** (ideas, pipeline, tasks, suppliers, forecasts, settings, weekly plan, notes — everything).

These same backup files are what Phase 2 imports into the Supabase build. Keep them in Drive/iCloud.

## Day one — team note

1. Bookmark the site link. Always use the bookmark, always the same browser.
2. New ideas go straight in from today. No backdating.
3. Spot a bug? Screenshot it + one line on what you expected. Fixes ship same day; refresh and check the version chip (top right) went up.

## Phase plan

1. **Now** — this build. Local save, live data from day one.
2. **~1 week** — export backups → Supabase build with logins → import → confirm → carry on.
3. **Week after** — multi-user testing on Supabase.
4. **Later** — fold into the wider BDL hub.
