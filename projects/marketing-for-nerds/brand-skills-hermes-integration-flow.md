---
type: project
title: Brand-Skills + Hermes Integration Flow — Automation Trigger Points
parent: projects/marketing-for-nerds/hermes-multi-project-automation-masterplan
created: '2026-06-16T00:00:00.000Z'
related:
  - projects/marketing-for-nerds/brand-building-skills-reference
  - projects/marketing-for-nerds/hermes-multi-project-automation-masterplan
ingested_via: 'mcp:put_page'
ingested_at: '2026-06-16T06:51:52.832Z'
source_kind: 'mcp:put_page'
tags:
  - brand-skills
  - hermes-automation
  - integration-flow
  - marketing-automation
  - workflow-orchestration
---

# Brand-Skills + Hermes Integration Flow

**Purpose:** Define where and how Hermes Agent calls Brand-Skills to maintain brand consistency across multi-project automation.

**Status:** v1.0-draft (ready for implementation)  
**Last Updated:** 2026-06-16

---

## The Integration Model

```
┌─────────────────────────────────────────────────────────────┐
│                    HERMES AGENT (Orchestrator)              │
│  Central decision-making, memory, multi-project routing     │
└──────────────────┬──────────────────────────────────────────┘
                   │
        ┌──────────┼──────────┐
        ▼          ▼          ▼
   ┌────────┐ ┌─────────┐ ┌──────────┐
   │ Brand- │ │ OpenClaw│ │ Claude   │
   │ Skills │ │ (Tools) │ │ Code     │
   │        │ │         │ │(Planning)│
   └────────┘ └────┬────┘ └──────────┘
        │          │
        └────┬─────┘
             ▼
   ┌─────────────────────┐
   │ Content + Campaigns │
   │ (Mautic/Ads/Social) │
   └─────────────────────┘
```

---

## Trigger Points: Where Hermes Calls Brand-Skills

### 1. **Initialization Trigger** (On-Demand → Set Brand Context)

**When:** New brand added to portfolio OR existing brand strategy refresh  
**Hermes Action:** Detect brand onboarding request  
**Calls:** `brand-context` skill

```yaml
Trigger:
  source: Hermes Agent (user command or inbound request)
  event: "new brand [Brand Name] — [what it does], targeting [audience]"
  
Action:
  1. Parse brand details from request
  2. Execute brand-context skill → generates .agents/brand-context-[Brand].md
  3. Store `.agents/brand-context-[Brand].md` in brain at:
     projects/[brand-slug]/_brand-context.md
  4. Tag: #brand-context-set
  5. Notify via brain and Telegram: "Brand context ready for [Brand]"
```

**Output stored in brain:** `projects/[brand-slug]/_brand-context.md` (source of truth)

---

### 2. **Discovery Trigger** (Weekly or Demand → Full Strategy)

**When:** Campaign launch OR quarterly strategy review  
**Hermes Action:** Schedule recurring audit or respond to request  
**Calls:** `brand-strategy`, `target-audience`, `competitor-branding`

```yaml
Trigger:
  cron: "0 9 * * 1"  # Weekly Monday 9am (or on-demand)
  event: "campaign brief needed for [Brand]"
  
Action:
  1. Retrieve brand-context from brain
  2. Run brand-strategy skill → questionnaire + report
  3. Run target-audience skill → ICP + psychographics
  4. Run competitor-branding skill → market gaps
  5. Synthesize into "Campaign Brief" page:
     projects/[brand-slug]/campaign-brief-[date].md
  6. Tag: #campaign-brief, #discovery-phase
  7. Surface top gaps/opportunities to user via brain comment
```

**Output stored:** `projects/[brand-slug]/campaign-brief-[YYYY-WW].md`

---

### 3. **Content Creation Trigger** (Per-Campaign → Brand Consistency Injection)

**When:** Blog post, email, ad copy, social caption being written  
**Hermes Action:** Inject brand-voice + brand-messaging into Claude/OpenClaw context  
**Calls:** `brand-voice`, `brand-messaging`

