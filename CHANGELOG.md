<!--
Reviewer-Readiness Summary (delete this comment block before production deploy)

WHAT IS LOCKED:
- v5.0.0 entry text (verbatim from Wave 1 CHANGELOG-v5.0.0-entry.md)
- v4.0.1 -> v5.0.0 jump explainer paragraph at top of v5.0.0 entry
- 8 named structural-primitive skills list
- Four-layer Mode-Drift framing (L1 scaffolding, L2-4 hot from the start)
- Layer 4 attestation 8 sub-fields + 4 jurisdictional variants
- Reporter API path /v2v/conformance/charter-escalation (Naming Directive §B.3 carve-out)
- OpenAPI 3.1 wire contract version 1.1.0

WHAT IS PENDING YOHAY CONFIRMATION:
- v4.0.0 entry: reconstructed from CLAUDE.md (line 63: "v4.0.0: enforcement-first agent declarations,
  20 cross-domain specialist skills, UX Lead removed (design now via @ext-design)") + README.md
  v4.0 What's New section (lines 169-205 of current README). MARKED [reconstructed; needs Yohay
  confirmation] in the entry itself. No standalone v4.0.0 release notes file found in
  product-org-plugin/, /standard/, or root Product Org OS/.
- v4.0.1 entry: reconstructed from CLAUDE.md (line 63: "v4.0.1: repositioned as framework, dropped
  plugin wrapper, portable install.py installer, knowledge pack cleanup (28 packs, 10 unreferenced
  removed)") + footer note in current README ("Previously installed as a Claude Code plugin. v4.0.1
  repositions as a framework with a portable installer."). MARKED [reconstructed; needs Yohay
  confirmation].
- Release date for v4.0.0: NOT RECOVERED from any source. Marked [date TBD by Yohay] inline.
  Sources scanned: CLAUDE.md (only gives 4.0.1 = 2026-04-16), README.md, whats-new-v4.html (no
  release date in html metadata), product-org-plugin/standard/. Reasonable inference: late
  March 2026 (between [3.1.0] 2026-03-07 and [4.0.1] 2026-04-16). Inline placeholder reads
  "2026-04-XX" with the note.
- v5.0.0 release date "2026-05-XX (Phase 3 Day 10 target)" — Tech Lead picks actual date at publish.

WHAT NEEDS PMM-DIR CONFORMANCE-LANGUAGE PASS:
- v5.0.0 entry: zero forbidden phrasings as affirmative claims (Stream G found 4 acceptable
  forbidden-phrasing matches, all in negation/firewall enumeration contexts; this entry inherits
  the same discipline)
- Canonical claim §A.4 verbatim form is exactly correct
- Naming directive bullet does not drift toward affirmative V2V usage

WHAT IS PENDING YOHAY APPROVAL AT DRAFT URL:
- Draft branch deploys to https://yohayetsion.github.io/product-org-os-draft/
- Yohay reviews CHANGELOG entries (especially v4.x backfill text); confirms or sends edits
- Production push to main only after explicit approval
-->

# Changelog

All notable changes to Product Org OS will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [5.0.0] - 2026-05-XX (Phase 3 Day 10 target)

v5.0.0 is a major-version release marking Product Org OS's alignment to the Decision Provenance Standard v1.0. The version jump from v4.0.1 to v5.0.0 (skipping the v4.x release line) reflects the load-bearing nature of the Standard alignment: the OS now ships the runnable substrate (`standard/v5.0/`) for the Conformance Level 3 claim, which is a substantive scope expansion beyond the v4.x line, not a feature drop within it.

### Added — Vision to Value Standard Alignment Bundle

