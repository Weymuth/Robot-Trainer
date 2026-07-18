# LIVE — robot-trainer
**Date:** 2026-07-18 · **Session:** 02 · **Version:** v0.2

## Currently working on
Site shell built and delivered. Static HTML/CSS, no dependencies, no build step.
Five site files plus README and .gitignore. Nothing else started.

## Subsystems

| Subsystem | Current file | Status |
|---|---|---|
| Site shell | index.html, style.css, textbook.html, tutor.html, submit.html | Built v0.2. Entry-hall landing, 3-route nav, honest placeholders. Not yet pushed. |
| Textbook delivery | textbook.html | Stub page only. Reads from zumo, mechanism UNDECIDED. |
| AI Tutor | zumo/tutor.html | LIVE in zumo. tutor.html here is a stub; link-out not yet added. |
| Learning Mode | zumo/ZUMO_LEARNMODE_L03.md, zumo/L04_LEARNMODE_LOG.md | Prompt pattern as chat practice + 2 logs. Not a page. |
| Worker / API proxy | zumosupport.weymuthd.workers.dev | LIVE. Key server-side, not exposed. Source not yet reviewed. |
| Auth | — | Not started. Student ID method UNDECIDED. |
| Open-tracking | — | Not started. Worker + KV/D1. Build last. |
| Code submission | submit.html | Stub page only. Per-student repos, browser upload. |
| Grading record | — | Not started. Persistent file, written at session close. |

## Locked decisions
- Repo: Weymuth/robot-trainer. Delivery only.
- Student-facing name: **Robot Trainer** (provisional — reopen if a better name lands).
- zumo owns curriculum, Learning Mode prompts, diagnostic logs, book edits.
- robot-trainer reports book problems; DJ fixes them in zumo.
- Future platforms get own content repos. This site holds no book.
- Canvas keeps quizzes, grades, static materials. Not rebuilt here.
- Scope: reading verification (soft signal), AI support, code submission. Nothing more.
- Stack: GitHub Pages + Cloudflare Worker + KV/D1 + per-student repos.
- No GitHub Classroom. One-lesson data will NOT be exported — let it delete.
- Code submission via browser upload, not VS Code git. VS Code git failed with
  students last year; the Classroom VS Code extension was unmaintained since 2021.
- Reading verification is a soft signal: opens, scroll depth, dwell time.
  Canvas quizzes remain the comprehension check.
- Student progress stored Worker-side, student-unreadable and student-uneditable.
- Build order: site → repos → tracking.
- Class size 8–12.
- Landing page is an entry hall, not a dashboard. A dashboard requires auth and
  tracking; neither exists.
- Shell is static HTML/CSS with no framework, no build step, no dependencies.
- All session deliverables are produced as downloadable files.
- Every push is verified by fresh re-clone + checksum match before session close.
  A spoken "pushed" is not evidence.

## Open — DON'T GUESS
- Cloudflare account access and Worker source availability.
- Student identification: school Google account vs username/password vs code.
- Textbook delivery mechanism: copy files in, or read from zumo live.
- tutor.html should link out to the live zumo Tutor — exact URL not confirmed.

## Parked
- Teacher path: progress reports, issue tracking, error repair workflow.
- Wiring the zumo → robot-trainer content read.
- Zircon / 3Pi+ platform support.
- Weymuth/Robotics-I (created then abandoned) — delete or rename.
- Custom webfonts. Shell uses system-stack fallbacks; no files hosted.

## Hard dates
- School start — site should ship before this.
