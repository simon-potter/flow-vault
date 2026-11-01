---
type: concept
title: 'Extraction: Hermes Advanced Delegation Video'
source_page: >-
  processes/hermes-self-improvement/ingested-sources/hermes-delegation-advanced-2026-10-28
date_extracted: 2026-11-01T00:00:00.000Z
extraction_status: ready
source_kind: mcp:put_page
ingested_via: mcp:put_page
ingested_at: '2026-11-01T07:32:35.398Z'
trust_tier: agent_written
---

# Extraction: Hermes Advanced Delegation Feature Analysis

**Source:** YouTube video - "Hermes Agent Just Got Smarter at Managing AI Teams"  
**Channel:** Julian Goldie SEO  
**Duration:** 7:55  
**Published:** 2026-10-28  
**Extracted:** 2026-11-01  

---

## Executive Summary

The video demonstrates Hermes' new **Advanced Delegation plugin** that allows intelligent task routing to different models/profiles based on complexity. Key insight: previously all sub-agents used the same model (wasteful); now they can be specialized (cost + speed efficient).

**Improvements identified:** 6  
**Ready for implementation:** 5 (1 is aspirational)

---

## Extracted Improvements

### Improvement #1: Model Routes Documentation & Tutorial

**Idea Title:** Create comprehensive guide for model routes configuration  
**Category:** Documentation  
**Priority Suggested by Source:** High (featured as primary use case)  
**Your Assessment:** High  
**Difficulty:** Quick (< 1hr)

**Problem Solved:**  
Current Hermes docs briefly mention model routes but lack:
- Step-by-step setup guide
- Real config examples (YAML, CLI commands)
- Decision tree for when to use model routes vs profile routes
- Best practices for route naming

**Current State:**  
Documentation exists in `docs/reference/` but is minimal (~200 words).
Users ask in community: "How do I actually set up routes?"

**Proposed Solution:**  
Create new documentation page (or expand existing):
```
Content structure:
1. What are model routes? (problem + benefit)
2. Prerequisites (version, install)
3. Step-by-step setup (CLI, desktop app)
4. Config examples (YAML templates)
5. When to use (simple vs complex scenarios)
6. Troubleshooting (common mistakes)
7. Best practices (naming, defaults, monitoring)
```

**Difficulty to Implement:** Quick (1-2 hours)

**Dependencies/Blockers:** None

**Who Should Own This:** Technical writer or docs agent

**Acceptance Criteria (AC):**
- [ ] AC 1: Guide covers setup for CLI AND desktop app
- [ ] AC 2: Includes at least 3 real YAML config examples
- [ ] AC 3: Decision tree explains model routes vs profile routes vs no delegation
- [ ] AC 4: Guide includes 5+ troubleshooting scenarios
- [ ] AC 5: Doc is testable (all commands can be run successfully)

**Estimated Effort:** 1.5 hours  
**Evidence:** Video shows setup is simple, but docs question suggests users are confused

---

### Improvement #2: Profile Routes Documentation & Tutorial

**Idea Title:** Create comprehensive guide for profile routes configuration  
**Category:** Documentation  
**Priority Suggested by Source:** High (positioned as advanced feature)  
**Your Assessment:** High  
**Difficulty:** Medium (1-2 hrs)

**Problem Solved:**  
Profile routes are more powerful than model routes but also more complex:
- Requires understanding profiles (model + skills + permissions)
- Requires setting up allowed lists
- Requires understanding when each profile is used
- No examples in current docs for profile-based delegation

**Current State:**  
Profile routes mentioned in API docs but not tutorial docs.
Users must reverse-engineer from code examples.

**Proposed Solution:**  
New documentation page focused on profile routes:
```
1. What are profiles? (model + skills + permissions)
2. How delegation uses profiles (routing logic)
3. Step-by-step: create profiles for specialization
4. Step-by-step: set up allowed lists
5. Real examples:
   - Marketing team (researcher, writer, editor profiles)
   - Software dev team (coder, debugger, reviewer profiles)
   - Research team (data analyst, writer, synthesizer profiles)
6. When profile routes > model routes
7. Troubleshooting (profile not found, permissions denied, etc.)
```

**Difficulty to Implement:** Medium (2-3 hours)

**Dependencies/Blockers:** Depends on Improvement #1 (model routes guide) for context

**Who Should Own This:** Technical writer or docs agent

**Acceptance Criteria (AC):**
- [ ] AC 1: Guide explains profiles (model + skills + permissions concept)
- [ ] AC 2: Includes setup steps for creating delegation-enabled profiles
- [ ] AC 3: Documents allowed list syntax and permissions model
- [ ] AC 4: Includes 3+ real-world profile route examples (marketing, dev, research)
- [ ] AC 5: Troubleshooting section covers 5+ common issues

