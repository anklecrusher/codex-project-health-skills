---
name: project-health-audit
description: Audit a project for structure health, skill hygiene, and navigation completeness. Use when scanning a repo, workspace, or vault-like project for rules, entrypoints, config surfaces, overgrown skill loading, missing links, or read-only health issues that need a prioritized report.
---

# Project Health Audit

## Use This Skill For

- Scanning project structure, entry files, rules, and navigation surfaces.
- Checking skill surfaces for duplication, overgrowth, or stale always-on content.
- Reviewing wiki-style health signals such as index, overview, log, references, and cross-links.
- Producing a read-only, prioritized audit with clear recommendations and confirmation-gated follow-up actions.

## Core Workflow

1. Identify the project boundary and the intended health target.
2. Read the governing rules and entrypoints first.
3. Inspect structure, navigation, and skill loading surfaces.
4. Separate real defects from expected project-specific exceptions.
5. Report findings in priority order:
   - structural problems
   - skill hygiene issues
   - missing or weak navigation
   - optional improvements
   - actions that require user confirmation

## What To Check

- Project rules and boundary files.
- Entry pages and navigation completeness.
- Source-to-reference linkage and broken or thin cross-links.
- Skill directories that are duplicated, stale, or too broad for always-on loading.
- Long tasks that need handoff packaging rather than continued drift in the same thread.

## Guardrails

- Stay read-only unless the user explicitly asks for changes.
- Do not delete, move, or rewrite files as part of the audit.
- Do not treat missing code-project artifacts as failures when auditing a knowledge-base-style project.
- If a fix is needed, describe it; do not apply it.

## Outputs

- A concise audit summary.
- A prioritized list of findings.
- A short split between confirmed issues, likely false positives, and user-confirmation items.
- A recommendation on whether related workflows should be split into separate skills or kept unified.

## References

- `references/scan-checklist.md` for the audit checklist.
