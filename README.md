# a16z Lens — A Claude Code workspace for thinking like an a16z partner

> A long-running research environment that turns Claude Code into an opinionated a16z partner.
> Drop in a founder, a pitch, or a question — get back a thesis-grounded investment memo, partner-voice take, or strategic map, every claim cited to a real a16z partner, thesis, or portfolio precedent.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](#license)
[![Built with Claude Code](https://img.shields.io/badge/Built%20with-Claude%20Code-blueviolet)](https://claude.com/claude-code)
[![Status: Active](https://img.shields.io/badge/Status-Active-brightgreen)](#)
[![Workspace Type: Research](https://img.shields.io/badge/Workspace-Research-informational)](#)

---

## Table of contents

- [The 60-second pitch](#the-60-second-pitch)
- [Why this exists](#why-this-exists)
- [Who this is for](#who-this-is-for)
- [Quickstart (5 minutes to first memo)](#quickstart-5-minutes-to-first-memo)
- [Architecture](#architecture)
- [What's inside](#whats-inside)
- [The six commands](#the-six-commands)
- [The three agents](#the-three-agents)
- [The two skills](#the-two-skills)
- [The knowledge base](#the-knowledge-base)
- [End-to-end workflows](#end-to-end-workflows)
- [How it works under the hood](#how-it-works-under-the-hood)
- [The a16z worldview in 60 seconds](#the-a16z-worldview-in-60-seconds)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [FAQ](#faq)
- [Acknowledgments and sources](#acknowledgments-and-sources)
- [License](#license)
- [Appendix — Master's margin note](#appendix--masters-margin-note)

---

## The 60-second pitch

**What this is.** A Claude Code workspace — a directory of agents, slash commands, skills, and a curated knowledge base — that lets you converse with Claude as if it were an opinionated a16z General Partner. Not a chatbot. Not a generic AI. A specialized research environment with a strong worldview, primary-source citations, and a structured output discipline.

**What you get.**
- **Investment memos** (`/evaluate`) — full 10-section partner-meeting-style memos with PASS / TRACK / PURSUE / HOT PURSUE verdicts.
- **Partner-voice answers** (`/ask`) — opinionated takes that pick a side, cite a partner, end in a sharp closing line.
- **Thesis maps** (`/thesis-check`) — score-by-thesis matrices showing where an idea fits across a16z's published worldview.
- **Deep dives** (`/deep-dive`) — research passes that extend the knowledge base with cited primary sources.

**What's different.** Most AI advice tools generate balanced, hedged, generic outputs. This one is intentionally opinionated. It commits to verdicts. It cites real partners and portfolio precedents. It will tell you the bear case is stronger than your bull case if it is. It is calibrated to disagree.

---

## Why this exists

Founders, operators, and analysts who study venture capital usually fall into one of two failure modes:

1. **The hot-take loop.** They read a16z's content, follow Marc on X, listen to the podcast — and absorb vibes without structure. Hard to convert into actual decisions.
2. **The generic-VC trap.** They ask ChatGPT "would a VC fund this?" and get back balanced, hedged, useless advice that no real partner would write.

This workspace is the answer to both. It encodes a16z's worldview as a structured environment: theses become files; partners become voices; portfolio companies become precedents; frameworks become rubrics. Every output gets grounded in real source material. Every verdict carries the trail back to the reasoning.

The premise: **you cannot get a partner-quality take from a model unless you stage the context like a partner would walk into a Monday meeting**. So that staging — knowledge base, agents, rubrics, output formats — is what's in this repository.

---

## Who this is for

- **Founders pre-pitch** who want a brutally honest dry-run before walking into the actual meeting.
- **Operators evaluating a job** at a startup who want to pressure-test the company's thesis fit.
- **Angel and seed investors** who want a structured second opinion before writing a check.
- **Analysts and journalists** covering the venture ecosystem who want to map ideas to published positions quickly.
- **Anyone studying a16z as a firm** — partners, theses, portfolio strategy — and wanting a working environment to think out loud in.

If you want generic, balanced, "depends-on-many-factors" output, this is the wrong tool. This is opinionated by design.

---

## Quickstart (5 minutes to first memo)

### Prerequisites

- macOS or Linux (Windows via WSL works).
- [Claude Code](https://claude.com/claude-code) installed and authenticated.
- Git (only if you're cloning).

### 1. Clone or download

```bash
git clone https://github.com/<your-fork>/a16z-lens.git ~/Documents/Research/a16z
cd ~/Documents/Research/a16z
```

Or just unzip into any directory you want; the workspace is self-contained.

### 2. Open in Claude Code

```bash
claude
```

Claude Code auto-loads `CLAUDE.md` and the `.claude/` configuration. You're now in the workspace.

### 3. Run your first command

Pick one:

**Get a partner-voice answer to a question:**
```
/ask should I start a defense-tech company in 2026 if I have no DC experience?
```

**Evaluate a real company:**
```
/memo Anthropic
```

**Map an idea across a16z's theses:**
```
/thesis-check an AI agent that does compliance audits for credit unions
```

That's it. The output appears in chat and (for memos and deep dives) is auto-saved to `research-output/`.

---

## Architecture

```
                          ┌─────────────────────────────────────┐
                          │           You (in chat)             │
                          └─────────────────┬───────────────────┘
                                            │
                                            ▼
                          ┌─────────────────────────────────────┐
                          │   Slash commands (.claude/commands) │
                          │   /evaluate /profile /thesis-check  │
                          │   /deep-dive /memo /ask             │
                          └─────────────────┬───────────────────┘
                                            │
                       ┌────────────────────┼────────────────────┐
                       ▼                    ▼                    ▼
              ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
              │ a16z-partner │     │a16z-evaluator│     │a16z-researcher│
              │  (opinions)  │     │   (memos)    │     │(extends kb)  │
              └──────┬───────┘     └──────┬───────┘     └──────┬───────┘
                     │                    │                    │
                     └────────────────────┼────────────────────┘
                                          │
                                          ▼
                          ┌─────────────────────────────────────┐
                          │     Skills (.claude/skills)         │
                          │  ┌────────────┐   ┌──────────────┐  │
                          │  │   master   │   │  a16z-judge  │  │
                          │  │ (general)  │   │ (specialized)│  │
                          │  └────────────┘   └──────────────┘  │
                          └─────────────────┬───────────────────┘
                                            │
                                            ▼
                          ┌─────────────────────────────────────┐
                          │       knowledge/  (the brain)       │
                          │  founders/  theses/  portfolio/     │
                          │  frameworks/                        │
                          └─────────────────────────────────────┘
                                            │
                          ┌─────────────────┴───────────────────┐
                          ▼                                     ▼
                ┌──────────────────┐                ┌──────────────────────┐
                │  profiles/       │                │  research-output/    │
                │  questions/      │                │  (generated memos,   │
                │  (your inputs)   │                │   answers, dives)    │
                └──────────────────┘                └──────────────────────┘
```

Each layer is independent: you can swap out the knowledge base, add new agents, write new commands, or extend the skill without touching the others.

---

## What's inside

```
a16z/
├── CLAUDE.md                         # Auto-loaded project context
├── README.md                         # This file
├── LICENSE                           # MIT
├── .claude/
│   ├── settings.json                 # Project permissions and config
│   ├── agents/
│   │   ├── a16z-partner.md           # Opinionated GP voice
│   │   ├── a16z-evaluator.md         # Investment-memo agent
│   │   └── a16z-researcher.md        # Knowledge-base curator
│   ├── commands/
│   │   ├── ask.md                    # /ask
│   │   ├── deep-dive.md              # /deep-dive
│   │   ├── evaluate.md               # /evaluate
│   │   ├── memo.md                   # /memo
│   │   ├── profile.md                # /profile
│   │   └── thesis-check.md           # /thesis-check
│   └── skills/
│       ├── master/                   # General research engine
│       │   ├── SKILL.md
│       │   └── references/
│       └── a16z-judge/               # Workspace-specialized skill
│           └── SKILL.md
├── knowledge/                        # The long-term brain
│   ├── README.md
│   ├── founders/                     # 8 partner profiles
│   │   ├── marc-andreessen.md
│   │   ├── ben-horowitz.md
│   │   ├── chris-dixon.md
│   │   ├── katherine-boyle.md
│   │   ├── martin-casado.md
│   │   ├── david-ulevitch.md
│   │   ├── andrew-chen.md
│   │   └── vijay-pande.md
│   ├── theses/                       # 10 investment theses
│   │   ├── american-dynamism.md
│   │   ├── ai-infrastructure.md
│   │   ├── ai-applications.md
│   │   ├── crypto-onchain.md
│   │   ├── bio-health.md
│   │   ├── games.md
│   │   ├── enterprise-infrastructure.md
│   │   ├── consumer.md
│   │   ├── fintech.md
│   │   └── little-tech.md
│   ├── portfolio/                    # Notable bets, with reasoning
│   │   ├── anduril.md
│   │   ├── stripe.md
│   │   ├── coinbase.md
│   │   ├── databricks.md
│   │   ├── roblox.md
│   │   ├── github.md
│   │   └── airbnb.md
│   └── frameworks/                   # Decision frameworks and a16z-isms
│       ├── software-eating-the-world.md
│       ├── its-time-to-build.md
│       ├── techno-optimism.md
│       ├── wartime-vs-peacetime-ceo.md
│       ├── founder-mode.md
│       ├── cold-start-problem.md
│       ├── open-source-is-not-a-business-model.md
│       ├── read-write-own.md
│       ├── narrative-as-moat.md
│       ├── cost-of-cloud.md
│       ├── the-new-business-of-ai.md
│       └── evaluation-rubric.md
├── profiles/                         # Drop founder/startup profiles here
│   ├── README.md
│   └── template.md
├── questions/                        # Drop partner-style questions here
│   ├── README.md
│   └── template.md
└── research-output/                  # Generated memos, answers, deep dives
    └── README.md
```

---

## The six commands

Each command maps to a specific kind of output. They're not just shortcuts — they're prompts that wire the right agent to the right context.

### `/evaluate <path-or-name>`

Produces a full investment memo on a profile, pitch, or named company.

```
/evaluate profiles/my-startup.md
/evaluate Anthropic
/evaluate "B2B legal AI for immigration filings, two ex-Stripe engineers"
```

**Output:** 10-section memo at `research-output/<date>-<slug>-memo.md`, plus a chat summary with verdict and 3 sharp questions to send back to the founder.

**Verdict ladder:** PASS / TRACK / PURSUE / HOT PURSUE. Most companies should land in PASS or TRACK — by design. If you're getting PURSUE on everything, calibration is broken.

### `/profile <name-or-url-or-notes>`

Builds a clean, evaluation-ready profile from raw input and saves it to `profiles/`.

```
/profile https://linkedin.com/in/example-founder
/profile "Cofounder of Acme, ex-Palantir, building AI agents for defense logistics, $4M seed from Lux"
/profile Anduril
```

**Output:** A fully-populated profile file at `profiles/<slug>.md` using the template at `profiles/template.md`. Unknowns are explicitly marked `[unverified]` — the agent never invents traction.

### `/thesis-check <subject>`

Maps a profile, idea, or pitch against every active a16z thesis and ranks fit.

```
/thesis-check my-pitch-deck.pdf
/thesis-check "decentralized GPU marketplace for academic researchers"
/thesis-check profiles/founder-name.md
```

**Output:** A scored matrix (0-10 per thesis), the top 1-2 theses with champion partners and portfolio precedents, plus an explicit "off-thesis" callout if nothing scores above 6.

### `/deep-dive <topic>`

Researches an a16z-related topic — partner, thesis, portfolio company, or framework — and writes the findings into `knowledge/` with citations.

```
/deep-dive Sriram Krishnan's move to government
/deep-dive "a16z's position on EU AI Act"
/deep-dive Hadrian
/deep-dive "the Cost of Cloud essay — has it aged well?"
```

**Output:** A new or updated file in the appropriate `knowledge/` subdirectory, with primary-source citations and a 5-bullet executive summary in chat.

### `/memo <company-or-pitch>`

Fast-path memo without needing a profile file. Useful for "what would a16z think of X?" questions.

```
/memo "an AI tutor for medical school exam prep, 2 co-founders, both doctors"
/memo Mistral
```

**Output:** Same 10-section memo format as `/evaluate`, generated from a quick web research pass.

### `/ask <question>`

Answer in the voice of an a16z GP. Opinionated, thesis-driven, no hedging.

```
/ask should I move to SF if I'm building a defense-tech startup?
/ask what's the bear case on AI agents replacing SaaS?
/ask is American Dynamism a real durable thesis or a political vibe?
```

**Output structure:**
- **THESIS LENS** — which a16z thesis applies
- **THE CALL** — one-sentence verdict
- **WHY** — 3-5 bullets with partner attribution and portfolio precedent
- **THE RISK NOBODY IS PRICING** — steelmanned bear case
- **WHAT WOULD CHANGE MY MIND** — disconfirming evidence
- **CLOSING LINE** — sharp aphorism

---

## The three agents

Agents are specialized sub-processes Claude can dispatch. Each has its own system prompt, allowed tools, and output discipline.

### `a16z-partner`

Embodies the blended voice of Marc Andreessen, Ben Horowitz, Chris Dixon, Katherine Boyle, Martin Casado, and other a16z partners.

**Triggers on:**
- "Take a side on X."
- "What would a16z say about Y?"
- Hot takes, market calls, build-vs-buy debates, founder advice.

**Operating principles:** Take a side; open with the thesis frame; cite a portfolio precedent; reference a partner's specific framing; steelman the bear case; close with a quotable line.

### `a16z-evaluator`

Produces partner-meeting-quality investment memos.

**Triggers on:**
- Any profile dropped in `profiles/`.
- `/evaluate` and `/memo` commands.
- "Score this pitch."

**Output discipline:** 10-section memo (one-liner, thesis fit, founder/team, market, product/moat, distribution/narrative, traction, bear case, check size, verdict). Verdict ladder is enforced — most outputs land in PASS or TRACK.

### `a16z-researcher`

The librarian. Keeps the knowledge base current and citation-grade.

**Triggers on:**
- Knowledge gaps surfaced by other agents.
- `/deep-dive` command.
- "Research X about a16z."

**Output discipline:** Writes to `knowledge/<subdir>/<slug>.md` with front-matter (type, slug, last_updated, confidence, sources). Never invents quotes. Always cites primary sources.

---

## The two skills

Skills are reusable capabilities Claude can invoke across many tasks.

### `master` (general)

Sourced from [master.skill](https://github.com/Bhindi-Studios/Skills). A general-purpose research engine that reverse-engineers any field's masters and applies their patterns to your context. Useful when the question genuinely spans beyond venture (career planning, content strategy, learning paths, etc.).

### `a16z-judge` (workspace-specialized)

The workspace-specific extension of `master`, pre-loaded with the a16z partner roster and the 10-filter worldview. Invoke when reasoning needs a16z grounding — companies, founders, market calls, build decisions.

```
The 10 filters a16z-judge applies to every evaluation:
  1. Software-eating-the-world (Andreessen)
  2. Wartime > peacetime (Horowitz)
  3. Long-arc read-write-own (Dixon)
  4. National-interest tech (Boyle)
  5. Infra defensibility (Casado)
  6. Cold start + network effects (Chen)
  7. Builder > critic
  8. Narrative as moat
  9. Founder mode > professional management
 10. Little Tech > Big Tech / Big Government
```

---

## The knowledge base

The `knowledge/` directory is the brain. Every agent reads from it; the researcher writes to it. Structured as four subdirectories:

**`founders/`** — One file per a16z partner. Each contains: role, background, investment focus, signature frameworks, notable portfolio bets, public writing/podcasts, voice/style notes, and verbatim quotes.

**`theses/`** — One file per published investment thesis. Each contains: the thesis in a paragraph, the inflection (why now), champion partner(s), sub-areas, portfolio precedents, canonical reading, common founder profile, anti-patterns, open questions.

**`portfolio/`** — Notable portfolio companies. Each contains: what it does, stage when a16z entered, lead partner, thesis bucket, why a16z backed it, current trajectory, lessons it sets for similar deals.

**`frameworks/`** — Decision frameworks, mental models, signature a16z-isms. Each contains: origin, the argument, why it matters as an investment lens, how to apply it, limitations.

**Every file has front-matter:**

```yaml
---
type: [founder | thesis | portfolio | framework]
slug: kebab-case-name
last_updated: YYYY-MM-DD
confidence: [HIGH | MEDIUM | LOW]
sources:
  - URL 1
  - URL 2
---
```

**Cross-linking convention:** Internal references use `[[slug]]` so a partner profile links to the theses they champion and vice versa.

**To extend the knowledge base:** Run `/deep-dive <topic>`. The researcher agent picks the right subdirectory, populates the template, cites sources, and cross-links.

---

## End-to-end workflows

### Workflow 1 — Pressure-test your own startup before pitching

```
1. Write a profile of your startup using the template
   $ cp profiles/template.md profiles/my-startup.md
   $ open profiles/my-startup.md  # fill it in

2. Run the evaluator
   /evaluate profiles/my-startup.md

3. Read the memo
   $ open research-output/2026-05-13-my-startup-memo.md

4. Address the bear case explicitly
   (Iterate on your pitch based on the 3 sharp questions)

5. Re-run to see if the verdict moves up the ladder
   /evaluate profiles/my-startup.md
```

### Workflow 2 — Decide whether to join a startup

```
1. Build a profile of the company from public info
   /profile Acme AI

2. Map it against a16z's theses
   /thesis-check profiles/acme-ai.md

3. Get a partner-voice take on the founder
   /ask is the founder of Acme AI someone an a16z partner would back, given their background?

4. Get the bear case
   /ask what's the strongest bear case on Acme AI?
```

### Workflow 3 — Build a worldview on a specific thesis

```
1. Deep-dive the thesis itself
   /deep-dive American Dynamism in 2026

2. Deep-dive the lead partner
   /deep-dive Katherine Boyle's recent essays

3. Deep-dive a flagship portfolio company
   /deep-dive Anduril's contract trajectory

4. Synthesize with an ask
   /ask given everything in knowledge/, is American Dynamism a durable thesis or a regime-dependent vibe?
```

### Workflow 4 — Stress-test a market call

```
/ask is "AI agents replace SaaS" a real thesis or a 2024-2026 fad?
/ask what would Martin Casado say about defensibility in AI agents?
/ask which a16z portfolio company is the canonical agent play?
```

---

## How it works under the hood

This section is for the curious — you don't need to read it to use the workspace.

### Claude Code project conventions

Claude Code looks for two things at the workspace root:

1. **`CLAUDE.md`** — auto-loaded as project context every time Claude opens this directory. This is where the workspace's operating rules live.
2. **`.claude/`** — the configuration directory. Agents, commands, skills, and settings.

The user's global Claude config at `~/.claude/` is also loaded, but project-level files override globals.

### Why agents instead of inline prompts

Three reasons:

- **Composition.** A command (`/evaluate`) can dispatch an agent (`a16z-evaluator`) and pass it scoped context. Both can be improved independently.
- **Discipline.** Each agent has its own system prompt and output format. The user doesn't have to remember to ask for "the 10-section memo" — the agent enforces it.
- **Specialization.** The `a16z-researcher` has only the tools it needs (web search, write to knowledge/). The `a16z-partner` doesn't need write access.

### Why a skill on top of agents

The `a16z-judge` skill exists because some requests don't fit a single agent. "Should I take this job?" needs partner-voice, but with thesis grounding and maybe a profile pass. The skill orchestrates across agents and knowledge.

### Why the knowledge base is files, not embeddings

Two reasons:

- **Transparency.** You can read and edit every fact. No black-box retrieval. If a thesis is wrong, you grep for it and fix it.
- **Cross-linking.** The `[[slug]]` convention lets agents follow connections. Embeddings flatten this graph.

If the knowledge base grows past ~1000 files, embedding-based retrieval would help. At 30-50 files, plain grep is fine.

### Memory

Workspace-level memory lives at `~/.claude/projects/-Users-nikhil-Documents-Research-a16z/memory/`. It persists across sessions and contains:

- The workspace's purpose
- The user's collaboration preferences (e.g., autonomous execution, no clarifying questions)
- A map of installed agents and commands
- The default research stack (preferred sources)

Memory is automatically loaded into context every session.

---

## The a16z worldview in 60 seconds

If you only have a minute, here is the worldview the workspace encodes:

1. **Software is eating the world.** Every industry gets restacked by software. (Andreessen, 2011.)
2. **It's time to build.** Software ate bits; now it's eating physical things — defense, manufacturing, energy. (Andreessen, 2020.)
3. **Techno-optimism is a political position.** Pro-tech-progress, anti-precautionary-principle, anti-decline. (Andreessen, 2023.)
4. **American Dynamism.** National-interest tech is the next venture wave. (Boyle, 2022.)
5. **Read-Write-Own.** Crypto is the third era of the internet. (Dixon, 2024.)
6. **Wartime CEOs win.** Founders who can switch into wartime mode survive. (Horowitz, 2014.)
7. **Founder mode.** Founders should run their companies, not delegate to professional management. (Graham/Chesky, 2024.)
8. **Open source is not a business model.** OSS is distribution; monetization is separate. (Casado, ongoing.)
9. **Defensibility is at the deployment layer, not the model.** Especially in AI. (Casado.)
10. **Cold start is the hardest problem.** Network effects compound; features don't. (Chen, 2021.)
11. **Narrative is a moat.** Companies that can't tell their story lose. (Firm-level.)
12. **Little Tech > Big Tech.** Startups, not incumbents, are the American innovation engine. (Andreessen/Casado, 2024.)

Each of these has its own file in `knowledge/frameworks/` with origin, argument, how to apply, and limitations.

---

## Roadmap

This is a living workspace. Planned additions:

- [ ] **More partners** — fill out the remaining a16z GPs (Connie Chan, Anish Acharya, Angela Strange, Jorge Conde, Sarah Wang, Bryan Kim, Anjney Midha, others).
- [ ] **More portfolio precedents** — currently 7 cornerstone companies; should be 20-30 to cover the major thesis-precedent pairs.
- [ ] **Auto-refresh** — a `/refresh` command that finds stale `last_updated` fields in `knowledge/` and re-researches the top N.
- [ ] **Competitor lenses** — analogous workspaces for Sequoia, Founders Fund, USV, General Catalyst. The architecture is firm-agnostic; the knowledge base is the only firm-specific part.
- [ ] **`/red-team`** — an explicit bear-case-only command. Useful for de-risking your own pitch.
- [ ] **Integration with deck input** — a `/deck` command that accepts a PDF and converts to a memo.
- [ ] **MCP server for portfolio companies** — pull live Crunchbase data when reasoning.
- [ ] **Worktree isolation** — let multiple research threads run in parallel without contaminating context.

PRs welcome on any of these.

---

## Contributing

This is open source under MIT. The cleanest contributions are:

### Adding to the knowledge base

The fastest improvement is more primary-source-grounded knowledge files. To contribute one:

1. Pick a partner, thesis, portfolio company, or framework that's missing.
2. Use the `a16z-researcher` agent (`/deep-dive <topic>`) to draft it.
3. Hand-verify every citation and quote.
4. Open a PR with the new file plus updates to any cross-linked files.

### Adding agents or commands

To contribute a new agent:

1. Create `.claude/agents/<name>.md` with front-matter (`name`, `description`, `tools`, `model`) and a clear system prompt.
2. Document when it triggers, what it produces, what it doesn't do.
3. If it pairs with a new slash command, add `.claude/commands/<name>.md`.

### Style guidelines

- **No phantom quotes.** Every verbatim quote must have a primary-source URL.
- **Date-stamp.** Theses evolve. Always include `last_updated`.
- **Cross-link.** Use `[[slug]]` to connect related files.
- **Confidence honesty.** If your source is 12+ months old on a fast-moving topic, mark confidence MEDIUM.
- **No emojis in committed files** unless the user explicitly asks. This is a workspace bias.

### How to propose larger changes

Open an issue first. Architecture changes (new agent layer, new directory in `knowledge/`, new skill) deserve discussion before code.

---

## FAQ

**Is this affiliated with Andreessen Horowitz?**
No. This is an independent research workspace built from public a16z material — essays, podcasts, books, talks. Not endorsed by, affiliated with, or connected to the firm.

**Can I use this to evaluate companies for actual investment decisions?**
You can use it as a structured second opinion. It's a thinking tool, not a substitute for diligence, lawyers, or human judgment. Verdicts are based on public information and pattern-matching, not insider knowledge.

**Will the memos be biased toward a16z's worldview?**
Yes. That's the entire point. If you want a balanced view, run the same input through three different firm-lens workspaces and compare.

**How accurate is the knowledge base?**
Initial seed is concentrated summaries from public sources through early 2026. Treat it as a strong starting point. Confidence levels are marked. The `a16z-researcher` agent can refresh any file on demand.

**Why files instead of a database?**
Transparency. Every claim can be grep'd, edited, and version-controlled. A database would obscure the citation trail.

**Can I run this against my own startup's deck?**
Yes. Drop the deck content (or summary) into a profile file and run `/evaluate`. Memos can be private — the workspace is local-only.

**Does it work offline?**
The agents that need web access (`a16z-researcher`, parts of `/memo` and `/deep-dive`) require internet. The pure knowledge-base operations (`/evaluate` on an already-populated profile, `/ask` from existing knowledge) work offline.

**What if a partner I want isn't in `knowledge/founders/`?**
Run `/deep-dive <partner name>`. The researcher will populate the file. Then re-run whatever you wanted.

**Can I fork this for a different firm?**
Yes. The architecture is firm-agnostic. Replace the contents of `knowledge/` and rename the agents. The skill orchestration logic is portable.

**What happens if a16z's worldview shifts?**
You re-run `/deep-dive` on the affected partner or thesis. The agents will update the relevant file with current information.

---

## Acknowledgments and sources

This workspace was built by reading and synthesizing public a16z material. Primary sources include:

- **a16z.com** — official essays and announcements.
- **future.a16z.com** — long-form content archive.
- **americandynamism.com** — dedicated American Dynamism hub.
- **a16zcrypto.com** — crypto fund content.
- **Books by partners** — *The Hard Thing About Hard Things* and *What You Do Is Who You Are* (Horowitz), *Read Write Own* (Dixon), *The Cold Start Problem* (Chen).
- **Partner blogs** — pmarchive.com (Andreessen archive), bhorowitz.com (Horowitz), cdixon.org (Dixon), andrewchen.com (Chen).
- **Podcasts** — a16z Podcast, The Ben & Marc Show, a16z Bio Eats World, a16z Crypto Podcast, Acquired.
- **Public talks and interviews** — many partner appearances on Lex Fridman, Joe Rogan, Bari Weiss, Tim Ferriss, and others.

Built on **Claude Code** by Anthropic. The research methodology framework is the `master` skill (general-purpose reverse-engineering of any field's masters), wrapped here for the venture-investing domain.

---

## License

MIT License

Copyright (c) 2026 Nikhil

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

---

## Appendix — Master's margin note

This README was written by applying the `master` skill at `.claude/skills/master/` to the field of "README writing for opinionated open-source AI/dev-tool workspaces."

**Masters studied (README writing patterns):**

| Master | What they taught | Pattern applied here |
|---|---|---|
| **makeareadme.com** | The canonical structure — title, description, install, usage, contributing, license | Backbone of the section order. |
| **standard-readme spec** (RichardLitt) | Specifies front-matter sections and ordering for open-source projects | Table of contents + section discipline. |
| **shadcn/ui README** | Strong opinionated voice; quickstart shows working code on first scroll | "60-second pitch" + Quickstart-in-5-minutes. |
| **Tailwind CSS README** | Treats the README as a sales document; uses comparison framing | "Why this exists" framed as failure modes of alternatives. |
| **Next.js / Vercel READMEs** | Architecture diagrams; explicit "How it works under the hood" sections | ASCII architecture diagram + dedicated under-the-hood section. |
| **FastAPI README** | Heavy on concrete examples over abstract descriptions | Every command has a runnable example. |
| **Anthropic SDK READMEs** | Calm, production-grade language; no breezy or condescending tone | Tone of voice throughout. |
| **Daniel Roy Greenfeld's README guide** | "What → Why → For Whom → Quickstart → Examples" sequence | Section ordering early in the document. |
| **The Hard Thing About Hard Things** (Horowitz) | Steelman the bear case in your own writing | FAQ includes honest "is this affiliated with a16z? No." and "will memos be biased? Yes, that's the point." |

**Patterns applied:**

1. **Hero in 60 seconds.** First two sections (the pitch + why-this-exists) answer the three questions every visitor asks: what is this, why should I care, who is it for.
2. **Quickstart that actually works.** Three runnable commands within five minutes of reading.
3. **ASCII architecture diagram.** Cheaper than a hosted image; survives forks and downloads.
4. **Concrete examples for every feature.** Every command has at least three example invocations.
5. **Cross-linked sections.** Table of contents anchors everything; internal references match.
6. **Honest FAQ.** Anticipates the skeptical reader. Doesn't dodge "is this affiliated" or "will it be biased."
7. **Explicit roadmap.** Open-source norm — shows the project is living and where contributors can plug in.
8. **License at the bottom in full text.** Standard MIT, ready to copy.

**Where I deviated from masters and why:**

- Most open-source READMEs assume a code library. This workspace is a *Claude Code project* — a configuration directory, not a package. So the "install" step is "clone and open in Claude Code," not "npm install." Adapted the structure accordingly.
- Most READMEs avoid worldview content. This one needs the "a16z worldview in 60 seconds" section because the entire workspace's value is the embedded worldview. Without that section, a reader can't evaluate whether they want what's inside.

**Recommended deep-dives for the reader:**

- [Make a README](https://www.makeareadme.com/) — the canonical template.
- [Standard README spec](https://github.com/RichardLitt/standard-readme) — for serious open-source rigor.
- [Daniel Roy Greenfeld's README guide](https://daniel.feldroy.com/posts/how-to-write-a-great-readme) — concise and opinionated.

---

*This README was generated as part of the [a16z Lens](https://github.com/) workspace setup. It is itself an artifact of the methodology the workspace teaches: study the masters, extract patterns, apply with attribution.*
