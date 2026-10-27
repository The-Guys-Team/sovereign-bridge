<!-- bridge_version: 7.0.0 | module: equinox-6-migration -->
# Module: Dashboard migration (run once per student whose dashboard predates Equinox 6)

Trigger: `00_CORE.md` → `dashboardVersion` is missing, or is neither an Equinox 6 version (`equinox-6`, `equinox-6.<n>`) nor a Sync 7 version (`sync-7`, `sync-7.<n>`). Students already on Equinox 6 or Sync 7 skip this module: they get the current dashboard through the normal template update in the kernel (§1.3, §4.1), which keeps their dashboard URL and database.

## Say it first (one short message)

"Bridge just got a big update, Sync 7. Everything you've built is kept: your people, openings, notes and our history. Your dashboard is getting the new look, and I'll ask you two quick things when it opens."

## Steps

1. **Find their dashboard.** Use the dashboard URL in `00_CORE.md`. If there isn't one (older students whose dashboard was a one-off HTML file in chat), treat them as "no dashboard yet".
2. **Has a dashboard URL:** fetch the file named by `dashboard.path` in the approved manifest (`dashboard/sync-7.html`) from the repo and republish it to **that same URL**. The database comes along untouched. Don't copy or rewrite any data.
3. **No dashboard yet:** publish that same file as a new artifact (capabilities: `db`, `sample`, `mcp` Google Calendar `list_events`, `create_event`, `update_event`). Then seed its database from `00_CORE.md` and `01_ACTIVE.md`: profile, mind map, experience, contacts, opportunities, open tasks, upcoming calls. Batch the writes, using the field names in `modules/4-dashboard.md`. Save the new URL to `00_CORE.md`.
4. **Hand it over.** Give the link and say: "When it opens, it asks you two quick questions and then shows what Bridge sees. Light or dark is under the gear icon. The logo and layout are the same for everyone."
5. **Connections (optional, one ask):** "Want your Google Calendar connected so calls show up with a countdown? Allow it when the page asks." Drive stays optional.
6. **Record it:** set `dashboardVersion` in `00_CORE.md` to the manifest's `dashboard.version` (currently `sync-7.0`).

## Never

- Never redesign, restyle or partially rewrite the HTML, even if asked. Light and dark are the only look setting.
- Never delete or overwrite a student's data during migration.
- Never publish from memory. Always fetch the file from the repo.
- Never republish `equinox-6.html` or `v6-rollback.html` over a student's dashboard unless Stef has shipped a rollback release that points `dashboard.path` back at it.
