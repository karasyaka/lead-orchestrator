# Lead Orchestrator

Lead Orchestrator is a compact coordination skill for AI coding work that must continue while keeping its available decisions, scope, and approval boundaries in view. It tells an agent how to recover the task, choose a proportionate next action, and report evidence at the end.

Use it for a multi-step task, a handoff, or a task with constraints that the next agent must preserve. A trivial, self-contained edit usually does not need this workflow. The intended behavior is to keep the stated boundaries in view, delegate only authorized work when that helps, and make the result and remaining uncertainty clear. It provides instructions only; it does not add tools, accounts, memory, permissions, a server, or a separate running agent.

## What it helps with

- Recover the available task context before choosing the next action.
- Preserve stated scope, approvals, and unrelated work already in progress.
- Use bounded delegation when appropriate, then report evidence and blockers.

[Українською](README.uk.md) · [Validation](VALIDATION.md) · [Contributing](CONTRIBUTING.md)

[Read the project case study](https://hrybachov.com/en/cases/lead-orchestrator) for the problem, implementation scope, and current limitations.

## A practical use

You are preparing a release in a repository with unrelated work already in progress. Ask the agent to use Lead Orchestrator, recover the agreed scope, delegate a bounded task if appropriate, and preserve the unrelated changes. A request such as “plan only” or “do not deploy” remains a boundary; coordination is not permission to change production.

## Quick start

Use this package as the single source of truth. Install it in one host-specific `lead-orchestrator` folder, then invoke it in a new or existing conversation.

### Codex

Current Codex documentation uses a personal `~/.agents/skills/lead-orchestrator/` folder or a repository `.agents/skills/lead-orchestrator/` folder. This host previously tested the older `~/.codex/skills/lead-orchestrator/` location. Check your host documentation and current installations before choosing one.

Copy these files while preserving their relative paths:

```text
SKILL.md
agents/openai.yaml
```

For a personal installation, the layout is:

```text
~/.agents/skills/lead-orchestrator/SKILL.md
~/.agents/skills/lead-orchestrator/agents/openai.yaml
```

For a repository installation, use `.agents/skills/lead-orchestrator/` with the same layout. Do not install duplicate copies in old and current Codex locations unless you intentionally maintain both; there is no automatic migration or synchronization.

In a new or existing conversation:

```text
Use $lead-orchestrator to continue this task within the agreed scope.
```

## Prompts and expected response shape

Use a short instruction that names the boundary you need preserved. A response should state the recovered objective, scope, evidence, and any blocker in plain language; its exact wording depends on the host and task.

Plan without edits:

```text
Use $lead-orchestrator to plan this release only. Do not edit files or deploy.
```

Expected shape: a proposed scope, the next read-only checks, material risks, and no edits or deployment.

Prefer a suitable executor:

```text
Use $lead-orchestrator to continue this task. Prefer Claude for suitable delegated work.
```

Expected shape: the task continues under the existing permissions; a suitable delegated task may use that preference, and any deviation is explained.

Keep delegation exclusive or reset it:

```text
Use only Claude for delegated work on this task.
Return to automatic selection for this task.
```

Expected shape: `only` stops dependent delegated work if the requested executor cannot satisfy it; `automatic` clears that preference for future assignments. Neither instruction adds host permissions or restarts work already running.

If native discovery has not refreshed in an already open conversation, ask the agent to read the installed `SKILL.md` by its full path. That is manual loading, not proof that native `$lead-orchestrator` discovery works.

See the [Codex skill documentation](https://learn.chatgpt.com/docs/build-skills).

### Claude Code

For a personal skill, copy `SKILL.md` to:

```text
~/.claude/skills/lead-orchestrator/SKILL.md
```

For a project skill, use this exact file path:

```text
.claude/skills/lead-orchestrator/SKILL.md
```

Claude Code does not use `agents/openai.yaml` for this skill.

In a new or existing Claude Code conversation:

```text
/lead-orchestrator Continue the current task within the agreed scope.
```

See the [Claude Code skills documentation](https://code.claude.com/docs/en/skills).

### Antigravity CLI

Copy `SKILL.md` unchanged to the nested layout tested on this host:

```text
~/.gemini/antigravity-cli/skills/lead-orchestrator/SKILL.md
```

Antigravity documentation describes a flat layout, while the recorded local runtime test used the nested layout above. Verify discovery in your environment with `/skills`, then invoke `/lead-orchestrator` in a new or existing session. IDE locations can differ.

See the [Antigravity CLI plugin documentation](https://antigravity.google/docs/cli/plugins/).

## Choose an executor

State the preference in ordinary language:

```text
For this task, prefer Claude for suitable delegated work.
Use only Claude for delegated work.
Return to automatic selection for this task.
```

`prefer` selects the requested executor when suitable and authorized, and explains a deviation. `only` stops dependent work if that executor cannot meet the task or required review. `auto` returns to the host's ordinary proportional choice. A preference applies to the task unless explicitly extended to the current chat; it does not restart running work or transfer to another chat. Reported quota percentages are unverified planning hints, not a verified balance, routing authority, or a promise of zero lead cost. These preferences do not grant tools, permissions, account access, or a provider call.

## Update or uninstall safely

Before an update, resolve and inspect the exact installed `lead-orchestrator` folder. Replace only files in that folder from this source package, preserving the host-required layout. For Codex, compare both installed `SKILL.md` and `agents/openai.yaml` with the source after copying.

To uninstall, remove only the resolved `lead-orchestrator` folder. Do not remove a parent `skills` folder. Removal does not erase instructions already loaded into an active conversation; ask that conversation to leave lead mode.

## Compatibility and boundaries

- The skill depends on host tools, permissions, instructions, and executor capabilities. It has no package or server dependency of its own.
- Historical evidence covers Codex delivery of TXT and images, and Claude delivery of TXT/PDF and images. It does not establish universal host compatibility.
- Visual access is not proof of accuracy. OCR can fail; check consequential image values against their source.
- DOCX, XLSX, audio, and video were not tested and remain host-dependent.
- A recorded Antigravity unattended-write failure places a scoped hold on affected unattended writes until corrected and independently verified. It is not a global provider ban.
- The skill does not transfer chat history, credentials, file access, or permissions between hosts.

## Privacy and troubleshooting

Lead Orchestrator does not collect telemetry or create persistent memory by itself. It works only with context and tools your host already exposes. Review the host's data handling and project instructions before giving an agent sensitive material.

| Symptom | What to check |
| --- | --- |
| The skill is not listed | Confirm the host-specific path and refresh discovery as required. Manual file loading in an existing conversation is a separate fallback. |
| The agent edits after “plan only” | Stop the task and restate the boundary. Report a reproducible issue if explicit scope or approval limits are not preserved. |
| An executor preference cannot be met | `prefer` may use a suitable authorized alternative; `only` should stop dependent work and explain why. |
| An image value matters | Check the original source; delivery or a screenshot does not establish OCR accuracy. |
| An Antigravity write is unattended | Keep the affected write on hold until the recorded behavior is corrected and independently verified. |

## Package contents

| File | Purpose |
| --- | --- |
| `SKILL.md` | Portable behavior instructions |
| `agents/openai.yaml` | Codex display metadata and default prompt |
| `README.md` | English installation and use guide |
| `README.uk.md` | Ukrainian installation and use guide |
| `VALIDATION.md` | Evidence boundaries and release checks |
| `LICENSE` | MIT license |
| `CONTRIBUTING.md` | Focused contribution guidance |
| `CHANGELOG.md` | Current local-package note and release history policy |
| `.github/ISSUE_TEMPLATE/bug_report.md` | Reproducible behavior report template |
| `.github/pull_request_template.md` | Focused pull-request checklist |

## Validation and license

Read [VALIDATION.md](VALIDATION.md) before treating the package as ready for publication. File validation, source behavior evaluation, native discovery, and public-release checks establish different facts.

This package is available under the [MIT License](LICENSE). It is not presented as officially endorsed by OpenAI, Anthropic, Google, or another provider.
