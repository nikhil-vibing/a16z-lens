# profiles/

Drop founder or startup profiles here. One file per subject, named in `kebab-case.md`.

## Quick workflow

1. Either:
   - Copy `template.md` to `<your-subject>.md` and fill it in by hand, OR
   - Run `/profile <name | URL | raw-notes>` and let the agent build it for you.
2. Run `/evaluate profiles/<your-subject>.md` for the investment memo.
3. The memo lands in `research-output/<date>-<subject>-memo.md`.

## What makes a good profile

- **Specific** — "Built X at Y, sold to Z for $N" beats "experienced operator."
- **Sourced** — Link to LinkedIn, GitHub, prior startup, press, deck.
- **Honest about gaps** — Mark unknowns with `[unverified]`. Don't make up traction.
- **Founder-market-fit hypothesis** — Why is THIS person the right person for THIS problem? Make the argument.

## What gets evaluated

The `a16z-evaluator` agent runs every profile through the same 10-section memo: thesis fit, team, market, product/moat, distribution, traction, bear case, check size, verdict.
