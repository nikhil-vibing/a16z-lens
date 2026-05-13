---
description: Map a profile, idea, or question to a16z's published investment theses. Shows fit-by-thesis and which partner would champion.
argument-hint: <path-to-profile.md | company name | idea description>
allowed-tools: Read, Glob, Grep, WebSearch, WebFetch
---

# /thesis-check

Map `$ARGUMENTS` against every active a16z thesis and rank fit.

## Procedure

1. Read the input (file or treat as text).
2. Scan `knowledge/theses/` for all thesis documents.
3. For each thesis, score fit 0-10 with one-line justification.
4. For the top 1-2 theses, identify:
   - The **champion partner** at a16z most likely to engage.
   - 2-3 **portfolio precedents** within that thesis bucket.
   - The **specific essay or podcast** that articulates that thesis.

## Output format

```
THESIS FIT MAP: [subject]

╔══════════════════════════════════════════════════╤═══════╤═══════════════════╗
║ Thesis                                           │ Fit   │ One-line          ║
╠══════════════════════════════════════════════════╪═══════╪═══════════════════╣
║ American Dynamism                                │ 8/10  │ Defense-adjacent..║
║ AI Infrastructure                                │ 6/10  │ Compute-heavy...  ║
║ AI Applications                                  │ 3/10  │ Not a wedge here. ║
║ Crypto / Onchain                                 │ 1/10  │ Off-thesis.       ║
║ Bio + Health                                     │ 0/10  │ N/A.              ║
║ Games                                            │ 0/10  │ N/A.              ║
║ Enterprise / Infrastructure                      │ 5/10  │ B2B sales motion. ║
║ Fintech                                          │ 2/10  │ Adjacent.         ║
║ Consumer                                         │ 1/10  │ Off-thesis.       ║
║ Little Tech / Builders                           │ 7/10  │ Hardware builders.║
╚══════════════════════════════════════════════════╧═══════╧═══════════════════╝

PRIMARY THESIS: [Top-scoring]
  Champion partner: [Name]
  Why: [2-3 lines]
  Portfolio precedents: [3 companies]
  Canonical reading: [Essay/podcast with URL]

SECONDARY THESIS: [Second]
  ...

OFF-THESIS: [What we're explicitly NOT — why a16z would say no on this dimension]
```

## Rule

If the highest fit is below 6/10, say so plainly: "This is off-thesis for current a16z." Don't manufacture fit.
