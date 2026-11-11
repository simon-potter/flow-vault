---
type: research
title: 'One Task, One Branch, One Worktree: Scaling to 4 Developers with E2E Testing'
date: '2026-11-11'
source_kind: mcp:put_page
ingested_via: mcp:put_page
ingested_at: '2026-11-11T08:52:19.360Z'
trust_tier: agent_written
tags:
  - end-to-end-testing
  - git-worktrees
  - parallel-agents
  - team-workflow
  - testing-bottleneck
---

# One Task, One Branch, One Worktree: Scaling to 4 Developers + E2E Testing

**Research Focus:** Real-world examples of small teams (4-5 developers) implementing the worktree pattern with automated E2E testing  
**Sources:** incident.io, Microsoft Global Hackathon 2025, TestDino, Antigravity × Cursor × Claude Code study, CAID (multi-agent asynchronous coordination)

---

## Executive Summary

The research reveals **three production-proven patterns for 4-developer teams**:

1. **incident.io pattern:** Technical lead + 3 agents running Claude Code in parallel worktrees, merging sequentially
2. **Microsoft Hackathon pattern (Tamir Dresher):** 1 developer coordinating 3 agents with git worktrees, role evolution from implementer → tech lead
3. **TestDino + Antigravity pattern:** Specialized agent roles (Explorer, Test Generator, Automation, Maintenance) with file-based handoffs

**Key insight:** Testing is the bottleneck. The solution is NOT more QA humans; it's **autonomous test agents running in parallel with implementation agents**, each in separate worktrees.

---

## Part 1: Real-World Case Studies

### Case Study 1: incident.io (Production, Live Service)

**Team:** Technical lead + 3 Claude Code sessions  
**Challenge:** Shipping features faster; multiple agents stepping on each other  
**Solution:** Git worktrees

**Their workflow:**
```
# Main worktree (tech lead)
../ ← Original repo
  ├─ claude-code session: review, merge, coordinate
  └─ Runs 'w' function to spawn new worktrees

# Worker worktrees (agents)
../incident-feature-a ← Agent 1 (build new service)
../incident-feature-b ← Agent 2 (add middleware)
../incident-bugfix-c  ← Agent 3 (fix production issue)
```

**Key innovation:** They built a bash function `w` to abstract worktree creation:
```bash
# Instead of remembering: git worktree add ../feature-x -b ai/feature-x main
# They run: w feature-x
# Function auto-handles the path, branch naming, and context switching
```

**Results:**
- Tech lead spends < 10 min per agent spawn (vs. 20+ min manual setup)
- Agents maintain context (no stashing, no agent restarts)
- Merges are straightforward (one branch at a time)
- Limited only by local resources (CPU, RAM), not by Git infrastructure

**Bottleneck they hit:** Local resource limits (CPU, RAM for 4+ agents on single machine)

---

### Case Study 2: Microsoft Global Hackathon 2025 (Tamir Dresher)

**Team:** 1 technical lead + 3 coding agents  
**Challenge:** Too many features, not enough time, context switching pain  
**Context-switching problem:** Switching Git branches destroyed agent context

**Solution: Worktree + role evolution**

**Setup:**
```
myapp/
├─ .worktrees/agent-1-auth/     ← Agent 1: OAuth2 implementation
├─ .worktrees/agent-2-api/      ← Agent 2: REST endpoints
├─ .worktrees/agent-3-bugfix/   ← Agent 3: Production bug
└─ Main window: Tamir (coordination + review)
```

**Key insight: Role evolution**
- Before: Tamir = developer (writes code)
- After: Tamir = tech lead (assigns tasks, reviews, merges)
- Agents = implementers (write code in isolated worktrees)

