---
name: thread-handoff
description: Compress an overgrown Codex conversation into a compact, faithful context summary and optionally deliver it to a new or existing thread. Use when a task needs continuity, context compaction, restart, transfer to another agent, or preservation of decisions, constraints, evidence, current state, and next steps. If thread-management tools are available and the user asks to hand off or continue in another thread, use those tools; otherwise provide a copyable handoff summary.
---

# Thread Handoff

## Use This Skill For

- Compressing long tasks into a compact, faithful context summary.
- Preparing a new thread to continue work without inheriting noise.
- Preserving decisions, constraints, evidence, current state, and next steps.
- Delivering the handoff to a new or existing thread when tools and user intent allow it.

## Core Workflow

1. Compress the old context.
   - Preserve the goal, scope, user constraints, decisions, completed work, verification evidence, risks, and next step.
   - Drop repeated status chatter, failed exploratory branches that no longer matter, and background the next thread can rediscover cheaply.
2. Check summary fidelity.
   - Verify the handoff covers the available task context needed for continuation.
   - Mark anything not checked or possibly missing instead of pretending the summary is complete.
3. Transfer or output.
   - If the user asks to send, fork, create, or continue in another thread, look for thread-management tools and use them when available.
   - If tools are unavailable, fail, or the user only wants a draft, provide a copyable handoff summary.

## Handoff Format

Include these sections when relevant:

- Role
- Goal
- Must preserve
- Current state
- Completed work
- Evidence / verification
- Open risks
- Next safest step
- Do not repeat
- Possibly missing
- Ignore

## Transfer Tooling

When the user asks to transfer the handoff to another thread, first look for available thread tools such as `create_thread`, `fork_thread`, `send_message_to_thread`, `handoff_thread`, or an equivalent Codex thread-management tool.

- Prefer direct delivery over writing a local handoff file when delivery tools are available.
- Do not claim delivery succeeded unless the thread tool succeeded.
- If no delivery tool is available, say so briefly and provide the handoff text as the fallback.
- Do not create or message a thread when the user explicitly asked only for a handoff draft.

## Fidelity Check

Before delivery, check that the summary answers:

- What is the latest user goal?
- What constraints, boundaries, and "do not" instructions must survive?
- What files, pages, screenshots, links, commands, tools, or thread IDs matter?
- What has been completed, and what evidence proves it?
- What failed paths or false starts should not be repeated?
- What remains blocked, risky, unverified, or pending user confirmation?
- What can the next thread safely ignore?

## Guardrails

- Keep the handoff concise and executable.
- Do not restate all background unless it changes the next move.
- Do not claim completion without verification evidence.
- Do not broaden scope beyond the transfer point unless the user asks.
- Do not turn this into a project health audit. Inspect project health only when it directly affects the handoff.
- Do not write a local handoff file as the primary result when the user asked to send the handoff and thread tools are available.

## Outputs

- A compact handoff summary.
- A fidelity note listing any possibly missing or unchecked context.
- A direct thread transfer when requested and available, or a copyable fallback when not.
- A short judgment on whether a new thread is justified.

## References

- `references/handoff-format.md` for the handoff template.
