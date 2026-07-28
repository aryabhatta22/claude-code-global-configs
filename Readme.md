# Claude Code — Global Config

Personal `~/.claude` configuration, version-controlled so switching or reinstalling
machines doesn't mean losing the setup. Only the files below are tracked; everything
else (plugin binaries, sessions, logs, history, caches) is machine-local runtime
state and is intentionally gitignored — see `.gitignore` for the exact list.

## What's tracked

- `CLAUDE.md` — living toolbox index: which skills/plugins/hooks exist, when to use
  them, and the rules for adding new ones. Source of truth for *current state*.
- `settings.json` — model, permissions, hooks, and which plugins are enabled.
- `skills/` — custom skills (below).
- `hooks/`, `agents/` — reserved for future custom hooks/agents (empty for now).
- `Readme.md` — this file: how to restore the setup on a new machine.

Plugins themselves are **not** committed (reinstallable, machine-specific) — install
them fresh per the steps below.

## Restore on a new machine

```bash
git clone git@github.com:yourusername/claude-global-config.git ~/.claude
claude login
```

Then, inside a session, reinstall the plugins listed in `settings.json`:

```
/plugin install context7@claude-plugins-official
/plugin install security-guidance@claude-plugins-official
/plugin install claude-code-setup@claude-plugins-official
```

`superpowers` lives in a third-party marketplace, already registered via
`extraKnownMarketplaces` in `settings.json`. If Claude Code doesn't pick it up
automatically, add it explicitly first:

```
/plugin marketplace add obra/superpowers-marketplace
/plugin install superpowers@superpowers-marketplace
```

## Plugins

| Plugin | Marketplace | Default | Purpose |
|---|---|---|---|
| context7 | claude-plugins-official | enabled | Current library/API docs — prefer over guessing |
| security-guidance | claude-plugins-official | enabled | Passive security review |
| claude-code-setup | claude-plugins-official | enabled | Run once per new repo, not a standing tool |
| superpowers | superpowers-marketplace | **disabled** | Full brainstorm → spec → TDD methodology |

`superpowers` is installed but left disabled by default — it costs ~820 tokens/session
while on. Enable it with `/plugin` only when starting feature-heavy work, and disable
it again afterward. Don't run `grill-me` on top of it (redundant).

`claude-in-chrome` (browser automation / live page inspection) is used but managed
outside this repo's plugin list — install separately if missing.

## Skills (`skills/`)

| Skill | Invoke | Purpose |
|---|---|---|
| project-setup | `/project-setup` (manual only) | Scaffold a new fullstack repo from scratch |
| update-tracker | `/update-tracker` (manual only) | Update TRACKER/PLAN files at end of a session |
| grill-me | say "grill me" / auto-triggers | Adversarial critique of a plan before executing — default plan-check |
| caveman | `/caveman` toggles on, "normal mode" turns off | Ultra-compressed terse responses (~75% fewer tokens) |

## Hooks (in `settings.json`)

- **PreCompact** — reminds to run `/update-tracker` if tasks were completed this session.
- **PostToolUse** (`Edit`/`Write`) — auto-runs `ruff format` on any edited `.py` file.

## Permissions baseline

- Allowed without prompting: `git status`/`diff`/`log`, `uv run pytest`/`ruff`, `npm run test`/`lint`.
- Denied: reading `.env`/`.env.*`/`secrets/`, force-pushing.
- Individual project repos may layer on additional deny rules via their own
  `.claude/settings.json` — check there too.

## Not installed (on purpose)

`planning-with-files`, `claude-mem`, `frontend-design`, `claude-statusbar` — see
`CLAUDE.md` for the reasoning behind each. Before installing anything new: check
whether an existing tool already covers it, and only add a tool after the same
manual pain has come up ~3 times.

## Keeping this in sync

`CLAUDE.md` is the authority on current toolbox state — whenever a skill, plugin, or
hook is added or removed, it gets updated in the same sitting. This README only needs
touching when the *restore steps* change (new plugin/marketplace, new tracked
directory, etc.).
