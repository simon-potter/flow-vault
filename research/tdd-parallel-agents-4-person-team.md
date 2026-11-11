---
type: concept
title: 'TDD + Parallel Agents: Red-Green-Refactor at Scale with 4 Developers'
date: '2026-11-11'
source_kind: mcp:put_page
ingested_via: mcp:put_page
ingested_at: '2026-11-11T09:00:28.034Z'
trust_tier: agent_written
tags:
  - 4-person-team
  - git-worktrees
  - parallel-agents
  - test-driven-development
---

## Core Insight: TDD Unlocks Parallelization

**Traditional single-dev TDD (serial):**
```
Dev writes test (Red) → Dev writes code (Green) → Dev refactors (Refactor) → Loop
              5 min                 10 min              5 min
```

**Multi-agent TDD (parallel worktrees):**
```
Agent 1 writes test (Red)           →    Agent 2 writes code (Green)     →     Agent 3 refactors (Refactor)
       5 min (isolated worktree)          10 min (isolated worktree)            5 min (isolated worktree)
              ↓                                   ↓                                    ↓
      Commits test to branch         Commits code to branch             Commits refactoring
               (LOCKED - cannot be modified)
```

**Key difference:** Tests are committed BEFORE code is written. This locks in the contract.
- Dev 2 cannot "fix" the test to make code pass faster
- Dev 3 has a passing test suite to refactor against
- Each agent works in isolation (no merge conflicts)

---

## The TDD + Parallel Workflow for Your 4-Person Team

### Phase 1: Spec Design (30 min, all devs + product)
**Who:** Dev 1 (Tech Lead)
**Deliverable:** OpenAPI spec + acceptance criteria + data model

**Example spec:**
```yaml
# Feature: Payment Processing

API Contract (OpenAPI):
  POST /api/payments
    Request: { amount, cardToken, customerId, transactionId }
    Response: { status, transactionId, timestamp }
    Errors: InvalidCard, InsufficientFunds, Timeout

Database Schema:
  Payments: id, customerId, amount, status, createdAt, transactionId
  Unique: (customerId, transactionId)

Acceptance Criteria:
  1. Valid payment → status: SUCCESSFUL
  2. Invalid card → 400 InvalidCard
  3. Insufficient funds → 400 InsufficientFunds  
  4. Idempotent on retry (same transactionId)
```

**Why:** No ambiguity. All parallel agents see the same contract. DB schema locked. API locked.

---

### Phase 2: Test-First (RED) — Dev 3 Starts Immediately
**Who:** Dev 3 (Test Specialist)
**Worktree:** `feature/payment-tests`
**Duration:** 10-15 min
**Deliverable:** Test suite with all cases FAILING

Tests confirm they fail, then committed (LOCKED):
```bash
git worktree add ../payments-tests
cd ../payments-tests
pytest tests/api/test_payments.py
# FAILED: all 5 tests (no implementation yet)
git add tests/api/test_payments.py
git commit -m "[RED] Payment API tests — all failing as expected"
```

Key: Tests are now LOCKED. Dev 2 cannot modify them.

---

### Phase 3: Implementation (GREEN) — Dev 2 in Parallel
**Who:** Dev 2 (Implementation Specialist)
**Worktree:** `feature/payment-impl`
**Constraint:** Make tests pass, do NOT modify tests
**Duration:** 20-25 min
**Deliverable:** Code that makes all tests pass

```bash
git worktree add ../payments-impl
cd ../payments-impl
# Pull the locked tests from Dev 3
git fetch origin feature/payment-tests
git merge origin/feature/payment-tests -- tests/

# Implement code
# ... write src/payments/api.py ...

pytest tests/api/test_payments.py
# PASSED: all 5 tests ✓

git add src/payments/
git commit -m "[GREEN] Payment API — all tests passing"
```

**Constraint enforced:** Prompt says "Tests are LOCKED. Do not modify. Only write code in src/."

---

### Phase 4: Refactoring (REFACTOR) — Dev 4 in Parallel
**Who:** Dev 4 (Code Quality Specialist)
**Worktree:** `feature/payment-refactor`
**Constraint:** All tests must still pass
**Duration:** 10 min
**Focus:** Remove duplication, improve naming, add logging, optimize queries