- **`standard/v5.0/`** — new top-level directory with the runnable substrate that supports the Conformance Level 3 claim:
  - `state-machines/charter-state-machine.md` — Charter 5-state forward-only lifecycle (`open` → `mode-declared` → `fields-required` → `fields-completed` → `closed`) plus `review-required` RECORD-state interrupt
  - `state-machines/decision-record-state-machine.md` — `dispatched` / `drafted` / `closed` lifecycle plus `review-required` interrupt
  - `schemas/article-50-disclosure-metadata.json` — 5 required Article 50 disclosure metadata fields per Section 4 §4.6 of the Standard (`declaring_authority`, `ai_system_identity`, `jurisdictional_applicability`, `disclosure_text_pointer`, `attached_at`)
  - `schemas/charter.schema.json` — Charter object schema (JSON Schema Draft 2020-12)
  - `schemas/decision-record.schema.json` — Decision-record object schema (JSON Schema Draft 2020-12)
  - `conformance/reporter-api-spec.md` — `POST /v2v/conformance/charter-escalation` contract (OAuth 2.0 client_credentials, idempotency-key, sync ack-only, standardized error envelope, 60/min rate limit)
  - `conformance/reporter-api.openapi.yaml` — OpenAPI 3.1 wire contract (info.version 1.1.0; `escalation_type` enum 9 values per M1 v1.1 amendment)
  - `conformance/signal-vocabulary.md` — Conformance signal vocabulary across Levels 1, 2, 3 with sample audit-cadence binding (15% rolling sample with first-100 + edge-case overrides)
  - `mode-drift/layer-1-detection.md` — Statistical detection scaffolding (D.2.1 sub-track owns enforcement at OS v5.0 lifecycle Week 7+)
  - `mode-drift/layer-2-audit-hook.md` — 4-question Substantive-Authorship Challenge at Mode-1 record close, fires hot from the start
  - `mode-drift/layer-3-mode-confirmation.md` — `review-required` RECORD-state interrupt + 5-rule peer-reviewer designation (pool minimum 3, author/Charter-owner exclusions, recusal carve-out), fires hot from the start
  - `mode-drift/layer-4-attestation.md` + `layer-4-attestation.schema.json` — `mode_classification_attestation` structured object with 8 required sub-fields (full name, role, employer, timestamp, jurisdiction enum, language version, verbatim signed text, capacity) + 4 jurisdictional variants (US/UK/EU/IL), fires hot from the start
  - `tests/cross-stream-conformance-check.md` — Stream E test apparatus, 9-category test matrix
  - `tests/synthetic-charter-library.md` — 8 synthetic Charters covering all jurisdictions and edge cases

### Changed — 8 Named Structural-Primitive Skills

The following skills are aligned to emit Vision to Value Standard conformance signals (Level 1, 2, 3 vocabulary). Frontmatter `version:` bumped to 5.0.0 with new `vision_to_value_standard:` metadata block:

- `/decision-charter` — output schema matches Standard Section 3 (5-state lifecycle + 15 fields + 3-value mode-declaration enum)
- `/decision-record` — schema matches Standard Section 5; adds `dispatch_mode` and `disclosure_metadata_pointer` fields
- `/escalation-rule` — aligns with Layer 3 Mode-Confirmation Audit primitive (firing authority for `no_silent_mode_drift_in_sample` Level 2 signal on Seam 3 cadence)
- `/ownership-map` — emits `accountable_owner_named` Level 1 signal
- `/customer-value-trace` — emits Level 2 signal stub
- `/collaboration-check` — emits Level 2 signal stub
- `/scale-check` — emits Level 2 signal stub
- `/phase-check` — emits Level 1 + Level 2 signals

### Added — Conformance Reporter API Wire Contract

- OpenAPI 3.1 spec at `standard/v5.0/conformance/reporter-api.openapi.yaml` (info.version 1.1.0) — additive enum extension over the locked M1 v1.0 contract; backward-compatible for v1.0 clients
- Prose specification at `standard/v5.0/conformance/reporter-api-spec.md` — locked at v1.1.0 with three-way co-sign (AI Architect + Backend Dev + Chief Architect) on the `peer_reviewer_pool_underflow` enum extension

### Added — Stream E Test Apparatus

- 9-category cross-stream conformance check matrix
- 8-Charter synthetic library covering US/UK/EU/IL jurisdictions and Mode 1 / Mode 2 / mode-1-with-embedded-mode-2-summary edge cases

### Documentation

