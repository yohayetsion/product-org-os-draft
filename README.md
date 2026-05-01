<!--
Reviewer-Readiness Summary (delete this comment block before production deploy)

WHAT IS LOCKED (do not edit without re-opening the lock):
- Canonical claim verbatim form: "Product Org OS v5.0 implements the Decision Provenance Standard's reporter protocol at Conformance Level 3."
- 5 acceptable phrasings; 10 forbidden phrasings absent throughout
- "Vision to Value" full spelling in all human-facing prose; v2v retained only in /v2v/ API path
- Version stamp v5.0.0 (Yohay 2026-04-30 override; Stream G GO verdict)
- v4.0.1 -> v5.0.0 jump explainer paragraph
- Skill counts harmonized at 133; knowledge packs unchanged at 28; 12 agents

WHAT IS PENDING YOHAY CONFIRMATION:
- Skill count mismatch in source: README front-matter says 133 throughout; existing CHANGELOG.md is silent on v4.x; CLAUDE.md says current 4.0.1. This README harmonizes at 133 per Wave 1 README-diff.md decision. Confirm at draft URL review.
- Path A (decisionprovenance.ai) vs Path B (executiveoperatingsystems.org/standard/) for Standard hub URL. This README ships Path A wording with Path B fallback note. Confirm at Day 4 domain decision.
- "Interactive Presentation" link target unchanged at https://yohayetsion.github.io/product-org-os; that surface IS the production marketing site per Wave 2 addendum item 7. No separate marketing domain.

