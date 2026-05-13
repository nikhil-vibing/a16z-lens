---
description: Write a standalone a16z-style investment memo from scratch on a company/idea. Shortcut for `/evaluate` when there's no profile file yet.
argument-hint: <company name or one-paragraph pitch>
allowed-tools: Read, Write, WebSearch, WebFetch, Glob, Grep, Bash, Task
---

# /memo

Write a full a16z-style investment memo on `$ARGUMENTS`.

## Procedure

1. If `$ARGUMENTS` is a company name, run a web search to gather public information (website, founders, traction, recent press, funding).
2. If `$ARGUMENTS` is a free-form pitch, take the text as canonical.
3. Dispatch the `a16z-evaluator` agent with the gathered context. Output to `research-output/<YYYY-MM-DD>-<slug>-memo.md`.
4. Surface a 5-bullet summary + verdict in chat.

## Behavior

- This is the fast path. Use when the user says "what would a16z think of [X]?" or "write me a memo on [Y]".
- For longer engagements (the user wants to iterate on a profile first), prefer `/profile` → `/evaluate`.
