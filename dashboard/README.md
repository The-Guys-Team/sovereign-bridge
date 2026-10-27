# Bridge dashboard: Sync 7

`sync-7.html` is **the** Bridge dashboard. Every student gets this exact file. Claude never designs, restyles, or rewrites it for a student. It only publishes this file and fills the student's database with their own data.

## Rules for Claude (the kernel points here)

1. **Publish, don't design.** To create or update a student's dashboard, publish `sync-7.html` byte-for-byte as an Artifact with capabilities `db`, `sample`, and `mcp` (Google Calendar `list_events`, `create_event`, `update_event`). Existing dashboard: republish to the **same URL**, so the database (all their data) is kept.
2. **Style requests get the look answer.** Colors, fonts, logo and "make it pink" are all out of scope. Point the student to the gear icon: Light, Dark, or Match my device.
3. **Content is theirs, layout is ours.** Pages and copy tailor themselves from `profile/main` (class year, opportunity type). Don't hand-edit the HTML to tailor it.
4. **Writing to the database** follows `modules/4-dashboard.md` (field names, the posting contract: open the page first, at most 8, never invent).

## Where the brand lives (for us, not students)

Everything visual that we might change is in the stylesheet at the top of the file:

- The base `BRAND TOKENS` block, plus the final `Sync 7 · Slate look` block, which sets the colors (light and dark), fonts (Newsreader, Manrope) and component shapes.
- `BRAND` JS object: the logo SVG (the cable-stayed bridge on a rounded tile).

A new color or logo is a block edit, a version bump, and a republish. Text contrast must stay at 4.5:1 or better in both looks.

## Database shape (Equinox 6 shape, plus optional Sync 7 fields)

Docs: `profile/main`, `mindmap/main`, `brief/main`, `chat/main`, `coach/main`, `resume/main` (new)
Collections: `experience`, `network`, `interactions`, `sessions`, `prep`, `candidates`, `projects`, `opportunities`, `outreach`, `tasks`, `reflections`, `guidance`, `activity`

Every Sync 7 addition is an optional field; the list is in `modules/4-dashboard.md`. Equinox 6 data renders unchanged, and Equinox 6 ignores the new fields.

## Rollback

`equinox-6.html` (Equinox 6.1) and `v6-rollback.html` stay in this folder. To roll back, ship a new PATCH release whose manifest `dashboard.path` points at the older file; students then get it through the normal template update, on the same URL. The data is compatible both ways. Don't move or delete a release tag.
