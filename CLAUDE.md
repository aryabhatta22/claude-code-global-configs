# My Toolbox (keep this list current — one line per tool)
When I seem unsure what tooling I have, or a task matches one of these, remind me.

## My skills
- /project-setup — scaffold a new fullstack repo (manual invoke only)
- /update-tracker — update TRACKER/PLAN files at end of session (manual invoke only)
## Workflow
- grill-me — adversarial critique of a plan BEFORE executing. Default plan-check.
- superpowers — INSTALLED BUT DISABLED. Full brainstorm → spec → TDD methodology.
  Enable via /plugin + restart when starting feature-heavy work; disable after.
  Costs ~820 tok/session while on. Don't run grill-me on top of it.
- caveman (lite) — terse output; /caveman to toggle, "normal mode" to stop.
  Never run /caveman-compress on CLAUDE.md or spec files.

## Plugins
- context7 — current library docs; prefer it over guessing API details
- security-guidance — passive security review
- claude-code-setup — run ONCE per new repo, not a standing tool
- claude-in-chrome — browser automation / live page inspection

## Known but deliberately NOT installed
planning-with-files (update-tracker covers it) · claude-mem (using native memory)
· frontend-design (only if UI becomes the bottleneck)
· claude-statusbar (terminal-only; I use the VS Code extension — use /usage and /cost instead)

## Enforcement (not invoked — always on)
- Hooks: PreCompact (tracker reminder) · PostToolUse (ruff format on .py edits)
- Deny rules: .env and secrets reads · git force push
- Per-project deny rules may add more — check .claude/settings.json in-repo

## Known but deliberately NOT installed
grill-me (redundant with superpowers) · planning-with-files (update-tracker covers it)
· claude-mem (using native memory) · frontend-design (only if UI becomes the bottleneck)

## Toolbox rules
- Before installing anything new: does an installed tool already cover this?
- A tool earns installation only after the same manual pain occurs ~3 times.
- On adding/removing any skill, plugin, or hook: update this list in the same sitting.
- Model: opusplan default. /model fable only for deliberate long-horizon work (~2× usage).
