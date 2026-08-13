# Claude Code — Global Config

Personal `~/.claude` configuration, version-controlled so switching or reinstalling
machines doesn't mean losing the setup. Only the files below are tracked; everything
else (plugin binaries, sessions, logs, history, caches) is machine-local runtime
state and is intentionally gitignored — see `.gitignore` for the exact list.

## What's tracked

- `CLAUDE.md` — living toolbox index: which skills/plugins/hooks exist, when to use
  them, how to write to me, and the rules for adding new ones. Source of truth for
  *current state*.
- `settings.json` — model, output style, permissions, hooks, and which plugins are enabled.
- `skills/` — custom skills (below).
- `output-styles/` — custom output styles (below).
- `hooks/`, `agents/` — reserved for future custom hooks/agents (empty for now).
- `Readme.md` — this file: how to restore the setup on a new machine.
- `.gitignore` — the allowlist that decides everything above.

Plugins themselves are **not** committed (reinstallable, machine-specific) — install
them fresh per the steps below.

## Restore on a new machine

```bash
git clone git@github.com:yourusername/claude-global-config.git ~/.claude
claude login
```

Then, inside a session, reinstall the plugins listed in `settings.json`:

/plugin install context7@claude-plugins-official
/plugin install security-guidance@claude-plugins-official
/plugin install claude-code-setup@claude-plugins-official

`superpowers` lives in a third-party marketplace, already registered via
`extraKnownMarketplaces` in `settings.json`. If Claude Code doesn't pick it up
automatically, add it explicitly first:

/plugin marketplace add obra/superpowers-marketplace
/plugin install superpowers@superpowers-marketplace

Skills and output styles need no install step — they are plain files, and cloning
this repo puts them in place. The `outputStyle` key is already in `settings.json`,
so the style is active from the first session.

## Output style

One custom style: **Plain language** (`output-styles/plain-language.md`).

What it does: forces plain English in chat answers and in every document Claude
writes. Short sentences, everyday words, terms defined on first use. Code, file
paths, commands, and error strings are left exact. Documents get a plain summary
first; deep technical content goes in its own "Technical detail" section.

It sets `keep-coding-instructions: true`, so normal coding behaviour is kept.

### Things worth knowing

- The style is set by `"outputStyle": "Plain language"` in `settings.json`.
- That key is read once when a session starts. Changes need `/clear` or a restart.
- The style applies to the main conversation only. Subagents run their own system
  prompt and ignore it. The "How to write to me" section in `CLAUDE.md` is the
  backup for those cases.
- This covers Claude Code only. Claude.ai chat and Projects read a separate field
  (Settings → "Instructions for Claude"), which is not in this repo. Keep the two
  in sync by hand.

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

`claude-in-chrome` (browser automation / live page inspection) is a separate Chrome
extension / companion install, not a `/plugin` from this repo's marketplaces — it
doesn't appear in `settings.json` at all, so there's no restore step to run here;
just reinstall the extension itself if it's missing.

## Skills (`skills/`)

| Skill | Invoke | Purpose |
|---|---|---|
| project-setup | `/project-setup` (manual only) | Scaffold a new fullstack repo from scratch |
| update-tracker | `/update-tracker` (manual only) | Update TRACKER/PLAN files at end of a session |
| grill-me | say "grill me" / auto-triggers | Adversarial critique of a plan before executing — default plan-check |
| caveman | `/caveman` (manual only) | Cuts word count for throwaway lookups |

`caveman` saves tokens. It does **not** make answers easier to read — it drops
articles and conjunctions, which makes English harder to parse, not simpler. It
conflicts with the Plain language output style. Don't run both. It also does not
auto-trigger despite what its description claims; you have to call it.

## Output styles (`output-styles/`)

| Style | Active | Purpose |
|---|---|---|
| plain-language | **yes** (set in `settings.json`) | Plain English everywhere; technical depth in its own section |

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

`CLAUDE.md` is the authority on current toolbox state — whenever a skill, plugin,
output style, or hook is added or removed, it gets updated in the same sitting.
This README only needs touching when the *restore steps* change (new plugin or
marketplace, new tracked directory, etc.).
