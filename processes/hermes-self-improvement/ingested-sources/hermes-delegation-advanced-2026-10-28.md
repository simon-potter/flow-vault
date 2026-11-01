---
type: concept
title: 'Hermes Agent Advanced Delegation: Model & Profile Routes'
source: youtube
video_id: 3SAirL3cykU
channel: Julian Goldie SEO
date_published: '2026-10-28'
duration_minutes: 7
duration_seconds: 55
captions_type: en-orig (auto-generated)
transcript_words: 1882
source_kind: mcp:put_page
ingested_via: mcp:put_page
ingested_at: '2026-11-01T07:31:50.528Z'
trust_tier: external_untrusted
tags:
  - agent-delegation
  - feature-update
  - hermes
  - model-selection
  - self-improvement
  - sub-agents
---

# Hermes Agent Advanced Delegation: Model & Profile Routes

**Source:** YouTube video by Julian Goldie SEO  
**Title:** Hermes Agent Just Got Smarter at Managing AI Teams  
**Duration:** 7:55  
**Published:** 2026-10-28  
**Transcript:** Auto-generated (1,882 words)

---

## Overview

This video presents Hermes' new **Advanced Delegation** plugin that allows orchestrator agents to assign different models or profiles to sub-agents based on task type. Previously, all sub-agents used the same model regardless of task complexity. Now, agents can intelligently route work:

- **Simple tasks** (lookups, summaries, edits) → Fast/cheap model
- **Complex tasks** (debugging, design, planning) → Powerful model
- **Specialized work** (code, research, design) → Custom profile

---

## Key Problem Solved

**Before:** All sub-agents share one model
- Wasteful: expensive heavy model runs trivial tasks
- Slow: fast simple tasks wait in queue with complex work
- Inefficient: no specialization

**After:** Each sub-agent gets the right tool
- Cost-efficient: cheap models handle simple work
- Fast: quick jobs run fast, hard jobs get power
- Specialized: profiles can match job type

---

## Two Implementation Approaches

### 1. Model Routes (Simple)

**What it does:** Orchestrator picks from a list of named models

**Setup:**
```
define routes:
  - fast: cheap, quick model (GPT-4 mini, Claude 3.5 haiku)
  - deep: powerful model (Claude Opus, GPT-4 Turbo)
  - local: on-device model (privacy-critical work)
```

**How it works:**
- Agent sees only route NAMES + descriptions (not credentials)
- When a task comes in, agent chooses: "This is quick, use fast"
- Agent never invents routes, only picks from your menu
- Credentials/endpoints stay hidden from the agent

**Use case:** Simple task routing when one profile is sufficient

### 2. Profile Routes (Advanced)

**What it does:** Orchestrator delegates to full profiles with different skills

**Setup:**
```
define profiles:
  - Researcher: web research, analysis, writing skills
  - Coder: code generation, debugging, testing skills
  - Designer: design planning, UX research, wireframing
```

**How it works:**
- Each profile has its own model, skills, permissions, personality
- Orchestrator hands tasks to specialized profiles
- Each profile shows up with exact tools needed
- Allowed list ensures no unauthorized profiles can be used

**Use case:** Complex multi-specialist workflows

---

## Setup Process

### Prerequisites
- Hermes version: **0.22.5 or newer**

### Installation

**CLI:**
```bash
hermes plugins install advanced-delegation
```

**Desktop app:**
- Settings → Model section → Sub-agents → Install button

**Enable/configure:**
```bash
hermes delegation config
# Choose mode: model-routes OR profile-routes
# Define your routes/profiles
```

**In-session toggle:**
```
/delegation
# Switch modes or set default
```

### Configuration Details

**Per-profile installation:** Plugin installed in the profile that does delegating, not globally

**One mode at a time:** Can't run model-routes AND profile-routes simultaneously; can switch between them

**Default route:** Set one route as fallback if agent doesn't choose one

**Preserve settings:** Switching modes remembers old config, no data loss

---

## Safety Features

**1. Agent Isolation**
- Agent sees ONLY route names + descriptions
- Never sees API keys, credentials, model IDs, endpoints
- Can't invent routes or access unauthorized resources

**2. Profile Whitelisting**
- Profiles can only delegate to helpers on explicit allowed list
- No sneaking in unauthorized profiles
- Admin/human controls team membership

**3. Audit Trail**
- Every completed task logs which route/profile it used
- Full visibility: "Job X used fast model, Job Y used deep"
- No guessing or black boxes

**4. Config Persistence**
- Switching modes doesn't lose old config
- Can flip back and forth, full undo capability

---

## Practical Examples

### Example 1: Marketing Content Pipeline

```
Orchestrator task: "Write 10 SEO articles about marketing"
  │
  ├→ Route: research (fast model)
  │   Do: keyword research, competitor analysis (2-3 min each)
  │
  ├→ Route: write (deep model)
  │   Do: long-form content, SEO optimization (10-15 min each)
  │
  └→ Route: edit (local model)
      Do: quick proofreading, formatting (1-2 min each)

Cost/speed: 30-40% faster, 25-30% cheaper than all-deep
```

