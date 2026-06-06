---
type: research
title: Market Research
parent: projects/invisico
source_url: 'https://youtu.be/OAgU6sOmih0'
ingested_via: 'mcp:put_page'
ingested_at: '2026-06-06T12:56:13.789Z'
source_kind: 'mcp:put_page'
tags:
  - active
  - ai-systems
  - knowledge-base
  - market-research
---

# Market Research — Invisico

## Video Summary: Building AI Specialists with Curated Knowledge Bases

**Video:** https://youtu.be/OAgU6sOmih0  
**Creator:** Ali Abdaal (Better Creating)  
**Focus:** Building specialized AI advisors in Notion powered by curated knowledge bases, not generic chatbots

---

## Core Concept

Rather than using generic AI chatbots trained on broad internet data, the video demonstrates how to build **specialist AI collaborators** with dedicated knowledge bases:

- **Grounded in curated sources** you choose (books, research, frameworks)
- **Specialized instructions** that define the agent's role and behavior
- **Reusable skills** that encode processes and actions
- **Self-improving systems** that refine knowledge over time

This allows solo founders and small teams to scale expertise without hiring additional headcount.

---

## Three Core Components of an AI Specialist System

### 1. Agent Instructions
- Job description for the AI agent
- Who it is, how it behaves, mission
- Must reference the knowledge base as mandatory first step
- Boundaries and handoff rules to avoid scope creep

### 2. Skills (Reusable Playbooks)
- Step-by-step processes the agent can execute
- Examples: meeting note summarization, inbox sweep, consulting pitch drafting
- Linked to agents via the system UI
- Improve through iterative refinement and feedback

### 3. Knowledge Base (The Heart)
- Curated database of frameworks, principles, case studies, examples
- **Critical:** sourced from materials you trust, not generic AI training data
- Structure: Topic, Category, Key Insight, When to Apply, Confidence Level, Source
- Properties: organized by category (pricing, positioning, audience) and confidence (proven vs untested)
- Enables agents to give **grounded advice** rather than generic guidance

---

## Key Takeaway: Knowledge Base > Generic AI

> "Without the knowledge base, the AI tends to be generic. With a clear knowledge base following a specific process, it becomes genuinely useful."

The knowledge base is what transforms a chatbot into a specialist advisor.

---

## Practical System: Agent OS (Notion-based)

**Architecture:**
- **Global Instructions** — orchestration layer that selects specialist modes
- **Specialist Agents** — sub-agents with dedicated knowledge bases and skills
- **Personal Agent Interface** — chat-based (not custom agents, which are more expensive)
- **Multimodal** — LLM-agnostic (can use Claude, Notion AI, others)

**Available at:** bettercreating.com/asiOS (free template + updates)

---

## Building a Specialist: Step-by-Step

### Phase 1: Planning
- Define the specialist's role (e.g., "Marketing Strategy Expert")
- Identify source material (books, frameworks, case studies)
- Determine key skills needed
- Structure the knowledge base schema

### Phase 2: Knowledge Base Creation
- Create structured database with fields: Topic, Category, Key Insight, When to Apply, Confidence, Source
- Add views: By Category, By Confidence, Board view
- Begin ingesting curated material

### Phase 3: Agent Instructions
- Write 1-page job description for the agent
- Reference knowledge base as mandatory entry gate
- Define scope boundaries and handoff rules
- Optimize for token efficiency (Notion tip: keep it concise)

### Phase 4: Skills
- Build reusable processes (e.g., book ingestion helper)
- Link skills to the agent
- Iteratively refine based on results

### Phase 5: Integration
- Register specialist mode in global instructions
- Add to agent selection list
- Test and iterate

---

## Example: Marketing Strategy Specialist

**From:** Seth Godin's *This is Marketing*

**Knowledge Base Entries:**
- The myth of rational choice (framework)
- Positioning strategies
- Customer segmentation
- Marketing principles

**Skills:**
- Book ingestion helper (extract → atomize → normalize into KB entries)
- Positioning audit skill

**Test Result:**
- Asked: "How should I position my business OS for solo founders?"
- Agent correctly: loaded mode, checked KB for entries (found none), deferred to general knowledge
- Response was grounded and specific, not generic

---

## Critical Patterns

### Ingesting Content into Knowledge Base

1. **Get chapter list first** — provides structure before deep ingestion
2. **Extract atomically** — break content into discrete concepts
3. **Normalize** — fit into knowledge base schema
4. **Add confidence levels** — new material starts as low confidence
5. **Link across sources** — connect similar concepts across books/experts

### Iterative Refinement

- AI can draft instructions, but **you must review and refine**
- Request token efficiency improvements (e.g., "55% shorter")
- Highlight sections in Notion to update specific areas
- Update instructions after discovering gaps

### Personal Agent vs Custom Agents

- **Personal Agent (Recommended):** Interactive chat, part of Notion Business Plan, credit-efficient
- **Custom Agents:** Team-wide, scheduled, specific jobs but cost more credits
- Use Personal Agent for specialist consultancy

---

## Advanced: Self-Improving Knowledge Base

Create a compounding loop:

1. **Scheduled Review** — agent reviews KB weekly/monthly
2. **Gap Analysis** — identify missing frameworks, outdated entries
3. **Research** — agent researches from reputable sources
4. **Propose & Add** — suggest and add new entries to KB
5. **Iterate** — knowledge base improves each cycle

**Implementation Options:**
- Custom Agent (costs credits, runs automatically on schedule)
- Skill + manual trigger (cheaper, run 1x/month via personal agent)

---

## Applications Shown

1. **Content Strategist** — absorbs retention studies, helps design thumbnails, write descriptions
2. **YouTube Specialist** — curated from sticky scripting and niche focus frameworks
3. **Productivity Coach** — helps with goal-setting and decision-making
4. **Marketing Strategist** — expert positioning advice for solo founders

---

## Practical Gotchas & Tips

- **Don't use PDFs longer than 15 pages** — paste text content instead
- **Highlight sections in Notion** — AI sees your edits and can refine that specific area
- **Keep instructions concise** — token efficiency matters (50%+ reduction often possible)
- **Test before ingesting full content** — run live tests to confirm agent behavior
- **Use chat history** — Notion system to maintain context across sessions
- **Monitor token usage** — Personal Agent on Business Plan is efficient but watch credit usage

---

## Why This Works

**Generic AI Problem:** ChatGPT-style assistants give the same generic advice to everyone, backed by broad internet training data.

**This Solution:** 
- Grounds advice in frameworks and case studies **you've chosen**
- Creates consistent lens across all agent interactions
- Improves over time as you refine KB
- Scales expertise without hiring
- Can embed any expert's framework (Alex Hormozí, Obama, Seth Godin, etc.)

---

## Key Resources

- **Video:** https://youtu.be/OAgU6sOmih0
- **Agent OS Template:** bettercreating.com/asiOS
- **Concept:** Agentic Design Patterns (free resource online)
- **Related:** Claude Code + Hermes for local/development agent work

---

## Confidence Level

**High** — This is a comprehensive system the creator actively uses and updates. Concrete examples shown working live in Notion. Framework validated through iteration and refinement.

[Source: Ali Abdaal "Building AI Specialists with Notion" YouTube, 2024-2025]
