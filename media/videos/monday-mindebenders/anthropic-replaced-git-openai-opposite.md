---
type: media
title: >-
  Anthropic Replaced Git. OpenAI Did the Opposite. — Multi-Agent Source Control
  at Scale
media_type: video
date: '2026-11-07'
source_url: https://youtu.be/ZtOA71C_Nco?is=h1moMwfbZ7tPvEw_
channel: Better Stack
duration: '9:17'
source_kind: mcp:put_page
ingested_via: mcp:put_page
ingested_at: '2026-11-11T08:34:19.698Z'
trust_tier: agent_written
tags:
  - MondayMindBenders
---

# Anthropic Replaced Git. OpenAI Did the Opposite.

**Series:** #MondayMindBenders  
**Channel:** Better Stack  
**Upload Date:** 2026-11-07  
**Duration:** 9:17  
**Focus:** Multi-agent code generation at scale; source control bottlenecks; divergent solutions from OpenAI and Anthropic

---

## Core Problem

AI coding agents generate code **faster than source control can handle**.

**Scale:**
- **Anthropic:** 2,500 → 30,000 code changes/day (12x increase in 4 months)
- **OpenAI:** Monorepo reliability dropped below 90%; CI infrastructure performing 25M checkouts/day
- **Bottleneck:** Git's centralized architecture wasn't designed for hundreds of agents pushing simultaneously

**Impact on smaller teams:** When multiple coding agents work on same project → file conflicts, tests break, developers spend more time fixing merge conflicts than building features.

---

## Two Divergent Solutions

### **OpenAI: Pando (Git Backend Replacement)**

**Philosophy:** Keep Git UX, replace infrastructure