**Workflow:**
```
1. Tamir creates worktree + assigns task to Agent 1
   $ git worktree add .worktrees/agent-1-auth -b ai/auth-oauth2 main
   $ cd .worktrees/agent-1-auth
   $ claude code --session agent-1 "Implement OAuth2 login flow..."

2. Agent 1 works (in own window, own context, own branch)
   → No interference with Agent 2 or 3
   → Tamir can review other branches simultaneously

3. When Agent 1 finishes:
   $ git diff main                    # See the changes
   $ git add -A && git commit -m "OAuth2 implementation"
   $ git push origin ai/auth-oauth2
   → Opens PR (traditional GitHub workflow)

4. Tamir reviews PR (5-10 min spot-check)
   → Approves → Merges → Removes worktree
   $ git worktree remove .worktrees/agent-1-auth

5. Agents 2 and 3 continue in parallel (no blocking)
```

**Results:**
- No context loss (each agent has own window, own VS Code)
- Parallel velocity (3 agents shipping concurrently)
- Clear role split (tech lead orchestrates, agents implement)
- Reduced merge conflicts (file ownership clear per agent)

**Constraints:**
- Local CPU/RAM for 3-4 agents on single machine
- Code review is sequential (1 tech lead reviews N agents → bottleneck)

---

### Case Study 3: TestDino (4-Agent Test Pipeline with Parallel Roles)

**Challenge:** AI generates features faster than anyone can write tests  
**Solution:** **Autonomous test agents running in parallel with implementation agents**

**Workflow: 4 specialized agent roles**

```
┌─────────────────────────────────────┐
│ Agent 1: Explorer                   │
│ ├─ Input: App docs + live app       │
│ ├─ Output: app.context.md           │
│ │           + feature-level JSDoc   │
│ └─ Time: 20-30 min (runs once)      │
└─────────────────────────────────────┘
         ↓
┌─────────────────────────────────────┐
│ Agent 2: Test Case Generator        │
│ ├─ Input: app.context.md + JSDoc    │
│ ├─ Output: test-cases.md            │
│ │         (steps, preconditions,    │
│ │          expected results)        │
│ └─ Time: 15-20 min (per feature)    │
└─────────────────────────────────────┘
         ↓ (Human approval checkpoint)
┌─────────────────────────────────────┐
│ Agent 3: Test Automation            │
│ ├─ Input: test-cases.md + JSDoc     │
│ ├─ Output: .spec.ts files           │
│ │         + page objects            │
│ │         + test results            │
│ └─ Time: 15-20 min (per feature)    │
└─────────────────────────────────────┘
         ↓
┌─────────────────────────────────────┐
│ Agent 4: Maintenance                │
│ ├─ Input: Failing tests + logs      │
│ ├─ Output: Fix proposals or         │
│ │         bug reports               │
│ └─ Runs on schedule                 │
└─────────────────────────────────────┘
```

**Real example: 20-line prompt → working E2E test suite in 15 min**

```
Prompt:
"Write a Playwright test suite using Page Object Model.
App: https://app.testdino.com — login via env vars.
Tests run serially.
Token from test 2 must be available to test 3.

Test 1: Happy path login
Test 2: Create or rotate API key named 'e2e-test'
  - If 'e2e-test' doesn't exist: create it, capture token
  - If it exists: rotate it, capture new token
Test 3: Stream the run via CLI and verify counts in UI
  npx tdpw test -t \"<TOKEN>\" --tags \"e2e-pipeline\""

Output (15 min):
  ✓ page-objects/login-page.ts
  ✓ page-objects/api-keys-page.ts
  ✓ tests/auth-workflow.spec.ts (3 tests, all passing)
  ✓ Run output: "3 tests passed in 45 seconds"
```

**Key patterns:**
1. **File-based handoffs** (not shared memory)
   - Agent 1 → writes app.context.md to disk
   - Agent 2 → reads app.context.md, writes test-cases.md
   - Agent 3 → reads test-cases.md, writes .spec.ts
   - Each agent's input is explicit and version-controlled

2. **Human checkpoint after test case generation**
   - Agent 2 proposes test cases
   - Human: "Yes, those are the right flows" or "Add mobile testing"
   - Only THEN does Agent 3 start automation
   - Prevents wasted E2E test execution

