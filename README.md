# sovereign-bridge

Runtime instructions for **Bridge**, a career-coaching Claude Project. Each user's own Claude fetches the files in this repo at the start of every chat, so instruction updates reach everyone without anyone re-pasting anything. This repo intentionally contains no product code, no student data, and no business documents — just the instruction text — so it can stay public while the rest of the project stays private.

- `current.md` — the kernel (startup behavior, memory system, update/rollup logic).
- `manifest.json` — current version, which cohorts are active, and pointers to the files below.
- `modules/` — the program content, fetched only when needed.
- `templates/` — blank starting files for a new user's data.
- `migrations/` — upgrade steps when the shape of stored data changes between versions.
- `CHANGELOG.md` — what changed in each release.

Maintained from `The-Guys-Team/the-guys` (private); see that repo's `dev/RELEASING.md` for the release process.
