# Doc convention

## Two-layer pattern (every doc I write or ask Claude to write)

1. **Plain layer (always first).** What this is, what it does, how to
   use it — readable in one pass by a competent developer from a
   different specialty. Max ~10 lines.
2. **Technical layer (only if needed).** Under its own "Technical
   detail" heading. Full technical language allowed here.

End-user docs (README intro, setup guide, changelog, release note):
plain layer only. No technical layer unless asked.

Explicitly technical docs (ADR, architecture doc, API reference, schema
doc): plain layer first, then go as deep as the topic needs.

## Schema / API sync doc (frontend + backend)

For any project with a separate frontend and backend (e.g. React +
FastAPI), keep one plain-language doc that maps:
- each backend endpoint or DB table,
- what it means in plain terms,
- which frontend piece consumes it,
- and when they were last checked against each other.

Purpose: catch backend/frontend drift (a field renamed on one side, not
the other) by reading one doc, without digging through both codebases.
Update this doc in the same change that changes the endpoint/schema —
a change without a matching doc update is incomplete.

## Where these docs live in someone else's repo

Never put a personal doc inside a shared `docs/` folder others edit.
Put it under a path that's unambiguously mine, e.g. `docs/notes/tarun/`
or `docs/sync/tarun-api-map.md`. This avoids overriding a teammate's
file, and avoids a teammate's edit silently overriding mine.
