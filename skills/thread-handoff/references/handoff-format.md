# Thread Handoff Format

Use this format when a task should continue in a fresh thread or after context compression.

## Compact Handoff

```markdown
【Handoff】

Role:
- The next thread should act as ...

Goal:
- ...

Current state:
- ...

Completed:
- ...

Verification:
- Checked: ...
- Not checked: ...

Open risks:
- ...

Next safest step:
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

## What To Drop

- Old exploratory branches that did not affect the final state.
- Repeated status chatter.
- Tool outputs that can be summarized in one line.
- Background that the next thread can rediscover cheaply.

## New Thread Recommendation

Recommend a new thread when:

- The task has accumulated multiple unrelated branches.
- Context compression has already happened or is likely.
- The next step needs a different role.
- The current thread's injected tools or skill list is stale.

Do not recommend a new thread merely because the task is large if the current state is still clear.