- README.md updated for Vision to Value Standard alignment + Conformance Level 3 claim per Conformance Framing Locked Language Table §A.4 (verbatim canonical claim)
- CLAUDE.md updated with Standard ↔ OS Interface Contract pointer (`standard/v5.0/`)
- New `whats-new-v5.0.0.html` narrative page (companion to RELEASE-NOTES-v5.0.0.md)
- Naming Directive Distribution Pack applied to all human-facing artifacts: "Vision to Value" full spelling in prose; `v2v` retained ONLY in API endpoint paths (`/v2v/conformance/charter-escalation`), code identifiers (`v2v_conformance_signal`, `v2v_phase`), file system paths, and internal log streams per §B.3

### Deferred to v5.1 (4-6 weeks after v5.0.0 is published)

- ~125 ancillary OS skills receive Mode-awareness + disclosure metadata field alignment
- Layer 1 enforcement-mode activation (technically OS v5.0 lifecycle Week 7+, after Layer C adversarial corpus authoring completes Weeks 4-6)

v5.1 is NOT load-bearing for the Conformance Level 3 claim — it improves coverage breadth, not conformance depth. Charters authored using the v5.0.0 OS can achieve Level 3 today when deployer-side discipline matches the OS's structural support.

### Breaking Changes

None for end users. The 8 named structural-primitive skills retain their existing invocation syntax; alignment is internal (signal emission + schema field additions). The `standard/v5.0/` directory is additive.

For deployers integrating with the Conformance Reporter API: the wire contract is new; no prior version exists. The `escalation_type` enum extension from 8 to 9 values is additive and backward-compatible for any future v1.0 client implementations.

### Conformance Framing (Locked Language)

Per Conformance Framing Locked Language Table §A.3-§A.5:

**Acceptable verbatim canonical claim**:
> ***Product Org OS v5.0 implements the Decision Provenance Standard's reporter protocol at Conformance Level 3.***

**Forbidden** (NEVER appears as affirmative claim in v5.0.0 surfaces): "compliant with the Standard," "Standard-compliant" (single-token or compound forms), "certified Standard implementation," "guarantees Level 3 conformance," "the Standard guarantees Level [N]," "audit-defensible," "legally defensible," "audit-grade provenance," "compliance-aligned," "compliance-grade," "regulator-ready," "certification-ready."

Section 6 of the Standard grades the Charter; the Standard does not certify. Conformance is a deployer-side achievement, not an OS feature.

### Authority

- Phase 3 dispatch plan v1.1 §M4 + v1.2 amendment §F.4
- Stream D scope spec v1
- Stream E GO WITH CHANGES verdict (Stream G cleanup pass closure)
- M1 conformance reporter API contract v1.1.0 (locked; three-way co-sign on additive enum extension)
- Mode-Drift composed mitigation sub-spec FINAL
- 0.5.B Standard ↔ OS Interface Contract
- Conformance Framing Locked Language Table + Naming Directive Distribution Pack (re-locked 2026-04-30 at v5.0.0)

## [4.0.1] - 2026-04-16

> **[reconstructed; needs Yohay confirmation]** This entry is backfilled from the project README footer note and `Product Org OS/CLAUDE.md` line 63. No standalone v4.0.1 release notes file was located. Confirm at draft URL review.

### Changed
- **Repositioned as framework, not plugin** — the Product Org OS is no longer distributed as a Claude Code plugin wrapper. It is now distributed as a framework with a portable installer. Previous `claude plugins install github:yohayetsion/product-org-os` commands no longer apply. New install path: `git clone https://github.com/yohayetsion/product-org-os.git` + `python install.py` to copy skills into `~/.claude/skills/`.
- **Plugin wrapper dropped** — `plugin.json` and the Claude Code plugin metadata layer are no longer the distribution surface. Skills follow the Agent Skills specification and load natively in Claude Code (and technically in any tool that reads SKILL.md files; only Claude Code is validated end-to-end).
- **Knowledge pack cleanup** — knowledge pack count reduced from 38 to 28. 10 unreferenced knowledge packs removed after a coverage audit confirmed no agent or skill loaded them. The remaining 28 packs match actual agent and skill consumption.