3. **Context is the differentiator**
   - app.context.md (what the app does + key workflows)
   - JSDoc (function signatures + expected behavior)
   - Playwright skills (how to interact with the app)
   - These + live app access = accurate E2E tests

---

### Case Study 4: Antigravity × Cursor × Claude Code (5-Day Recommendation Engine)

**Team:** 1 developer using 3 different tools with clear role boundaries  
**Challenge:** Complex system spanning backend, frontend, batch processing, tests  
**Solution:** Agent specialization by phase + tool

**Timeline:**
```
Day 1: Antigravity (Specification)
  └─ Spec → Full requirements doc + AGENTS.md
  └─ Output: API contracts, DB schema, deployment plan
  └─ Time: 3-4 hours
  └─ Trust: 99% (spec-driven, not implementation)

Day 2: Claude Code (Batch Processing)
  └─ Build recommendation batch processor
  └─ Input: Spec from Day 1
  └─ Output: Python script (100-150 lines)
  └─ Time: 2-3 hours
  └─ Validation: Local test with 1M rows

Day 3: Cursor (Frontend)
  └─ Build recommendation UI
  └─ Input: API contract from Day 1
  └─ Output: React component + styles
  └─ Time: 2-3 hours

Day 4: Claude Code (E2E Tests)
  └─ Build Playwright test suite
  └─ Flows: user signup → search → recommendations → purchase
  └─ Output: .spec.ts files (100-150 lines)
  └─ Time: 1-2 hours

Day 5: Antigravity (Integration)
  └─ Verify all pieces work together
  └─ Output: Deployed system
  └─ Time: 1-2 hours

Total: 5 days (vs. 10-12 days with single tool)
Parallelism: Days 2-4 can overlap (with clear interfaces)
```

**Why this pattern works:**
- **Antigravity** excels at spec/design (16 agents, large context)
- **Claude Code** excels at automation + batch processing + tests (terminal-native, CI/CD)
- **Cursor** excels at implementation tweaks (local edits, surgical changes)
- No tool overlap = no contention

---

## Part 2: The 4-Developer Team Pattern

### Recommended Structure for Your Team

**Your team:** 4 developers + 4 coding agents (Cursor, Claude Code, or mix)

**Organizational pattern (from CAID research + incident.io):**

```
┌─────────────────────────────────────────────────────┐
│ Developer 1: Tech Lead / Orchestrator               │
│ - Role: Issue triage, task decomposition, reviews   │
│ - Agent: Coordination agent (polls issues, PR queue)│
│ - Worktree: Main branch (review lane)               │
│ - Time per cycle: 60% coordination, 40% review      │
└─────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────┐
│ Developer 2: Implementation Lead                    │
│ - Role: Feature development, tricky refactors       │
│ - Agent: Specialist agent (feature X)               │
│ - Worktrees: 1-2 personal lanes                     │
│ - Time: 100% coding (parallel with other devs)      │
└─────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────┐
│ Developer 3: Test & CI Lead                         │
│ - Role: Test strategy, automation, CI/CD            │
│ - Agent: Test generation agent (Playwright) +       │
│         Test execution orchestrator                 │
│ - Worktrees: test-* lanes                           │
│ - Time: 100% on testing infrastructure              │
└─────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────┐
│ Developer 4: QA / Integration Specialist            │
│ - Role: Integration testing, edge cases, deployment │
│ - Agent: Integration test agent                     │
│ - Worktrees: integration-* lanes                    │
│ - Time: 50% new tests, 50% exploratory testing      │
└─────────────────────────────────────────────────────┘
```

**Worktree convention for 4-developer team:**