```bash
git worktree add ../payments-refactor
cd ../payments-refactor
# Pull code + tests
git fetch origin feature/payment-impl
git merge origin/feature/payment-impl

# Refactor (improve code quality)
# ... optimize, add docstrings, better error handling ...

pytest tests/api/test_payments.py
# PASSED: all 5 tests ✓

git add src/payments/
git commit -m "[REFACTOR] Payment API: improve clarity, logging, error handling"
```

---

## Timeline: How Parallel Execution Kills the Testing Bottleneck

```
09:00 — Kickoff (all devs)
        Dev 1: Write spec (30 min)
        Devs 2-4: Prep worktrees

09:30 — SPEC LOCKED
        Dev 3: Write & lock tests (15 min) ────┐
        Dev 2: Waits                           │
                                               ▼
09:45 — TESTS LOCKED                  Tests published
        Dev 2: Implement code (25 min) ────────┐
        Dev 3: Done, reviews code             │
        Dev 4: Preps refactor                 │
                                               ▼
10:10 — CODE PASSING                   All tests passing
        Dev 4: Refactor (10 min) ──────────────┐
        Dev 2: Done, reviews refactor         │
        Dev 1: Final review                   │
                                               ▼
10:20 — REFACTOR COMPLETE              All gates pass
        All devs: Merge & celebrate
```

**The magic:** Dev 3's 15 min test writing happens while Dev 2 is WAITING. Then Dev 2's 25 min coding happens while Dev 4 is waiting. Then Dev 4's refactoring happens. Result:
- Sequential: Spec (30) + Tests (15) + Code (25) + Refactor (10) = 80 min
- **Parallel: Spec (30) + [Tests (15) + Code (25) parallel] + Refactor (10) = 50 min**
- **With 4 devs working, you ship 4 features in 50 min = 12.5 min per feature**

**Testing is NOT the bottleneck anymore.** It runs DURING implementation, not after.

---

## The 7 Parallel Workstreams (Beyond Dev 1-4 TDD)

While Devs 1-4 do TDD, these run in parallel (automated or separate agents):

### 1. **API Documentation Generation**
- Trigger: Spec updated
- Tool: Swagger/OpenAPI generator
- Output: Interactive API docs
```bash
openapi-generator-cli generate -i spec.yaml -o ./docs/api
```

### 2. **Database Schema Migration**
- Trigger: Data model defined in spec
- Tool: Flyway, Liquibase
- Output: Migration scripts ready to run
```bash
migration-generator create-migration --from schema_old.sql --to schema_new.sql
```

### 3. **Security Analysis (SAST)**
- Trigger: Code pushed
- Tool: Snyk, SonarQube, Semgrep
- Output: Security report
```bash
snyk test  # Vulnerable dependencies
semgrep -c p/security-audit  # Code vulns
```

### 4. **Performance Testing (Load/Stress)**
- Trigger: Code passes unit tests
- Tool: k6, Apache JMeter, pgBadger
- Output: Performance metrics
```bash
k6 run load-test.js  # How many requests/sec?
pg_stat_statements analyze  # Slow queries?
```

### 5. **Contract Testing**
- Trigger: API code available
- Tool: Pact, Specmatic
- Output: API contract validation
```bash
pact verify --provider-base-url http://localhost:3000
specmatic test --contract-file payments-api.yaml
```

### 6. **End-to-End Testing (UI)**
- Trigger: Full feature implemented
- Tool: Playwright, Cypress
- Output: Browser test results
```bash
playwright test --workers=4 tests/e2e/payment-flow.spec.ts
```

### 7. **Code Quality Gates**
- Trigger: Code pushed
- Tool: ESLint, Coverage.py, SonarQube
- Output: Lint, format, test coverage report
```bash
npm run lint && npm run format
coverage report --fail-under=80
```

---

## Full Parallel Architecture