**Estimated Effort:** 2.5 hours  
**Evidence:** Video spends significant time explaining profile routes but current docs lack tutorial

---

### Improvement #3: In-App Delegation Configuration Wizard

**Idea Title:** Add interactive delegation setup wizard (CLI + desktop)  
**Category:** Feature (UX enhancement)  
**Priority Suggested by Source:** Medium (quick to explain but valuable to implement)  
**Your Assessment:** High  
**Difficulty:** Complex (4-6 hrs)

**Problem Solved:**  
Current setup process requires users to:
- Understand YAML/config syntax
- Know which models are available
- Manually enter credentials/provider info
- Test if config works

A wizard would:
- Guide users through questions ("What's your fast model?")
- Validate as you go (test connection to model provider)
- Generate config automatically
- Explain each choice
- Let users review before saving

**Current State:**  
`hermes delegation config` command exists but is bare CLI (you provide everything).
Desktop app has install button but no guided setup flow.

**Proposed Solution:**  
```bash
hermes delegation config --interactive
# Q1: Model routes or profile routes?
# Q2: How many routes/profiles?
# Q3 (per route): Route name? Model? Provider? (with validation)
# Q4: Set default route?
# Q5: Test configuration?
# Review + Save
```

Desktop: Similar wizard in Settings > Sub-agents > Configure Routes

**Difficulty to Implement:** Complex (5-8 hours)

**Dependencies/Blockers:**
- Need list of available models (OpenRouter, Anthropic, OpenAI, local)
- Need validation logic (test model connection)
- Need config format validation

**Who Should Own This:** Feature engineer (backend + CLI)

**Acceptance Criteria (AC):**
- [ ] AC 1: Interactive wizard guides through model routes setup
- [ ] AC 2: Wizard guides through profile routes setup
- [ ] AC 3: Wizard validates model connection before saving
- [ ] AC 4: Generated config is correct YAML/valid
- [ ] AC 5: Desktop app has matching setup flow

**Estimated Effort:** 6 hours  
**Evidence:** Video emphasizes simplicity ("pretty simple") but wizard would make it even simpler

---

### Improvement #4: Route Decision Helper / LLM Agent Improvement

**Idea Title:** Improve agent's route selection logic / add decision hints  
**Category:** Feature (AI enhancement)  
**Priority Suggested by Source:** Medium  
**Your Assessment:** Medium  
**Difficulty:** Complex (4-6 hrs)

**Problem Solved:**  
Video mentions: agent needs to decide "This is a quick job, use fast"
Current implementation may not always choose correctly:
- Agent might over-use fast model (losing quality)
- Agent might over-use deep model (wasting cost/time)
- Agent might not understand which route for which task

Improvement: Give agent explicit decision hints:
```
routes:
  fast:
    for: "quick lookups, short summaries, simple edits, URL fetches"
    examples: "summarize article", "extract email from text"
  deep:
    for: "complex analysis, debugging, planning, synthesis"
    examples: "debug production error", "plan new feature"
```

Agent sees hints when deciding which route to use.

**Current State:**  
Agent sees route names + descriptions (currently ~10-20 words)
No explicit decision guidance.

**Proposed Solution:**  
1. Extend route description to include examples
2. Add "for" field explaining ideal use cases
3. Optionally: create decision prompt that explains routing logic to agent
4. Optionally: track route choices + refine hints based on actual usage

**Difficulty to Implement:** Complex (4-8 hours)

**Dependencies/Blockers:** Requires prompt engineering + testing

**Who Should Own This:** ML/prompting engineer

**Acceptance Criteria (AC):**
- [ ] AC 1: Routes can include "for" and "examples" fields
- [ ] AC 2: Agent considers these hints when choosing routes
- [ ] AC 3: Agent correctly routes 90%+ of simple vs complex tasks
- [ ] AC 4: Logging shows which hints were considered
- [ ] AC 5: Can improve hints based on usage patterns

**Estimated Effort:** 5 hours  
**Evidence:** Video emphasizes intelligent routing; this improves the intelligence

---

### Improvement #5: Delegation Audit Dashboard / Monitoring UI

**Idea Title:** Add dashboard showing delegation stats + cost savings  
**Category:** Feature (observability/monitoring)  
**Priority Suggested by Source:** Medium (video mentions "see which route it ran on")  
**Your Assessment:** High  
**Difficulty:** Medium (3-4 hrs)

**Problem Solved:**  
Video mentions: "Every finished task tells you which route it ran on"
But currently there's no dashboard view. Users see logs (raw) but not:
- Which routes are most used?
- Cost per route vs total?
- Time savings from using fast routes?
- Is agent making good routing decisions?

