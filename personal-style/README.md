# Personal style folder

This folder holds *my* working-style rules — not tied to any one project.
Nothing here is company code or company data. Safe to keep in a personal
git repo and copy between machines.

## Files
- `STYLE.md` — how I want replies written (plain language, answer shape).
- `DOCS-CONVENTION.md` — two-layer doc pattern + schema-doc habit.
- `TESTING.md` — my manual-test checklist format + verification habit.
- `TRACKER-CONVENTION.md` — generic tracker snapshot + lessons-log rule.
- `NEXT-TICKET.md` — generic "what should I pick up next" logic.

## How to use this on a new (work) machine
This machine's `~/.claude` is the git repo. On another machine, do **not**
clone this repo directly (it may pick up other personal/global settings you
don't want mixed with a work box). Instead:

1. Open each file above on this machine (or on GitHub).
2. Copy its content into the same filename under the other machine's
   `~/.claude/personal-style/` (or paste the relevant rule straight into
   that machine's `CLAUDE.md`, if that's where it needs to apply).
3. Before saving, ask Claude Code on that machine to run the check in
   `SYNC-CHECKLIST.md` — it compares the incoming text against whatever is
   already in that machine's `CLAUDE.md` / `settings.json` and flags
   conflicts (duplicate rules, contradicting instructions, hook clashes)
   before anything is applied.

## Where these rules live inside a *project* repo
`DOCS-CONVENTION.md` and `TESTING.md` describe things I do inside other
people's shared repos (docs, test checklists). To avoid overriding a
teammate's file or getting overridden by one, anything written into a
shared repo under these conventions goes in a path that is clearly mine,
e.g. `docs/notes/tarun/` — never into a shared `docs/` file others also
edit, unless the team already agreed to it.
