# Sync checklist (run on the receiving machine, before applying pasted content)

Use this whenever new/changed content from this folder is pasted into
another machine's Claude Code config, instead of git-cloning.

1. Show me the current content of the file about to be changed on this
   machine (`CLAUDE.md`, `settings.json`, or the target file here).
2. Diff it, in plain terms, against the incoming pasted text:
   - Any rule that contradicts an existing rule on this machine?
   - Any duplicate rule (already covered, just worded differently)?
   - Any hook, permission, or model setting in `settings.json` that the
     incoming text assumes exists but doesn't on this machine?
3. List conflicts found, if any, with a recommendation per conflict
   (keep mine / take incoming / merge).
4. Only after I confirm, apply the change.
5. If nothing conflicts, say so in one line and apply.

Never silently overwrite an existing rule because the incoming text is
newer — always flag it and let me decide.
