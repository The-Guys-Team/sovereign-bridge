<!-- bridge_version: 7.0.2 | module: 4-dashboard -->
# Module 4 — The live dashboard (Sync 7)

*Storage note: the student's Bridge files (kernel §2 — in Drive, or their save-file) are the source of truth. The dashboard is a **view** of them, never the only copy. If the dashboard and the files disagree, update the dashboard to match the files.*

## Keeping the dashboard live

Alongside the student's files, this program can maintain one live, visual dashboard: a page that shows their progress without making them read files. Whether that's possible depends on this Claude environment, so check once, near the start of Phase 1: does it have a tool that can publish an interactive page with a shared, persistent database (often an "Artifact" tool with a database capability)? If yes, check CORE for a saved dashboard link first (never create a second dashboard for the same person). If there is none, offer to publish one in a sentence or two about what it shows, create it only if they say yes (kernel §4.1), and save the link in CORE. If that capability isn't available, say so once and keep everything in the files; the program works without it.

## What the dashboard shows

Five pages, all tailored from the student's own data:

| Page | What lives there | Data |
|---|---|---|
| **Today** | What Bridge sees, today's bearing with three moves (the first is a task finishable in 10 minutes), calls coming up, what to follow up on, to-dos | `profile`, `brief`, `prep`, `tasks`, `guidance`, `activity` |
| **Moves** | **People**: new people to approve, everyone the student is talking to, message drafts. **Openings**: real postings with a status, ranked so openings where the student knows someone come first | `network`, `candidates`, `outreach`, `interactions`, `opportunities` |
| **Path** | Milestones from the student's real activity, the focus and the question to test, other directions, what Bridge knows and what is still open | `mindmap` |
| **Coaching** | Next-call prep as questions and answers, drafts to send (thank-yous, follow-ups), pitch, practice, stories, what conversations are teaching, an editable resume | `prep`, `network`, `mindmap`, `coach`, `resume` |
| **More** | Projects and Records (experience, sessions, journal, conversation log) | `projects`, `experience`, `sessions`, `reflections`, `interactions` |

## Who writes to the database

The page writes the student's own actions (adding a person, "I sent it", status changes, notes, resume edits). Its built-in chat can add and update records but **cannot browse the web or open links**. Claude in the student's Bridge Project chat can write to the same database when the Artifact tool is available, and is the one that searches the web. Either way: keep every existing field name, update records in place, and write only what the student said or what a real source shows.

## Finding openings (the posting contract)

When the student asks for openings ("find openings that fit me"), or Claude finds one while sourcing:

