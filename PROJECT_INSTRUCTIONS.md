# Project Instructions — robot-trainer (Delivery)

## Scope
This project owns DELIVERY: the student-facing site, per-student state, and the
mechanics of getting content to students. It does not own curriculum content.

Repo boundary:
- Weymuth/zumo AUTHORS: curriculum, designs, styles, Learning Mode prompts,
  diagnostic logs, book edit queue. robot-trainer NEVER writes to zumo.
- Weymuth/robot-trainer DELIVERS: site, routing, auth, per-student progress,
  tracking, page assembly.
- Learning Mode may surface book problems. robot-trainer REPORTS them; DJ fixes
  them in zumo. Reporting is not editing.
- If a task requires changing content, design, style, or curriculum, stop and say so.
- Future platforms (Zircon, 3Pi+) get their own content repos. This site reads
  from them; it never holds a book.

## Source of truth
The repo is the source of truth. Everything lives at
github.com/Weymuth/robot-trainer

LIVE_ROBOT_TRAINER.md is the single source of truth for project state.
If memory and LIVE_ROBOT_TRAINER.md disagree, the file ALWAYS wins.
Never trust a version number pasted into chat. Grep the actual file.

## Session open — do this automatically, unasked
1. git clone --depth 1 https://github.com/Weymuth/robot-trainer.git
2. Read LIVE_ROBOT_TRAINER.md — verify date / status / currently-working-on.
3. Read DRAFT_*.md in full if any exist.
4. Report what's live, then proceed.

Never wait for an upload of a file already in the repo. Only ask for a file if it
is genuinely not there (a new working draft, a photo, a screenshot).
If the clone fails, or LIVE_ROBOT_TRAINER.md is missing or stale, STOP and say so.

## Deliverables are always downloadable
Any file produced in a session — LIVE, DRAFT, HANDOFF, site files, code, reports,
grading records — is written to disk and presented as a downloadable file.
Never paste a file's contents into chat as the only delivery method.
Chat may show a summary or an excerpt; the file itself is always downloadable.
This applies whether or not DJ asks.

## Verify every push — never take "pushed" on faith
When DJ says "pushed," "committed," "it's up," or anything equivalent, VERIFY
before treating the session as closed or the state as locked:
1. Re-clone the repo fresh (do not reuse an earlier clone — it is stale).
2. Confirm every file from this session is present.
3. Confirm each file MATCHES what was generated — compare checksums, do not
   trust filenames alone. A file can exist and still be the wrong version.
4. Confirm LIVE_ROBOT_TRAINER.md shows the expected date, session, and version.
5. Report MATCH or DIFFERS per file. If anything differs or is missing, say so
   plainly and do not close the session.

This is the same principle as "grep the file, never trust a pasted version
number" — a spoken confirmation is not evidence. Verification is cheap; a
session closed on an unverified push means the next session starts from a
baseline that does not exist.

## What lives where
- Repo: locked/stable state — LIVE_ROBOT_TRAINER.md, site files, reference material.
- DRAFT_<name>.md: in-flight state too large for memory. Deleted once it locks.
- Memory: in-flight, not-yet-locked state only. Once locked, it moves to
  LIVE_ROBOT_TRAINER.md and is pruned from memory. Never both.

## LIVE_ROBOT_TRAINER.md format
Per subsystem: current filename + one-line status.
Nothing older. Superseded filenames are REMOVED, not annotated.

## Session close — load-bearing, do not skip
As the LAST step of every chat, without being asked:
1. Propose the LIVE_ROBOT_TRAINER.md delta (what changed, what locked).
2. Propose the memory delta (add / remove / replace).
3. Wait for explicit approval before anything is treated as locked.
4. ALWAYS produce, every session, no exceptions, as DOWNLOADABLE FILES:
   a. Complete regenerated LIVE_ROBOT_TRAINER.md (full replacement, never a patch).
   b. Complete regenerated DRAFT_*.md files, if any.
   c. HANDOFF.md — copy-paste handoff for the next chat, built from the approved
      deltas and final files, NOT from memory. Committed to the repo, overwritten
      each session. No history kept.

HANDOFF.md must contain: baseline verification (clone, confirm files and dates,
read DRAFT in full, STOP if stale); current state of work; open items flagged
DON'T GUESS; parked items; source-of-truth reminder; blank "Today's task:" line.

Without this step the system drifts within ~2 sessions.

## Student data
Per-student progress and diagnostics are NOT committed to a public repo.
They live Worker-side (KV/D1) or in a private store. Students cannot read or edit
their own progress files.

## Versioning
major = v#, moderate = v#.#, minor = v#.#.#. No letter suffixes.

## Archive policy
Old versions are DELETED, not archived. Local drive is the archive.

## Grading sessions
One session per assignment, all students in it. Results written to a persistent
file at close so the next session reads prior scoring and stays consistent.
The grading record is delivered as a downloadable file like everything else.
