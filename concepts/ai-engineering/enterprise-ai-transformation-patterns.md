---
title: "What the Top Companies Do Differently With AI Coding"
source: https://www.youtube.com/watch?v=21tuT-e4NVo
format: video
speakers:
  - "Martin Harrison, McKinsey"
  - "Prakhar Dixit, McKinsey"
  - "Shilpa (third speaker, McKinsey)"
channel: AI Engineer
uploaded: "2026-11-08"
duration: "0:20:28"
transcript_format: en-orig
word_count: 3918
tags:
  - "#MondayMindBenders"
  - "#ai-engineering"
  - "#mckinsey"
  - "#enterprise-transformation"
  - "#ai-sdlc"
  - "#quality-gates"
  - "#change-management"
---

# What the Top Companies Do Differently With AI Coding

**Source:** https://www.youtube.com/watch?v=21tuT-e4NVo  
**Speakers:** Martin Harrison, Prakhar Dixit, Shilpa — McKinsey Software Engineering & AI practice  
**Channel:** AI Engineer  
**Uploaded:** 2026-11-08  
**Duration:** 0:20:28  
**Format:** Video (auto-generated captions)  
**Word count:** 3918

## Summary

McKinsey consultants Martin Harrison, Prakhar Dixit, and Shilpa reveal what separates top 20–25% of companies getting 2x+ end-to-end productivity gains from the rest. They've moved past the "trough of disillusionment" (end-2025) when AI adoption was high but gains were meager. The four key levers: (1) operating model redesign (Kanban instead of sprints, night-shift agents + human validation), (2) talent structure (small pods of 2–4, collapsed role definitions), (3) tech stack (not new tools, but right context + semantic layer), and (4) change management (company-wide scaling, not just pilot teams).

Critical insight: **Quality is inversely correlated with speed.** As code generation accelerates, per-PR defect rates are going DOWN (not just absolute defect count). This requires coaching developers on REVIEWING generated code, not just producing it.

## Key Insights & Highlights

**Current Landscape (Mid-2026):**
- Coming out of "trough of disillusionment" from end-2025
- Previous widespread adoption but meager 10–15% perf gains
- Now: top 20–25% of companies seeing 2x+ end-to-end improvements (not incremental)
- Skeptics are becoming optimists; the patterns are working

**Four Key Levers for Success:**

### 1. Operating Model Redesign
- **Old way:** 2-week sprints, scrum teams
- **New way:** Kanban with 1–2 day cycles; agents run night shift, humans validate during day, loop repeats
- Requires upfront agent flow setup, but it's a ratchet: can't go back to sprints
- **Human review placement:** Strategic checkpoints where humans validate before next agentic loop
- **Confidence-driven:** As maturity grows, remove human checkpoints → more autonomous end-to-end orchestration
- **Scope expansion:** Last year (2025), loops focused on build & test. Now (2026), expanding to product & release stages
- **Artifact standardization:** Codify what feeds the loops (PRDs, specs, templates). With 600+ people, multiple storage conventions exist. Standardized artifacts are critical for scaling