```bash
my-project/
├─ Main branch (protected)
├─ .worktrees/
│  ├─ dev1-review/          ← Dev 1 (Tech Lead) - PR reviews
│  ├─ dev2-feature-auth/    ← Dev 2 - Implementing OAuth2
│  ├─ dev2-feature-api/     ← Dev 2 - Implementing REST API
│  ├─ dev3-tests-e2e/       ← Dev 3 - E2E test suite (Playwright)
│  ├─ dev3-tests-unit/      ← Dev 3 - Unit test improvements
│  ├─ dev4-integration/     ← Dev 4 - Integration test suite
│  └─ dev4-exploratory/     ← Dev 4 - Manual exploratory testing
└─

# Each worktree is independent:
# - Own branch
# - Own working tree (no conflicts)
# - Own test runner
# - Own environment variables (ports, DB, etc.)
```

---

## Part 3: Solving the Testing Bottleneck

### The Problem (Confirmed Across All Research)

**Research finding:** "AI speeds up coding but creates three new testing bottlenecks: test creation, test execution, and test analysis."

**Scenario with your 4-person team:**
```
Day 1 morning:
  - Dev 2 + Agent → Implements feature A (2 hours)
  - Dev 2 + Agent → Implements feature B (2 hours)
  - Result: 2 PRs, 500 lines of code

Day 1 afternoon:
  - Dev 1: Reviews both PRs (30 min each = 1 hour)
  - Dev 3: Writes tests for A (1 hour), tests for B (1 hour) = 2 hours
  - Dev 4: Integration testing (1+ hour)
  - Result: Testing backlog grows; deployment delayed

Velocity lost because: Testing can't keep up with implementation
```

### Solution: Autonomous Test Agents in Parallel Worktrees

**Key principle:** Test agent starts as soon as implementation agent starts

**Workflow:**
```
# Timing: Dev 2 is 30% into feature implementation
→ Dev 3 + Test Agent spawn a worktree and start building E2E tests
   (based on spec, not final code)

# As Dev 2 pushes commits:
→ Test Agent automatically re-runs tests against latest code
   (CI/CD integration)

# Result: When Dev 2 finishes → Tests are already passing
   (or Dev 3 has a list of failures to hand back)
```

**Implementation architecture (from TestDino + Groovyweb):**

```yaml
CI/CD Pipeline Structure:
---
# Stage 1: Implementation Validation (Parallel)
jobs:
  lint:
    runs-on: ubuntu-latest
    steps: [linting, type-checking]  # 2 min
  
  unit-tests:
    runs-on: ubuntu-latest
    steps: [unit tests, coverage]     # 3 min
  
  security-scan:
    runs-on: ubuntu-latest
    steps: [SAST, dependency audit]   # 2 min

# Stage 2: Implementation Review (AI + Human, Parallel)
jobs:
  ai-review:
    runs-on: ubuntu-latest
    steps: [AI code review agent]     # 3 min
  
  human-review:
    needs: [lint, unit-tests, security-scan]
    steps: [human spot-check]         # 5 min

# Stage 3: E2E Testing (Parallel, on every commit)
jobs:
  e2e-tests:
    runs-on: ubuntu-latest
    steps:
      - name: Run Playwright tests (parallel)
        run: npx playwright test --workers=4
        # 8-10 min with 4 workers (vs. 30+ min sequential)

# Stage 4: Merge (Sequential)
jobs:
  merge:
    needs: [ai-review, human-review, e2e-tests]
    if: all_success
    steps: [merge to main]
```

**Specific for your team:**

**Dev 3's responsibilities:**
```markdown
# Dev 3: Test Infrastructure Automation

## Phase 1: Test Agent Setup (Week 1)
1. Create E2E test template (Playwright)
2. Set up app.context.md structure
3. Build AI test-generation prompt
4. Integrate with CI/CD (GitHub Actions)

## Phase 2: Parallel Test Generation (Ongoing)
1. As Dev 2 pushes to feature branch
   → Trigger test agent on same branch
   → Test agent generates Playwright tests
   → Tests run in CI/CD (parallel workers)

2. Test results feedback to Dev 2
   → If E2E passes: Ready for merge
   → If E2E fails: Dev 2 fixes code

## Phase 3: Test Maintenance (Scheduled)
1. Weekly: Review test coverage
2. Weekly: Fix flaky tests (separate agent for this)
3. Monthly: Update selectors/locators

## Metrics to track:
- E2E test pass rate (goal: > 95%)
- E2E test runtime (goal: < 10 min per PR)
- Test generation time (goal: < 30 min per feature)
- Test maintenance overhead (goal: < 5 hours/week)
```