### Migration Notes
- Existing users who installed via `claude plugins install` should re-install via `git clone` + `python install.py`. Skills directory location moves to `~/.claude/skills/`. No content was lost in the framework reposition; all 133 skills, 12 agents, and 2 gateways are present in the new distribution form.
- The `setup-skills.py` script in the workspace root can sync skills directly from a local checkout into `~/.claude/skills/` without going through the plugin manager.

### Documentation
- README.md updated with new install instructions (`git clone` + `python install.py`).
- Footer note added: "Previously installed as a Claude Code plugin. v4.0.1 repositions as a framework with a portable installer."

## [4.0.0] - 2026-04-XX (date pending Yohay confirmation)

> **[reconstructed; needs Yohay confirmation]** This entry is backfilled from `Product Org OS/CLAUDE.md` line 63 ("v4.0.0: enforcement-first agent declarations, 20 cross-domain specialist skills, UX Lead removed (design now via @ext-design)") and the v4.0 What's New section in the project README (lines 169-205). The actual v4.0.0 release date was not recovered from any source file scanned (CLAUDE.md, README.md, `whats-new-v4.html`, or `product-org-plugin/standard/`). Reasonable inference is late March 2026 (between `[3.1.0] - 2026-03-07` and `[4.0.1] - 2026-04-16`). Confirm at draft URL review.

### Added — Enforcement-First Agent Architecture

- **Structured `metadata:` schema across all 12 agents** — every agent declares its core skills, supporting skills, knowledge packs, RACI matrix, delegation patterns, and v2v phases under the Agent Skills Specification standard. No more agents winging it from training data.
- **Three-tier knowledge pack enforcement**:
  - Tier 1 (always-loaded): preload knowledge packs at agent start
  - Tier 2 (conditional): trigger keywords activate the pack mid-task
  - Tier 3 (on-demand): agent loads the pack when explicitly required
