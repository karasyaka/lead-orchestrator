# Validation and release evidence

This document separates historical source-behavior evidence, local package checks, native-host checks, and release gates. A pass establishes only the fact named in its evidence boundary.

## Current source guard

`SKILL.md` is frozen for this package. Its SHA-256 is:

```text
FE3BD1820A058C80ACC7DCD3E36FB4450C3B795CA54EAA0FF9C06A6DE422CA98
```

`agents/openai.yaml` and `LICENSE` are also copied byte-for-byte from the source package. This document records evidence boundaries and does not assign a package-wide review score.

## Historical behavior and host evidence

The 28-scenario synthetic review on 2026-09-06 tested source SHA-256 `EFC29723C096CF460CE15F4CDE2876C6F3010B01C4FD98035B972B47F09B2763`, not the current source guard. All 28 scenarios passed independent semantic review of one fresh synthetic Claude response batch; this was manual instruction injection, not 28 native invocations or proof of discovery. It covered scope recovery, approval preservation, stopping, executor preference, capability boundaries, denied operations, and visual-artifact handling.

| Native or artifact check | Status | Evidence boundary |
| --- | --- | --- |
| Codex fresh desktop task | pass | Installed skill read; explicit preference and reset handled correctly. |
| Codex task with prior conversation | pass | Installed skill read; prior marker and edit-approval boundary retained. |
| Claude project-scoped fresh and resumed conversation | pass | Canonical policy expanded natively; existing marker recalled on resume; both processes exited 0 with closed streams. |
| Claude personal installation runtime | pass | One native invocation with user-skill discovery; transcript review matched the instruction body after metadata removal. |
| Antigravity CLI fresh conversation | pass | Runtime reported an expanded skill command after the nested installation was used. |
| Antigravity CLI resumed pre-installation conversation | pass | The same existing conversation expanded the skill after installation correction. |
| Antigravity already-running interactive session | not run | Check stopped at a workspace-trust prompt; no trust change was made. |
| Codex TXT reading | pass | Exact synthetic nonce returned. |
| Codex image access | pass | A blue circle was recognized. |
| Codex stylized image-number recognition | fail | Rendered `731` was read as `21`; visual access did not establish accurate reading. |
| Claude TXT/PDF reading | pass | One live call returned exact synthetic content after adapter repair. |
| Claude image delivery and basic inspection | pass | Image block received; blue circle identified. |
| Claude stylized image-number recognition | fail | Rendered `731` was read as `751`; exact-content interpretation did not pass. |
| DOCX, XLSX, audio, and video | not run | No completed end-to-end test covers these formats. |

The recorded Antigravity unattended-write failure remains a scoped hold for affected unattended writes until corrected and independently verified. It is not a provider-wide ban. Image delivery or a screenshot is not proof of accurate reading; consequential values require a source check.

## Package whitelist

The isolated repository must contain exactly these ten regular files:

1. `SKILL.md`
2. `agents/openai.yaml`
3. `README.md`
4. `README.uk.md`
5. `VALIDATION.md`
6. `LICENSE`
7. `CONTRIBUTING.md`
8. `CHANGELOG.md`
9. `.github/ISSUE_TEMPLATE/bug_report.md`
10. `.github/pull_request_template.md`

No hidden extras, generated files, images, binaries, symlinks, reparse points, submodules, internal audit material, private paths, session/account identifiers, or secret-like values may be exported. Image metadata is N/A because the package has no image. Use GitHub's default social preview unless separately approved assets exist.

## Historical pre-Git package check — 2026-09-06

This section records the local package state before the first repository commit and private push. At this snapshot, Git history did not yet exist and commit attribution had not yet been checked. See [Publication snapshot](#publication-snapshot--2026-09-06) for the newer private-publication evidence.

| Check | Status | Evidence boundary |
| --- | --- | --- |
| Source snapshot and protected-file comparison | pass | `SKILL.md`, `LICENSE`, and `agents/openai.yaml` matched the pre-change snapshot. |
| Skill validator | pass | `quick_validate.py` accepted the isolated export's `SKILL.md` front matter and instruction-file structure. |
| Exact export inventory | pass | Exactly ten regular whitelisted files; no `.git`, reparse point, or extra hidden file. |
| Source-to-export hashes and manifest | pass | All ten export files matched their source SHA-256; an internal manifest records names, hashes, and source mappings. |
| Markdown local targets and public-prose review | pass | Local targets resolved; review found no private-path, account-identifier, or secret-like pattern in the export. |
| Secret scanner | pass | Authorized official Gitleaks v8.30.1 directory scan: 44,025 bytes, zero findings, exit 0; redacted output. Git history does not exist yet and remains unscanned. |
| Commit author and GitHub noreply audit | not run | At this pre-Git snapshot, a first commit and its attribution did not yet exist. |

The Windows-host validator was run once through the configured compact-output wrapper. Its tool locations are intentionally not part of the public package.

## Compatibility references

- Codex: <https://learn.chatgpt.com/docs/build-skills>. Current documentation uses `~/.agents/skills/<name>` or `.agents/skills`; older `~/.codex/skills` installs were tested on this host and are not auto-migrated.
- Claude Code: <https://code.claude.com/docs/en/skills>. Personal skills use `~/.claude/skills/<name>/SKILL.md`; project skills use `.claude/skills/lead-orchestrator/SKILL.md`.
- Antigravity: <https://antigravity.google/docs/cli/plugins/>. Documentation describes a flat layout, while recorded host runtime evidence used `~/.gemini/antigravity-cli/skills/<name>/SKILL.md`.

Native discovery must be checked in each actual host. Manual loading by full path is a fallback and does not prove native discovery.

## Publication snapshot — 2026-09-06

The user confirmed the right to publish this package under its unchanged MIT license. The first private publication used a verified GitHub noreply address for commit attribution; no personal email was placed in the commit. The new repository was confirmed private after push, with the approved root commit and the ten-file tree.

The linked case page is live. It intentionally has no repository backlink while the repository remains private. Public visibility has user approval, but the visibility change and an anonymous check of the public repository, README, and reciprocal links are still pending.

## Publication gates

Local package completion does not approve external action.

| Gate | Required evidence | Status |
| --- | --- | --- |
| Fresh repository creation and private push | Approved creation; rights/licensing review; GitHub noreply attribution; exact root commit and ten-file remote tree | pass |
| Private repository verification | Confirmed private visibility, default branch, and exact remote tree | pass |
| README link to the live case | The package README links to the live case page | pass |
| Site case link to the repository | Add only after public visibility and anonymous repository/README proof | pending |
| Public visibility and anonymous verification | User approval is recorded; change visibility, then check the public repository, README, and reciprocal links without authentication | pending |

Prior reconnaissance found no available scanner. After separate user approval, the official portable Gitleaks v8.30.1 archive was verified against its release digest and the isolated export passed its directory scan. The later private publication does not substitute for the public visibility check or an anonymous check after that change. A fresh export repository must never inherit parent history, templates, hooks, or remotes.
