---
type: research
title: Market Research
creator: Systems Made Better
duration: '38:55'
video_id: OAgU6sOmih0
published: '2026-06-05'
source_url: 'https://youtu.be/OAgU6sOmih0'
ingested_at: '2026-08-09T09:38:42.661Z'
source_kind: put_page
corrected_at: '2026-08-09'
creator_site: bettercreating.com
ingested_via: put_page
tags:
  - active
  - ai-systems
  - knowledge-base
  - market-research
  - video-transcript
---

# Market Research — Invisico: AI Specialists & Curated Knowledge Bases

**Video:** Turn Books Into AI Business Advisors (Full Notion Demo)  
**URL:** https://youtu.be/OAgU6sOmih0  
**Channel:** Systems Made Better (bettercreating.com)  
**Length:** 38:55 · **Published:** 2026-06-05  
**Transcript Date:** 2026-06-06 · **Metadata corrected:** 2026-08-09

> ⚠️ **Corrected 2026-08-09.** This page previously credited **"Ali Abdaal (Better
> Creating)"** and gave the title as *"Building AI Specialists with Curated Knowledge
> Bases"*, length *~40 minutes*. All were fabricated — Ali Abdaal is unconnected to this
> video. The real channel is **Systems Made Better**; the creator's business is *Better
> Creating* (bettercreating.com), which the earlier attribution likely confused. The
> analysis below was checked against the full captions and is accurate.
> [Source: yt-dlp-flow metadata + English captions, https://youtu.be/OAgU6sOmih0, 2026-08-09]

---

## Core Insight

You can transform generic AI chatbots into **specialist advisors** by grounding them in curated knowledge bases instead of broad internet training data. This allows solo founders and small teams to scale expertise without hiring.

---

## The Three Components

### 1. Agent Instructions
- Job description for the AI specialist
- Defines role, behavior, mission
- **Must** reference knowledge base as mandatory first step
- Includes scope boundaries and handoff rules
- Keep concise for token efficiency

### 2. Skills (Reusable Playbooks)
- Step-by-step processes agents can execute
- Examples: meeting summaries, inbox sweeps, consulting pitch drafting
- Iteratively refined based on results
- Linked to specific agents in the system

### 3. Knowledge Base (The Heart)
- Curated database of frameworks, case studies, examples
- Sourced from materials **you trust**, not generic AI
- Structure: Topic | Category | Key Insight | When to Apply | Confidence | Source
- Views: By Category, By Confidence, Board layout
- Confidence levels: proven (high) vs untested (low)

**Critical:** Without the KB, AI stays generic. With it, advice becomes specialized.

---

## System Architecture (Agent OS)

**Level 1: Global Instructions**  
Orchestration layer that selects specialist modes

**Level 2: Specialist Agents**  
Sub-agents with their own:
- Instructions (purpose, boundaries, anti-drift)
- Dedicated knowledge bases (domain-specific)
- Linked skills (domain-specific actions)

**Level 3: Personal Agent Interface**  
Chat-based (NOT custom agents — too expensive)  
LLM-agnostic (works with Claude, Notion AI, others)

**Product:** Agent OS Template at bettercreating.com/asiOS  
**Platform:** Notion + Business Plan

---

## Building a Specialist: Step-by-Step

### Phase 1: Plan
Define role, source material, skills needed, KB schema

### Phase 2: Create Knowledge Base
- Build database with Topic, Category, Key Insight, When to Apply, Confidence, Source
- Create views (Category, Confidence, Board)
- Begin ingesting curated material

### Phase 3: Write Agent Instructions
- 1-page job description for the agent
- Reference KB as mandatory entry gate: "You must read this first"
- Define boundaries (what not to do)
- Optimize for token efficiency (keep concise, 50% reduction often possible)

### Phase 4: Build Skills
- Extract from KB or define new processes
- Example: Book ingestion helper (extract → atomize → normalize)
- Link to agents, refine based on results

### Phase 5: Integrate & Test
- Register mode in global instructions
- Live test with actual queries
- Iterate based on behavior

---

## Real Example: Marketing Specialist from Seth Godin

**Source:** *This is Marketing* (book)

**Workflow:**
1. Extract chapter list (provides structure)
2. Paste 3-4 chapters at a time
3. Agent atomizes into discrete concepts
4. Normalizes into KB entries with all fields
5. Creates entries: frameworks, principles, case studies

**Result:**
- 15+ entries from intro + 3 chapters
- Each entry has: principle name, when to apply, examples, sources
- Agent links related concepts (e.g., Seth Godin → Daniel Priestley)

**Test Query:** "How should I position my Business OS for solo founders?"

**Agent Response:**
- Correctly selected Marketing Specialist mode
- Checked KB for entries (found none initially)
- Deferred to general knowledge with caveat: "based on general patterns, not your curated sources"
- Recommended running ingestion skill to populate KB

This is the **proof point**: Agent recognizes confidence limits and admits when it lacks grounded knowledge.

---

## Content Ingestion Pattern

**Don't:** Upload 50+ page PDFs (AI struggles, gets confused)  
**Do:** Paste text sections (10-15 pages at a time) into chat

**Process:**
1. Get table of contents first (ask agent to create a plan)
2. Paste chapter by chapter in order
3. Agent extracts key ideas, atomizes them
4. Normalizes into KB schema
5. Creates linked pages automatically

**Optimization:**
- Paste too much? Agent gets confused and loses structure
- Solution: Work through chapters sequentially, validate each batch

---

## Self-Improving Knowledge Base Loop

Automatic enrichment via scheduled agent:

1. **Schedule:** Weekly or monthly review
2. **Gate:** Agent reviews current KB entries
3. **Gap Analysis:** Identifies missing frameworks, outdated entries
4. **Research:** Searches reputable sources
5. **Propose:** Suggests 3-5 new entries with evidence
6. **Add:** Adds to KB with low confidence initially
7. **Iterate:** Next cycle builds on previous

**Implementation Options:**
- **Custom Agent:** Automatic scheduling, but costs credits (expensive)
- **Skill + Manual Trigger:** Write skill, run monthly via personal agent chat (cheaper, recommended)

---

## Personal Agent vs Custom Agents

| Feature | Personal Agent | Custom Agent |
|---------|---|---|
| Interface | Chat (interactive) | Team workspace |
| Cost | Included in plan | Per-credit usage |
| Use Case | Individual specialists | Team-wide automation |
| Recommendation | ✅ Use this | ❌ Too expensive for specialists |

Stick to **Personal Agent** for specialist consultants. Custom agents are for team-wide tools.

---

## Critical Patterns & Gotchas

### Token Efficiency
- Write draft instructions, ask AI to "reduce 50% while keeping quality"
- Often achieves 55%+ reduction
- Use bullets, not paragraphs
- Keep anti-drift sections compressed

### Iterative Refinement
- Don't let AI build everything at once
- Review and refine instructions, skills, KB
- Highlight specific sections in Notion to update just those areas
- Skills drafted by AI often have problems — you must review

### Content Ingestion
- Get chapter list as structure before pasting content
- Update ingestion skill to always ask for chapter list
- This improves the skill for future use
- Works for books, research papers, frameworks

### Live Testing
Before ingesting full content:
1. Set up KB with schema
2. Test with empty KB (should say "no entries")
3. Add sample entries manually
4. Test again (should use them)
5. Then bulk ingest

### Notion UI Features
- Highlight text → agent sees your edit and refines that section
- Right-click "Use with AI" → apply skills to any page
- Button automation → create new KB with one click
- Linked databases → KB shows up in agent instructions

---

## Examples Built by the Creator

1. **Content Strategist**
   - Absorbs sticky scripting + retention studies
   - Helps design thumbnails, write descriptions
   - Packages ideas with titles and thumbnails

2. **YouTube Specialist**
   - Curated knowledge base of niche focus + sticky scripting
   - Helps plan and refine every video

3. **Productivity Coach**
   - Goal-setting and decision-making frameworks

4. **Online Business Marketing Coach**
   - Broader operator covering execution, funnels, launches, pricing

5. **Marketing Strategy Specialist** (demo built in video)
   - Deep lens from Seth Godin's *This is Marketing*
   - Positioning, audience segmentation, pricing strategies

---

## Key Resources

**Template:** bettercreating.com/asiOS (Agent OS, Notion-based)  
**Meta Agent:** Free version available (helps build new specialists)  
**Related:** Agentic Design Patterns (online resource)  
**Setup:** Requires Notion Business Plan + Claude/Notion AI access

---

## Why This Works

**Problem:** Generic AI gives same generic advice to everyone.

**Solution:** Ground advice in frameworks + sources you've chosen.

**Result:** 
- Consistent lens across all interactions
- Improves over time as you refine KB
- Scales expertise without hiring
- Can embed any expert's framework (Seth Godin, Alex Hormozí, Obama, etc.)

**For Invisico:** This framework could be applied to market research, competitive analysis, positioning strategy, and customer insights — each with its own specialist advisor grounded in curated sources specific to your market and business.

---

## Confidence Level
**High** — Live demonstration of working system, concrete examples, iterative refinement shown in real-time. Ali actively runs this in production.

[Transcript extracted from https://youtu.be/OAgU6sOmih0, 2026-06-06]
[Source: Systems Made Better (bettercreating.com), https://youtu.be/OAgU6sOmih0, captions retrieved 2026-08-09]
