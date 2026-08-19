---
type: media
title: Matt Pocock and Potato's AI Skills for Real Engineers — Deep Dive Review
date: '2026-08-19'
duration: ~40 minutes
presenter: Theo Browne
media_type: video
source_url: 'https://youtu.be/0oXOOlqVu5M?si=i8-ewea2Z4XprFdF'
ingested_via: 'mcp:put_page'
ingested_at: '2026-08-19T07:17:31.771Z'
source_kind: 'mcp:put_page'
tags:
  - MondayMindBenders
---

# Matt Pocock and Potato's AI Skills for Real Engineers — Deep Dive Review

**Series:** #MondayMindBenders

**Presenter:** Theo Browne (T3 Stack / Theo's Thots)

**Focus:** Comparative deep dive into two major AI skills repositories: **Matt Pocock's skills-engineering** (200k+ GitHub stars) and **Potato's Pstack** (Lauren McGuire from React Core Team, now at Cursor).

---

## Key Thesis

Don't blindly copy setups. Use others' configurations as **information sources to build your own systems**, not as templates to clone wholesale. Treating someone's entire setup as a code template is "cringe and bad engineering."

---

## Valuable Skills Identified & Incorporated

### From Pstack (Lauren/Potato)

#### 1. **Unslop** ⭐ (Primary catalyst for deep dive)
- **Purpose:** Remove AI-isms and add human voice to generated text
- **Why valuable:** Dramatically improves readability and semantic density
- **Tweaks Theo made:** Applied to all prompts first; now uses with "required unslop writing skill" to keep answers direct and scannable
- **Pattern detection rules:**
  - Kill content puffery ("pivotal moment," "testament to evolving landscape")
  - Cut superficial -ing phrases ("highlighting," "ensuring," "reflecting")
  - Remove promotional vagueness
  - Fix m-dash overuse
  - Eliminate chatbot filler ("I hope this helps," "let me know")
  - **Key insight:** Say what it DOES, not how it FEELS (e.g., "SQL returns the exact string sent to the database" beats "database stays close at hand")
  - Add soul: opinions > neutral pros/cons lists
  - Short sentences mixed with longer rhythm
  - First person acceptable when it fits
  - Be specific, not vague
- **Observed impact:** Went from slop-heavy GPT-4 output to dense, readable technical writing in one step

#### 2. **Arena** (Cross-candidate synthesis)
- **Purpose:** Fan out parallel attempts at same task, read all candidates, pick strongest, graft best ideas from others, verify
- **Why valuable:** Forces depth through multiple perspectives
- **Cost:** Hundreds of dollars in inference (parallel runs × model calls)
- **Framework:** Frame → Fan out → Cross judge → Pick → Graft → Verify → Descriptions
- **Theo's implementation pattern:** To-do list with one entry per phase before launch; keeps phases visible, prevents silent disappearance
- **Caveat:** Cursor-specific in its writeup; Theo wants someone to genericize it

#### 3. **Blast Radius** ⭐
- **Purpose:** Before shipping a change, find what ELSE it breaks somewhere in the codebase
- **Why valuable:** Prevents shipping cascading failures; caught multiple things that would've been "miserable" without it
- **Workflow:** "What could this break?" + "What could this change break elsewhere?"
- **Complement:** Works with "How" (what code does) and "Why" (design rationale) — Blast Radius adds "What does this break?"
- **Key behavior:** Calls out that historical writeups aren't trustworthy; forces proof by running actual code
- **Integration:** Calls unslop on final response to prevent messy output

#### 4. **Technical Writing Arena**
- **Purpose:** Dense, high-information output for technical contexts
- **Theo's adoption:** Excellent semantic density; easy to read
- **Why notable:** Demonstrates the power of good writing history; models follow good examples much more reliably

#### 5. **Interrogate, Prove It, Dissect, Triage** (mentioned but less detailed)
- Part of Theo's active rotation
- Ranked high for his use case but requires paired implementation

### From Matt Pocock's skills-engineering

#### 1. **Grill (with Docs)** 💀 (M-dash problem)
- **Purpose:** Relentless interview to sharpen a plan/decision, map as design tree
- **How it works:** Every decision branches into sub-decisions; work tree in rounds via decision frontier
- **Theo's workflow:** Copy-paste skill into prompt, use Opus 5, ask it to grill a specific project (Lakebed)
- **Why valuable:** Surfaces unasked questions, especially about stale/competing architectural models
- **Problem identified:** Matt uses 9+ m-dashes per page; Theo noticed this is where his m-dash generation comes from
- **Theo's UX observation:** "I almost want to fork Matt's repo just removing all the m-dashes"

#### 2. **Diagnosing Bugs**
- **Auto-invocation:** Doesn't require manual pull-in; fires automatically when debugging
- **Impact:** Agents find root cause and communicate more effectively than without it
- **Theo's assessment:** "Pretty solid" over the last few days

#### 3. **Wizard** ⭐
- **Theo's enthusiasm:** Very high; expecting to use "a ton"
- **Missed use cases:** Identified 4 things from yesterday he should have used it for
- **Documentation quality:** Praised as "a good docs page, lots to learn from"

#### 4. **Writing for Agents** (Agents MD / Claude MD reference)
- **Theo's use:** Primarily for prompting sub-agents; very helpful
- **Key concept:** Context pointers — references held in agent context encoding conditions for reaching material
- **Problem:** Heavily m-dashed; hard to parse despite good information

#### 5. **Set Up Matt Pocock Skills** (meta-skill)
- **Purpose:** Install and configure the entire suite
- **Design choice:** Matt uses `disable_invocation: true` on many skills → must be manually pulled in via slash/dollar command
- **Rationale:** Prevents unwanted auto-triggering; reasonable for heavy-weight skills

---

## Key Tweaks & Rationale

### Theo's Core Adaptations:

1. **Early unslop application**
   - *Tweak:* Make unslop + required unslop writing skill the FIRST thing in every prompt
   - *Why:* Immediate return on investment; transforms all downstream output

2. **Copy-paste over install** (for initial testing)
   - *Tweak:* Copy skill markdown directly into prompt instead of installing
   - *Why:* Avoids friction; tests viability before committing to full setup
   - *Limitation:* Doesn't work for skills with associated scripts (but can be worked around)

3. **Manual skill pull-in for heavy skills**
   - *Observation:* Matt's `disable_invocation` is wise
   - *Theo's adoption:* Will likely adopt for Wizard and other expensive/heavy skills

4. **Audit-driven selection** (personal workflow)
   - *Tweak:* Prompted Opus to audit his machine usage (MacBook, Leftbook, BB1) against Pstack skills
   - *Result:* Ranked skills by fit + benefit; identified top 10 to actively use
   - *Why:* Prevents skill bloat; ensures only applicable tools land in workflow

5. **M-dash removal** (frustrated observation)
   - *Intended tweak:* Would fork Matt's repo to remove m-dashes
   - *Why:* Matt's writing, while content-rich, has typography overhead that hurts readability

---

## Conclusions About Two Repos

### Matt Pocock's `skills-engineering` (200k+ stars)

**Strengths:**
- Relentless depth: Grill, Diagnosing Bugs, Wizard all force thorough thinking
- Comprehensive coverage: Ask Matt, Code Review, Codebase Design, etc. span the full dev lifecycle
- Good documentation patterns (skill mechanics, context pointers)
- Pragmatic auto-invocation toggles

**Weaknesses:**
- **Typography debt:** Excessive m-dashes hurt readability despite content quality
- **AI-written feeling:** Mostly AI-generated markdown; doesn't always feel human
- **Cursor-centric bias:** Some skills assume Cursor-specific workflows
- **Dense without always being concise:** Content is there but presentation is walls of text

**Overall assessment:** "Impressive but also kind of unsettling" — powerful but shows its age and origin.

---

### Pstack (Lauren/Potato, React Core contributor, now at Cursor)

**Strengths:**
- **Semantic density:** Unslop skill proves Lauren deeply understands readability
- **Behavioral alignment:** Skills are designed for real daily work, not theoretical perfection
- **Writing quality:** Even AI-generated text reads naturally; high signal-to-noise
- **Applicability:** Arena, Blast Radius, Unslop are immediately useful in coding workflows
- **Philosophy:** "Use as reference, not template" — matches how skilled engineers actually learn

**Weaknesses:**
- **Cursor bias:** Several skills are Cursor-specific; portable principles exist but wrapping is tight
- **Smaller scope:** Doesn't cover as many lifecycle phases as Matt's suite
- **Less documentation about process:** Matt documents HOW to apply skills better than Lauren does

**Overall assessment:** "Underrated gem" — smaller, more focused, dramatically more readable. Theo would be "pumped if someone cloned Pstack skills in a generic, non-Cursor-specific way."

---

## Comparative Meta-Observations

1. **Skill descriptions are triggers, not specs**
   - Theo's realization: Description role is to get the model to USE the skill, not accurately describe everything it does
   - Analogy: Like YouTube thumbnails — goal is to stop the scroller and get the click, not encapsulate everything in the video
   - Matt's descriptions feel like old Anthropic-era standards (pre-clarity on LLM orchestration)

2. **History + good examples matter hugely**
   - When Theo has unslopped text in conversation history, models follow it reliably
   - Without examples, they revert to default slop patterns
   - This suggests: skill quality ∝ writing quality of its markdown

3. **AI-written vs. human-written is blurry**
   - Theo tested Matt's Grill skill output on a human-detector: "100% human written"
   - Yet Pstack clearly reads as more human despite likely also being AI-generated
   - Conclusion: **The skill itself (Unslop) can make AI output read human**

4. **Token burnout drives discovery**
   - Arena is "super fun" for "token burners" (people with token budgets to burn)
   - Forces engineers with quota constraints to think differently
   - Hints at emerging "budget-aware" skill design as usage costs rise

---

## Personal Takeaway from Theo

**Process > Blind Installation:**
Theo's workflow (audit usage → rank skills → test copy-paste → integrate slowly) beats downloading 30 skills at once. He's using Unslop + Arena + Blast Radius + Wizard as his core rotation, with Matt's Grill and Diagnosing Bugs as situational pulls.

**Next phase:** Expects to create a fork/variant of Pstack that's fully generic (not Cursor-specific) to unlock potential in skills like Arena and Interrogate.

---

## Skill Highlights Summary

| Skill | Source | Status | Recommendation |
|-------|--------|--------|----------------|
| Unslop | Pstack | Active | **Essential** — use in every workflow |
| Arena | Pstack | Active (expensive) | High-value for synthesis; budget-conscious |
| Blast Radius | Pstack | Active | **Critical** — prevents cascading failures |
| Grill | Matt | Situational | Best for architectural reviews (m-dash caveat) |
| Diagnosing Bugs | Matt | Auto-fires | Solid; improves bug triage |
| Wizard | Matt | Planned | Very high anticipation |
| Technical Writing | Pstack | Active | Excellent semantic density |

---

## Related Topics

- [[topics/cto|CTO Topic]] — Leadership frameworks like Grill fit here
- Skills architecture and selection patterns
- AI tool workflow optimization
- Documentation and readability for LLM consumption
