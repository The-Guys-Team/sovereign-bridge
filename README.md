# sovereign-bridge

Method documents for **Bridge**, a career-coaching Claude Project. This repo intentionally contains no product code, no student data, and no business documents — just the method text — so it can stay public while the rest of the project stays private.

## How updates reach a student

Each student's Project contains a small, fixed bootstrap. At the start of a chat it:

1. **Reads `manifest.json` from `main`** to see the latest version and what's new.
2. **Asks the student to approve** any version newer than the one they're on. Nothing changes unless they say yes.
3. **Fetches the files pinned at tag `v<version>`** (e.g. `https://raw.githubusercontent.com/The-Guys-Team/sovereign-bridge/v5.2.0/current.md`). Every link inside those files points at the same tag, so a student always gets one consistent version.

Tags are never moved or rewritten, so an approved version stays exactly what the student approved. Only `manifest.json` is read from `main`.

## Files

- `current.md` — the kernel (how a session starts, the memory system, rollup and migration rules).
- `manifest.json` — latest version, what's new, active cohorts, and pointers to the files below.
- `modules/` — the program content, fetched only when needed.
- `templates/` — blank starting files for a new student's data.
- `migrations/` — upgrade steps when the shape of stored data changes between versions (run only with the student's okay).
- `CHANGELOG.md` — what changed in each release, plus the release rules.

Maintained from `The-Guys-Team/the-guys` (private); see that repo's `dev/RELEASING.md` for the release process.