```yaml
Trigger:
  event: "generate [content-type] for [Brand]"
  content_type: "email | blog | ad-copy | social-caption | landing-page"
  
Actions:
  1. Retrieve brand-context + brand-voice + brand-messaging from brain
  2. Format as system instructions for OpenClaw/Claude:
     """
     Brand Voice Guidelines:
     - Tone: [from brand-voice skill]
     - Vocabulary: [from brand-voice skill]
     - Forbidden words: [from brand-voice skill]
     
     Messaging Hierarchy:
     - Tagline: [from brand-messaging skill]
     - Value Props: [from brand-messaging skill]
     - Proof Points: [from brand-messaging skill]
     """
  3. Pass to OpenClaw with: "create [content-type] following these brand rules"
  4. OpenClaw generates content respecting voice/messaging constraints
  5. Store output at: projects/[brand-slug]/content/[content-type]/[title].md
  6. Tag: #branded-content, #[content-type]
  7. Hermes reviews output: "Does this match brand voice?" (auto-check or human)
```

**Output stored:** `projects/[brand-slug]/content/[type]/[title].md`

---

### 4. **Campaign Brief Trigger** (Per-Channel → Channel-Specific Optimization)

**When:** Launching paid media (Meta/Google) or owned channel (Email/SMS)  
**Hermes Action:** Route to channel-specific brand-skills  
**Calls:** `brand-identity` (visual), `paid-media` (Meta/Google), `owned-channels` (Email/WhatsApp)

```yaml
Trigger:
  event: "launch campaign [Brand] on [channel]"
  channels: "meta-ads | google-ads | email | whatsapp | asO"
  
Actions:
  Meta Ads:
    1. Retrieve brand-identity (visual guidelines)
    2. Run paid-media skill (Meta variant) → creative strategy
    3. Generate ad brief: projects/[brand-slug]/campaigns/meta-[date].md
    4. Output includes: ROAS targets, audience segments, creative specs
    5. Pass to OpenClaw: "create Meta ad copy following this brief"
  
  Email:
    1. Retrieve brand-voice (email tone / segment-specific messaging)
    2. Run owned-channels skill (Email variant) → nurture sequence
    3. Generate email brief: projects/[brand-slug]/campaigns/email-[date].md
    4. Store sequence template in Mautic via API
    5. Tag Mautic campaigns with brand-context slug for tracking
  
  Google Search Ads:
    1. Retrieve brand-messaging (value props, taglines)
    2. Run paid-media skill (Google variant) → keyword + copy strategy
    3. Generate brief: projects/[brand-slug]/campaigns/google-[date].md
    4. Pass to OpenClaw: "create Google ad copy + landing page headlines"
```

**Output stored:** `projects/[brand-slug]/campaigns/[channel]-[date].md`

---

### 5. **Measurement & Audit Trigger** (Monthly/Quarterly → Brand Health)

**When:** Recurring health check OR performance review meeting  
**Hermes Action:** Schedule automated audits + measurement runs  
**Calls:** `brand-audit`, `brand-measurement`

```yaml
Trigger:
  cron: "0 9 * * 0"  # Weekly Sunday 9am (or quarterly)
  event: "audit brand health for [Brand]" OR "track brand KPIs"
  
Actions:
  1. Retrieve brand-context + all recent campaign outputs
  2. Run brand-audit skill → 6-dimension health check:
     - Clarity: Is the brand position clear in messaging?
     - Consistency: Are all campaigns aligned?
     - Alignment: Do campaigns match brand-context?
     - Authority: Is the brand thought leadership evident?
     - Affinity: Customer sentiment/loyalty trending up?
     - Accessibility: Brand visible across all channels?
  3. Run brand-measurement skill → KPI dashboard:
     - Brand Lift (awareness, recall, sentiment)
     - CAC/LTV by channel
     - Content performance vs. brand-voice index
  4. Generate audit report: projects/[brand-slug]/audits/audit-[date].md
  5. Tag: #brand-audit, #measurement
  6. Flag issues: "Consistency drift detected in email tone — recommend retrain"
  7. Notify via Telegram: "Quarterly audit complete for [Brand] — 2 improvements recommended"
```