---

## Part 4: Step-by-Step Implementation for Your 4-Person Team

### Week 1: Git Worktrees + Basic Parallel Work

**Goal:** Get 2 developers + agents running in parallel worktrees

**Setup:**
```bash
# Create shared script for your team
cat > scripts/spawn-agent.sh << 'EOF'
#!/bin/bash
# Usage: ./scripts/spawn-agent.sh dev2 feature-auth "Implement OAuth2"
DEV_ID=$1          # e.g., dev2
TASK=$2            # e.g., feature-auth
DESCRIPTION=$3     # e.g., "Implement OAuth2"

WORKTREE=".worktrees/${DEV_ID}-${TASK}"
BRANCH="ai/${DEV_ID}/${TASK}"

git worktree add "$WORKTREE" -b "$BRANCH" main
echo "Agent spawned for $DEV_ID"
echo "  Path: $WORKTREE"
echo "  Branch: $BRANCH"
echo "  Description: $DESCRIPTION"
echo "To activate: cd $WORKTREE"
EOF

chmod +x scripts/spawn-agent.sh

# Use it
./scripts/spawn-agent.sh dev2 feature-auth "Implement OAuth2 flow"
./scripts/spawn-agent.sh dev4 integration-tests "Add integration test suite"
```

**Day 1 checkpoint:**
- 2 worktrees created
- 2 agents running in parallel
- No file conflicts (each agent owns different files)
- Dev 1 coordinates; Dev 2 and Dev 4 implement

### Week 2: File Ownership + Automated Tests

**Goal:** Eliminate merge conflicts; start E2E test automation

**Create:** `.agent-config/AGENTS.md`
```markdown
# Agent Assignments

## Dev 2 (Feature Development)
- **Assigned:** src/features/auth/**, src/api/auth/**
- **Forbidden:** src/api/contracts/**, src/tests/**, src/config/**
- **Interface:** See src/types/auth-contract.ts (locked)

## Dev 3 (Testing)
- **Assigned:** tests/e2e/**, tests/unit/**, .github/workflows/**
- **Forbidden:** src/** (read-only for test context)
- **Reads:** app.context.md (updated by exploratory process)

## Dev 4 (Integration)
- **Assigned:** tests/integration/**, src/integration/**, docker/**
- **Forbidden:** src/features/**, src/api/auth/**
- **Shares:** src/types/contracts/** (read-only)

## Shared Contracts (Locked Until Approved)
- src/types/auth-contract.ts → API request/response shape
- src/types/user-schema.ts → Database user model
(Any changes require Dev 1 review + all-team agreement)
```

**Dev 3's test automation task:**
```bash
# Create test generation prompt
cat > scripts/prompts/generate-e2e-tests.md << 'EOF'
Generate Playwright E2E test suite for feature: ${FEATURE}
Based on: app.context.md + src/types/contracts/**

Test flows:
1. User registration → login → verify email
2. User logout → login again
3. Update profile → verify changes
4. Delete account → verify cleanup

Constraints:
- Parallel: yes (no shared state)
- Timeout: 3 min total
- Screenshots: on failure
- Database: use test fixtures (seeded in setup)

Generate:
- tests/e2e/auth-flows.spec.ts
- tests/fixtures/auth-fixtures.ts
- README for test maintenance
EOF

# Trigger test generation when dev pushes
# (GitHub Actions workflow, see below)
```

