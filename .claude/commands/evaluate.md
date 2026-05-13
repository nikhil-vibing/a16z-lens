---
description: Evaluate a profile/pitch/company as an a16z investment committee would. Produces a structured memo.
argument-hint: <path-to-profile.md | company name | one-line pitch>
allowed-tools: Read, Write, Glob, Grep, WebSearch, WebFetch, Bash, Task
---

# /evaluate

Run an a16z-style investment evaluation on `$ARGUMENTS`.

## Procedure

1. **Locate the input.**
   - If `$ARGUMENTS` is a file path, Read it.
   - If `$ARGUMENTS` looks like a path under `profiles/`, Read it.
   - If `$ARGUMENTS` is a company name, do a web search for company background first.
   - If `$ARGUMENTS` is a free-form pitch, treat the text as the profile.

2. **Pull thesis context.** Scan `knowledge/theses/` and `knowledge/frameworks/` for relevant docs. If the relevant thesis isn't documented, dispatch the `a16z-researcher` agent first to fill the gap.

3. **Dispatch the `a16z-evaluator` agent** with:
   - The full profile/pitch content
   - A pointer to relevant thesis docs
   - Instruction to write the memo to `research-output/<YYYY-MM-DD>-<slug>-memo.md`

4. **Surface the verdict.** After the memo is written, summarize in chat:
   - Verdict (PASS / TRACK / PURSUE / HOT PURSUE)
   - Thesis fit
   - 3 sharp questions to send back to the founder
   - Link to the full memo file

## Rules

- Don't soften the verdict. Most companies should be PASS or TRACK.
- Always cite a specific a16z partner and a specific portfolio precedent.
- Bear case must be steelmanned, not strawmanned.
