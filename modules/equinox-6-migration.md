# Module: Equinox 6 migration (run once per student)

Trigger: the manifest says the current dashboard version is `equinox-6` and the student's memory (`00_CORE.md` → `dashboardVersion`) says anything older, or nothing.

## Say it first (one short message)

"Bridge just got an update, Equinox 6. Everything you've built is kept: your people, pipeline, notes and our history. Your dashboard is getting the new Bridge look, and I'll ask you two quick things when it opens."

## Steps

1. **Find their dashboard.** Use the dashboard URL in `00_CORE.md`. If there isn't one (older students whose dashboard was a one-off HTML file in chat), treat them as "no dashboard yet".
2. **Has a dashboard URL:** fetch `dashboard/equinox-6.html` from the repo and republish it to **that same URL**. The database comes along untouched. Don't copy or rewrite any data.
3. **No dashboard yet:** publish `equinox-6.html` as a new artifact (capabilities: `db`, `sample`, `mcp` Google Calendar `list_events`, `create_event`, `update_event`). Then seed its database from `00_CORE.md` and `01_ACTIVE.md`: profile, mind map, experience, contacts, opportunities, open tasks, upcoming calls. Batch the writes. Save the new URL to `00_CORE.md`.
4. **Hand it over.** Give the link and say: "When it opens, pick a palette and light or dark. That's the only look setting. The logo and layout are the same for everyone."
5. **Connections (optional, one ask):** "Want your Google Calendar connected so calls show up with a countdown? Allow it when the page asks." Drive stays optional, as it is in 5.1.
6. **Record it:** set `dashboardVersion: equinox-6` in `00_CORE.md`.

## Never

- Never redesign, restyle or partially rewrite the HTML, even if asked. Offer the palettes instead.
- Never delete or overwrite a student's data during migration.
- Never publish from memory. Always fetch the file from the repo.