**What they built:**
- Custom backend replacing Git's centralized bottleneck
- Users still run `git push`, `git pull` (no workflow change)
- Handles branch updates immediately (no shared queue)
- Caches Git pack files (repeated requests don't regenerate data)

**Results:**
- Medium push latency ↓ 80%
- Serves ~1 petabyte of Git data/day
- Designed by 1 engineer, implemented largely by Codex agents
- Kickoff to production: 10 weeks

**Tradeoff:** Reads across multiple branches aren't guaranteed perfectly synchronized (acceptable for their use case)

**Advantage:** Minimal workflow change; team didn't have to learn new system

---

### **Anthropic: Scion (Complete Git Replacement)**

**Philosophy:** Rethink version control for agent-native workflows

**What they built:**
- Complete replacement for Git
- Clients request only files they need (no large local repos)
- Commits, merges, history on server-side
- Designed for always-connected agents + CI jobs

**Results:**
- CPU/memory usage ↓ 200x vs. previous Git mirroring infrastructure
- Checkouts: minutes → seconds
- CI recovered 25% CPU capacity

**Cost:** Had to rebuild code review, code search, CI tooling to work with Scion (massive infrastructure investment)

**Advantage:** Purpose-built for agent workflows; significant efficiency gains

---

## What You Should Be Doing (The 4 Practical Principles)

### **1. Git Worktrees for Multi-Agent Parallelization**

**Problem:** Multiple agents in same checkout → editing same files → interference

**Solution:** Create isolated working directories

```bash
# Create separate worktrees for each agent
git worktree add branch-feature-1
git worktree add branch-feature-2

# Each agent works in its own folder + branch independently
# No file conflicts during execution

# View all active worktrees
git worktree list

# Merge and clean up when done
git merge branch-feature-1
git worktree remove branch-feature-1
```

**Benefit:** Agents work in parallel without interfering; conflicts deferred to merge time (which is manageable)

**Applicability:** Works TODAY with standard Git (no infrastructure changes needed)

---

### **2. Sparse Checkouts for Large Repos**

**Problem:** Don't need entire monorepo checked out to work on one service

**Solution:** Use Git sparse checkouts

```bash
git clone --sparse <repo>
git sparse-checkout add services/service-a
```

**Benefit:** Reduces checkout time, disk space, and initial latency for agents

---

### **3. Optimize CI Pipeline**

**Problem:** 5 agents → 5 PRs → 5 full test suites run (redundant work)

**Solution:**
- Cache dependencies aggressively
- Avoid duplicate jobs
- Run only relevant tests (e.g., tests for changed files)
- Skip full suite when safe

**Example Optimization:**
- Monorepo with services A, B, C
- Agent modifies Service A only → run only Service A tests + integration tests
- Skip unrelated Service B/C test suites

**Benefit:** As agents get faster, CI becomes the new bottleneck; this keeps it competitive

---

### **4. Code Review & Validation (The Hard Part)**

**Key Insight:** Solving source control doesn't automatically solve code review bottleneck

**Reality:**
- Agents can generate code faster
- But humans still need to review, validate, check security, test
- Code review + testing now becomes bottleneck (not source control)

**What teams should do:**
- Invest in automated code review (linting, type checking, security scanning)
- Build agent-specific validation (e.g., "did this agent follow patterns from existing code?")
- Parallel code review workflows (don't serialize reviews)
- Consider hybrid human-agent review (agent reviews → human spot-check)

---

## Key Takeaways

| Aspect | OpenAI (Pando) | Anthropic (Scion) | Your Team Now |
|--------|---|---|---|
| **Approach** | Keep Git, optimize backend | Replace Git entirely | Use Git worktrees + optimize CI |
| **Workflow Change** | None | Massive (new tools required) | Minimal (Git commands still work) |
| **Efficiency Gains** | 80% latency improvement | 200x CPU/memory reduction | 30-50% improvement (from worktrees + CI optimization) |
| **Adoption Barrier** | Low (transparent) | High (rebuild all tooling) | Very low (standard Git features) |
| **When to consider** | Very high Git push volume | Complete DevOps rewrite | Now (multi-agent workflows) |

---

## Multi-Human + Multi-Agent Workflow Implications

### **Current State Problem:**

1. **2 agents + 1 human dev** on same repo
   - Agent A: Building feature in `/src/feature`
   - Agent B: Fixing bug in `/src/utils`
   - Human: Refactoring `/src/core`
   - **Without worktrees:** All three conflict, waste time resolving merges

2. **Code review bottleneck:**
   - 3 agents generate 3 PRs (each 500+ lines)
   - 1 human reviewer
   - Reviewer becomes 3x slower than agent velocity
   - Queue grows; velocity caps

### **Recommended Workflow:**

```
┌─────────────────────────────────────┐
│ Agent Assignment Strategy           │
├─────────────────────────────────────┤
│ Agent A → Worktree: feature-x       │
│ Agent B → Worktree: bugfix-y        │
│ Human   → Worktree: refactor-z      │
│                                     │
│ All work in parallel (no conflicts) │
└─────────────────────────────────────┘
         ↓ (commit + create PR)
┌─────────────────────────────────────┐
│ Parallel Code Review Stage          │
├─────────────────────────────────────┤
│ • Automated checks (linting, types) │
│ • Security scanning                 │
│ • Agent-generated tests pass?       │
│ • Human spot-check (10 min)         │
└─────────────────────────────────────┘
         ↓ (approved PRs)
┌─────────────────────────────────────┐
│ Merge Strategy                      │
├─────────────────────────────────────┤
│ • Sequential merges (avoid conflicts)│
│ • Sparse checkout + rebase if needed│
│ • CI runs only affected tests       │
└─────────────────────────────────────┘
```

### **Tools & Practices to Adopt:**

1. **Branch-per-agent assignment**
   - Agent lifecycle: create worktree → work → PR → merge → cleanup
   - Clear ownership per branch

2. **Hybrid review (Agent + Human)**
   - Automated agent: style, types, basic tests
   - Human: architecture, correctness, business logic (5-10 min review)
   - Approval gate: both must pass

3. **Queue-based task distribution**
   - Don't assign 3 agents to overlapping code
   - Use dependency tracking (task A → agent, task B after A approved)
   - Maximize parallelization without conflicts

4. **Observe CI metrics**
   - When does CI become the bottleneck (vs code review)?
   - Optimize test suites as velocity increases
   - Alert when queue grows > 5 PRs

---

## Open Questions for Implementation

1. **How do we automatically assign agents to non-conflicting code areas?**
2. **Can we build predictive merge conflict detection?** (Warn before agent creates conflicting code)
3. **Should code review be parallelized** (3 reviewers for 3 agents) **or serialized** (1 reviewer, fast feedback loop)?
4. **What metrics indicate we need Scion-like infrastructure** (replacement source control)?
5. **How do we handle "failed" agent PRs** without human intervention? (Auto-revert, auto-fix, or escalate?)

---

## Related

- [[topics/cto|CTO Topic]] — DevOps and infrastructure scaling
- Multi-agent orchestration
- CI/CD optimization
- Code review workflows
