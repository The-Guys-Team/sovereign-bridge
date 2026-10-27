# Bridge changelog

Batch updates: collect changes, then ship one release (see `dev/RELEASING.md` in the `the-guys` repo — that folder is kept private, alongside onboarding materials and the test suite; this repo holds only what students' Claude sessions fetch at runtime). Never edit `current.md` in place without also bumping the version, adding an entry here, and updating `manifest.json`.

Versioning: `MAJOR.MINOR.PATCH`.
- **PATCH** — wording/tone fixes, no behavior change.
- **MINOR** — new or changed behavior; no change to the shape of student data.
- **MAJOR** — visual/experience overhaul (e.g., the planned version 6).
- **Schema version** (separate number in `manifest.json`) increases *only* when the shape of the student's Drive files changes. It always ships with a migration file.

Release rules:
- Every release is tagged `v<version>` (e.g. `v5.2.0`) on its merge commit in `main`. Students' bootstraps fetch files from that tag, so a release isn't live until the tag is pushed.
- Tags are never moved, deleted, or rewritten. To fix a release, ship a new version with a new tag.
- All links inside the fetched files point at the same `v<version>` tag as the kernel, never at `main`.

---

## 7.0.1 — 2026-10-27 (schema 2)

Dashboard only (`dashboard/sync-7.html`, dashboard version `sync-7.1`). No change to the shape of student data and no kernel behavior change; the kernel only carries the new version number.

- Moves > People: people you know on the left and new suggestions on the right (wide screens); on a phone a My people / New for you switch shows one at a time (remembered). Suggestions show three with "Show more". Once there are six or more people, the list gets a search box and status filters (Follow up, Waiting, In conversation, Not contacted).
- The manifest lists the pinned address of every file (`urls`), because a student's Claude may only fetch addresses it has been given.

Students on 7.0.0 (`dashboardVersion: sync-7.0`) get the new page through the normal template update: same dashboard URL, same database.

---

## 7.0.0 — 2026-10-27 (schema 2)

Sync 7. MAJOR: new look and a rebuilt dashboard (`dashboard/sync-7.html`, dashboard version `sync-7.0`). **No change to the shape of student data:** every addition is an optional field in the dashboard's own database, so schema stays 2 and there is no migration. Equinox 6 data renders unchanged, and `equinox-6.html` / `v6-rollback.html` stay in the repo for rollback.

- New look: Slate, light and dark only (the Sky and Sand palettes and the palette picker are gone). Logo and wordmark in the header; serif headlines; one accent.
- First run: welcome, two quick questions, an intake chat that reads the person (asks for a pasted resume first, saves impressions as it goes), "What I see" with evidence and editable details, then a first path.
- Today: what Bridge sees, a bearing with three moves (the first is a 10-minute task), a first-visit tour, a "Got more time?" list, and what changed since the last visit.
- Moves: People (approve new people and get a drafted first message, add someone you met, "I sent it", dated notes) and Openings (real postings with a link, source and checked-on date; application status; openings where you know someone are ranked first and suggested links to people already in your data wait for your confirmation).
- Path: milestones across a bridge computed from real activity, the focus with a question to test, other directions, what Bridge knows and what is still open, and why anything changed.
- Coaching: next-call prep as questions and answers, a debrief after the call, drafts to send (thank-yous and follow-ups), and a resume built only from the student's experience (green = new or rewritten, amber = fill in) that the student can type in.
- More: Projects and Records on one page.
- Text contrast is 4.5:1 or better on every page in both looks.
- Kernel: §1.3 no longer re-runs the Equinox 6 migration for Sync 7 students (it now recognizes `sync-7` versions) and the template update republishes the file named by `dashboard.path`. §4.1 points at `sync-7.html`, and the look answer is Light / Dark / Match my device.
- Modules: `modules/4-dashboard.md` rewritten for Sync 7, including the posting contract (open the page first, at most 8, never invent, connection first). `modules/3-networking.md` gains "Finding openings: people first". `modules/equinox-6-migration.md` now moves older dashboards onto the current dashboard file.
- Data safety: updates republish to the same URL and add only optional fields; profile writes only merge and are refused if the profile could not be read; Settings has "Copy a backup"; the kernel asks Claude to snapshot the dashboard database before a republish and to confirm the data is still there afterward.
- The page's own chat cannot browse or open links; openings are found in the student's Bridge Project chat and written to the dashboard database.
- Not included (backlog): resume file upload, Outlook calendar, a Sunday weekly wrap-up.

**Runtime files.** New: `dashboard/sync-7.html`. Changed: `current.md`, `manifest.json`, `dashboard/README.md`, `modules/3-networking.md`, `modules/4-dashboard.md`, `modules/equinox-6-migration.md`.

---

## 6.1.0 — 2026-09-23 (schema 2)

Dashboard only, no change to the shape of student data. Dashboard version `equinox-6.1`.

- "Connect your apps" sheet:
  - New users see it while their career map builds.
  - Existing users see it once, the next time they open their dashboard.
  - Apps the dashboard uses (Google Calendar) are allowed in one Claude permission prompt.
  - Apps used in Bridge chats (Drive, Granola, Gmail, Notion, Linear) get an "Add in Claude" button.
- Settings lists every app with On / Allow / Add in Claude.
- Usage limits: messages save and queue instead of failing, then get answered when Claude is back. The career map builds on the next visit if the limit hit mid-build.
- Direction timeline line ends at the last dot.
- Kernel: whenever the approved version's manifest `dashboard.version` differs from the student's `dashboardVersion`, Claude republishes `dashboard/equinox-6.html` from that version's tag to their existing dashboard URL and records the new version. This is how existing dashboards pick up template changes. The Equinox 6 migration now triggers only for students whose `dashboardVersion` isn't an Equinox 6 version yet.

## 6.0.0 — 2026-09-23 (schema 2)

### Equinox 6
- One locked dashboard for everyone (`dashboard/equinox-6.html`). Claude publishes it and never redesigns it.
- Shared Bridge branding: cable-stayed bridge logo on a rounded tile, two palettes (Sky, the default, and Sand), each light and dark or matching the device. Chosen in Settings.
- Chat: survives tab switches (auto-abort and one quiet retry), always dismissible to an "Ask Bridge" pill, saves drafts.
- One chat message now updates contacts, tasks, pipeline and prep together, then refreshes the bearing automatically.
- People as compact rows. Chips centered.
- Pipeline tailored to stage: students see Internships, Research and Classes; grads see Roles, Programs and Warm paths.
- Coaching: "Stories to tell" replaces the resume dump. Conversation intel is short takeaways.
- Projects: notes grouped into decisions, progress, open questions and ideas, with a "tidy with Bridge" button.
- Records: resume first. Conversations, sessions and reflections are merged into one searchable timeline. Stats and Journal tabs removed.
- Direction: survey/readout step bar removed. First-time users get a real readout (mind map, stories, first moves) built from the intake.
- Migration: existing data is kept; the dashboard is republished to the same URL. Rollback file included.
- First run: welcome page → Get started → full-screen intake chat → career map → dashboard + palette pick.
- Chat reliability: removed the page-side 90s timeout (it was killing slow but healthy replies), streams replies as they're written, uses the quick model for chat, and never runs background jobs while a chat reply is in flight.
- Bearing: short, directional headline (max 12 words), verb-first moves.
- To-dos finished today stay on the list, crossed out, until tomorrow.
- Coaching buttons send straight to the chat and open the conversation. Stories can be matched to upcoming calls.
- Direction: career-map diagram at the top; rail dots centered.
- Projects: "toss in an idea" box; each note gets sorted, tightened, turned into a task when it implies one, and updates "Where it stands".
- Google Calendar two-way: calls booked in chat become calendar events (list_events, create_event, update_event); prep cards have "Add to Google Calendar".
- Direction: map runs left to right; tapping a stop jumps to its details below and fills its dot.
- First run: the career map is built from the whole intake conversation in one step, so a broken save block mid-chat can't stall it. A "Build my career map" button appears after 5 replies as a manual fallback.
- Direction: the timeline line now ends exactly at the last stop's dot.

**Runtime files.** New: `dashboard/equinox-6.html`, `dashboard/v6-rollback.html`, `dashboard/README.md`, `modules/equinox-6-migration.md`. `current.md` now has a "Publish, don't design" dashboard rule (§4.1) and points to `dashboard/README.md` instead of `modules/4-dashboard.md`. The first chat after the update runs the one-time Equinox 6 migration (§1.3, §7). `manifest.json` gets a `dashboard` entry (`equinox-6`) and lists `equinox-6-migration` under `migrations`. No schema change.

## 5.2.0 — 2026-09-22 (schema 2)

**MINOR: consent-based update flow, pinned tags.** Students' Projects now carry a fixed bootstrap that reads `manifest.json` from `main`, asks the student to approve any new version, and then fetches the files pinned at tag `v<version>`.

- Changed: `current.md` rewritten as a method document the student chose to adopt. Removed the identity line, the "follow exactly / don't summarize" line, and the "only sources of developer instructions" rule; kept the rule that contacts' emails, transcripts, and other student-provided content are data.
- Removed: manifest fetch and cohort gate from the startup steps (the bootstrap handles version checks). Cohort status is now an optional, friendly notice. Also removed the Drive kernel cache (`_system/kernel_cache.md`); the bootstrap handles fetching.
- Changed: the Drive `Bridge/` folder is created only after the student agrees to connect Drive.
- Changed: existing data (including v5.0 Project docs) is never migrated, moved, archived, or deleted without asking first; approved migrations and rollups snapshot to `_backup/` first. The monthly rollup now asks before running.
- Changed: module, template, and migration links resolve against the same `v5.2.0` tag as the kernel, not `main`.
- New: `approved_version` field in `_META.md` (added to existing files on first run of 5.2.0; no schema bump).
- Tone audit of modules, templates, and the `1-to-2` migration: the dashboard is offered, not auto-created; the migration asks first and leaves the old docs where they are.

## 5.1.1 — 2026-09-21 (schema 2)

**Repo split.** Moved out of `the-guys` (private) into this dedicated public repo, `sovereign-bridge`, so only Bridge's runtime instructions are public — the product code, dashboard, and outreach tooling stay in `the-guys`. All URLs in the bootstrap and kernel updated; paths flattened (no more `bridge-program/` prefix). No change to program behavior. This is the first release actually reachable by a student's Claude (the earlier `the-guys`-hosted attempt 404'd).

## 5.1.0 — 2026-09-21 (schema 2)

**Distribution + memory architecture.** First release delivered through the GitHub-hosted kernel.

- New: kernel (`current.md`) with a startup protocol that runs on the student's first message in any chat, so no "let's go" phrase is needed.
- New: student data is kept in four tiers (Core, Active, Archive, Digests). If the student connects Google Drive (optional, offered once right after the welcome, never a gate), it lives in a `Bridge/` folder in their own Drive. Without Drive, "plain mode" gives them a save-file to keep in their Project's files.
- New: structured-row schemas, dated facts, one-source-of-truth rule, write-as-you-go, handoff note.
- New: automatic monthly rollup and size budgets.
- New: schema versioning with migrations. `1-to-2` imports the v5.0 Project docs into Drive.
- New: cohort gating and broadcast `message` via `manifest.json`.
- Changed: v5.0 program text split into four modules, fetched only when needed. Content unchanged except: welcome message now fires on the first message of a new student (not on "let's go"); "project docs" replaced by the Drive file mapping; hypothesis changes now recorded with a date and reason.

## 5.0.0 — 2026-09-16 (schema 1)

The original single-document program (Project docs + optional dashboard). Baseline for migration.