- **MANDATORY FIRST ACTIONS** — blocking reads and skill invocations before substantive work, declared in agent prompts.
- **Mandatory skill invocations with task-type triggers and escape valves** — agents declare which skills must run for which task types and what escape conditions are acceptable.
- **Self-Check enforcement sections** — every response is verified against the agent's declared context-loading and skill-invocation requirements before output.
- **20 cross-domain specialist skills** added to broaden the OS coverage of cross-functional product work (specific skills enumerated in the v4.0 What's New presentation at `whats-new-v4.html`).

### Changed
- **Vision to Value methodology consolidated into single `PRINCIPLES.md`** — replaces the prior multi-file principles layout. All agents inherit a single principles document.
- **100% metadata coverage across all 12 agents** — every agent SKILL.md frontmatter conforms to the v4 metadata schema (`metadata.skill_type`, `metadata.team`, `metadata.core_skills`, `metadata.preload_knowledge_packs`, `metadata.delegation_patterns`, etc.). See `.claude/rules/agent-metadata-schema.md` for the v4.0 schema definition.

### Removed
- **UX Lead agent retired** — full design coverage moved to the `@ext-design` Extension Team gateway. The UX Lead skill file is removed from the OS distribution; design work routes through the Extension Teams Design gateway.
- **Deprecated frontmatter fields removed** from agent SKILL.md files: `supporting-skills:`, `knowledge-packs:`, `primary-skills:`, `validator-skills:`. These fields migrated to `metadata.core_skills`, `metadata.supporting_skills`, `metadata.preload_knowledge_packs` per the v4.0 schema.

### Migration Notes
- **No breaking changes to invocation syntax.** `@agent` and `/skill` invocations continue to work as in v3.x.
- Deprecated frontmatter fields migrate automatically when running the v4 SKILL.md update script. See `.claude/rules/agent-metadata-schema.md` for the full mapping table.
- UX Lead invocations (`@ux-lead`) should be replaced with `@ext-design` gateway calls.

### Documentation
- New `whats-new-v4.html` interactive presentation at the GitHub Pages site documenting the v4.0 architecture changes.
- README.md updated with the v4.0 What's New section and the "Structured Agent Architecture" sub-section.
- New `agent-guide.md` providing a complete top-to-bottom guide for any coding agent to understand, install, and operate the system.

## [3.1.0] - 2026-03-07

### Added
- **4 New Discovery & Learning Skills**
  - `/assumption-map` (Phase 1) — Assumption mapping based on Itamar Gilad's framework. Identify, surface, score (impact × uncertainty), prioritize via 2×2 matrix, and plan validation.
  - `/opportunity-tree` (Phase 1) — Opportunity solution tree based on Teresa Torres' Continuous Discovery Habits. Define outcomes, discover opportunities, structure tree, assess, generate solutions, design experiments.
  - `/experiment-design` (Phase 1-2) — Experiment design based on Savoia's pretotyping. 8 experiment types (Fake Door, Concierge, Wizard of Oz, etc.), hypothesis-driven with guard rails.
  - `/compound` (Phase 6) — Learning extraction and compounding. Extract insights from outcomes, root cause analysis, generalize into reusable principles, save to context layer.

### Changed
- **Skill Routing Updated** — `rules/skill-awareness.md` and `rules/v2v-flow.md` updated with new skills in Phase 1 and Phase 6 tables, routing keywords for discovery/validation, and task type mapping. Document-generating skill count: 43 → 47.

## [3.0.1] - 2026-02-13

### Changed
- **Agent Skills Standard Alignment** — All 93 SKILL.md files updated to align with Anthropic's Agent Skills open standard
  - Enhanced `description:` fields with trigger phrases for improved auto-routing and skill discovery
  - Added `user-invocable:` field to all agent skills (false for agents, true for template skills)
  - Added `metadata:` block (author, version, category) to all skills for distribution readiness
  - Added `compatibility:` field declaring Product Org OS v3+ dependency
  - Zero functional changes — all existing behavior preserved

### Scope
- 13 OS agent SKILL.md files
- 8 OS alias SKILL.md files
- 2 OS gateway SKILL.md files
- 61 OS template/workflow SKILL.md files
- 9 misc SKILL.md files (marketing-growth, developer-workflow, creative-process)

## [3.0.0] - 2026-02-10

### Added
- **Product Mentor agent** (`@mentor` / `@product-mentor`) — Career coaching, PM skill assessment, stakeholder navigation, OS usage optimization

- **MCP Integration Framework** — agents auto-detect and use connected tools
  - `rules/mcp-integration.md` — core integration rule with detection pattern and graceful fallback
  - `integrations/` folder with 6 setup templates (Jira, Linear, Slack, Notion, GitHub, Analytics)
  - Integration Awareness section added to 8 agent SKILL.md files
  - Tool integration line added to agent spawn protocol (Section 2)

- **9 Domain Knowledge Packs** in `reference/knowledge/`
  - Prioritization, Pricing Frameworks, Discovery Methods, Metrics Frameworks
  - Competitive Frameworks, GTM Playbooks, Stakeholder Management
  - User Research, Financial Modeling
  - Three-layer architecture: Vision to Value Process → Domain Knowledge → Agent Persona
  - Knowledge Sources section added to 12 agent SKILL.md files
  - Knowledge pack catalog added to `rules/skill-awareness.md`

- **Enhanced Context Layer**
  - `rules/auto-context.md` — automatic context injection before deliverable creation
  - `rules/context-graph.md` — cross-reference graph connecting decisions, bets, feedback, learnings
  - `context/index.json` upgraded to v3.0 schema with structured indexes
  - Enhanced 6 context skill SKILL.md files with graph traversal and auto-linking
  - Updated `rules/context-management.md`, `CONTEXT-LAYER-DESIGN.md`, `context/README.md`

- **4 Agent Delegation Patterns**
  - `rules/delegation-protocol.md` — Consultation, Delegation, Review, Structured Debate
  - Updated `rules/agent-spawn-protocol.md` Section 5 with pattern selection
  - Updated `rules/parallel-execution.md` with delegation-enhanced patterns

- **Claude Agent SDK Design** (Project SaaS)
  - `sdk-bridge-design.md` — OS-to-SDK architecture mapping
  - `api-contract.md` — REST + WebSocket API specifications
  - `data-model.md` — PostgreSQL schema for cloud context layer
  - `agent-runtime.md` — CLI vs. cloud execution model
  - `migration-guide.md` — CLI to cloud migration path

### Changed
- **Conversational-First Response Model** — all 13 agents keep responses to 2-4 paragraphs, create documents for detailed analysis. Prevents parent session compression from losing agent voice. Enforced via agent spawn protocol Section 2.
- **Meeting Mode Enforcement** — Claude Code is invisible infrastructure when Product Org is active. Agent responses are the complete output with zero preamble/postamble. Synthesis attributed to named senior agent, never unnamed. `rules/meeting-mode.md` defines format and self-check.
- **No Fabricated Numbers Rule** — agents never invent financial projections, timeline estimates, or implementation costs. Use frameworks, placeholders (`[TBD]`), and calculation structures instead. `rules/no-estimates.md` expanded with detailed examples and redirect patterns.

- **Agent Skills Standard Alignment** — all SKILL.md files updated
  - `tools:` → `allowed-tools:` in all frontmatter (63 files)
  - `user-invocable: true/false` added to all SKILL.md files
  - `plugin.json` updated to v3.0.0 with `"standard": "agent-skills"`
  - Cross-platform compatibility with Cursor, Copilot, Gemini CLI

- **Documentation Overhaul**
  - README.md rewritten with v3 features, cross-platform support
  - PRODUCT-ORG-CLAUDE.md updated with 5 new sections (MCP, Knowledge, Delegation, Context, Cross-Platform)
  - Plugin statistics updated (5 gateways, 9 knowledge packs, 6 integration templates, 4 delegation patterns)
  - Cross-platform language audit throughout

- **Setup Command** (`/setup`) updated for v3
  - Pre-flight audit expanded from 28 to 32 items (added v3 rules)
  - `context/index.json` template upgraded to v3.0 schema
  - Tour language updated for cross-platform

## [2.4.1] - 2026-01-25

### Added
- **`/tour` skill** - Interactive 5-step walkthrough of Product Org OS
  - Gateways → Agents → Skills → Documents → Utilities
  - Works anytime, not just during setup
  - Uses demo data for hands-on learning
- **Demo Auto-Filtering** - Demo data hides automatically in production
  - `rules/demo-data-handling.md` defines filtering behavior
  - Demo excluded from queries when production data exists
  - Use `--include-demo` flag to see demo alongside production
  - Use `--demo-only` flag for testing/learning
- Updated `/setup` with new onboarding options:
  - "Take the tour" - 5-step interactive walkthrough
  - "Explore on my own" - Quick reference card

### Changed
- `/context-recall`, `/feedback-recall`, `/portfolio-status`, `/relevant-learnings` - Auto-filter demo data
- Skill count: 60 → 61
- Marketing site updated with demo auto-filtering messaging

## [2.4.0] - 2026-01-25

### Added
- **Demo Environment** for exploring plugin capabilities
  - Pre-populated demo content: 3 decisions, 2 strategic bets, 7 feedback entries, 1 PRD
  - `/clear-demo` skill to remove demo content for production use
  - `/reset-demo` skill to restore demo content for testing/demos
  - First-run welcome experience in `/setup`
- **ROI Tracker** for measuring time savings
  - `reference/roi-baselines.md` with time-savings estimates per skill
  - `rules/roi-display.md` for mandatory ROI display after skill completion
  - `context/roi/` for session tracking
  - `/roi-report` skill for ROI dashboard
- **Scalable Context System** with JSON indexing
  - `context/index.json` for fast topic-based retrieval
  - `/index-folder` skill for folder indexing
  - Updated `/context-save` with JSON indexing (Step 5)
  - Updated `/context-recall` with JSON index as primary search
- **New Rules**
  - `rules/intelligent-routing.md` for automatic request routing
  - `rules/no-estimates.md` to avoid time predictions

### Changed
- **All 13 agent personas enhanced** with full Vision to Value template:
  - Core Accountability, How I Think, RACI breakdown
  - Sub-agent spawning patterns (permissive: "Don't ask for permission")
  - Anti-patterns as redirects, not blocks
  - Success signals and collaboration patterns
  - Emojis in response format for visual identity
- Skill count: 56 → 60

## [2.3.1] - 2026-01-23

### Added
- **Agent Shortcuts** for faster access to common agents
  - `/pm` → `/product-manager`
  - `/plt` → `/product-leadership-team`
  - `/pm-dir` → `/director-product-management`
  - `/pmm-dir` → `/director-product-marketing`
  - `/pmm` → `/product-marketing-manager`
  - `/vpp` → `/vp-product`
  - `/prodops` → `/product-operations`
- Documents context item in Context Layer (tracked via registry)

### Changed
- Marketing site: "Free & Open Source" now links to GitHub repo
- Marketing site: "13 Specialized Agents" → "13 Role-Based Agents"
- Marketing site: Agent cards show shortcuts (/pm, /plt, etc.)
- Marketing site: Dynamic examples use natural language patterns
- Marketing site: "How to Use It" examples are conversational
- Marketing site: Use Cases show practical team/org workflows
- Marketing site: Context Layer shows 6 balanced items including Documents
- Marketing site: Footer links to LinkedIn profile

## [2.3.0] - 2026-01-23

### Added
- **Document Intelligence** for 43 document-generating skills
  - Three modes: Create, Update, Find
  - Automatic mode detection based on user input signals
  - Confidence-based decision thresholds (≥85% auto-proceed)
  - Document Registry support for tracking strategic documents
- Document Intelligence Template (`templates/document-intelligence.md`)
- "Document Continuity Across Phases" guidance in v2v-flow.md

### Changed
- 43 skill files enhanced with Document Intelligence block
- Skill descriptions updated to reflect Create/Update capability
- Argument hints now show update path option
- Marketing site dynamic examples include agents and skills
- Marketing site "Start Creating" includes update mode examples

### Documentation
- Added "Document Intelligence" section to PRODUCT-ORG-CLAUDE.md
- Added "Document Intelligence" section to rules/skill-awareness.md
- Added "Working with Existing Documents" examples to README.md
- Added favicon to marketing site (index.html)

## [2.2.1] - 2026-01-22

### Added
- LICENSE file in plugin directory (MIT)
- CHANGELOG.md with version history

### Changed
- Fixed URLs in plugin.json to point to `yohayetsion/product-org-os`
- Fixed URLs in README.md (install command, presentation links)

### Distribution
- Submitted to official Claude Code plugin directory (PR #20135)
- Available via: `claude plugins install github:yohayetsion/product-org-os`

## [2.2.0] - 2026-01

### Added
- `/product` gateway as single entry point to the product organization
- 5 principle validator skills: `/ownership-map`, `/customer-value-trace`, `/collaboration-check`, `/scale-check`, `/phase-check`
- 4 new rules: `v2v-flow.md`, `principles-enforcement.md`, `parallel-execution.md`, `skill-awareness.md`
- Vision to Value phase reference mapping (`reference/v2v-skill-map.md`)
- Principles tracking folder with scorecard template

### Changed
- All 13 agents now have full access to all 56 skills
- 35 skills updated with Vision to Value phase markers
- 4 skills enhanced with principle additions (`decision-record`, `outcome-review`, `strategic-bet`, `commitment-check`)
- Context layer expanded with Vision to Value phase tracking and principles tracking
- Updated documentation with gateway, parallel execution, and principle validators

## [2.1.0] - 2026-01

### Added
- Vision to Value phase markers across all skills
- Principle additions to key skills
- Parallel execution patterns

## [2.0.0] - 2025-12

### Added
- Context layer for organizational memory
- Feedback capture and recall system
- 13 role-based agents

### Changed
- Skills reorganized by Vision to Value phase

## [1.0.0] - 2025-11

### Added
- Initial release with 41 skills
- Core deliverable templates
- Basic plugin structure
