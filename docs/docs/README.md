# UB / PL Sourcing Tracker — Phase 1 (local save)

One page, two trackers plus a combined pipeline view. **Unique Bundles** (the team) and **Private Label** (Jack), side by side under one URL. All data stays in the browser it was typed into — no database, no accounts, nothing leaves the machine. Phase 1 of the rollout plan.

## Files — push all four to the repo root

| File | What it is |
|---|---|
| `index.html` | The PLUB shell — tab bar, loads the two apps, and the merged **Pipeline** tab (reads both apps' data in this browser) |
| `ub.html` | Unique Bundle Tracker (localStorage, key `ub_tracker_v1`) |
| `pl.html` | PL Sourcing in local mode (localStorage, key `pl_sourcing_v1`) |
| `README.md` | This file |

GitHub Pages serves `index.html` automatically. First deploy: repo → Settings → Pages → Deploy from branch → main → root.

## Pushing an update

1. Drag the new `docs` folder in (GitHub overwrites the changed files).
2. Two lines near the bottom of `index.html`: **`BUILD`** is the version people see — moves by 0.1 each release. **`STAMP`** must change on **every** push, even a same-version fix — it's what forces browsers and GitHub Pages to drop the cached copy. (I bump both in every folder I send.)
3. Push. Live in about a minute. Refresh and check the chip top-right.

**Updates never touch anyone's data.** Data lives in the browser, keyed to the site address — not in these files. Pushing new HTML changes the app, never the data.

## Rules that keep data safe

- **Never rename** `ub.html` or `pl.html`, and never change the storage keys inside them.
- **The site URL is the anchor.** Moving to a different domain later is fine, but it must be planned: everyone exports a backup, opens the new address, imports. One minute — but it does not happen automatically.
- **No private/incognito windows** — data typed there vanishes when the window closes.
- **Don't clear browsing data** for this site — that is where the tracker lives.
- **Same browser, same profile, every time.** Chrome on the same laptop is a different store than Safari on the same laptop.
- **One tab at a time.** A second tab of the tracker goes read-only on purpose (it stops two tabs overwriting each other). Close it and carry on in the first.

## Backups (daily while the data lives only on one laptop)

- **UB tab:** click the green **Saved** chip in the top bar — the Action Centre reminds you daily. Send the file to Jack: it's the off-site copy, and it's how he sees the pipeline.
- **PL tab:** Settings → Backup & migration → **Download full backup** (ideas, pipeline, tasks, suppliers, forecasts, settings, weekly plan, notes — everything).

These same backup files are what Phase 2 imports into the Supabase build. Keep them in Drive/iCloud.

## Day one — team note

1. Bookmark the site link. Always use the bookmark, always the same browser.
2. New ideas go straight in from today. No backdating.
3. Spot a bug? Screenshot it + one line on what you expected (or press the ⚑ button in the app). Fixes ship same day; refresh and check the version chip (top right).
4. Read **How it works** in the app once — it explains every page, the questions, sessions and the KPIs.

## Phase plan

1. **Now** — this build. Local save, live data from day one.
2. **~1 week** — export backups → Supabase build with logins → import → confirm → carry on.
3. **Week after** — multi-user testing on Supabase.
4. **Later** — fold into the wider BDL hub.

## v0.1 — what's in this release (UB)

- **Three monthly KPIs**, all automatic: Sourcing hours 32h · Ideas captured 10 · Products launched 2. Judged against how far through the month we are. Everything else is information, not a target.
- **Pipeline flow** on the Action Centre: what entered, moved, got stuck, is waiting, was dropped, launched — last 7 days and right now.
- **Hamper or Bundle** questionnaire: 6 questions for a bundle, 4 for a hamper, numbers only, red flags for under-100 search volume and under-£15.99 price, optional seasonal tag with a "source by" date.
- **Sessions**: two kinds (fresh sourcing / working existing ideas), counts itself from what you do, asks after 45 idle minutes and ends itself at 50, end-of-session summary, correctable durations.
- **Launched** = stock bought + listing live (two ticks).
- **Seasonality** as forward planning: each season shows the sourcing deadline and whether the window is open.
- Compact layout, collapsible sidebar, Review Queue (was Review Inbox), archive outcomes and notes, restructured Settings, full staff guide, no more slashed-zero font.

## v0.1 (same day, later) — shell + PL

- **PLUB** top bar: 40px, new mark, three tabs — Unique Bundles · Private Label · **Pipeline**.
- **Merged Pipeline tab**: both apps on one board in plain stages (Ranked ideas → Sourcing → Validating → Samples → Ordered / stock → Ready to launch → Launching → Launched this month). Cards are colour-tagged UB / PL, show days in stage, stuck (over the stage limit) and waiting. Click a card to open it in its app. It reads whatever each app has saved *in this browser* — on Jack's laptop that's PL plus whatever UB export he's imported.
- **Private Label re-skinned** in UB's language: same ground, type, left sidebar, top bar, cards and chips. PL logic untouched. Dark only.
- **Sidebar rebuilt from scratch** on both apps: colour-coded duotone icons, badges only when there's a count, live session timer, collapse to a rail (remembered).
- **Import adds, never wipes**: Settings → Import backup → "Add to tracker" / "Add to what's here instead".
- **Settings → Delete & reset**: remove an import batch, clear the queue / completed reviews / ideas / sessions / tasks, wipe (backup downloads first) — every delete has Undo.

## Importing a work list (for Becki)

Jack sends a `.json` file. Two ways in, both safe:

1. **Drag the file anywhere onto the tracker.** A drop zone appears; let go.
2. Or **Tasks → ⬆ Import a list**.

A panel shows exactly what's about to be added — how many tasks, broken down by type (ASINs to check, Keepa searches, storefronts), with the first few by name — before anything happens.

They land on the **Tasks** page. Each one opens its link ("Open keepa filter ↗"), carries Jack's note, and has **+ Send finds to review queue** so anything worth scoring goes straight into the Review Queue. Tick it off when it's done.

Nothing already on the list is touched — the file is *added*. Anything already there is skipped. Jobs already marked done on Jack's sheet are left out of the file entirely, so the list is only what still needs doing.

If it goes wrong: **Settings → Data & backups → Delete & reset → Undo the last delete**.
