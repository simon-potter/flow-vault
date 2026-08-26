---
type: media
title: 6 AI Design Skills That Actually Work for Claude Design
date: '2026-08-19'
presenter: AI Labs
media_type: video
source_url: 'https://youtu.be/Ysr7oNDajJI?si=iXTN4C2t8sshOrul'
ingested_via: 'mcp:put_page'
ingested_at: '2026-08-26T04:16:27.500Z'
source_kind: 'mcp:put_page'
tags:
  - MondayMindBenders
---

# 6 AI Design Skills That Actually Work for Claude Design

**Series:** #MondayMindBenders

**Channel:** AI Labs

**Focus:** Tested design skills that work with Claude Design (and also Claude Code, Codex, other agents). These skills are tested in production and actually deliver results.

---

## Core Insight

Models are powerful but follow predictable patterns in design. Without guidance skills, output looks generic and uninspired. These skills steer models away from default patterns and deliver distinctive, production-quality designs.

**Key principle:** Skills added to Claude settings work in Claude Design AND other agents (Claude Code, Codex, etc.).

---

## Skill Sets

### 1. **Emil Kowalski's Design System** (9 Skills)

**Repository:** GitHub (Emil Kowalski)

**What it does:** Comprehensive design toolkit with 9 modular skills, each targeting a different design area

