---
description: Deep-research an a16z topic — partner, thesis, portfolio company, or framework. Writes to knowledge/ with citations.
argument-hint: <topic — e.g., "Katherine Boyle", "American Dynamism", "Anduril", "founder mode">
allowed-tools: WebSearch, WebFetch, Read, Write, Edit, Glob, Grep, Bash, Task
---

# /deep-dive

Run an a16z-flavored research pass on `$ARGUMENTS`, write findings into the appropriate `knowledge/` subdirectory, then surface a summary.

## Procedure

1. **Classify the topic:**
   - Person → `knowledge/founders/<slug>.md`
   - Thesis or theme → `knowledge/theses/<slug>.md`
   - Company → `knowledge/portfolio/<slug>.md`
   - Framework or aphorism → `knowledge/frameworks/<slug>.md`

2. **Dispatch the `a16z-researcher` agent** with the topic. Researcher:
   - Pulls from a16z.com, partner Substacks, podcasts, Twitter, primary press.
   - Cross-checks with Wikipedia / Crunchbase for hard facts.
   - Writes a structured document using the template from the researcher agent.
   - Cites every claim.

3. **Update MEMORY.md** if the topic reveals a durable user research interest.

4. **Surface in chat:**
   - 5-bullet executive summary.
   - Best primary source the user should read themselves.
   - 2-3 follow-up topics worth queueing as additional `/deep-dive` calls.

## Calibration

- Quick mode (single partner profile, single thesis stub): 5-10 searches, 1 doc written.
- Deep mode (full thesis breakdown with sub-areas and portfolio map): 15-25 searches, multiple cross-linked docs.

Default to deep mode unless the user prefixed `quick:` in the argument.
