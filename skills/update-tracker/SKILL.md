---
name: update-tracker
description: Updates project tracking files (TRACKER.md, PLAN.md, etc.) at end of session with evidence-verified statuses and a session log entry.
disable-model-invocation: true
context: fork
---
You are updating the progress tracking files for this project. Follow these steps in order.

**Step 1 — Discover tracking files**
Look for files matching these patterns in priority order:
- TRACKER.md, tracker.md, TASKS.md
- PLAN.md, PLANNING.md, ROADMAP.md, ARCHITECTURE.md
If none found, STOP. Report which files you looked for and ask the user to
confirm the correct names. Do not modify anything.

**Step 2 — Read and understand structure**
Read each file you found. Do not assume a structure — learn it from the file.
Identify: where task statuses are tracked, where a session log lives (if any),
where scope or architecture changes are recorded (if any).

**Step 3 — Check implementation state**
List files that exist under the project. For each task in the tracker marked "Not Started"
or "In Progress," check whether the described implementation actually exists.
Do not mark a task Done unless the "Done Looks Like" criteria (or equivalent) are met.

**Step 4 — Update statuses**
Change task statuses that have changed based on evidence. Do not change tasks
you cannot verify. Do not rewrite or reformat content you are not changing.

**Step 5 — Append session log**
If the tracker has a session log section, append one row with today's date,
a one-line summary of what was done this session, any current blockers, and
what should happen in the next session. Do not modify existing log rows.
Write log entries in plain English. One short sentence each.
No jargon unless the jargon is the thing being tracked.

**Step 6 — Record scope changes**
If any architecture or scope decisions changed this session, append one row to the
changes table (or equivalent section). If nothing changed, do not touch this section.

**Step 7 — Confirm**
Report: which files were updated, which task statuses changed (with the evidence
used), and what was appended to the session log. If you could not determine
something, say so explicitly.