**Skills in collection:**
- Apple Design (Apple's design principles for web)
- Animation Vocabulary (vague descriptions → exact model-readable language)
- Email Design Engineering (beautifully engineered UI components + animations) ⭐ **Most used**
- Animate (complete workflow for adding animations to built sites) ⭐ **Most used**
- Plus 5 others covering various design domains

**How to use:**
1. Add to Claude settings
2. In Claude Design, type `/` + skill name
3. Tell it what site you want
4. Skill asks clarifying questions, then builds

**Key feature:** Email Design Engineering asks questions first (like Claude Design does normally) before building. Animate refines animations on already-built sites.

**Results:**
- Initial designs come out minimal/monotone
- Animate refines animations, syncs them with scroll
- Final output looks polished and intentional
- Works especially well on functional app UI (forms, buttons, hover states)

**Best for:** Starting point for any design; animation polish

---

### 2. **Connard Lee's Garden Skill** (5 Skills, with focus on Web Design Engineer)

**Repository:** GitHub (Connard Lee)

**What it does:** Collection focused on visual design excellence (not functional correctness)

**Main skill:** Web Design Engineer

**How it works:**
1. Clarifies requirements through questions
2. Searches for real reference designs to work from
3. Philosophy: "Good design never starts from thin air; everything is inspired by what came before"
4. Includes references covering:
   - How to judge design quality
   - Common design mistakes
   - Style recipes for Apple, Linear, other well-known sites

**Key differentiator:** Uses real existing designs as reference models

**Results:**
- More interesting, thorough, visually stunning than Claude Design defaults
- Better from design perspective than unguided Claude Design
- Can score existing designs in different areas
- Iterate design by running skill repeatedly until perfect score achieved

**Other skills in collection:** Video presentations, images, etc.

**Best for:** Visually stunning designs; teams that want world-class aesthetics

---

### 3. **Elia Design's AI Design Skill** (1 Skill)

**Repository:** GitHub (Elia Design)

**What it does:** Specialized single-file skill for landing pages only

**Core function:** Takes idea → creates visual system (rules for colors, type, spacing that entire page follows)

**Philosophy:** Landing pages ≠ homepages
- Homepage: serves many audiences
- Landing page: ONE job = drive a specific action
- Models make homepages OK but aren't specialized in landing pages

**How it works:**
1. Install in Claude settings
2. Run with prompt describing what site you want
3. Asks questions first
4. Builds landing page structured around single CTA

**Key features:**
- Keeps design to consistent visual style
- Addresses SEO (often overlooked)
- Focuses all elements toward single action

**Results:**
- Sites feel like real brands
- Matched exact desired vibe
- Structure makes visitors more likely to convert/purchase

**Best for:** Landing pages specifically; high-conversion design

---

### 4. **Meng To's Design System** (Multiple skills focused on storytelling)

**Creator:** Meng To (veteran designer, known for immersive scroll-based storytelling)

**Approach:** System of design skills based on decades of design experience

**Key skills:**

#### Video to Super Prompt
- Takes screen recording or walkthrough of website
- Converts to prompt for agent

#### **Awards Quality Sites** ⭐ (Primary focus)
- Based on design principles from Awwwards (competition for stunning design)
- Lists principles + design details of award-winning sites
- Claude doesn't build at Awwwards level on its own
- Skill includes **actual techniques and effects** that make sites look expensive (what models won't produce alone)

**How to use:**
1. Add Awards skill
2. Give it a prompt describing site you want
3. Returns design structured like Awwwards-winning sites

**Results:**
- Subtle animated backgrounds
- Scroll-based storytelling approach (signature of featured Awwwards sites)
- Structured and designed like actual award winners

**Philosophy:** Design that tells a story, not just looking visually good

**Best for:** Award-quality, storytelling-driven designs

---

### 5. **Jakob Krehel's Component System** (Multiple skills, modular approach)

**Repository:** GitHub (Jakob Krehel)

**Approach:** Unlike others (one skill handles everything), this splits into multiple skills so each design element gets its own skill

**Skills cover:**
- Typography
- Color
- Accessibility
- Layout
- Review
- And more

**You add only what you need** (don't need all of them)

**Key skills in their stack:**

#### Review Skill ⭐ **Most used by presenters**
- Comprehensively reviews all aspects of design
- Scores design
- You iterate based on feedback
- Works better with GitHub integration (compares before/after)
- Checks: animations, accessibility, responsive design
- Flags things that worked before but broke with recent changes
- Lists everything to fix

#### Better Layout Skill
- Addresses spacing, positioning, alignment (where Claude Design struggles)
- Thorough review of layout
- Example: caught that a date field needed more room, told them exact pixels needed
- Won't make site look dramatically different but corrects against proper design principles

**Philosophy:** Modular so you can cherry-pick what you need

**Best for:** Detailed design refinement; catching subtle issues

---

### 6. **Design Laws Skills** (Research-grounded, named laws)

**Approach:** Grounded in actual research and named design laws; separate skill for each

**What it covers:**
- Why people leave websites halfway through
- How behavior appears as users move through sites

**Modular:** Only install the skills that fit your workflow

**Key skills in their stack:**

#### Screen Critique
- Takes a screen, reviews across multiple angles
- Tells you where it's going wrong
- Works from proper guidelines for design quality

#### Perception Laws
- Instructions on how human eye sees and comprehends design
- Applied to site, makes whole thing feel more refined
- Feedback includes: what stands out first, type, spacing

**Results:**
- Sites feel more refined after perception laws applied

**Best for:** Understanding design psychology; refining visual hierarchy

---

## Comparison Matrix

| Skill Set | Focus | Approach | Best For | Key Strength |
|-----------|-------|----------|----------|---------------|
| **Emil Kowalski** | Components + animations | Modular (9 skills) | Getting started; animation refinement | Email Design Engineering + Animate combination |
| **Connard Lee** | Visual excellence | Reference-based | World-class aesthetics | Uses real designs as reference |
| **Elia Design** | Landing pages | Specialized single-file | High-conversion landing pages | CTA-focused structure |
| **Meng To** | Storytelling + awards | Experience-based | Award-quality, narrative-driven | Scroll-based storytelling |
| **Jakob Krehel** | Component refinement | Modular (skills per element) | Detailed polish; catching issues | Review + GitHub integration |
| **Design Laws** | Psychology-grounded | Research-based | Visual hierarchy; refinement | Perception laws |

---

## Workflow Recommendation (From Presenters)

**For new designs:**
1. Start with **Emil Kowalski's Email Design Engineering** (foundation)
2. Refine with **Animate** skill
3. Add storytelling with **Meng To's Awards Skill** (if you want award-quality)
4. Polish with **Jakob Krehel's Review + Layout** skills
5. Finalize with **Design Laws' Perception Laws**

**OR go specialized:**
- Landing page? → Elia Design
- Stunning visuals? → Connard Lee
- Award-winning narrative? → Meng To
- Detailed component work? → Jakob Krehel

---

## Critical Note

**These skills work differently than solo Claude Design:**
- They steer models away from default patterns
- They encode design expertise (not available in base model)
- They provide references and frameworks
- They work with ANY agent (Claude Code, Codex, Claude Design, etc.)
- Same skill added to Claude settings works everywhere

**Private skills:** Presenters (AI Labs) use additional in-house skills available only in **AI Labs Pro** community

---

## Related

- [[topics/cto|CTO Topic]] — Agent-driven design systems
- Design skill composition patterns
- Agent-native design workflows
