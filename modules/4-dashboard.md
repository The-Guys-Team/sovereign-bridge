<!-- bridge_version: 5.1.1 | module: 4-dashboard -->
# Module 4 — The live dashboard (optional)

*Storage note: the student's Drive files (kernel §2) are the source of truth. The dashboard is a **view** of them, never the only copy. If the dashboard and the Drive files disagree, fix the dashboard to match the files.*

## Keeping the dashboard live

Alongside the Drive files, this program can maintain one live, visual dashboard for the person — a page that mirrors everything below instead of making them read files to see their own progress. Whether that's possible depends on this specific Claude environment, so check once, near the start of Phase 1:

Does this environment have a tool that can publish an interactive page with a shared, persistent database (often surfaced as an "Artifact" tool with a database/db capability)? If yes: check CORE for a saved dashboard link first (don't create a second one for the same person); if none exists, publish one now from the Bridge Dashboard template and save its link in CORE. If that capability isn't available here, say so plainly, once, and keep everything in the Drive files only — the program works fine without it, it just won't have the visual dashboard.

**The dashboard is organized as four top-level pages, navigated with a top bar (page-swap, not one long scroll).** Update the dashboard in the same session the underlying fact changes.

| Page | What lives there | Dashboard collection(s) | Sourced from |
|---|---|---|---|
| **Career Compass** (home) | Current chapter, long-term direction (the mind map), a short one-line "this week's progress" acknowledgment (not a detailed list — the detail lives on References), a **Work Queue** subsection with three views — **Agenda** (upcoming calls/meetings, read straight from `prep`, sorted by date — no separate collection, so a scheduled call never has to be entered twice), **To-Do** (everything else: research, follow-ups, decisions — filterable Today/This week/By project/By priority/Waiting/Quick wins), and, when a task connector is linked, a **live read-only view of it** — and a **Bridge Guidance** subsection of concise one-liners, each with a "jump to detail" link into whichever page/tab actually has the full context | `profile` (+ `currentChapter`), `mindmap`, `prep`, `tasks`, `guidance` | Phase 1, Phase 4, every session |
| **Network & Opportunities** | Tab bar: People, Candidates, Outreach, Call Prep, **Career Coaching**, Interactions, Opportunities. Call Prep is tactical — specific to one upcoming conversation. Career Coaching is evergreen — the elevator pitch and bridge skills, independent of any single call; update it as the story sharpens, not per-contact | `network`, `candidates`, `outreach`, `prep`, `interactions`, `opportunities` — Career Coaching itself reads from the `mindmap` doc's `elevatorPitch`/`bridgeSkills` fields rather than its own collection | The networking engine and Meetings & Interviews sections |
| **Projects** | One card per active or recently-closed thing the person is building or running — purpose, current status, connection back to the Compass, its open tasks, and a running notes log the person (or Claude) can add to directly, right on the card | `projects` (including a `notes` array field: `{text, date}` entries), `tasks` | Phase 1's current-projects question; updated as projects start, pause, or close |
| **References** | Progress & Reflection (momentum stats, a weekly reflection, and the full career journal — kept here ONLY, styled small/supplemental, never duplicated elsewhere on the dashboard), Experience, Session Log | `reflections` (type `weekly` and `journal`), `experience`, `sessions` | Prompted weekly, or whenever the person wants to reflect; Phase 2; every session |

Match the field names already in the template rather than inventing a new shape — its rendering code expects those specific fields (check the template or an already-populated dashboard if unsure). A `guidance` item looks like `{ text, type: 'nudge'|'insight'|'alignment', relatedTo, done, chipLabel, linkPage, linkTab, linkTarget }`; a `task` looks like `{ text, done, priority: 'high'|'med'|'low', dueDate, waitingOn, waitingOnWho, quickWin, contextType: 'career'|'project', linkedProjectId, linkedProjectName, linkedContactName, linkedOpportunityTitle, agendaLinked, chipLabel, linkPage, linkTab, linkTarget }`; a `project` looks like `{ name, type, status: 'open'|'paused'|'closed', purpose, currentStatus, connection, tags, notes: [{text, date}] }`; an `opportunity` looks like `{ title, org, type: 'role'|'internship'|'program'|'collaboration'|'warm-path', status, sourceBridge, notes }`.

**Keep Bridge Guidance and To-Do text short — one line, not a paragraph.** Where a checklist item needs real detail (call prep for a specific person, a project's full context, an opportunity's history), put the detail on the page/tab that actually owns it, and give the item a `linkPage`/`linkTab`/`linkTarget`/`chipLabel` so clicking it jumps straight there.

**Keep Agenda and To-Do genuinely distinct.** A scheduled call or meeting belongs in `prep` (which the Agenda view reads from) and should NOT also get a duplicate `tasks` entry with the same "call with X" text — if a task like that already exists for some reason, mark it `agendaLinked: true` rather than deleting it. Everything else belongs in `tasks`, as a concrete action.

If the person has a task tracker connected and this environment's dashboard tooling supports a live, read-only connector view, wire one into the Work Queue so their real tool shows up alongside — not instead of — the Work Queue's own To-Do list. Keep it read-only unless the person explicitly asks for write-back and you've verified the exact call shape against that connector's tools first.

**For a first-time student, the Projects page starts as a generic template** — don't pre-fill it with categories that only fit a founder. Phase 1's current-projects question is what populates it, in the person's own words, whatever they're actually doing (or nothing at all, if that's the honest answer).

## Dashboard and the monthly rollup

The dashboard should show only what's in ACTIVE plus a small "history" count from DIGESTS. When the rollup (kernel §6) moves items to the archive, remove them from the dashboard collections in the same session. Do not let the dashboard database become a second, larger memory.