### 2. Talent Structure Transformation
- **Team size:** Shrinking from traditional scrum teams (8–10) → pods of 2–4
- **Head count:** Not necessarily reducing, but multiplying smaller pods (more teams, smaller each)
- **Role collapse:** Especially in large enterprises/banks with multiple role layers
  - Product roles → "Definer" (more generalist)
  - Dev + QA roles → "Builder"
  - Trend: single standardized definition (industry hasn't agreed on names yet)
- **Responsibility expansion:** Manual activities get automated; remaining responsibilities collapse into fewer role types

### 3. Tech Stack (Context & Semantics, Not Tools)
- **Tooling:** "Solved" — most market tools work great. It's not a differentiator.
- **Real edge:** Semantic layer, IP, domain context
- **Challenge for large orgs:** Context often trapped in SME heads (20-year tenured employees)
- **Solution:** Document knowledge so agents can access it repeatedly without bottlenecking on humans
- **Trust layer:** "AI itself is the trust layer" — governance, security, stability
- **Skills curation:** Hundreds of thousands of skills exist; challenge is WHICH FIT YOUR CONTEXT
  - Example: 1,700 skills for writing a PRD alone
  - Paralysis in decision-making is the real bottleneck, not availability

### 4. Change Management at Scale
- **Pilot trap:** Easy to get 10x productivity in a front-runner team over 6 days (great story)
- **Real challenge:** Scaling across hundreds of thousands of engineers
- **Prerequisite:** Pre-work on operating model, talent structure, tech stack BEFORE unleashing agentic PDLC on everyone
- **Cost dimension:** AI FinOps now critical (token usage, cost tracking)
- **Risk layers:** Compliance, governance, design, all have rules that must encode into agents sideways (not just in build/test)
  - Example: Bank requires specific color schemes + colorblind accessibility checks on customer-facing app
  - These rules used to require a person to run around and manually translate; now agents need this encoded upfront

**Quality & Code Review Crisis:**
- **Paradox:** As code generation SPEEDS UP, quality per PR is going DOWN (inverse correlation)
- **Root cause:** Developers are generating code faster but reviewing it worse (or not at all)
- **Solution:** COACH on reviewing, not just generating
- **Golden examples:** Feed agents with curated "golden examples" (not production average) of what good looks like
- **Encoding standards:** Policy checkpoints throughout the PDLC
  - Maintainability: Is it complex? Can it merge cleanly?
  - PRD clarity: Requirements well-defined?
  - Release readiness: Enterprise constraints mapped upfront?

**Bottleneck Shift:**
- Used to be: build & test (hero use cases, lots of acceleration)
- Now: Upfront (requirements clarity, connecting agents to enterprise context) and downstream (release frequency & Enterprise requirements)
- Sideways: Parallel processes (risk, compliance, governance, design) weren't getting acceleration; now must encode them

**Measurement & Impact (Still a Gap):**
- Huge gap between AI adoption and organizations confident they're measuring RIGHT things
- Early approaches: measure traditional metrics (velocity, defect rate)
- Emerging: Use AI itself to score value of what's being built, figure out intent
- Pragmatic hack: Reduce pod size to half, create twice as many teams, think short-term about "3 teams for 8 weeks" — massive acceleration in near term (but obviously need sophistication over time)

## People Mentioned
- Martin Harrison — McKinsey Software Engineering practice lead
- Prakhar Dixit — McKinsey consultant, software engineering & AI
- Shilpa — McKinsey consultant, software engineering & AI

## Companies Mentioned
- **McKinsey** — consulting firm, authors of this framework
- **Google** — referenced for tools/practices context
- **Anthropic** — referenced for AI tools
- (Implicit: large enterprises, banks, financial institutions as clients)

## Technical Concepts Extracted
- Kanban PDLC (1–2 day cycles vs. 2-week sprints)
- Agentic orchestration (night shift agents + human validation)
- Role consolidation in enterprise teams
- Semantic layer & context encoding
- Agent-friendly governance (sandbox, approval rules)
- Code quality metrics (per-PR defect rate, not aggregate)
- FinOps for AI (token tracking, cost optimization)
- Multi-agent context switching & orchestration
- Enterprise compliance encoding in agent workflows
- Change management at scale (pilots → company-wide)

## Tone & Nuance
- **Data-driven:** Explicit mention of surveying "few hundred large enterprises"
- **Realistic about roadblocks:** Change at scale is hard; most pilots happen to be visible wins, but scaling is where real work is
- **Not prescriptive:** "This is what we're seeing," not "this is the only way"
- **Emphasis on systems thinking:** It's 100 different things coordinated, not one tool change
- **Cautious optimism:** Early data shows 2x–3x+ improvements are possible, but only for the disciplined ones