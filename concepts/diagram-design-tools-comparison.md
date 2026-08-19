---
type: research
title: Diagram Design Tools for AI Agents — Comparison & Alternatives
ingested_via: 'mcp:put_page'
ingested_at: '2026-08-19T09:30:55.493Z'
source_kind: 'mcp:put_page'
tags:
  - agent-tools
  - diagram-generation
  - visualization
---

# Diagram Design Tools for AI Agents — Comparison & Alternatives

## Primary Tool: Diagram Design

**What Matthew Berman covered:**
- Agent-powered diagram generation
- Multiple diagram types: flowchart, architecture, state machine, timeline, quadrant
- Integrates with Codeex, Cloud Code, Cursor, Pi, Hermes Agent
- One-minute install in Hermes
- Auto-invokes when agent asked to create diagrams

---

## Comparable Alternatives

### 1. **LikeC4** ⭐⭐⭐ (5,448 stars)
- **URL:** https://github.com/likec4/likec4
- **Positioning:** "Visualize, collaborate, and evolve software architecture with always-actual, live diagrams from your code"
- **Key differentiator:** Code-first architecture diagramming; diagrams stay in sync with codebase
- **Use case:** Teams that want architecture diagrams as living documentation
- **vs Diagram Design:** LikeC4 is pull-from-code; Diagram Design is push-from-agent-request
- **Maturity:** High (5.4k stars, active community)
- **Agent integration:** Likely via text generation; less direct than Diagram Design

### 2. **Swark** (1,695 stars)
- **URL:** https://github.com/swark-io/swark
- **Positioning:** "Create architecture diagrams from code automatically using LLMs"
- **Key differentiator:** LLM-native approach; understands code semantics
- **Use case:** Automatic architecture documentation from existing codebases
- **vs Diagram Design:** Swark extracts from code; Diagram Design generates on-demand
- **Maturity:** Growing (1.7k stars)
- **Agent integration:** Could be paired with agents for discovery workflows

### 3. **CodeBoarding** (2,390 stars)
- **URL:** https://github.com/CodeBoarding/CodeBoarding
- **Positioning:** "Interactive architecture diagrams for codebases"
- **Key differentiator:** Focus on interactivity and exploration
- **Use case:** Visual codebase exploration; understanding architecture at a glance
- **vs Diagram Design:** CodeBoarding is interactive viewer; Diagram Design is generator
- **Maturity:** Solid (2.4k stars)
- **Agent integration:** Could surface diagrams to agents for analysis

### 4. **DesignScribe** (new, early stage)
- **URL:** https://github.com/Leighroyus/designscribe
- **Positioning:** "CLI tool that watches your coding agent work and automatically generates architecture documentation, data flow diagrams, and design decision logs — in real-time"
- **Key differentiator:** **Watches agent actions in real-time**; generates docs as-you-go
- **Use case:** Automatic documentation generation during agent-driven development
- **vs Diagram Design:** DesignScribe is passive observer/documenter; Diagram Design is active generator
- **Maturity:** Very early (June 2026, 0 stars)
- **Agent integration:** Designed to run alongside agents (monitoring pattern)
- **Status:** Fresh project; worth watching

### 5. **Hand-Drawn Diagrams** (60 stars)
- **URL:** https://github.com/muthuishere/hand-drawn-diagrams
- **Positioning:** "Hand-drawn diagram skill for Claude Code and Codex"
- **Diagram types:** Architecture, workflow, UX blueprints (monochrome PNG)
- **Key differentiator:** Aesthetic focus (hand-drawn style)
- **vs Diagram Design:** Hand-drawn is style preference; Diagram Design is professional/clean
- **Agent integration:** Direct (Claude Code + Codex skills)
- **Maturity:** Niche project (60 stars)

### 6. **arch-flows-visualizer** (22 stars)
- **URL:** https://github.com/matheuscfrade/arch-flows-visualizer
- **Positioning:** "Generates interactive HTML visualizations from structured JSON"
- **Key differentiator:** JSON-first; output is interactive HTML
- **Use case:** Rendering pre-structured data as diagrams
- **vs Diagram Design:** More of a renderer than a generator
- **Maturity:** Very early (22 stars)
- **Agent integration:** Via Grok skill

---

## Comparison Matrix

| Tool | Use Case | Maturity | Agent Native | Input Method | Output | Best For |
|------|----------|----------|--------------|--------------|--------|----------|
| **Diagram Design** | On-demand diagrams | High | ✅ Yes (Codeex, Hermes) | Agent request | SVG/PNG | Real-time agent requests |
| LikeC4 | Architecture as code | High | ⚠️ Possible | Code inspection | Live diagrams | Teams with live docs |
| Swark | Code-to-diagram | Medium | ⚠️ Possible | Source code analysis | SVG | Auto-generating docs |
| CodeBoarding | Interactive exploration | High | ⚠️ Possible | Codebase | Interactive viz | Understanding architecture |
| DesignScribe | Concurrent documentation | Very Early | ✅ Yes (observer) | Agent actions | Markdown + diagrams | Documenting agent work |
| Hand-Drawn | Aesthetic diagrams | Low | ✅ Yes (Claude/Codex) | Agent request | PNG | Design/UX focused |
| arch-flows-visualizer | JSON rendering | Very Early | ⚠️ Possible | JSON | Interactive HTML | Structured data viz |

---

## Recommendation by Use Case

### If you want **real-time diagram generation during agent execution:**
→ **Diagram Design** (what Matthew covered) is the right choice
- Lowest friction (1-minute install)
- Direct agent integration
- Multiple diagram types
- Proven in production (Codeex, Hermes)

### If you want **architecture diagrams that stay in sync with code:**
→ **LikeC4** 
- Requires code-first approach
- High maturity
- Good for teams
- Less agent-native

### If you want **automatic documentation from existing codebases:**
→ **Swark** or **CodeBoarding**
- Extract-from-code approach
- Good for onboarding
- Can feed results to agents

### If you want **concurrent documentation of agent actions:**
→ **DesignScribe** (emerging, worth watching)
- New, but solves a real problem
- Passive monitoring pattern
- Could pair with Diagram Design

### If you want **hand-drawn/aesthetic style:**
→ **Hand-Drawn Diagrams**
- Niche but functional
- Good for design-focused workflows

---

## My Assessment

**For your CTO needs (developer-facing documentation + agent infrastructure):**

1. **Primary:** Diagram Design (already covered by Matthew)
   - Agent-native, fast, flexible
   - Start here

2. **Secondary:** LikeC4
   - For living architecture documentation
   - Complement to Diagram Design
   - Good for team alignment

3. **Experimental:** DesignScribe
   - Monitor this project
   - Could be valuable for documenting agent-driven development
   - Pair with Diagram Design for full pipeline

**Why not the others (for your case):**
- Swark: Good but less agent-integrated
- CodeBoarding: More viewer than generator
- Hand-Drawn: Aesthetic, but not practical for CTO infrastructure
- arch-flows-visualizer: Too early, limited scope

---

## Action Items

1. **Immediate:** Use Diagram Design as primary tool (install via Matthew's method)
2. **Short-term:** Evaluate LikeC4 for architecture documentation layer
3. **Watch-list:** Track DesignScribe — could be valuable once mature
