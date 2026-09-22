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
