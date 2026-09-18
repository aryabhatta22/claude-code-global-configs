# Tracker snapshot + lessons log (generic)

Adapt to whatever tracker/ticket system the project already uses
(Jira, Linear, a markdown TRACKER file, GitHub Projects). Don't force a
new tracker on a project that has one — plug into it.

## Snapshot doc

At the end of a work session (or a batch of tickets), keep one short
generated snapshot doc — not hand-edited, always regenerated — with:
- current version/milestone,
- open ticket count / done count / next ticket,
- anything built that diverges from its spec/ticket, one line each,
- open questions still waiting on someone,
- date of the last real end-to-end verification pass.

It states counts and pointers only — never a rule, a formula, or a
fact that isn't also written somewhere else. If a fact only exists in
this snapshot, that's a bug — move it to the real source (the spec, the
ticket, the code).

## Lessons log

At the end of a ticket, add one line to a lessons log only if one of
these is true:
- the spec/requirements were unclear and needed to stop and ask,
- something broke that nothing predicted,
- the task took much longer than expected.

If none of those happened, add nothing — don't invent a line to fill
the row. Never rewrite an existing line; only append.
