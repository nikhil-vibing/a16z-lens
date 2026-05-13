---
type: framework
slug: open-source-is-not-a-business-model
last_updated: 2026-05-13
confidence: HIGH
sources:
  - Martin Casado public talks and essays
  - https://a16z.com/the-new-business-of-ai-and-how-its-different-from-traditional-software/
---

# Open Source Is Not a Business Model

## Origin
Martin Casado, paraphrased and articulated across many essays and talks. Not a single canonical post, but a consistent thread of his investing philosophy.

## The argument
Open source is a *distribution* strategy, not a *monetization* model. Adoption ≠ revenue. Successful OSS companies make money in distinct ways:
1. **Hosted / managed product** (Databricks, MongoDB Atlas, Confluent Cloud).
2. **Premium proprietary modules / enterprise features** (GitLab, HashiCorp model — with limits).
3. **Support / services contracts** (Red Hat — the historical archetype, harder to do at venture scale today).
4. **Owning the deployment surface** — open the protocol, sell the network (Stripe's old "open API" play, partially).

The mistake to avoid: assuming a popular OSS project will naturally turn into a venture-scale business. It rarely does without explicit, intentional monetization design.

## Why it matters for a16z
- Casado evaluates every OSS-led pitch through this lens.
- The default question: "What's the monetization vector, and how strong is it relative to your distribution?"
- OSS that has no clear path to monetization is interesting but not investable at venture scale.

## How to apply it as an evaluator
- For any OSS-led pitch: "Where does the dollar come from?" — and that answer needs to be specific.
- Ask: "Why won't the OSS community build the monetized version themselves and route around you?" — answers usually involve operational complexity, scale, or proprietary integrations.
- Be skeptical of "we'll figure out monetization later" — by the time it's a $100M business that hasn't been figured out, the OSS project is captured by competitors.

## Anti-patterns
- OSS-as-marketing without a real product.
- "Star count = company value" — GitHub stars don't pay payroll.
- License changes (BSL, etc.) made too late, alienating the community without recapturing revenue.

## Patterns of successful OSS monetization
- Hosted/cloud version is the default monetization vector in 2026.
- Multi-product surface (Datadog: integrations + observability + APM; HashiCorp: Terraform + Vault + Nomad + Consul).
- Enterprise security/compliance features as the premium tier.

## Cross-links
- [[martin-casado]] — author.
- [[enterprise-infrastructure]] (thesis).
- [[databricks]], [[github]] (portfolio).
