# Project Health Audit Checklist

Use this checklist after reading the project's own rules.

## Boundary

- Confirm the project root and any nested real root, such as an Obsidian vault.
- Identify whether this is a code repo, content vault, automation workspace, or mixed project.
- Treat missing git, test, or build files as context, not automatic failure.

## Rules And Entrypoints

- Read project rules before judging structure.
- Look for files such as `AGENTS.md`, `CLAUDE.md`, `README.md`, `schema/`, `docs/`, `wiki/index.md`, `wiki/overview.md`, and `wiki/log.md`.
- Check whether entrypoints explain roles, boundaries, and where future agents should start.

## Structure Health

- Confirm source material has a durable target layer.
- Check that index or overview pages expose task-based navigation, not only file lists.
- Check logs or changelogs for recent changes when the project depends on continuity.
- Flag stale TODOs only when they contradict current state or block future work.

## Skill Surface

- List always-on skill directories and disabled or archived skill directories.
- Flag duplicates across active roots.
- Classify skills as keep active, move to on-demand or disabled, merge, or investigate.
- Prefer archiving over deletion unless the user explicitly asks for cleanup.

## Report Shape

Group findings as:

- Confirmed issues
- Likely false positives
- Optional improvements
- Requires user confirmation

Always state what was read and what was not checked.