**Current State:**  
Logs exist in task history but no UI to visualize.
Users must parse logs manually.

**Proposed Solution:**  
Add delegation monitoring dashboard:
```
showing:
- Tasks per route (pie chart)
- Cost breakdown (bar chart: fast vs deep vs local)
- Speed comparison (avg time per route)
- Cost savings vs all-deep baseline
- Route decision trends over time
- Quality metrics (task success rate per route)

Access: hermes dashboard delegation
Or: Desktop app > Analytics > Delegation
```

**Difficulty to Implement:** Medium (3-5 hours)

**Dependencies/Blockers:**
- Need historical data (logs already captured)
- Need analytics backend (might exist)
- Need dashboard UI (Hermes has dashboard framework)

**Who Should Own This:** Data + frontend engineer

**Acceptance Criteria (AC):**
- [ ] AC 1: Dashboard shows tasks per route
- [ ] AC 2: Shows cost breakdown (model costs + API costs)
- [ ] AC 3: Shows speed/time savings comparison
- [ ] AC 4: Shows cumulative savings vs baseline (all-deep)
- [ ] AC 5: Data refreshes automatically, accessible via CLI or UI

**Estimated Effort:** 3.5 hours  
**Evidence:** Video emphasizes visibility ("you always know what did what")

---

### Improvement #6 (ASPIRATIONAL): Auto-Optimal Route Selection

**Idea Title:** Machine learning-based automatic route optimization  
**Category:** Feature (AI/ML enhancement)  
**Priority Suggested by Source:** Mentioned (future direction)  
**Your Assessment:** Low (aspirational, complex)  
**Difficulty:** Complex (12+ hrs)

**Problem Solved:**  
Currently: Users manually define routes and agent picks from menu
Future: System learns from task complexity + outcome to suggest optimal routes

Example:
```
Suggestion: "Your route 'fast' is under-utilized. 
Tasks like 'summarize' and 'extract' run successfully on fast.
Consider moving more to fast to save cost."
```

Or automatically:
```
1. Track: task type + complexity + route used + cost + success
2. Learn: which tasks succeed on which routes
3. Suggest: "Tasks of type X should use route Y"
4. Adapt: auto-adjust route recommendations based on patterns
```

**Current State:**  
Not implemented. Requires ML/analytics.

**Proposed Solution:**  
1. Collect delegation metrics (type, complexity, route, cost, success)
2. Analyze patterns (what works on fast vs deep)
3. Generate recommendations
4. Optionally: auto-adjust if user enables

**Difficulty to Implement:** Complex (12-20 hours)

**Dependencies/Blockers:**
- Need analytics pipeline
- Need ML model for pattern detection
- Need feedback mechanism
- Privacy/data considerations

**Who Should Own This:** ML engineer + data engineer

**Acceptance Criteria (AC):**
- [ ] AC 1: System collects routing metrics
- [ ] AC 2: Can analyze which task types use which routes
- [ ] AC 3: Generates recommendations ("move X tasks to fast")
- [ ] AC 4: Recommendations are accurate (validated against manual analysis)
- [ ] AC 5: User can accept/reject recommendations

**Estimated Effort:** 15 hours  
**Evidence:** Video sets foundation; this is next-level improvement for future

---

## Summary

| # | Improvement | Category | Difficulty | Effort | Priority | Status |
|---|---|---|---|---|---|---|
| 1 | Model Routes Doc | Docs | Quick | 1.5h | High | Ready |
| 2 | Profile Routes Doc | Docs | Medium | 2.5h | High | Ready |
| 3 | Setup Wizard | Feature | Complex | 6h | High | Ready |
| 4 | Route Decision Logic | Feature | Complex | 5h | Medium | Ready |
| 5 | Delegation Dashboard | Feature | Medium | 3.5h | High | Ready |
| 6 | Auto-Optimization | Feature | Complex | 15h | Low | Aspirational |

**Total improvements found:** 6  
**Ready for Kanban:** 5 (skip #6, aspirational)  
**Estimated total effort:** 18.5 hours (implement 1-5)  

---

## Kanban Tasks to Create

Create one task per improvement (1-5):
1. HERMES-2801: Model Routes Documentation
2. HERMES-2802: Profile Routes Documentation
3. HERMES-2803: Delegation Setup Wizard
4. HERMES-2804: Improve Route Decision Logic
5. HERMES-2805: Delegation Audit Dashboard

(Improvement #6 will be tracked separately as future research)

---

**Extraction completed:** 2026-11-01  
**Ready for Kanban creation:** Yes  
**Implementation priority:** 5 high-value improvements, 1-2 hr each (3-5)
