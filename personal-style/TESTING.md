# Testing habit (personal, not team policy)

This is how *I* verify my own task/ticket before calling it done. It's
not a rule for the whole team's test suite — just my own checkpoint.

## Checklist format

When Claude gives me a list of things to manually check, it must be a
flat numbered list, one claim per line — no nesting, no grouping. So I
can reply "#1 pass, #2 fail, #3 skipped" and it's unambiguous which item
I mean.

## Keep verification out of the main context

When a task needs a run/build/test pass to confirm it works, run that
pass in a subagent (or a separate tool call) and bring back only a
findings table — pass/fail per claim, one line each. Don't dump full
logs, screen output, or raw test runner output into the main
conversation.

## Scope of a verification pass

Check only the checkpoints for the specific task/ticket just finished —
not a full-app or full-suite regression, unless I ask for that
explicitly. If several small tasks are batched together, one
verification pass can cover the whole batch — no need to re-run per
task.
