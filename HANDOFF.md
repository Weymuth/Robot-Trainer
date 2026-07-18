# HANDOFF — robot-trainer · after Session 01 (2026-07-18)

## Baseline verification — do this first, unasked
1. git clone --depth 1 https://github.com/Weymuth/robot-trainer.git
2. Read LIVE_ROBOT_TRAINER.md in full. Confirm date 2026-07-18, Session 01, v0.1.
3. Read any DRAFT_*.md in full. (None exist as of Session 01.)
4. If LIVE_ROBOT_TRAINER.md is missing, older than 2026-07-18, or disagrees with
   this handoff — STOP and say so. Do not proceed on assumption.
5. Report what's live, then wait for today's task.

## Where things stand
Session 01 was design only. Nothing is built. The repo contains
LIVE_ROBOT_TRAINER.md and HANDOFF.md and nothing else.

robot-trainer is the student-facing delivery site. zumo owns all curriculum.
Scope is three features: reading verification (soft signal), AI support
(Tutor + Learning Mode), code submission via per-student GitHub repos.
Canvas keeps quizzes, grades, and static materials — do not rebuild them.

Infrastructure already exists: GitHub Pages hosts zumo; a Cloudflare Worker at
zumosupport.weymuthd.workers.dev proxies the AI Tutor with the API key held
server-side. Verified not exposed. The Worker is the intended home for auth,
tracking, and per-student state via KV or D1.

Build order: site shell first (no dependencies, useful on ship day), then
per-student repos before school starts, then tracking last.

## Standing rule
All deliverables are produced as downloadable files, every session, whether or
not DJ asks. Never paste a file's contents into chat as the only delivery.

## Open items — DON'T GUESS, ask DJ
- Cloudflare account access and whether the Worker source is available to read.
- Student identification method: school Google account, username/password, or code.
- Whether to export the one-lesson GitHub Classroom data before 2026-08-28.
- Textbook delivery: copy zumo files into robot-trainer, or read from zumo live.

## Parked — not now
- Teacher path (progress reports, issue tracking, error repair).
- Wiring the zumo → robot-trainer read.
- Zircon / 3Pi+ support.
- Weymuth/Robotics-I: created then abandoned. Delete or rename.

## Source of truth
The repo is the source of truth. LIVE_ROBOT_TRAINER.md beats memory and beats
this handoff. Grep the file; never trust a pasted version number.
robot-trainer NEVER writes to zumo. It reports; DJ fixes.
Student data never goes in a public repo.

## Hard dates
- 2026-08-28 — GitHub Classroom decommissioned.
- 2026-09-04 — Classroom data deleted.
- School start — target ship date for the site.

## Today's task:
