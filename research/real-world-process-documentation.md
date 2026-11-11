---
type: concept
title: 'Real-World Process Documentation: Teams Doing Parallel Agents + TDD at Scale'
date: '2026-11-11'
source_kind: mcp:put_page
ingested_via: mcp:put_page
ingested_at: '2026-11-11T12:04:04.169Z'
trust_tier: agent_written
tags:
  - case-studies
  - documented-processes
  - parallel-agents
  - team-workflows
---

## Overview

These are **production teams** documenting their exact process for parallel agent development. Not theory—what's actually working in practice.

---

## 1. **Abnormal AI: "Specs, Not Sprints"** ⭐ Most Detailed

**Read:** https://builders.abnormal.ai/p/specs-not-sprints

**Team Size:** 8+ developers

**Workflow Model:**
- **Before Monday:** Engineers write a "tech concept" (short doc with intended UX, hard requirements, design decisions, DB schemas, API contracts)
- **Monday Planning Meeting:** Team reviews tech concepts, generates first-pass implementation spec
- **Tuesday-Friday:** Execution against specs
  - Most engineers run ~5 background agents (parallel)
  - Also run ~5 local Claude Code sessions (for back-and-forth work)
  - Agents test their own work: spin up services, hit endpoints, click through UI with Playwright
- **Friday Demos:** Show work to security team, catch misalignment early

**Key Insight:** "The bare minimum is using a Cursor agent. At the highest level, you're completely delegating across a suite of background agents. You're writing the spec, not touching code at all."

**Metrics:**
- Multiple specs in flight simultaneously (asynchronous progression through review + implementation)
- Developers can spec competing approaches in parallel, evaluate side-by-side before committing

**Parallel Safeguards:**
- Static analyzers + linters (Ruff, MyPy)
- Custom internal lint rules
- Cloud code sub-agents for self-review
- "Review by proof" — agents provide screenshots/evidence of testing
- CodeRabbit pulls in markdown architecture files as context

**Related Resources:**
- "Our Design Docs Write Themselves" — Auto-generated specs from design review recordings + Slack threads + PR comments (weekly agent runs)
- "Make Every PR Prove Itself" — Pre-commit test plans define evidence, agents configure testboxes with pre-existing + just-in-time integration tests
- "GTM Engineering With Abnormally" — Engineers build scalable connectors + agent tools; PMs use Claude Code to assemble them

---

## 2. **SDLC-Kit: Jira → Reviewed MR Out** ⭐ Most Practical

**GitHub:** https://github.com/aniketshukla1/sdlc-kit

**What it is:** Drop-in Cursor kit (rules, skills, checks, hooks) for agents

**The Flow:**
1. Jira ticket in
2. Agent writes tests first (RED phase — /write-tests skill)
3. Tests FAIL (confirmed in PROGRESS.md)
4. Agent writes code to make tests pass (GREEN phase — /db-migration, /backend-implement, /frontend-implement)
5. Local CI runs (check_all.sh: lint, types, tests, migrations, 11 guards)
6. If passing → GitLab MR opened
7. Remote CI + CodeRabbit review
8. Reviewed MR ready

**Key Guardrails:**
```
Phase          Skill           Done When
════════════════════════════════════════════════════════════════
1. Plan        /plan           GitHub issues created
2. Explore     /codebase       Repo map written
3. Design      /design         ADR drafted
4. Build       /write-tests    Tests failing
           /db-migration    Migration scripts ready
           /backend-impl    Code passes tests
5. Review      /self-review    Agent checks own work
6. Commit      /commit         Branch pushed + PR open
```

**Tests Written First:** Every task starts with failing tests. Agent cannot say "done" until tests pass.

**Test Coverage Gate:** Changed lines must be covered by tests (default 90%). Lowering this minimum fails the guard.

**Who This Works For:**
- Cursor, Claude Code, Codex
- GitLab or GitHub
- Python/JS/TS stacks

---

## 3. **Agent Engineering Playbook: Battle-Tested Process**

**GitHub:** https://github.com/chuckconway/agent-engineering-playbook

**What it is:** 1,400+ line comprehensive guide extracted from production

**Main Problem Solved:** "Agent writes code fast, but doesn't follow your conventions, breaks patterns, creates inconsistent commits. You spend as much time fixing the agent as coding yourself."

**Solution Layers:**

### A. Agent.md as Project Constitution
- Single file that makes every agent session productive
- Defines conventions, patterns, exceptions
- Loaded into every agent context

### B. Skills System (Reusable Workflows)
- `/commit` → commit + push + PR + cleanup
- `/review` → multi-persona code review (security, architecture, performance, style)
- `/brainstorm` → design exploration
- Each skill has persona documents (what to hunt for, what to ignore, calibration guidance)

### C. Branching & Worktree Workflow
- Parallel-safe isolation for humans + agents working simultaneously
- Git worktrees for each parallel task

### D. Two-Tier Quality Gates
- **Local CI** (before push): same checks as remote, so you know it will pass
- **Remote CI** (safety net): runs on main, catches race conditions
- Single source of truth for checks (ci-checks.json)

### E. Code Health Metrics
- Maintainability index
- Cyclomatic complexity
- File size
- Duplication
- Quality ratchet (only improves, never regresses)

### F. Compound Learning Loop
1. **Consult:** Before starting, search `docs/lessons-learned/`
2. **Capture:** After resolving non-trivial bug, write a lesson
3. **Promote:** When lesson recurs, elevate it to a rule in Agent.md

**Copy-Pasteable Examples Included:**
- ci_check_local.py (local CI runner)
- check_code_health.py (MI, CC, SLOC, duplication)
- quality_delta.py (PR quality regression gate)
- Skills: commit, code-review, brainstorm

**Tech Stack (This Repo):** Python/FastAPI + React/TypeScript
**Adaptable To:** Any stack (alternatives listed for linters, type checkers, etc.)

---

## 4. **AI-Native Team Playbook: "Bolt" Methodology**

**GitHub:** https://github.com/camillanapoles/claude-code-agent-scaffold/blob/main/docs/ai-native-team-playbook.md

**Core Innovation:** Replaces fixed-duration sprints with **scope-boxed iterations** (bolts)

**Traditional Agile Problem:** Writing code is NOT the bottleneck anymore. Specifying + verifying are.

| Traditional | AI-Native |
|---|---|
| Writing code = bottleneck | Specifying + verifying = bottleneck |
| Devs spend most time coding | Devs spend most time reviewing, testing, specifying |
| Story points estimate coding effort | Story points underweight review (the hard part) |
| Code review = lightweight gate | Code review = primary quality assurance |

**Bolt Lifecycle (3 Phases):**

| Phase | Time Share | Activities | Who |
|---|---|---|---|
| Spec | ~20% | Requirements, AC, technical design, contracts, exit conditions | PM, Tech Lead, devs |
| Build | ~50% | AI-assisted impl, iterative dev, unit tests | AI agents + devs |
| Verify | ~30% | Code review, security review, integration tests, manual verification, docs | Devs, reviewers |

