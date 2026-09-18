---
name: update-tracker
description: Updates project tracking files at end of session with evidence-verified statuses and a session log entry.
disable-model-invocation: true
context: fork
---
You are updating the progress tracking files for this project.

**Step 0 — Read the project's own format rules**
If the tracker has a "## For Claude Code" section, that section overrides
everything below where they differ. Follow the file's own rules, not your
assumptions about tracker formats.

**Step 1 — Find the tracking files**
TRACKER.md, tracker.md, TASKS.md, then PLAN.md, ROADMAP.md, ARCHITECTURE.md.
If none found, STOP. Say what you looked for. Change nothing.

**Step 2 — Learn the structure**
Read each file. Do not assume a shape. Find: where statuses live, where a
session log lives, where scope changes are recorded, whether a separate
archive file exists for finished work.

**Step 3 — Rebuild what happened this session**
Do not rely on memory of the conversation. Run `git log` and `git diff --stat`
since the last tracker edit, plus `git status --porcelain`. That is your
evidence base.

**Step 4 — Change statuses only on named evidence**
A ticket becomes Done only if one of these exists and you can name it:
  - a test run with counts (e.g. "275/275 passing"), or
  - a commit hash containing the work, or
  - a dated owner confirmation of a manual walkthrough.
"The file exists" is NOT evidence. "It looks implemented" is NOT evidence.
If evidence is missing, leave the status alone and say why.
Never invent a walkthrough the owner did not report.

**Step 5 — Move finished detail out**
When a ticket turns Done, MOVE its long comment/notes into the archive file,
keyed by ticket ID. Do not copy — the tracker must not hold two versions.
Leave behind: ID, title, the plain "After:" line, Status, archive link.

**Step 6 — Update the top-of-file summary**
Rewrite the "Where we are" line: last done, next ticket, waiting-on-owner.
Update stage markers (✅/🔵/⬜) and the "you are here" pointer.
If tickets were added this session, increment the scope counter and record
one reason each: found bug / owner change / split from a larger ticket.

**Step 7 — Clean stale cross-references**
Any gate or caveat in the header that names a ticket now Done is stale.
Fix it or delete it. Report every line you changed here.

**Step 8 — Append the session log**
One row: today's date, one short sentence on what got done, blockers, what's
next. Plain English. Do not touch existing rows.

**Step 9 — Record scope changes**
Only if architecture or scope actually changed. Otherwise skip the section.

**Step 10 — Confirm**
Report: files touched · statuses changed with the evidence named for each ·
detail moved to archive · stale references cleaned · log row added.
Say explicitly what you could not determine. Never fill a gap with a guess.