### Example 2: Software Development Pipeline

```
Profile setup:
  - Researcher: finds docs, explains problem
  - Coder: writes/fixes code, runs tests
  - Debugger: analyzes errors, suggests fixes
  - Reviewer: checks code quality, security

Orchestrator: "Debug this production error"
  - Researcher finds error logs + context
  - Debugger analyzes root cause
  - Coder implements fix
  - Reviewer checks + approves

Benefit: Specialized profiles, no context switching
```

### Example 3: Research Project

```
Routes:
  - fast: summaries, quick lookups
  - deep: complex analysis, synthesis
  - local: proprietary data processing

Tasks:
  - Gather 50 news items (fast model, parallel)
  - Analyze trends (deep model, single instance)
  - Process private data (local model, secure)

Benefit: Right tool, right job, secure processing
```

---

## Configuration Examples

### Model Routes Config

```yaml
delegation_mode: model_routes
routes:
  fast:
    description: "Quick tasks, summaries, simple edits"
    model: gpt-4-mini-turbo
    provider: openai
  
  deep:
    description: "Complex problems, planning, debugging"
    model: claude-opus
    provider: anthropic
  
  local:
    description: "Private/sensitive data, no external calls"
    model: llama-2-70b-local
    provider: ollama

default_route: fast
```

### Profile Routes Config

```yaml
delegation_mode: profile_routes
allowed_profiles:
  - researcher
  - coder
  - designer
  - reviewer

profiles:
  researcher:
    model: claude-opus
    skills: [web-research, data-analysis, writing]
    
  coder:
    model: gpt-4-turbo
    skills: [code-gen, debugging, testing]
    
  designer:
    model: claude-opus
    skills: [ux-research, wireframing, design-review]

default_profile: researcher
```

---

## Performance Impact

**Cost Efficiency:**
- Fast routes cost ~10-30% of deep routes
- 50-60% of tasks typically qualify for fast route
- **Overall savings: 25-35%** compared to all-deep

**Speed:**
- Fast routes respond 2-4x faster
- Parallel processing of simple tasks
- Complex tasks get dedicated power
- **Overall speedup: 30-50%** for mixed workloads

**Quality:**
- No degradation in complex task output
- Better resource allocation
- Reduced queue time = faster feedback loops

---

## When to Use Each Approach

### Use Model Routes if:
- Single profile doing delegating
- Tasks vary mainly in complexity (simple vs hard)
- Want simple setup with cost/speed benefits
- Example: Marketing content pipeline (research, write, edit)

### Use Profile Routes if:
- Need specialized helpers (code, research, design)
- Tasks require different skill sets
- Want full team management with permissions
- Example: Software dev (researcher, coder, reviewer, debugger)

### Use Both (switch as needed):
- Start with model routes for simplicity
- Add profile routes when specialization needed
- Can switch modes, settings preserved

---

## Gotchas & Tips

**Gotcha 1:** Plugin must be installed in delegating profile
- Not global, per-profile only

**Gotcha 2:** Can only run one delegation mode at a time
- Can't mix model routes + profile routes simultaneously
- Can switch, but not parallel

**Gotcha 3:** Version requirement (0.22.5+)
- Older versions won't recognize the plugin
- Silent failure if not updated

**Tip 1:** Set a sensible default
- Falls back if agent doesn't choose a route
- Prevents "task stuck waiting" scenarios

**Tip 2:** Name routes clearly
- "fast", "deep", "local" are better than "model1", "model2"
- Agent reasoning is clearer

**Tip 3:** Monitor task routing
- Check logs to see which routes get used
- Validate agent is making smart choices
- Adjust if over/under using fast vs deep

**Tip 4:** Start simple, add complexity
- Begin with model routes
- Graduate to profile routes as needed
- Don't over-engineer from day one

---

## Key Takeaways

1. **Problem:** Previously all sub-agents used the same model (wasteful, slow)

2. **Solution:** Two routing approaches
   - Model routes: pick model by task complexity
   - Profile routes: delegate to specialized profiles

3. **Implementation:** `hermes delegation config` or `/delegation` command

4. **Safety:** Agent never sees credentials, profiles whitelisted, full audit trail

5. **Impact:** 25-35% cost savings, 30-50% speed improvement for mixed workloads

6. **Requirements:** Hermes 0.22.5+, plugin installed, one mode at a time

---

## Related Feature: Sub-Agents Delegation

This feature builds on Hermes' existing sub-agents capability:
- **Sub-agents:** Orchestrator splits big job into smaller parallel tasks
- **Advanced delegation:** Now each sub-agent can get specialized resources
- **Together:** Powerful multi-team workflows with optimized resource allocation

---

**Raw transcript:** `/opt/hermes/workspace/media-raw/video-3SAirL3cykU/`
