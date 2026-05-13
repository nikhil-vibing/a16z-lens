---
description: Build or refine a founder/startup profile from raw notes, a LinkedIn URL, or a website. Saves to profiles/.
argument-hint: <name or URL or raw-notes>
allowed-tools: Read, Write, Edit, WebSearch, WebFetch, Bash
---

# /profile

Build a clean, evaluation-ready profile from `$ARGUMENTS` and save it to `profiles/<slug>.md`.

## Procedure

1. **Identify the subject.**
   - URL → fetch and parse.
   - Person name → search LinkedIn, GitHub, Twitter, personal site.
   - Company name → search website, Crunchbase, recent press.
   - Raw notes → structure them.

2. **Use the profile template at `profiles/template.md`** as the schema.

3. **Fill in everything you can verify; mark unknowns explicitly.** Never invent traction numbers or background details.

4. **Save** to `profiles/<kebab-case-name>.md`.

5. **Offer the next step:** "Profile saved at `profiles/<slug>.md`. Run `/evaluate profiles/<slug>.md` to get the investment memo, or `/thesis-check profiles/<slug>.md` to see which a16z theses it touches."

## Quality bar

- Every claim has a source or is marked `[unverified]`.
- Founder background must include: prior companies, technical depth signal, network/credentials, founder-market-fit hypothesis.
- Company section must include: one-liner, product, traction (if any), GTM motion, competitive landscape, raised-to-date.