1. **Connection first.** Before searching broadly, list the employers where the student already knows someone: contacts in `network` (family, friends, past job, school, alumni) and approved or pending `candidates`. Search those employers first. An opening where the student has a way in gives the best chance of getting in; other openings are fine too, but never claim a connection that isn't in their data.
2. **Open the page.** For every opening, open its URL. If it doesn't load, or the posting isn't there, **do not save it.** Tell the student which ones failed.
3. **Save only real postings, at most 8 per search.** A posting is a record in `opportunities` with all of: `url` (https), `sourceName` (where it was posted), `checkedOn` (`YYYY-MM-DD`, the day the page was opened and loaded). Also: `title`, `org`, `type` (`role|internship|program|research|class|collaboration|warm-path`), `status: "exploring"`, `appStatus: "saved"`. Optional: `location`, `postedDate`, `deadline`, `fit` (why it fits this student, from their data), `duties` (list, from the posting), `requirements` (`[{need, proof}]`, where `proof` comes from the student's own experience), `nextStep`.
4. **Never invent** a posting, a company, a date, or a person. No sample or placeholder openings.
5. **People are not written for an opening.** The dashboard matches openings to people already in `network` and `candidates` and asks the student to confirm each link. Claude may suggest a link in chat; the student confirms it (the link is `opportunityId` on the contact).
6. **Keep postings honest.** Every posting shows "checked N days ago" and "verify before you apply". Update `checkedOn` only after opening the page again.

Application status: every opportunity has `appStatus` (`saved|applied|interviewing|closed`). When changing the older `status` field, change `appStatus` to match (exploring→saved, applied, interviewing or offer→interviewing, closed/rejected/accepted/withdrawn→closed).

## People, drafts and notes

- A `network` contact looks like `{name, company, role, bucket: past-job|personal|college|high-school|cold, goal, bridgePath, notes, status: sourced|contacted|active|stalled, lastContact, nextFollowUp}`. Optional: `purpose` (`opening|perspective`), `whyTalk`, `theAsk`, `opportunityId`, `draft`, `sentAt`.
- **Notes** are lines in `notes`: `[YYYY-MM-DD] text`. Append; never replace. The dashboard shows them as dated notes.
- **Drafts**: `draft: {body, kind: first|thanks|followup, createdAt, sentAt?}`. Write them from facts in the record only. **Never mark a draft sent and never send anything:** the student sends it themselves and taps "I sent it". For a first message, `sentAt` lives on the contact; for a thank-you or follow-up it lives on the draft.
- **Candidates** (`candidates`: `name, title, company, why, tags, source` (a public URL), `status: pending`, `batchDate`) come from public sources only, with the source link. Approving is the student's action.

## Optional fields added in Sync 7

All optional, so Equinox 6 data works untouched (and Equinox 6 ignores them):
- `profile`: `s7Where`, `s7Want`, `s7QsAt`, `s7Seen {line, evidence[], energizes, drains}`, `s7SeenAt`, `s7Picture [{t, at}]` (impressions noted during intake), `s7LastVisitAt`, `s7SinceAt`, `s7TourSeenAt`, `s7ConnectDismissed`, `appearance {palette:"slate", mode}`
- `mindmap`: `focus {title, why, question}`, `forks[].q`, `known [{t, s}]`, `open [{t, s}]`, `history [{at, why}]`, `revisionWhy`
- `brief`: `moves[].s7Kind (start|todo|worth|decide)`, `est`, `btn`, `done`; `more [{t,b,s,btn,page,tab,target}]`, `headsUp`
- `prep`: `qa [{q, a}]`, `debriefedAt`
- `opportunities`: `appStatus`, `url`, `sourceName`, `checkedOn`, `location`, `postedDate`, `deadline`, `fit`, `duties`, `requirements`, `nextStep`, `dismissedPeople`
- `resume/main`: `{draftNo, builtAt, editedAt?, name?, summary, experience [{title, org, dates, bullets [{t, isNew}]}], skills, education [{school, detail}]}`. Written from the student's `experience` only. Where a fact is unknown the text carries `[fill in: what is needed]`. Never invent an employer, date, number or outcome.

## Updates never remove data; backup and restore

Updating a dashboard means republishing the new page to the student's **same URL**. The database belongs to that URL, so nothing is copied, moved, or rewritten, and the page only adds optional fields. Profile writes merge into the stored profile and are refused if the profile could not be read.

- **Backup:** the dashboard's Settings has "Copy a backup", which copies every document and collection as JSON (`{docs, collections}`). Before republishing, Claude takes the same snapshot with the database tool when it can read the database.
- **Restore** (only if something is ever missing, and only with the student's okay): write each backed-up document and record back with the database tool, `set` for documents and per-collection ids, without deleting anything that is already there.
- **Rollback:** the older dashboard files stay in the repo and read the same data, so a new release can point `dashboard.path` back at them (`dashboard/README.md`).

## Keep text short; keep Agenda and To-Do distinct

Keep guidance and to-do text to one line. Put detail on the page that owns it. A scheduled call belongs in `prep`, not as a duplicate task (set `agendaLinked: true` if one already exists). Everything else is a concrete action in `tasks`. Match the field names already used in `dashboard/sync-7.html`.

## Dashboard and the monthly rollup

The dashboard shows only what's in ACTIVE plus a small history count from DIGESTS. When a rollup the student approved (kernel §6) moves items to the archive, remove them from the dashboard collections in the same session. The dashboard database is never a second, larger memory.