**GitHub Actions workflow (auto-trigger test generation):**
```yaml
# .github/workflows/generate-tests.yml
name: Auto-Generate E2E Tests
on:
  pull_request:
    paths:
      - 'src/features/**'
      - 'src/api/**'

jobs:
  generate-tests:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Generate E2E tests with Claude Code
        run: |
          # Spawn test agent (Claude Code)
          claude code --prompt-file scripts/prompts/generate-e2e-tests.md
      - name: Commit tests
        run: |
          git config user.name "Test Agent"
          git config user.email "agent@company.com"
          git add tests/e2e/
          git commit -m "[auto] Generated E2E tests for ${{ github.head_ref }}"
          git push
```

### Week 3: Parallel Review + Execution

**Goal:** Unblock code review as bottleneck

**Setup AI code review (runs before human review):**
```yaml
# .github/workflows/ai-review.yml
name: AI Code Review
on: [pull_request]

jobs:
  review-security:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Security review agent
        run: |
          claude code --prompt-file scripts/prompts/security-review.md

  review-performance:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Performance review agent
        run: |
          claude code --prompt-file scripts/prompts/perf-review.md

  review-tests:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Test coverage agent
        run: |
          claude code --prompt-file scripts/prompts/coverage-review.md

# All 3 reviews run in parallel
# Results aggregated before human review
```

**Dev 1's review workflow (now faster):**
```
PR #42 opens
  ├─ AI review agents run in parallel (5 min)
  │  ├─ Security agent: "No secrets found ✓"
  │  ├─ Perf agent: "No N+1 queries ✓"
  │  └─ Test agent: "Coverage at 88% ✓"
  │
  ├─ Dev 1 spot-check (5 min)
  │  └─ Read AI summaries → "Looks good"
  │
  └─ Approve + Merge
     └─ E2E tests run in parallel (8 min)
     └─ All pass → Merged to main

Total time: 18 min (vs. 45 min without automation)
```

### Week 4: Measurement & Scaling

**Key metrics to track:**

```
┌─────────────────────────────────────┐
│ Velocity Metrics                    │
├─────────────────────────────────────┤
│ PRs merged/day: Target 6-8 (vs. 2)  │
│ Features completed/week: Target 12+ │
│ Bug fixes/week: Target 8-10         │
└─────────────────────────────────────┘

┌─────────────────────────────────────┐
│ Testing Metrics (Your Bottleneck)   │
├─────────────────────────────────────┤
│ E2E test pass rate: Target > 95%    │
│ E2E test runtime: Target < 10 min   │
│ Test generation time: < 30 min      │
│ Test maintenance overhead: < 5 h/wk │
│ Flaky tests: Target 0-1/day         │
└─────────────────────────────────────┘

┌─────────────────────────────────────┐
│ Review Metrics                      │
├─────────────────────────────────────┤
│ Time PR → Merged: Target < 30 min   │
│ Dev 1 review time/PR: Target 5 min  │
│ AI review effectiveness: Track      │
│  regressions caught by AI/human     │
└─────────────────────────────────────┘
```

**Monthly review checkpoint:**
```
If E2E test runtime > 15 min:
  → Parallelize more workers
  → Split tests into smaller suites
  → Run smoke tests before full suite

If test generation time > 45 min:
  → Improve app.context.md (clearer specs)
  → Add test patterns to prompt
  → Create reusable test fixtures

If PR review time > 20 min:
  → Add more AI review agents (security, perf, etc.)
  → Improve AI review prompts
  → Request lighter-weight reviews (style vs. logic)
```

---

## Part 5: Real Workflow Example (Your Team, Day 1)

### Morning (9am)

**Dev 1 triages issues:**
```markdown
## Issue: User Authentication (OAuth2)
Acceptance Criteria:
- Users can log in with Google/GitHub
- Session persists across page reloads
- Logout clears session

→ Assign to Dev 2 + Implementation Agent
→ Assign test writing to Dev 3 + Test Agent
→ Assign integration to Dev 4 + Integration Agent

Estimate: 1 day (parallel)
```

