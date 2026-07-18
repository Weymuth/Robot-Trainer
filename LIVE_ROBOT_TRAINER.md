# LIVE — robot-trainer
**Date:** 2026-07-18 · **Session:** 01 · **Version:** v0.1

## Currently working on
Nothing built. Design locked this session; no code, no site, no files committed
beyond LIVE_ROBOT_TRAINER.md and HANDOFF.md.

## Subsystems

| Subsystem | Current file | Status |
|---|---|---|
| Site shell | — | Not started. GitHub Pages. First build target. |
| Textbook delivery | — | Not started. Reads from zumo, mechanism undecided. |
| AI Tutor | zumo/tutor.html | LIVE in zumo. Worker proxy confirmed. Link only for now. |
| Learning Mode | zumo/ZUMO_LEARNMODE_L03.md, zumo/L04_LEARNMODE_LOG.md | Prompt pattern exists as chat practice + 2 logs. Not a page. |
| Worker / API proxy | zumosupport.weymuthd.workers.dev | LIVE. Key server-side, not exposed. Source not yet reviewed. |
| Auth | — | Not started. Student ID method UNDECIDED. |
| Open-tracking | — | Not started. Worker + KV/D1. Build last. |
| Code submission | — | Not started. Per-student repos, browser upload. |
| Grading record | — | Not started. Persistent file, written at session close. |

## Locked decisions
- Repo: Weymuth/robot-trainer. Delivery only.
- zumo owns curriculum, Learning Mode prompts, diagnostic logs, book edits.
- robot-trainer reports book problems; DJ fixes them in zumo.
- Future platforms get own content repos. This site holds no book.
- Canvas keeps quizzes, grades, static materials. Not rebuilt here.
- Scope: reading verification (soft signal), AI support, code submission. Nothing more.
- Stack: GitHub Pages + Cloudflare Worker + KV/D1 + per-student repos.
- No GitHub Classroom — decommissioned 2026-08-28, sign-ups already closed.
- Code submission via browser upload, not VS Code git. VS Code git failed with
  students last year; the Classroom VS Code extension was unmaintained since 2021.
- Reading verification is a soft signal: opens, scroll depth, dwell time.
  Canvas quizzes remain the comprehension check.
- Student progress stored Worker-side, student-unreadable and student-uneditable.
- Build order: site → repos → tracking.
- Class size 8–12.
- All session deliverables are produced as downloadable files.

## Open — DON'T GUESS
- Cloudflare account access and Worker source availability.
- Student identification: school Google account vs username/password vs code.
- Export one-lesson GitHub Classroom data before 2026-08-28, or let it delete.
- Textbook delivery mechanism: copy files in, or read from zumo live.

## Parked
- Teacher path: progress reports, issue tracking, error repair workflow.
- Wiring the zumo → robot-trainer content read.
- Zircon / 3Pi+ platform support.
- Weymuth/Robotics-I (created then abandoned) — delete or rename.

## Hard dates
- 2026-08-28 — GitHub Classroom decommissioned; data inaccessible after.
- 2026-09-04 — Classroom data permanently deleted.
- School start — site should ship before this.
