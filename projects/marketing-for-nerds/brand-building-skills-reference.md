---
type: reference
title: Brand-Building Skills — AI Agent Skills Library for Brand Strategy
created: '2026-06-16T00:00:00.000Z'
source_url: 'https://github.com/arnabbagxd/Brand-building-skills'
source_type: github-repo
related_projects:
  - marketing-for-nerds
  - hermes-multi-project-automation-masterplan
ingested_via: 'mcp:put_page'
ingested_at: '2026-06-16T06:51:33.874Z'
source_kind: 'mcp:put_page'
tags:
  - agent-skills-spec
  - ai-agents
  - brand-skills
  - brand-strategy
  - marketing-automation
---

# Brand-Building Skills — AI Agent Skills Library

**Repository:** [arnabbagxd/Brand-building-skills](https://github.com/arnabbagxd/Brand-building-skills)  
**Type:** Agent Skills Library (compatible with Claude Code, Cursor, Windsurf, Agent Skills spec)  
**Author:** arnabbagxd  
**Installation:** `npx skills add arnabbagxd/brand-building-skills`

---

## Overview

A comprehensive, production-ready collection of AI agent skills designed for **brand strategists, agency owners, and founders**. Provides specialized workflows for brand development, identity, positioning, messaging, and channel-specific marketing execution.

**Key differentiator:** Enforces brand consistency across all outputs through the foundational `brand-context` skill—a single source of truth that all downstream skills reference.

---

## Core Skill Categories

### 1. Strategy & Foundation (Discovery Phase)

| Skill | Purpose | Output |
|-------|---------|--------|
| **brand-context** | Mandatory foundational skill; creates `.agents/brand-context.md` | Unified brand reference (all other skills depend on this) |
| **brand-strategy** | Full discovery workflow with questionnaires | Comprehensive strategy report + client recommendations |
| **brand-naming** | Generate or evaluate brand names with strategic rationale | Name options with reasoning + trademark research |
| **brand-architecture** | Define relationships between sub-brands (Branded House vs. House of Brands) | Architecture diagram + governance rules |
| **brand-manifesto** | Craft belief-driven brand declarations | Belief statement + purpose narrative |

### 2. Identity & Messaging (Creation Phase)

| Skill | Purpose | Output |
|-------|---------|--------|
| **brand-identity** | Visual identity brief (logos, color palette, typography, imagery) | Design brief for external designers |
| **brand-voice** | Verbal identity rules, tone guidelines, channel adaptations | Voice matrix (tone, vocabulary, formality by channel) |
| **brand-story** | Origin narratives in 3 formats (long, short, one-liner) | Story formats + emotional hooks |
| **brand-messaging** | Full messaging hierarchy (taglines, value props, proof points) | Messaging pyramid + 50+ variations by audience |

### 3. Audience & Positioning (Research Phase)

| Skill | Purpose | Output |
|-------|---------|--------|
| **target-audience** | ICP definition with psychographics + behavioral patterns | Audience profile + seasonal/contextual triggers |
| **brand-positioning** | Competitive mapping + positioning territory statement | Perceptual map + 3-5 unique positioning options |
| **competitor-branding** | Market gap analysis + differentiation opportunities | Competitive landscape analysis + white space opportunities |

### 4. Growth & Channel Marketing (Execution Phase)

#### Paid Media
- **Meta Ads Strategy** — ROAS optimization, creative testing, audience segmentation
- **Google Ads Strategy** — Search/PMax bidding, keyword strategy, landing page optimization

#### Owned Channels
- **Email Strategy** — Segmentation, nurture sequences, lifecycle automation (integrates with Mautic)
- **WhatsApp Strategy** — Messaging cadence, opt-in flows, contact management
- **ASO** (App Store Optimization) — Keyword research, creative testing, localization

#### Content & Influencer
- **UGC Strategy** — User-generated content sourcing, rights management, distribution
- **Influencer Marketing** — Vetting criteria, brief templates, FTC compliance, contract templates

#### D2C vs. B2B Specialization
- **D2C** — Unit economics framework, CAC/LTV optimization, seasonal campaigns, retention tactics
- **B2B** — Buying committee mapping, thought leadership, account-based marketing, nurture timing

### 5. Management & Evolution (Governance Phase)

| Skill | Purpose | Output |
|-------|---------|--------|
| **brand-audit** | Health assessment across 6 dimensions (clarity, consistency, alignment, authority, affinity, accessibility) | Audit report + improvement roadmap |
| **rebranding** | Guide strategic transformation + transition narratives | Rebranding playbook + stakeholder communication |
| **brand-measurement** | Define KPIs + tracking systems for brand equity | Dashboard spec + attribution model |
| **brand-guidelines** | Create final standards document (Figma-ready) | Brand guidelines PDF/Figma export |

---

## Workflow Sequences

### New Brand Launch (6-8 weeks)
```
1. Context          → brand-context (mandatory first step)
2. Research         → target-audience + competitor-branding
3. Strategy         → brand-positioning + brand-strategy
4. Creation         → brand-naming + brand-identity + brand-voice
5. Messaging        → brand-messaging + brand-story
6. Documentation    → brand-guidelines (final client deliverable)
7. Execution        → channel-specific strategies (Meta, Email, etc.)
```

### Agency Client Onboarding (2-week sprint)
```
1. Discovery        → brand-strategy (questionnaire + report)
2. Development      → brand-naming + brand-identity + brand-voice
3. Delivery         → brand-messaging + brand-guidelines
```

### Recurring Audit Cycle (quarterly)
```
1. Assessment       → brand-audit (6-dimension health check)
2. Measurement      → brand-measurement (KPI tracking)
3. Updates          → brand-positioning or brand-messaging (if drift detected)
```

---

## Technical Specifications

### Installation & Structure
```bash
npx skills add arnabbagxd/brand-building-skills
# Installs to: .agents/skills/

# Directory structure:
skills/skill-name/
├── SKILL.md              # Main instructions (max 500 lines)
├── evals/                # Test cases (evals.json)
└── references/           # Additional documentation
```

### Validation
```bash
bash validate-skills.sh   # Ensures compliance before contribution
```

### Compatibility
- ✅ Claude Code
- ✅ Cursor
- ✅ Windsurf
- ✅ Any agent supporting [Agent Skills spec](https://agentskills.io)

---

## Integration with Hermes Agent (Strategic Fit)

### Where Brand-Skills Fit in Your Stack

**Layer in the Hermes automation hierarchy:**
```
Hermes Agent (Orchestrator)
    ├── Brand-Skills (Strategic context)
    ├── OpenClaw (Multi-tool execution)
    ├── Claude Code (Complex planning)
    └── Mautic/Ad Platforms (Campaign execution)
```

**Primary Integration Points:**

1. **Pre-Campaign Phase** — Hermes calls brand-skills to:
   - Generate brand context snapshots
   - Validate messaging consistency
   - Create channel-specific briefs

2. **Content Generation Phase** — OpenClaw/Claude inject brand-voice + brand-messaging outputs:
   - Email templates inherit voice rules
   - Ad copy respects positioning language
   - Social captions follow tone guidelines

3. **Campaign Measurement Phase** — Hermes schedules brand-measurement skills:
   - Quarterly brand health audits
   - Equity tracking (Brand Lift studies)
   - Competitive positioning updates

4. **Multi-Brand Scalability** — For agencies managing 10+ brands:
   - Each brand gets `.agents/brand-context-[name].md`
   - Cron jobs run full discovery→guidelines cycles per brand
   - Outputs tagged/indexed in brain by client

---

## Raw GitHub Details

- **License:** Not specified in summary (check repo directly)
- **Dependencies:** Node.js (for `npx skills` CLI)
- **Maintenance:** Active (validate before each use)
- **Community:** Open contributions (follow directory structure + validation rules)

---

## Related Pages

- [[projects/marketing-for-nerds]] — Parent project
- [[projects/marketing-for-nerds/hermes-multi-project-automation-masterplan]] — Orchestration architecture
- [[projects/marketing-for-nerds/brand-skills-hermes-integration-flow]] — Integration workflow diagram
- [[projects/marketing-for-nerds/mautic-overview]] — Email/SMTP execution layer