```
Phase 1: SPEC DESIGN (Dev 1)
         ↓
Phase 2: RED (Dev 3)           Phase 2: API Docs (Automated)       Phase 2: DB Migration (Automated)
         ├─ Write tests         ├─ Generate from spec              ├─ Generate from schema
         ├─ Confirm failing     └─ Output: swagger.yaml            └─ Output: migration.sql
         └─ Commit (LOCKED)

Phase 3: GREEN (Dev 2)         Phase 3: Security Scan (Snyk)       Phase 3: Perf Test (k6)
         ├─ Pull locked tests   ├─ SAST on code                    ├─ Load test the API
         ├─ Implement code      └─ Output: security report         └─ Output: performance metrics
         ├─ Make tests pass
         └─ Commit

Phase 4: REFACTOR (Dev 4)      Phase 4: Contract Tests             Phase 4: E2E Tests (Playwright)
         ├─ Pull code + tests   ├─ Verify API spec compliance      ├─ Full workflow testing
         ├─ Improve clarity     └─ Output: contract report         └─ Output: test results
         ├─ All tests pass
         └─ Commit

Final: CODE REVIEW + MERGE (Dev 1)
       ├─ Review all branches
       ├─ All gates passing? (security, perf, contracts, E2E)
       └─ Merge to main ✓
```

---

## Your 4-Person Team: Who Does What

| Role | TDD Phase | Parallel Streams | Merge Gate |
|------|-----------|------------------|------------|
| **Dev 1 (Tech Lead)** | Spec design | Code review coordination | Final approval |
| **Dev 2 (Implementer)** | Implementation (GREEN) | Help with E2E tests | Ship |
| **Dev 3 (Test Lead)** | Tests (RED) | Contract tests, Security scans | Verify test coverage |
| **Dev 4 (QA/Perf)** | Refactoring | E2E tests, Load testing, Coverage | Performance sign-off |

---

## Why Testing Stops Being a Bottleneck

**Before (single dev, serial):**
```
Dev codes 25 min → Finds bug → Codes fix 10 min → Manually tests 30 min → TOTAL: 65 min
Bottleneck: Testing is 46% of total time
```

**After (4 devs, parallel TDD):**
```
Dev 3 writes tests (15 min) ────┐
Dev 2 writes code (25 min) ──────┼─ All parallel
Dev 4 writes E2E tests (20 min) ─┤
Dev 1 reviews (5 min) ───────────┘

Total time: 25 min (longest single path)
Bottleneck: SPEC DESIGN (because it's the first dependency)
```

**But here's the real magic:** 4 devs working in parallel means:
- Feature 1: Payment processing (50 min total)
- Feature 2: User auth (50 min total) — starts AFTER Feature 1's spec
- Feature 3: Notifications (50 min total) — starts AFTER Feature 2's spec
- Feature 4: Dashboard (50 min total) — starts AFTER Feature 3's spec

**Week throughput:** 4 features in 200 min = 1 feature every 50 min
**Without parallel:** 1 feature every 80 min (spec + test + code + refactor serial)

**Result: 60% faster output from same 4 people**

---

## Implementation: Week 1 Checklist

- [ ] **Pick one feature** (small, well-defined)
- [ ] **Dev 1:** Write spec + OpenAPI (30 min)
- [ ] **Dev 3:** Write tests, confirm failing, commit (15 min)
- [ ] **Dev 2:** Implement code, make tests pass (25 min)
- [ ] **Dev 4:** Refactor, all tests pass (10 min)
- [ ] **All:** Run full test suite + E2E (10 min)
- [ ] **Dev 1:** Merge to main (2 min)
- [ ] **Retrospective:** What took longer than expected? Why?

**Measure:** Total time end-to-end. Compare to your current single-dev flow.

---

## FAQ

**Q: What if a test is wrong?**
A: Dev 3 caught it during RED phase (before code was written). Push a new commit to the test branch. Dev 2 re-pulls and implements against the corrected test. Git worktree makes this seamless.

**Q: What if code + refactor conflict?**
A: They're on separate worktrees, so no conflict. Dev 2's branch stays untouched. Dev 4 pulls Dev 2's code + applies refactoring on top.

**Q: Can testing + refactoring run in true parallel?**
A: No, Dev 4 needs Dev 2's passing code first. But Dev 4 can prep the refactoring checklist while Dev 2 codes.

**Q: How many parallel agents can git handle?**
A: 5-10 worktrees without issue. Each needs ~500MB disk space. With 4 devs, you'll have 4-8 worktrees active.

**Q: Does this scale to 10 developers?**
A: Yes, but you'll hit other bottlenecks:
- Spec design (requires consensus, can't parallelize)
- Code review (1 reviewer can't review 10 changes at once)
- CI/CD runners (if you only have 2 parallel runners)

Mitigation: Stagger feature starts. Feature 1 (Devs 1-4) → Feature 2 (Devs 5-8) → Feature 3 (Devs 9-10).
