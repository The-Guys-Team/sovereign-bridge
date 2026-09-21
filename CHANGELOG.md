# Bridge changelog

Batch updates: collect changes, then ship one release (see `dev/RELEASING.md` in the `the-guys` repo — that folder is kept private, alongside onboarding materials and the test suite; this repo holds only what students' Claude sessions fetch at runtime). Never edit `current.md` in place without also bumping the version, adding an entry here, and updating `manifest.json`.

Versioning: `MAJOR.MINOR.PATCH`.
- **PATCH** — wording/tone fixes, no behavior change.
- **MINOR** — new or changed behavior; no change to the shape of student data.
- **MAJOR** — visual/experience overhaul (e.g., the planned version 6).
- **Schema version** (separate number in `manifest.json`) increases *only* when the shape of the student's Drive files changes. It always ships with a migration file.

---

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