**Dev 2 spawns implementation worktree (9:05am):**
```bash
./scripts/spawn-agent.sh dev2 auth-oauth2 "OAuth2 implementation"
cd .worktrees/dev2-auth-oauth2

# Claude Code session starts
claude code --session auth-agent
# Prompt: "Implement OAuth2 login flow using passport.js..."
```

**Dev 3 spawns test worktree (9:10am, PARALLEL):**
```bash
./scripts/spawn-agent.sh dev3 tests-auth "OAuth2 E2E tests"
cd .worktrees/dev3-tests-auth

# Test generation starts (based on spec, not final code)
claude code --session test-agent
# Prompt: "Generate Playwright tests for OAuth2 flow..."

# Tests created:
# - tests/e2e/oauth-login.spec.ts
# - tests/e2e/oauth-logout.spec.ts
# - tests/fixtures/oauth-fixtures.ts
```

### Afternoon (2pm)

**Dev 2 pushes commits to ai/dev2/auth-oauth2:**
```bash
cd .worktrees/dev2-auth-oauth2
git add .
git commit -m "feat: OAuth2 login implementation"
git push origin ai/dev2/auth-oauth2
```

**GitHub Actions triggers automatically:**
```
Stage 1: Lint + Unit Tests (2 min)
  ✓ ESLint passes
  ✓ Unit tests pass (97% coverage)

Stage 2: AI Review (5 min, parallel)
  ✓ Security agent: No secrets leaked
  ✓ Perf agent: No unnecessary re-renders
  ✓ Coverage agent: 97% coverage sufficient

Stage 3: E2E Tests (10 min, parallel)
  ✓ Login test passes
  ✓ Logout test passes
  ✓ Session persistence test passes
  ✓ All 8 E2E tests pass in 9 min

Stage 4: Dev 3 Integration Tests (5 min, parallel)
  ✓ Integration tests all pass
  ✓ No conflicts with existing code
```

### Late afternoon (4:30pm)

**Dev 1 reviews PR #99:**
```
PR opened at 2:15pm
CI results ready at 2:35pm (5 min later)

Dev 1 review (5 min):
  - Read AI review summaries ✓
  - Glance at key files (20 lines) ✓
  - Approve ✓
  - Merge ✓

Main branch updated at 4:35pm
Dev 2 worktree cleaned up
```

**Dev 4 exports integration tests to main:**
```bash
cd .worktrees/dev4-integration
git add tests/integration/
git commit -m "chore: OAuth2 integration tests"
git push
# Goes through same CI flow
# Merges at 4:50pm
```

### Summary: 1 Day, 1 Feature, Done

```
Feature: OAuth2 login (complete end-to-end)
Implementation: Dev 2 + Agent (started 9:05am)
Tests: Dev 3 + Agent (started 9:10am, parallel)
Integration: Dev 4 + Agent (started 9:15am, parallel)
Review: Dev 1 (5-10 min)

Result:
  ✓ Feature merged at 4:50pm
  ✓ 3 agents working in parallel (no conflicts)
  ✓ Full E2E test coverage
  ✓ 0 bottlenecks (review was 5 min, testing was 10 min)
  ✓ Deployed to production same day

Traditional waterfall approach:
  Day 1: Dev 2 implements (6 hours)
  Day 2 morning: Dev 3 writes tests (4 hours)
  Day 2 afternoon: Dev 1 reviews (1 hour)
  Day 3: Deploy
  Total: 2.5 days

With worktrees + parallel agents: 1 day
```

---

## Part 6: Pitfalls & How to Avoid Them

### Pitfall 1: Flaky E2E Tests

**Problem:** E2E tests pass locally, fail in CI  
**Cause:** Race conditions, timing issues, environment differences

