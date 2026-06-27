# Codex Project Health Skills

Two lightweight Codex skills for keeping long-running AI projects understandable:

- `project-health-audit`: scan project structure, entrypoints, skill hygiene, and navigation health.
- `thread-handoff`: compress long tasks into a faithful context summary and optionally deliver it to a new thread.

Chinese documentation: [README.zh-CN.md](README.zh-CN.md)

## What Problem This Solves

AI coding and knowledge-work projects tend to fail in quiet ways:

- project rules grow but nobody knows which files are authoritative;
- too many always-on skills or tools pollute context;
- vaults, repos, and automation folders get judged by the wrong standards;
- long threads lose decisions after compaction or restart;
- the next agent receives a wall of history instead of a usable handoff.

These skills split the work into two focused actions:

1. audit the project without changing it;
2. package the current task state so another thread can continue safely;
3. deliver that package to another thread when thread-management tools are available.

## Included Skills

### `project-health-audit`

Use this when you want Codex to inspect a repo, workspace, Obsidian vault, or mixed project and produce a read-only health report.

It checks:

- project boundaries and nested roots;
- rule files such as `AGENTS.md`, `CLAUDE.md`, `README.md`, `schema/`, or docs entrypoints;
- navigation surfaces such as `index`, `overview`, `log`, or changelog files;
- source-to-reference links and thin cross-links;
- active skill directories, duplicated skills, and overgrown always-on skill surfaces;
- likely false positives that come from applying code-repo assumptions to non-code projects.

The expected output separates:

- confirmed issues;
- likely false positives;
- optional improvements;
- actions that require user confirmation.

### `thread-handoff`

Use this when a task is too long, has been compacted, needs a fresh thread, or must be handed to another agent.

Its primary job is compression with fidelity: preserve the decisions, constraints, evidence, current state, and next step while dropping noise. It is not a project audit skill.

It captures:

- role and scope;
- goal;
- must-preserve constraints;
- current state;
- completed work;
- verification status;
- blockers and open risks;
- next safest step;
- failed paths not to repeat;
- possibly missing or unchecked context;
- context the next thread can ignore.

If the user asks to send the handoff to a new or existing thread, the skill should use available Codex thread-management tools. If no delivery tool is available, it falls back to a copyable handoff summary.

## Installation

Clone the repository:

```bash
git clone https://github.com/anklecrusher/codex-project-health-skills.git
```

Copy the skills into your Codex skills directory:

```bash
mkdir -p ~/.codex/skills
cp -R codex-project-health-skills/skills/project-health-audit ~/.codex/skills/
cp -R codex-project-health-skills/skills/thread-handoff ~/.codex/skills/
```

On Windows PowerShell:

```powershell
$skills = Join-Path $env:USERPROFILE .codex\skills
New-Item -ItemType Directory -Force -Path $skills | Out-Null
Copy-Item -Recurse -Force .\codex-project-health-skills\skills\project-health-audit $skills
Copy-Item -Recurse -Force .\codex-project-health-skills\skills\thread-handoff $skills
```

Restart Codex or open a new thread if the skill list does not refresh immediately.

## Usage

Example prompts:

```text
Use project-health-audit to audit this workspace. Stay read-only and separate confirmed issues from false positives.
```

```text
Use project-health-audit to check whether my always-on skills are too broad or duplicated.
```

```text
Use thread-handoff to create a clean handoff for a new thread. Include verified work, open risks, and the next safest step.
```

```text
Use thread-handoff to compress this long task before context compaction.
```

## When To Use Which Skill

Use `project-health-audit` when:

- starting work in an unfamiliar project;
- project rules or entrypoints feel unclear;
- a knowledge base, repo, or automation workspace may have structural drift;
- Codex skills, MCP tools, or always-on context feel too noisy;
- you need an audit report before approving cleanup.

Use `thread-handoff` when:

- the thread is getting long or has already compacted;
- another agent or thread needs to continue the task;
- you need a concise restart point;
- the current discussion contains useful decisions mixed with noisy exploration.
- you want the current thread to check that the summary includes the important available context before transfer.

Use both when:

- a project health check reveals that the current thread is also too noisy;
- you want to audit the project first, then hand off the next action cleanly.

## Safety Model

Both skills are intentionally conservative:

- default to read-only behavior;
- do not delete or move files without explicit user confirmation;
- separate real issues from project-specific exceptions;
- avoid treating every missing code artifact as a failure;
- preserve verification evidence instead of trusting done claims;
- do not claim thread delivery succeeded unless a thread-management tool actually succeeded.

## Repository Structure

```text
skills/
  project-health-audit/
    SKILL.md
    agents/openai.yaml
    references/scan-checklist.md
  thread-handoff/
    SKILL.md
    agents/openai.yaml
    references/handoff-format.md
```

## License

MIT
