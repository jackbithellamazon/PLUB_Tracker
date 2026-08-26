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
2. Two lines near the bottom of `index.html`: **`BUILD`** is the version people see — moves by **0.05** each release (0.1 → 0.15 → 0.2 …). **`STAMP`** must change on **every** push, even a same-version fix — it's what forces browsers and GitHub Pages to drop the cached copy. (I bump both in every folder I send.)

   The version is shown in three places — the top-right chip, both sidebars, and inside every export file. Each app now reads it from a single `APP_VER` constant near the top of its script, so a bump is one edit per file and they cannot drift apart. It sat on v0.1 through a dozen releases because it used to be typed out in four separate places.
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

If it goes wrong: **Settings → Data & backups → Delete & reset → Undo the last change** — a copy of the tracker is taken immediately before every import and every delete, so one click puts it back.

## Latest changes

- **Tasks redesigned** — compact grouped list instead of 80 identical cards. Grouped by type (Keepa searches, ASINs, storefronts…), sorted worst-first, one row each with the note inline. Filter chips, search, and By type / By status / One list.
- **Priority now means something** — a coloured dot on each row: red urgent, amber high, grey normal, dark low. It sorts the list. Click the dot to change it. Only urgent/high get a visible label; everything imported arrives as normal.
- **Sidebar aligned** — the brand row is exactly the height of the top bar in both apps, with the collapse toggle inside it. Collapsed, the logo tile expands it again.
- **PL Action Centre restyled** to UB's language — coloured KPI tiles, readable badges, compact action cards with colour spines.
- **Fixed:** PL badges were rendering black-on-black (a token clash) — text is visible everywhere again. PL's top bar now shows which page you're on.

## Fixed after testing (same day)

- **The session bar now moves while you work.** Its live tally (`0 ideas · 0 reviewed · 0 greens · 0 progressed`) was frozen at zero for the whole session and only caught up if you switched browser tab and came back. The end-of-session summary was always right — it was just the live readout that was stale. It's the flow meter, so it has to move.
- **An import can now be undone.** A copy is taken immediately before an import lands, exactly as it is before a delete. The import confirmation now says so.
- **Import message reads properly** — it used to lead with "Added 0 to the queue" on a tasks-only file, which read like a failure. It now names only what actually landed.

## First month is scaled (v0.1, 26 Aug)

Starting on the 26th used to mean opening the app 26.8 hours behind on a 32-hour target — judged against 25 days you never had. Now the first partial month scales:

- **Targets shrink to the days you actually got.** 32h becomes 6.2h across 6 days; 10 ideas becomes 2. The card foot says `scaled from 32h` so the odd number explains itself.
- **A target that scales to nothing says so** — 2 launches across 6 days reads **From September**, not "behind".
- **Pace counts the part of today that has actually happened**, so opening at 9am on day one doesn't report you behind on a day you haven't had.
- **Settings → KPIs & targets → Tracking since** holds the date and can be changed. The monthly targets you type stay the real monthly numbers.

From the 1st of next month everything runs on full calendar months as before.

## PL — Ideas density (v0.1, 26 Aug)

Same fix as the UB queue: 49 near-identical cards is a wall. Cards are **21% shorter** and the page is **18% less scrolling**, because the three buttons repeated on every card (→ Pipeline · Export · Delete) now appear on hover, and the 56px of padding that was reserving room for them goes with them. Touch devices keep the buttons visible.

## PL — bulk import ideas (v0.1, 26 Aug)

**··· menu → Import ideas**, or drag the `.json` anywhere onto the page.

This **adds**; it never replaces. That matters — the existing *Restore backup* wipes the tracker and puts a saved copy back, which is right for a migration and wrong for "here are this week's products". Before anything happens you see exactly what will land: how many are new, how many are already here, and every name in a list.

An idea already in the tracker is **not duplicated**. Its score and answers are left alone, and the new session notes plus any ASINs you were missing get attached to the record that already exists. So a second look on a product stays one record with two sets of notes.

## PL — less typing when adding an idea

The ASIN box now takes **Amazon links, not just codes** — and a whole block of them at once. Paste ten product URLs and you get ten ASIN rows. It ignores anything that isn't an ASIN and skips ones already on the idea.