**Solution (from Playwright best practices):**
```typescript
// ❌ Bad (timing-based, flaky)
await page.goto('/');
await new Promise(r => setTimeout(r, 2000));  // Hope 2 sec is enough
await page.click('button');

// ✓ Good (wait for element, not time)
await page.goto('/');
await page.waitForSelector('button:text(\"Login\")');
await page.click('button');

// ✓ Best (Playwright built-in retry logic)
await page.locator('button:text(\"Login\")').click();
// Auto-retries if element not visible, auto-waits for actionable state
```

**Dev 3's checklist for E2E tests:**
- [ ] No `setTimeout()` (use Playwright waits)
- [ ] No hard-coded timeouts > 5 sec
- [ ] Run tests 5x locally → All pass?
- [ ] Use `.describe.serial()` only for dependent tests
- [ ] Log failures with screenshot + console output

### Pitfall 2: Test Maintenance Overhead

**Problem:** Selectors break after UI changes → Tests need fixing every sprint  
**Cause:** Tight coupling between tests and UI

**Solution (Page Object Model + data-testid):**
```typescript
// ❌ Brittle (tightly coupled to UI structure)
test('login', async ({ page }) => {
  await page.click('div > div > button:nth-child(2)');  // BREAKS with any UI change
});

// ✓ Better (uses semantic selectors)
test('login', async ({ page }) => {
  await page.click('button[aria-label="Log In"]');
});

// ✓ Best (Page Object Model + data-testid)
// pages/LoginPage.ts
class LoginPage {
  constructor(private page: Page) {}
  
  async login(email: string, password: string) {
    await this.page.fill('[data-testid="email-input"]', email);
    await this.page.fill('[data-testid="password-input"]', password);
    await this.page.click('[data-testid="login-button"]');
  }
}

// Developers add data-testid to UI (2 min)
// Tests never need touching (HUGE maintainability win)
```

**Ownership:**
- Dev 2 (implementer) adds `data-testid` to UI components
- Dev 3 (tester) uses those testids in Page Objects
- When UI changes, only testids need updating (not test logic)

### Pitfall 3: Merge Conflicts Despite Worktrees

**Problem:** Agents touch the same files (routes, config, package.json)  
**Cause:** Poor task decomposition

**Solution (Identify hotspots, serialize if needed):**
```markdown
# Hotspot files (collision risk, serialize)
- package.json (dependencies)
- src/routes.ts (routing table)
- src/config.ts (config)

# If multiple agents need to edit these:
1. Dev 1 locks the file
2. Agent A goes first, finishes, merges
3. Agent B rebases onto new main
4. Agent B goes, finishes, merges
# Result: No merge conflicts
```

**Rule:** If conflict rate > 10%, your decomposition is wrong (not your git workflow)

---

## Conclusion

**For your 4-person team:**

1. **Week 1:** Git worktrees + 2 agents in parallel
2. **Week 2:** File ownership + E2E test automation
3. **Week 3:** Parallel code review + CI/CD gates
4. **Week 4+:** Measure, optimize, scale

**Expected results:**
- Velocity: 2x (2 features/week → 4 features/week)
- Review time: 5 min per PR (vs. 20 min)
- E2E test time: 10 min per PR (fully automated)
- Testing bottleneck: Eliminated (tests run in parallel with implementation)

**Key success factor:** Testing must be automated and parallel, not human-bottlenecked.

---

## References

- **incident.io:** "How we're shipping faster with Claude Code and Git Worktrees"
- **Microsoft Global Hackathon 2025:** Tamir Dresher (worktree + role evolution pattern)
- **TestDino:** 4-agent test pipeline with file-based handoffs
- **Antigravity × Cursor × Claude Code:** Tool specialization for 5-day projects
- **CAID (Multi-agent Asynchronous Coordination):** Manager + engineers pattern
- **Testkube:** AI test automation bottlenecks
- **Groovyweb:** CI/CD pipelines for AI agent teams
- **Playwright best practices:** E2E testing reliability
