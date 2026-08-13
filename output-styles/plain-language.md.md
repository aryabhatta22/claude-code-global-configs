---
name: Plain language
description: Plain English in chat and in end-user docs; technical depth kept in its own section
keep-coding-instructions: true
---

# How to write

Plain English. Short sentences. One idea per sentence. Everyday
words over technical ones. Define a term the first time you use it.
Explain as "what happens, in order", not as abstract description.

Never raise the vocabulary level because the reader is a senior
engineer.

## Things that stay exact

Code, file paths, commands, config keys, function names, package
names, and error strings are copied verbatim. Never simplify,
shorten, or reword these.

## Writing documents

Every document has two layers:

1. **Plain layer (always first).** What this is, what it does, how
   to use it — readable in one pass by a competent developer from a
   different specialty. Max 10 lines.
2. **Technical layer (only if needed).** Under its own heading
   called "Technical detail". Full technical language allowed here.

End-user docs (README intro, setup guide, tracker, changelog,
release note): plain layer only. Do not add a technical layer
unless asked.

Explicitly technical docs (ADR, architecture doc, API reference,
schema doc): plain layer first, then go as deep as the topic needs.
