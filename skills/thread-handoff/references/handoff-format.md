# Thread Handoff Format

Use this format when a task should continue in a fresh thread or after context compression. The goal is compression with fidelity: preserve the context needed to continue, and drop noise.

## Compact Handoff Summary

```markdown
【Thread Handoff Summary】

Role:
- The next thread should act as ...

Goal:
- ...

Must preserve:
- ...

Current state:
- ...

Completed:
- ...

Evidence / verification:
- Checked: ...
- Not checked: ...

Open risks:
- ...

Next safest step:
- ...

Do not repeat:
- ...

Possibly missing:
- ...

Ignore:
- ...
```

## What To Preserve

- Role and scope boundaries.
- Files, pages, commands, or tools already used.
- User decisions and explicit constraints.
- Current unresolved blockers.
- Verification evidence, including commands, screenshots, logs, or readback checks.
- Failed paths or false starts that the next thread should not repeat.
- Unknowns that are not verified but may matter.

## What To Drop

- Old exploratory branches that did not affect the final state.
- Repeated status chatter.
- Tool outputs that can be summarized in one line.
- Background that the next thread can rediscover cheaply.

## Fidelity Check

Before delivering the handoff, verify the summary covers the available context needed for continuation:

- latest user goal and success criteria;
- explicit constraints, boundaries, and "do not" instructions;
- relevant files, pages, screenshots, links, commands, tools, and thread IDs;
- completed work and exact verification evidence;
- failed attempts and reasons they should not be repeated;
- blockers, open risks, and user-confirmation items;
- context the next thread can safely ignore.

If any part cannot be verified, list it under `Possibly missing` instead of silently omitting it.

## New Thread Recommendation

Recommend a new thread when:

- The task has accumulated multiple unrelated branches.
- Context compression has already happened or is likely.
- The next step needs a different role.
- The current thread's injected tools or skill list is stale.

Do not recommend a new thread merely because the task is large if the current state is still clear.

## Delivery Rule

If the user asks to send, fork, create, or continue in another thread, use available thread-management tools when possible. If no such tool is available or the tool fails, provide the handoff summary as a copyable fallback and say that delivery did not happen.