**Key Differences from Sprints:**
- No fixed duration (ends when scope verified, not timebox expires)
- Scope is LOCKED (doesn't change; if it changes, new bolt)
- Verify is first-class (not leftover time)
- Smaller scope (1-3 days, not 2 weeks)

**Mob Rituals:**
1. **Planning Mob** (40 min)
   - PM presents user problem + AC (10 min)
   - Tech Lead proposes technical approach + contracts (10 min)
   - Group refines exit conditions (15 min)
   - Identify risks + unknowns (5 min)
   - Decide: proceed or split (5 min)
   - Output: Spec with concrete AC, contracts, machine-verifiable exit conditions

2. **Async Code Review**
   - Impl posts summary (what + why)
   - Reviewers post findings (within 4 hours)
   - Mechanical fixes → resolve async
   - Architectural → schedule 15-min sync

**Common Anti-Patterns & Fixes:**

1. **Test Debt**
   - Symptom: "Tests pass but nothing's tested"
   - Fix: Human writes acceptance tests; AI can't be trusted with critical path

2. **Context Drift**
   - Symptom: Codebase diverges from vision; each bolt internally consistent, architecturally inconsistent
   - Fix: Monthly architecture reviews, maintain ADRs, tech lead audits for drift

3. **Over-Delegation**
   - Symptom: Dev delegates task, moves on without reading output
   - Fix: Require human review for critical paths; delegation without review = abdication

---

## 5. **Awesome Agentic Coding: Practical Roadmap**

**GitHub:** https://github.com/xqliu/awesome-agentic-coding

**What It Is:** Roadmap for teams adopting agentic workflows (not just a curated list)

**Progression (Step-by-Step):**

### Level 1: Everyday Work
- Agent explores unfamiliar code, explains it
- You verify against actual code
- Commit it → repo map for next session
- Agent learns once, team uses forever

### Level 2: Autonomous Loop
- Agent changes code → builds → runs static analysis + tests → reads failures → fixes → repeats
- Put build/lint/tests behind one command (must finish in minutes, same result every run)

### Level 3: Multi-Agent Review
- Before human reads diff, secondary context (reviewer sub-agent, second agent, or PR bot like CodeRabbit) reviews against spec

### Level 4: Skills & Hooks
- Reusable workflows agents activate on demand
- Pre-commit hooks enforce standards

### Level 5: MCP Integration
- Connect Model Context Protocol servers
- Agents access live tools (GitHub, Jira, Slack, databases)

### Level 6: Parallel Agents
- Multiple agents working in parallel git worktrees
- Isolated tool permissions per agent
- Each agent is a mini-project

### Level 7: Fleet Orchestration
- 5-10+ agents coordinating
- Agent-to-agent handoffs
- Cross-repo dependency management

---

## 6. **Spec-Driven Development: Three-Phase Process**

**GitHub:** https://github.com/calebdel/spec-driven-development

**Complete Guide with Examples & Templates**

**Three Phases:**
1. **Requirements Phase** → Structured requirements (EARS format)
2. **Design Phase** → Comprehensive design documents
3. **Tasks Phase** → Actionable coding tasks

**Worked Examples Included:**
- Simple features
- Complex systems
- Case studies (success + failures)
- Troubleshooting guide

**Case Study: Financial Microservices (75% Faster Integration)**
- Problem: Microservices failed when deployed together (API contract mismatches)
- Solution: Mandate API-first (OpenAPI specs before code)
- Result: 75% reduction in integration cycle time
- Mechanism: Specs → Specmatic mock servers → parallel dev → contract tests in CI

**Case Study: Enterprise Software (Reduced Ambiguity)**
- Problem: Devs + PMs disagreed on "done"
- Solution: Cucumber/Gherkin scenarios (executable examples)
- Result: Stakeholder-verifiable requirements, objective "done" definition

---

## Comparison: Which Fits Your 4-Person Team?

| Repo | Best For | Complexity | Setup Time |
|---|---|---|---|
| **SDLC-Kit** | Strict TDD + Jira → MR automation | Medium | 1-2 days (copy-paste mostly) |
| **Abnormal AI Blog** | Understanding spec-first + background agents | Theory | Read (2 hours) |
| **Agent Playbook** | Complete process (philosophies + copy-paste code) | High | 1 week (phased rollout included) |
| **AI-Native Playbook** | Team rituals + anti-patterns | Process | Read + adapt (2-3 hours) |
| **Awesome Agentic** | Roadmap + toolbox | Roadmap | Reference during implementation |
| **Spec-Driven Dev** | Examples + templates | Medium | 1-2 days (templates + case studies) |

---

## Recommended Starting Point for Your Team

### Week 1: Absorb
1. Read **Abnormal AI blog** (understand the mental model)
2. Read **AI-Native Playbook** (understand team rituals)
3. Skim **SDLC-Kit README** (see end-to-end automation)

### Week 2: Adapt
1. Create a **tech concept** (your version of Abnormal's prep)
2. Write a **spec with OpenAPI** (your version of Spec-Driven Dev)
3. Pick **2-3 skills** from SDLC-Kit that match your stack

### Week 3: Trial Run
1. Run **one feature** end-to-end with your adapted process
2. Document what worked, what was painful
3. Refine based on learnings

### Week 4+: Iterate
1. Add **quality gates** (from Agent Playbook)
2. Add **parallel agents** (git worktrees from SDLC-Kit)
3. Measure metrics (from Playbook: code health, test coverage)

---

## Key Takeaways Across All Teams

✅ **Specs come first** (not code)
✅ **Tests are locked** (can't be changed to make code pass)
✅ **Agents work in parallel worktrees** (no conflicts)
✅ **Quality gates are automated** (local = remote CI)
✅ **Review is async unless architectural** (speed)
✅ **Learning is captured + elevated** (compound knowledge)
✅ **Verification is first-class** (~30% of time, not afterthought)
