# Changelog

All notable public-package changes are documented here after review and release approval.

## 2026-09-08

- Require finite prompt input and the installed launcher for available Claude-to-Codex handoffs, explicit task-fit model/effort, and progress checks before retries. This instruction change is not enforcement over already-running chats.

## v0.1.0 — 2026-09-06

- Added instruction-only handoff guards in `SKILL.md`: give the receiving executor the exact current working directory and artifact paths only when a suitable reader exists; otherwise report the missing prerequisite as blocked without guessing paths.
- Added visible evidence-status, per-run journal privacy, and access-denial guards. A terminal executor lifecycle event, including `Stop` or `SubagentStop`, is not task-success evidence.
- This update does not include an automatic collector, overview, database, script, HTML artifact, hook configuration, or background telemetry.

## 2026-09-06

- Prepared local publication documentation, contributor guidance, and issue/pull-request templates.
- Expanded the English and Ukrainian README files with purpose, intended behavior, suitable use cases, and bounded invocation examples.
- Published the package and recorded anonymous repository, README, case-link, full-history scan, and live reciprocal-link evidence.
- Added the GitHub action to the English and Ukrainian home, work, and case surfaces after public verification.
- Added no dependency, runtime, or `SKILL.md` behavior change.
- Historical native-host and format limitations remain documented in `VALIDATION.md`; publication does not establish universal host compatibility or accurate interpretation of consequential image values.