**Output stored:** `projects/[brand-slug]/audits/audit-[YYYY-Q].md`

---

### 6. **Rebranding Trigger** (Demand → Strategic Evolution)

**When:** User requests brand pivot, refresh, or repositioning  
**Hermes Action:** Orchestrate full rebranding workflow  
**Calls:** `brand-positioning`, `rebranding`, `brand-identity`, `brand-guidelines`

```yaml
Trigger:
  event: "rebrand [Brand] — [new direction/market/positioning]"
  
Actions:
  Phase 1 (Research):
    1. Retrieve current brand-context
    2. Run brand-positioning skill (new positioning) → territory map
    3. Run competitor-branding skill (updated market) → differentiation
    4. Store at: projects/[brand-slug]/rebranding/positioning-options.md
    5. Surface to user: "3 positioning options ready for review"
  
  Phase 2 (Planning):
    1. User selects new positioning
    2. Run rebranding skill → transition narrative + stakeholder comms
    3. Store at: projects/[brand-slug]/rebranding/rebranding-plan.md
    4. Tag: #rebranding-in-progress
  
  Phase 3 (Creation):
    1. Run brand-identity skill (new identity) → design brief
    2. Run brand-voice skill (new voice)
    3. Run brand-messaging skill (new messaging hierarchy)
    4. Store briefs at: projects/[brand-slug]/rebranding/[brief-type].md
    5. Surface to design team: "Visual identity brief ready"
  
  Phase 4 (Finalization):
    1. Run brand-guidelines skill → final guidelines document
    2. Store at: projects/[brand-slug]/_brand-guidelines.md
    3. Update brand-context with new positioning/voice/messaging
    4. Notify: "Rebrand complete — all systems updated"
```

**Output stored:** `projects/[brand-slug]/rebranding/` (all phases)

---

## Cron Job Specifications

### Weekly Discovery Sync
```yaml
schedule: "0 9 * * 1"  # Monday 9am
skills: [brand-strategy, target-audience, competitor-branding]
prompt: |
  Review brand context for each active brand.
  Generate campaign briefs for any brands without a brief this month.
  Surface top 3 market opportunities per brand.
deliver: origin  # Back to Telegram thread
```

### Monthly Brand Audit
```yaml
schedule: "0 9 1 * *"  # 1st of month 9am
skills: [brand-audit, brand-measurement]
prompt: |
  Run health audit on all brands.
  Measure brand KPIs vs. baseline.
  Flag any consistency or positioning drift.
  Surface improvement recommendations.
deliver: origin
```

### Quarterly Reposition Assessment
```yaml
schedule: "0 9 1 */3 *"  # 1st of Q (Jan/Apr/Jul/Oct) 9am
skills: [competitor-branding, brand-positioning]
prompt: |
  Assess competitive landscape for market changes.
  Evaluate brand positioning durability.
  Recommend any repositioning or messaging updates.
  Surface white-space opportunities.
deliver: origin
```

---

## How Brand-Skills Fit in Content Generation Workflows

### Example: Email Campaign with Brand Consistency

```
User Request
    ↓
"Create nurture email sequence for [Brand]"
    ↓
Hermes Orchestrator
    ├─ Retrieve: brand-context[Brand]
    ├─ Retrieve: brand-voice (email tone)
    ├─ Retrieve: brand-messaging (value props)
    └─ Call: owned-channels skill → Email Strategy
        ↓
    OpenClaw receives:
    ├─ Email Strategy brief (from brand-skills)
    ├─ System prompt: "Follow brand voice rules + messaging hierarchy"
    └─ Generate: 5-email nurture sequence
        ↓
    Store: projects/[Brand]/campaigns/email-nurture-[date].md
    ├─ Tag: #email #nurture #branded-content
    ├─ Each email validated against brand-voice index
    └─ Ready for Mautic import
        ↓
    Mautic Automation
    └─ Sequence runs with brand context meta (for future audit)
```