## PL — pre-filled answers, and the badge that says so (v0.1, 26 Aug)

An imported idea arrives with all nine checklist answers filled in. Some of those are Jack's own words; some are a read of his notes. A score you didn't give is worse than no score if nothing tells you which is which — so:

- **Every idea carrying guesses wears an amber `⚑ check N` badge** on its card until it's been through.
- **`⚑ N to check`** above the grid filters to just those, so a review pass is one click in and one click out.
- **Clicking the badge marks it checked** and removes it. The answers stay; only the flag goes.
- **The reasoning lives next to the answer**, in the idea's Notes — every one of the nine tagged `YOUR WORDS`, `READ FROM YOUR NOTES` or `MY GUESS`, with the evidence, guesses listed first.

Merging into an idea that already has answers **never touches them** — his answers win, and that record gets no badge. Blank fields on an existing idea get filled; answered ones don't.

## Five stages, not six (v0.1, 26 Aug)

**Sourcing → Jack Validation → Listing & test → Buy & receive → Live.**

- **Ready to Source is gone.** It was a waiting room, not work — an idea that leaves ranking is being sourced.
- **Order/Purchase, Launch and Launched were one phase pretending to be three.** They are now **Buy & receive**, one stage with five ticks: bought · arrived & checked · prepped · sent to Amazon · live. Buying and receiving stock is one long wait, and dragging a card through four columns to say "still waiting on the supplier" is admin, not progress. The card shows a row of pips and *2 of 5*, so a 28-day stage still reads as movement.
- **Prepare to Launch is now Listing & test** and covers the 72-hour test. Its threshold moved 7 → 10 days to match (if you had set your own number, yours is kept).

**Nothing in flight is lost.** Records on the old six stages migrate on load: Ready-to-Source and Source fold into Sourcing; Order/Purchase and Launch fold into Buy & receive. Old ticks map onto the new wording — *All required components ordered* becomes *Stock bought*, *Components received/checked* becomes *Components received & checked*. Work with no equivalent is kept, still ticked, but no longer required, so the card reads *2 of 5* rather than *3 of 8*. Every migrated product gets a line in its History saying what changed.

## Paste your notes into a new idea (UB)

**Add Idea → ⇩ Paste from your notes.** Paste a block — a Helium 10 line, an Amazon link, a page of notes — and it fills the name, the ASIN and the four numbers it recognises. Nothing already filled in is overwritten.

It reads the shapes people actually write: `Search Volume` on one line and `1,540` on the next, `2 main competitors`, `SV 28,961 · £9.99 · 600 comp sales/mo · 40 competitors`, and a `PRODUCT 3 — CHICORY COFFEE` heading.

## PL — scored well, then stalled

Above the ideas list, up to three ideas that **scored 60%+, have not been touched in 14+ days, and still are not in the Pipeline** — with a one-click **→ Pipeline**. A "top three by score" strip would only repeat the first three cards; what actually goes missing is the idea that looked good weeks ago and then went quiet. Nothing stalled, no strip.

## Fixed in pre-ship testing (26 Aug)

- **Day one showed full monthly targets.** `loadState` returned early when there was no saved data, so the start date was never stamped and the part-month scaling never ran — on a brand-new browser, the exact case it exists for. A first visit now opens on **0 / 6.2h · scaled from 32h**, not 0 / 32h with "26.6 expected by today".
- **New products entered Sourcing with the wrong checklist** — a hard-coded pair of tasks left over from Ready to Source, so a product arrived with 2 ticks instead of Sourcing's 8. Seeded from the stage definition now.
- **Jack's "Send back" offered stages that no longer exist** (Ready to Source / Source). It would have parked a product on a stage with no column. One option now: Sourcing.
- **Stale copy across the app** — buttons, toasts, history lines and the whole guide stage table still described six stages and "Ready to Source". All updated. The archive's "died late" count keeps the old stage names alongside the new ones so historical drops still count.

## v0.15 — 26 Aug

Everything above from "First month is scaled" onward ships as **v0.15**: five pipeline stages, part-month targets, paste-your-notes, the PL idea import with pre-filled checklists, the density pass, and the pre-ship fixes. Backups written by v0.1 still import into v0.15 — nothing checks the version number.