WHAT NEEDS PMM-DIR CONFORMANCE-LANGUAGE PASS:
- All 5 acceptable phrasings used correctly in §Quick Start, §What's in this repo, §What's Included, §What's New
- Zero forbidden phrasings as affirmative claims (verified by grep at sign-off; forbidden phrasings appear ONLY in negation enumeration in the v5.0.0 What's New section)
- Cross-artifact veto authority not invoked

WHAT IS PENDING YOHAY APPROVAL AT DRAFT URL:
- Draft branch deploys to https://yohayetsion.github.io/product-org-os-draft/
- Yohay reviews; production push to main -> https://yohayetsion.github.io/product-org-os/ only after explicit approval
- Cache-invalidation 10-step checklist (DEPLOY-PLAN.md §3.B) executes on production push
-->

# Product Org OS

**An entire product organization that becomes your superpower.**

> Intent → Decisions → Commitments → Execution → Outcomes → Learning

**v5.0.0** — Vision to Value Standard alignment release. Product Org OS v5.0 implements the Decision Provenance Standard's reporter protocol at Conformance Level 3.

12 agents · 133 skills · 28 knowledge packs · Structured metadata · Enforcement-first runtime · MCP integrations · Standard-aligned by design

[**View the Interactive Presentation →**](https://yohayetsion.github.io/product-org-os)

---

## Quick Start

```bash
git clone https://github.com/yohayetsion/product-org-os.git
cd product-org-os
python install.py
```

New to Claude Code skills? See [Anthropic's skills docs](https://docs.claude.com/en/docs/claude-code/skills).

> **New here?** Read [`agent-guide.md`](./agent-guide.md) — a complete top-to-bottom guide for any coding agent to understand, install, and operate the system.

> **Standard-aligned by design.** Product Org OS v5.0 ships a runnable substrate at [`standard/v5.0/`](./standard/v5.0/) — Charter and decision-record state machines, Article 50 disclosure metadata schema, the Conformance Reporter API (OpenAPI 3.1), and the four-layer Mode-Drift Composed Mitigation. Eight named structural-primitive skills (`/decision-charter`, `/decision-record`, `/escalation-rule`, `/ownership-map`, `/customer-value-trace`, `/collaboration-check`, `/scale-check`, `/phase-check`) emit Vision to Value Standard conformance signals. See the [Vision to Value Standard hub](https://decisionprovenance.ai) (or `executiveoperatingsystems.org/standard/` if the standalone domain has not yet attached) for the full Standard text and citation guidance.

> **What's New →** [v5.0.0 release notes](./standard/v5.0/release/RELEASE-NOTES-v5.0.0.md) · [What's New in v5.0.0 (narrative)](./whats-new-v5.0.0.html)

---

## What's in this repo

| Path | Purpose |
|------|---------|
| `agent-guide.md` | Invocation patterns (`@agent`, `/skill`, gateways) |
| `PRINCIPLES.md` | Vision to Value methodology principles |
| `skills/` | 133 skills — the product-org workflows |
| `standard/v5.0/` | **NEW v5.0.0** — Vision to Value Standard alignment bundle: state machines, schemas, Conformance Reporter API spec, Mode-Drift four-layer mitigation, conformance signal vocabulary, and the Stream E test apparatus |
| `rules/` | 20 behavioral rules injected into Claude Code sessions |
| `reference/` | Knowledge packs and templates |
| `install.py` | Portable installer — copies skills into `~/.claude/skills/` |
| `CHANGELOG.md` | Release history |

---

## Two Invocation Patterns

| Syntax | Purpose | Example |
|--------|---------|---------|
| `@agent` | **Delegate** — spawn autonomous agent | `@pm create a PRD for auth` |
| `/skill` | **Inline** — use template/workflow directly | `/prd` `/decision-record` |

### @product Gateway

The single entry point. Routes requests to the right agents automatically.

```
@product Launch freemium for SMBs. Context: @pricing-research.md
@product Q2 planning. Inputs: @customer-interviews/ @eng-capacity.md
```

**Response Depth** (`+`/`-` modifiers):

| Modifier | Effect | Example |
|----------|--------|---------|
| `-` | Brief — executive summary | `@product What's launch status? -` |
| *(none)* | Standard — balanced depth | `@product What's launch status?` |
| `+` | Deep — full analysis | `@product What's launch status? +` |

**Meeting Mode**: `@product` and `@plt` return responses from individual agents speaking in their own voice, with attribution, points of agreement, tension, and synthesis. Not a monolithic AI response — a product org thinking together.

**Multi-Product Organizations**: Filter context by product.

```
/context-recall pricing product:AXIA
/feedback-recall onboarding product:SKYMOD
/portfolio-status product:AXIA
```

### Delegate to Agents (`@agent`)

Spawn autonomous agents to handle tasks. Each agent reasons independently and returns results.

```
@cpo review @board-feedback.pdf and update strategic intent
@pm break down @epic.md into user stories
@plt review @portfolio-health.md - should we pivot?
@bizops analyze @pricing-data.xlsx and create pricing model
```

**Agent Shortcuts:**

| Shortcut | Full Agent | Domain |
|----------|------------|--------|
| `@pm` | `@product-manager` | PRDs, specs, user stories |
| `@plt` | `@product-leadership-team` | Portfolio decisions |
| `@pm-dir` | `@director-product-management` | Roadmap governance |
| `@pmm-dir` | `@director-product-marketing` | GTM strategy |
| `@pmm` | `@product-marketing-manager` | Campaigns, enablement |
| `@ci` | `@competitive-intelligence` | Market analysis |
| `@prod-ops` | `@product-operations` | Launch, process |
| `@mentor` | `@product-mentor` | Career coaching, PM development |

### Use Skills Directly (`/skill`)

Create, update, or find specific deliverables inline.

```
Create a /prd for SSO integration - see @slack-thread.md
Run /competitive-analysis on Acme - @their-demo-notes.md
Update the /roadmap-theme for Growth with mobile initiatives
Find all authentication PRDs using /prd find
```

### Mix Both Patterns

Combine agents and skills naturally.

```
@pm-dir review @launch-data.xlsx and update the /gtm-strategy
@cpo review @board-feedback.pdf and update /strategic-intent
@vp-product review @sales-feedback.md and run /pricing-strategy
```

---

## What's Included

### 12 Role-Based Agents
Chief Product Officer, VP Product, Director of Product Management, Director of Product Marketing, Product Manager, Product Marketing Manager, Product Mentor, Business Operations, Business Development, Competitive Intelligence, Product Operations, Value Realization

### 2 Gateways
Product and Product Leadership Team — route to relevant agents automatically

### 133 Skills
PRDs, roadmaps, business cases, GTM strategies, pricing models, launch plans, QBR decks, competitive analyses, decision records, ROI tracking, plus 31 strategy frameworks including Porter's Five Forces, Blue Ocean, SWOT, PESTLE, Business Model Canvas, Lean Canvas, Shape Up, Wardley Maps, Seven Powers, Kano Analysis, OKR Writer, and more. Plus CRO skills, marketing psychology, programmatic SEO, email sequences, and GEO/LLM SEO.

**Eight named structural-primitive skills aligned to the Vision to Value Standard in v5.0** — `/decision-charter`, `/decision-record`, `/escalation-rule`, `/ownership-map`, `/customer-value-trace`, `/collaboration-check`, `/scale-check`, `/phase-check` — emit Conformance Level 1, 2, and 3 signals. The remaining ~125 ancillary skills receive Mode-awareness and disclosure-metadata field alignment in v5.1 (4-6 weeks after v5.0.0 is published). v5.1 is not load-bearing for the Conformance Level 3 claim.

### 28 Knowledge Packs
Professional frameworks that agents load automatically based on task context — covering prioritization, pricing, discovery, metrics, competitive analysis, GTM playbooks, stakeholder management, user research, financial modeling, and more.

### Context Layer
Organizational memory that persists across sessions:
- **Auto-registration**: All skill outputs automatically tracked in `context/documents/`
- **Decisions & Bets**: Strategic choices with assumptions and re-decision triggers
- **Feedback**: Customer and market signals linked to decisions
- **Learnings**: Accumulated wisdom from retrospectives and outcomes
- **Cross-reference graph**: Decisions, bets, feedback, and learnings linked automatically
- **Interaction History**: Full conversation logging across sessions — query with `/interaction-recall [topic]`

Query anytime with `/context-recall [topic]`

### Demo Environment
Ships with pre-populated sample data so you can explore immediately:
- 3 decision records, 2 strategic bets, 7 feedback entries, 1 PRD
- Run `/tour` for a 5-step interactive walkthrough
- **Auto-filtering**: Demo data hides automatically once you add your own content
- Demo coexists safely—use `--include-demo` flag to see it alongside production data
- `/clear-demo` removes demo entirely when ready

### ROI Tracking
Full cost-value transparency after every skill completion:
```
⏱️ ~1.5hrs saved in 31s, 19k tkns ~$0.1 cost, Value ~$150
```
- Time saved, token usage, estimated cost, and dollar value per deliverable
- Per-agent breakdown for multi-agent sessions
- Session totals and historical tracking with `/roi-report`

### Vision to Value Framework
Six phases from strategic intent to learning loop, with skills mapped to each phase

---

## What's New in v5.0.0 — Vision to Value Standard Alignment

**The runnable substrate behind the canonical claim.** v5.0.0 is a major-version release marking Product Org OS's alignment to the Decision Provenance Standard v1.0. The version jump from v4.0.1 to v5.0.0 (skipping the v4.x release line) reflects the load-bearing nature of the Standard alignment: the OS now ships the runnable substrate at `standard/v5.0/` for the Conformance Level 3 claim, which is a substantive scope expansion beyond the v4.x line.

- **`standard/v5.0/` alignment bundle** — Charter 5-state machine, decision-record lifecycle, Article 50 disclosure metadata schema (5 required fields), Conformance Reporter API (OpenAPI 3.1) at `POST /v2v/conformance/charter-escalation`, signal vocabulary across Levels 1/2/3
- **Four-layer Mode-Drift Composed Mitigation** — Layer 1 statistical detection (scaffolding in v5.0; enforcement at v5.0 lifecycle Week 7+), Layer 2 in-flow audit hook (hot from the start), Layer 3 Mode-Confirmation Audit primitive with `review-required` interrupt (hot from the start), Layer 4 named human-attestation (hot from the start) with 8 required sub-fields and 4 jurisdictional variants (US/UK/EU/IL)
- **Eight named structural-primitive skills aligned** — `/decision-charter`, `/decision-record`, `/escalation-rule`, `/ownership-map`, `/customer-value-trace`, `/collaboration-check`, `/scale-check`, `/phase-check`
- **Stream E cross-stream conformance test apparatus** — 9-category test matrix + synthetic Charter library
- **Naming directive applied** — "Vision to Value" spelled in full in human-facing prose; `v2v` retained in API endpoint paths and code identifiers per Naming Directive Distribution Pack §B.3

> ***Product Org OS v5.0 implements the Decision Provenance Standard's reporter protocol at Conformance Level 3.***

Section 6 of the Standard grades the Charter; the Standard does not certify. Conformance is a deployer-side achievement, not an OS feature. Charters authored using the OS can achieve Level 3 when deployer-side discipline matches the OS's structural support.

[**Full v5.0.0 release notes →**](./standard/v5.0/release/RELEASE-NOTES-v5.0.0.md) · [**What's New in v5.0.0 (narrative) →**](./whats-new-v5.0.0.html)

### v4.0 Foundation (carried into v5.0.0)

The v4.0 architecture — agents that know their own job, structured `metadata:`, three-tier knowledge enforcement, MANDATORY FIRST ACTIONS — is preserved and extended in v5.0.0. The 8 named structural-primitive skills inherit the v4.0 enforcement architecture and add `vision_to_value_standard:` metadata blocks.

[**What's New in v4.0 (archived) →**](./whats-new-v4.html)

### Structured Agent Architecture (v4.0)
Every agent declares what skills it uses, what knowledge it reads, and when — with mandatory enforcement. No more agents winging it from training data.

- **`metadata:` schema**: core_skills, supporting_skills, mandatory_skill_invocations, knowledge packs, RACI, delegation patterns — all under the Agent Skills Specification standard
- **Three-tier knowledge enforcement**: always-loaded (Tier 1), conditional (Tier 2), on-demand (Tier 3) — agents consult authoritative sources before producing output
- **MANDATORY FIRST ACTIONS**: blocking reads and skill invocations before substantive work
- **Self-check before output**: every response verified against context loading and skill invocation requirements

> **Upgrading from v3?** No breaking changes to invocation syntax. Deprecated frontmatter fields (`supporting-skills:`, `knowledge-packs:`, `primary-skills:`, `validator-skills:`) migrated automatically to `metadata:`. Install and go.

### Automatic Context Tracking
Decisions, deliverables, ROI, conventions — all tracked automatically across sessions.

- `hooks/os-tracker.py` — standalone CLI, zero dependencies
- Claude Code hooks for automatic triggering
- Self-diagnosis + repair when indexes drift
- See [`agent-guide.md`](./agent-guide.md) for full setup across all platforms

### MCP Integrations
Agents auto-detect connected tools (Jira, Slack, Analytics) and use them when available. Graceful fallback to text output.

### Agent Delegation Patterns
Five structured collaboration patterns: Consultation, Delegation, Review, Structured Debate, and Adversarial Review.

---

## Use Cases

| Who | What You Get |
|-----|--------------|
| **Solo PM** | Senior-level guidance on every deliverable |
| **Product Team** | Consistent standards, shared memory |
| **Product Org** | Decision frameworks, institutional knowledge |

---

## Documentation

- [**Agent Guide**](./agent-guide.md) — complete system overview for any coding agent
- [Interactive Presentation](https://yohayetsion.github.io/product-org-os) — visual overview
- [Full Documentation](./PRODUCT-ORG-CLAUDE.md) — skill reference
- [Context Tracking Setup](./AGENT-INTEGRATION.md) — hooks, CLI, platform wiring

---

## License

MIT for the Product Org OS framework code; CC-BY 4.0 for the Vision to Value Standard text and reference materials shipped under `standard/v5.0/`.

**Free & Open Source.** World-class product capabilities shouldn't be locked behind enterprise software.

Based on the Vision to Value Executive Manifesto by Yohay Etsion.

---

> *v4.0.1 repositioned Product Org OS as a framework with a portable installer; v5.0.0 preserves that posture and adds the Vision to Value Standard alignment bundle at `standard/v5.0/`. Previous `claude plugins install` commands no longer apply — use `git clone` + `python install.py` above. The Standard text is licensed under CC-BY 4.0 and citable at `https://decisionprovenance.ai` (canonical URL pending domain attachment per Phase 3.5 dispatch plan §F.2; fallback `https://executiveoperatingsystems.org/standard/`).*
