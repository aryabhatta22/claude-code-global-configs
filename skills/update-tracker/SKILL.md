---
name: update-tracker
description: Updates project tracking files at end of session. Use when session tasks are complete.
user-invocable: true
disable-model-invocation: false
---
You are updating the progress tracking files for this project. Follow these steps in order.

**Step 1 — Discover tracking files**
Look for files matching these patterns in priority order:
- TRACKER.md, tracker.md, TASKS.md
- PLAN.md, PLANNING.md, ROADMAP.md, ARCHITECTURE.md
If none found, tell the user which files you looked for and ask them to confirm the correct names.
Do not proceed until you have identified at least one tracking file.

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

**Step 6 — Record scope changes**
If any architecture or scope decisions changed this session, append one row to the
changes table (or equivalent section). If nothing changed, do not touch this section.

**Step 7 — Confirm**
Tell the user which files were updated, which task statuses changed, and what was
appended to the session log. If you could not determine something, say so explicitly.
