---
type: framework
slug: cost-of-cloud
last_updated: 2026-05-13
confidence: HIGH
sources:
  - https://a16z.com/the-cost-of-cloud-a-trillion-dollar-paradox/
---

# The Cost of Cloud (Trillion Dollar Paradox)

## Origin
Martin Casado and Sarah Wang, a16z.com, May 2021. One of the most-cited and most-debated a16z essays of the 2020s.

## The argument
At scale, public cloud (AWS/GCP/Azure) is expensive — sometimes 2-3x the cost of running equivalent infrastructure on bare metal or owned datacenters. As companies grow, the cost burden of cloud increasingly drags on margins; for large SaaS / consumer / data-intensive companies, hundreds of millions or billions of dollars in market cap is being transferred to the hyperscalers.

The implication: **at sufficient scale, cloud repatriation becomes economically rational.** Companies should be moving back to bare metal or hybrid architectures.

## Why it matters
- Triggered industry-wide reassessment of cloud-only architectures.
- Validated emerging companies in cloud-cost-management, hybrid infrastructure, bare-metal-as-a-service.
- Pre-staged a16z's enthusiasm for AI compute infrastructure (Lambda Labs, etc.).
- Influenced 37signals' high-profile cloud-exit (Hey, Basecamp moved off AWS in 2023).

## Counter-arguments and debates
- AWS and other hyperscalers argue the essay underestimates the operational/staffing cost of running owned infrastructure.
- For most companies under a certain scale, cloud is unambiguously the right choice.
- The "repatriation" trend is real but smaller than essay enthusiasts claim.

## How to apply it as an evaluator
- For infrastructure pitches: cloud-cost reduction is a real, growing wedge.
- For AI infra: COGS analysis is critical; AI workloads have very different economics than SaaS.
- For B2B SaaS at scale: ask about gross margin trajectory under different infrastructure choices.

## Cross-links
- [[martin-casado]] — co-author.
- [[enterprise-infrastructure]] (thesis).
- [[ai-infrastructure]] (thesis) — related economic frame.
- [[the-new-business-of-ai]] (adjacent framework).
