# Validation and release evidence

This document separates historical source-behavior evidence, local package checks, native-host checks, and release gates. A pass establishes only the fact named in its evidence boundary.

## Current source guard

`SKILL.md` at this revision has SHA-256:

```text
9A50FD52C2FCD4026C364406851107A78F5817E208C624C15ED249EA70471985
```

`agents/openai.yaml` and `LICENSE` are also copied byte-for-byte from the source package. This document records evidence boundaries and does not assign a package-wide review score.

## Current bounded file and browser checks

The installed, canonical and public skill copies were compared byte-for-byte. These checks prove named scenarios, not universal file or provider support.

| Check | Status | Evidence boundary |
| --- | --- | --- |
| Antigravity browser text | pass | Exact heading, paragraph and link verified after reading an offloaded source artifact. |
| Screenshot capture and image inspection | pass | Native image reader loaded the generated screenshot; concrete layout details matched the same image inspected by the lead. |
| PNG, UTF-8 Markdown and CSV | pass | Unprompted image markers/shapes, text markers and numeric total matched fixtures. |
| Native Antigravity PDF/DOCX/XLSX reader | unsupported | MIME errors; no access-denial bypass. |
| PDF/DOCX/XLSX extracted-content handoff | pass | Page markers, paragraphs/table rows, both sheets, cell values and formula/cache distinction preserved through format-specific readers. |
| Word page rendering and inspection | pass, bounded | LibreOffice rendered one DOCX fixture; native image reader and lead confirmed table, markers and no clipping/overlap. Not arbitrary complex-layout compatibility. |
| Image-only PDF | pass | Empty text extraction confirmed; rendered page was read as an image and all control text/numbers matched. |
| Spreadsheet recalculation | pass, bounded | Artifact Tool 2.8.59 recalculated SUM from 25 to 36 after changing an input in a disposable in-memory copy. Not Microsoft Excel compatibility proof. |

No claim covers arbitrary formulas, macros, password-protected files, unreadable scans, audio or video. Original files remained unchanged. Provider model aliases were requested; exact runtime versions were not independently confirmed.

## Historical instruction-only handoff update

The earlier handoff update was checked at SHA-256 `DDAAB3F07D85FE990636F9F9BA333A93D4EB3E246392D4612AD091F3809ABB70`. That update added only instructions for exact handoff paths and a suitable-reader prerequisite, evidence-based statuses, authorized per-run journal/privacy/denial guards, and the rule that lifecycle completion is not task success. It does not add an automatic collector, overview, database, script, HTML artifact, hook configuration, or telemetry.

| Check | Status | Evidence boundary |
| --- | --- | --- |
| Historical source-to-export `SKILL.md` hash | pass | Byte equality at the earlier handoff-update hash. |
| Structural skill validation | pass | `quick_validate.py` had already passed the identical source structure. |
| Native historical checks against the new guard hash | not run | Earlier native checks remain historical and were not rerun for this instruction-only update. |
| Separate local Codex journal pilot | pass, bounded | One task observed `Stop` and matching `SubagentStart`/`SubagentStop`; this does not validate all-chat telemetry or current skill behavior across hosts. |

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

This section records the local package state before the first repository commit and private push. At this snapshot, Git history did not yet exist and commit attribution had not yet been checked. See [Final public publication snapshot](#final-public-publication-snapshot--2026-09-06) for the later publication evidence.

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

## Final public publication snapshot — 2026-09-06

The user confirmed the right to publish this package under its unchanged MIT license. The initial public opening was verified at commit `4e45586ab190046ef7effc8968746c9ef517ab56`. Seven anonymous repository, README, and case HTTP checks confirmed public visibility, the exact commit, both raw README files, and their case links.

The live site deployed commit `4463334362719a7d55f711f33c2906c745bbe5fd`. Fresh browser checks covered the English and Ukrainian README benefits and case-link navigation. Twelve live UK/EN home, work, and case checks across desktop and mobile confirmed the exact GitHub URL and label, the case-page GitHub popup, reciprocal links, and preserved SEO metadata.

## Publication gates

Local package completion does not approve external action.

| Gate | Required evidence | Status |
| --- | --- | --- |
| Public repository and exact commit | User-confirmed MIT publication right; public visibility; exact commit; both raw README files and their case links checked anonymously | pass |
| Public repository, README, and case HTTP checks | Seven anonymous repository, README, and case HTTP checks | pass |
| README link to the live case | The package README links to the live case page | pass |
| Site case link to the repository | Fresh browser checks of the English and Ukrainian case pages, including the GitHub popup | pass |
| Reciprocal links and live UI | Twelve UK/EN home, work, and case checks across desktop and mobile; exact GitHub URL/label and SEO metadata retained | pass |

Prior reconnaissance found no available scanner. After separate user approval, the official portable Gitleaks v8.30.1 archive was verified against its release digest and the isolated export passed its directory scan. The final public snapshot also includes a full-history scan with zero findings. A fresh export repository must never inherit parent history, templates, hooks, or remotes.
