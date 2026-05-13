---
type: framework
slug: the-new-business-of-ai
last_updated: 2026-05-13
confidence: HIGH
sources:
  - https://a16z.com/the-new-business-of-ai-and-how-its-different-from-traditional-software/
---

# The New Business of AI

## Origin
Martin Casado and others (with Matt Bornstein, Guido Appenzeller), a16z.com, 2020 and ongoing series.

## The core argument
AI businesses have fundamentally different economics from traditional SaaS:

1. **High variable COGS.** Each AI inference call costs real money (GPU compute, API fees). SaaS marginal cost is near zero; AI marginal cost is meaningful.
2. **Gross margin pressure.** Mature SaaS companies hit 75-85% gross margins; AI companies often hit 50-60% if not careful.
3. **Heavy services component.** Especially early-stage, AI deployment requires customization, prompt engineering, model fine-tuning — services revenue creeps in.
4. **Foundation-model dependency risk.** Companies built atop a single model provider face pricing volatility and discontinuation risk.
5. **Defensibility doesn't come from the model.** It comes from proprietary data, distribution, vertical workflow integration, brand.

## Why it matters
- Recalibrates investor expectations for AI companies.
- Reframes "what's the moat" away from model-level thinking and toward deployment-layer thinking.
- Justifies discounting some early-stage AI revenue (it may be services in disguise).

## How to apply it as an evaluator
- Ask about unit economics: gross margin, COGS per query, dependency on third-party model providers.
- Ask: "If GPT/Claude pricing changes 2x, what happens to your business?"
- Ask: "Where's the moat NOT at the model layer?" — proprietary data, distribution, brand, vertical workflows are the answers.
- Discount valuation multiples relative to SaaS comparables unless gross margin justifies otherwise.

## Patterns of strong AI businesses under this lens
- Vertical AI with deep workflow integration (Harvey for law, Hippocratic for healthcare).
- Companies that own a proprietary data source the foundation models can't replicate.
- Distribution-first plays (consumer brands with AI-as-feature).
- Infrastructure layer that compounds across foundation-model changes (Pinecone, Lambda).

## Patterns of weak AI businesses
- "GPT wrapper" with no data/distribution/workflow moat.
- Pure-services consulting disguised as product.
- Companies whose entire business depends on undifferentiated access to a foundation model.

## Cross-links
- [[martin-casado]] — co-author.
- [[ai-infrastructure]] (thesis).
- [[ai-applications]] (thesis).
- [[cost-of-cloud]] (adjacent framework).
- [[open-source-is-not-a-business-model]] (adjacent framework).