### Example: Paid Media Campaign with Brand Reinforcement

```
User Request
    ↓
"Launch Meta ads for [Brand] product launch"
    ↓
Hermes Orchestrator
    ├─ Retrieve: brand-context[Brand]
    ├─ Retrieve: brand-identity (visual guidelines)
    ├─ Retrieve: brand-messaging (taglines + value props)
    └─ Call: paid-media skill (Meta variant)
        ↓
    Brand-Skills Output:
    └─ Meta Brief:
        ├─ Creative strategy (3 angles)
        ├─ Copy hooks
        ├─ Visual guidelines (colors, fonts)
        ├─ Call-to-action framework
        └─ Audience targeting logic
        ↓
    Claude Code generates Ad Sets:
    ├─ 3 ad variants (A/B test)
    ├─ Copy respects brand voice
    ├─ Visuals follow brand-identity
    └─ Store: projects/[Brand]/campaigns/meta-launch-[date].md
        ↓
    OpenClaw executes:
    ├─ Connects to Meta Ads API
    ├─ Creates campaign + ad sets
    ├─ Sets ROAS targets from brand-skills brief
    └─ Launches with brand-level tracking params
```

---

## Implementation Roadmap

### Phase 1: Foundational (Week 1-2)
- [ ] Install `npx skills add arnabbagxd/brand-building-skills`
- [ ] Store sample `.agents/brand-context.md` files in brain for each active brand
- [ ] Test `brand-context` skill with Hermes manually (no automation yet)

### Phase 2: Single Brand Workflow (Week 3-4)
- [ ] Create first cron job: Weekly Discovery Sync
- [ ] Run brand-strategy + target-audience for one pilot brand
- [ ] Log outputs to brain (projects/[brand]/)
- [ ] Validate outputs in Telegram review

### Phase 3: Content Integration (Week 5-6)
- [ ] Wire brand-voice + brand-messaging into OpenClaw system prompts
- [ ] Test: Generate email copy for pilot brand (should match voice)
- [ ] Validate consistency via manual review + automated voice-index check

### Phase 4: Multi-Channel Expansion (Week 7-8)
- [ ] Add paid-media and owned-channels skills to triggers
- [ ] Create campaign briefs for Meta + Email simultaneously
- [ ] Integrate with Mautic (import email sequences)
- [ ] Test: Launch small campaign with brand-skills-generated briefs

### Phase 5: Full Automation + Measurement (Week 9-10)
- [ ] Enable Monthly Brand Audit cron job
- [ ] Wire brand-measurement skill into reporting
- [ ] Create dashboard: Brand Health by dimension
- [ ] Enable monthly notifications to Telegram

### Phase 6: Multi-Brand Scalability (Week 11+)
- [ ] Duplicate workflow for all brands in portfolio (40+ projects)
- [ ] Tag each brand with context slug
- [ ] Consolidate audit + measurement reports across entire portfolio
- [ ] Build agency-facing brand scorecard dashboard

---

## Success Metrics

✅ **Consistency:** All campaign content validates against brand-voice rules (100% compliance)  
✅ **Speed:** Campaign briefs generated in <30 min vs. 2-3 hours manual  
✅ **Scale:** Handle 10+ brands without manual context switching  
✅ **Measurement:** Quarterly brand audits automated (6-dimension health)  
✅ **Governance:** Brand guidelines always current (single source of truth)  

---

## Related Pages

- [[projects/marketing-for-nerds/brand-building-skills-reference]] — Full skills reference
- [[projects/marketing-for-nerds/hermes-multi-project-automation-masterplan]] — Parent architectural guide
- [[projects/marketing-for-nerds/mautic-overview]] — Email execution layer
- [[projects/marketing-for-nerds/hermes-ai-sales-automation]] — Sales automation parallel
