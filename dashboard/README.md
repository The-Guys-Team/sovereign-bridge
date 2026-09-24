# Bridge dashboard: Equinox 6

`equinox-6.html` is **the** Bridge dashboard. Every student gets this exact file. Claude never designs, restyles, or rewrites it for a student. It only publishes this file and fills the student's database with their own data.

## Rules for Claude (the kernel points here)

1. **Publish, don't design.** To create or update a student's dashboard, publish `equinox-6.html` byte-for-byte as an Artifact with capabilities `db`, `sample`, and `mcp` (Google Calendar `list_events`, `create_event`, `update_event`). Existing dashboard: republish to the **same URL**, so the database (all their data) is kept.
2. **Style requests get the palette answer.** Colors, fonts, logo and "make it pink" are all out of scope. Point the student to the gear icon: two palettes (Sky, the default, and Sand) and Light / Dark / Match device.
3. **Content is theirs, layout is ours.** Tabs, lanes and copy tailor themselves from `profile/main` (class year, opportunity type). Don't hand-edit the HTML to tailor it.

## Where the brand lives (for us, not students)

Everything visual that we might change is in two places at the top of the file:

- `BRAND TOKENS` CSS block: palettes (light + dark each) and fonts.
- `BRAND` JS object: the logo SVG (the cable-stayed bridge on a rounded tile) and the palette list shown in Settings.

A new logo or color is a one-block edit, a version bump, and a republish.

## Database shape (unchanged from v6, plus four additions)

Docs: `profile/main`, `mindmap/main`, `brief/main`, `chat/main`, **`coach/main`** (new: conversation intel)
Collections: `experience`, `network`, `interactions`, `sessions`, `prep`, `candidates`, `projects`, `opportunities`, `outreach`, `tasks`, `reflections`, `guidance`, `activity`

New fields (all optional, so v6 data works untouched):
- `profile.appearance` `{palette, mode}`, `profile.e6SeenAt` (welcome sheet shown), `profile.e6NewUser`
- `mindmap.stories` `[{skill, title, story, useWhen}]`, `mindmap.revisedAt`
- `projects[].notes[].kind` `decision | progress | question | idea`, `projects[].digest {summary, at}`
- `brief.trigger` (what change caused the last bearing refresh)
- `tasks[].waitingOn`, `waitingOnWho` (already read by v6; now written by chat)

## Rollback

`v6-rollback.html` is the last v6 build. Republish it to the same URL to roll back. The data is compatible both ways.
