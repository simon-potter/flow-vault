---
title: "Invisico Interventions — Follow-On Structured Frameworks"
type: reference
created: 2026-08-11
updated: 2026-08-11
source: invisico-interventions skill (corrected)
---

# Invisico Interventions: Follow-On Structured Frameworks

## What We Built

A **framework for specifying follow-on structured decision frameworks** that users can apply *after* hearing initial counselor perspectives. These are optional, user-initiated deepens that provide systematic rigor around specific decision dimensions.

---

## Core Insight: The Flow

**Before:**
1. User presents problem
2. Counselors respond (unconstrained, natural perspectives)
3. Synthesis surfaces agreements/disagreements/reflection question
4. **Session ends**

**Now:**
1. User presents problem
2. Counselors respond (unconstrained, natural perspectives)
3. Synthesis surfaces agreements/disagreements/reflection question
4. **System suggests relevant intervention:** "I notice [pattern]. Want to apply [Intervention] to stress-test this further?"
5. User optionally engages with follow-on structured framework
6. **Session deepens** with rigor + systematic analysis

---

## Interventions Are NOT

- ❌ The initial counselor framework (those responses are unconstrained)
- ❌ Mandatory (user chooses to engage)
- ❌ Coordinator-level logic (they happen post-synthesis)
- ❌ Repeating counselor work (they reference and build on what was said)

---

## Interventions ARE

- ✅ Optional follow-on tools
- ✅ Suggested based on patterns in what counselors actually said
- ✅ User-initiated deepening
- ✅ Building on counselor responses (not contradicting or replacing them)
- ✅ Systematic rigor applied to specific decision dimensions

---

## Five-Component Anatomy

### 1. Trigger Pattern
What pattern in counselor responses suggests this intervention?

**Example (AVA/EVA):** Counselors diverge on confidence levels, identify asymmetric downside, flag hidden assumptions, surface time-dependent risk.

**System recognizes:** "You got conflicting advice on likelihood and different views on what could go wrong."

### 2. Problem Class Definition
What decision situation is this intervention designed for?

**Example (AVA/EVA):** High-stakes irreversible decisions with asymmetric downside, incomplete information, sunk-cost traps.

### 3. Framework Steps (3-5 phases)
What does the user work through, *given the counselor responses already in session*?

**Example (AVA/EVA) — 5 Steps:**
1. **Refine Scenarios** — User fleshes out the futures counselors mentioned
2. **Surface Hidden Cards** — System extracts assumptions counselors flagged; user ranks by leverage
3. **Assign Probabilities** — User reflects on counselor probability estimates; assigns their own
4. **Calculate Expected Value** — Algorithmic calculation; user notes on resilience
5. **Script the Failure** — User commits to exit triggers counselors identified

### 4. Counselor Integration
How does each counselor's contribution from the session inform this intervention?

**Example (AVA/EVA):**
- Marcus: Which outcomes test character? → informs Step 5 (principle-violation exit trigger)
- Munger: What exceptions are you betting on? → informs Step 2 (hidden assumptions), Step 3 (base-rate probability)
- Drucker: Operational feasibility by phase? → informs Step 4 (correlation analysis), Step 5 (month 6 ops gate)
- Jobs: Design/integration gaps? → informs Step 2 (hidden complexity), Step 5 (40% slip trigger)
- Buffett: 10-year implications? → informs Step 3 (long-term probability), Step 5 (month 3 emotional inflection)

**Key:** Intervention references what they said. Doesn't ask for new 5 perspectives.

### 5. Output Specification
What does the user produce?

**Example (AVA/EVA):**
- Refined scenario map (4-5 futures + user payoff estimates)
- Hidden card ranking (top 3-5 assumptions by leverage)
- Personal confidence bands (where user sits vs. counselor estimates)
- EV summary (highest EV scenario + most resilient)
- Exit ramp commitment (which triggers user will actually act on)
- Reflection (how did analysis change thinking?)

---

## AVA/EVA Reference Implementation

### Trigger Pattern
Counselors diverge on confidence levels, identify asymmetric downside, flag hidden assumptions, surface time-dependent risk.

**System suggests:** "Want to apply Expected Value Analysis to stress-test these scenarios and commit to exit triggers?"

### Framework: Five Steps (Follow-On)

**Step 1: Refine Scenarios**
- Reference from session: "The counselors mentioned these futures: [extract]"
- User fleshes out payoffs (not just money — time, reputation, health, relationships)
- Counselors' observations annotate each scenario

**Step 2: Surface Hidden Cards**
- Reference from session: "The counselors flagged these assumptions: [extract]"
- Create two-column table: Known facts vs. Hidden cards/bets/hopes
- Rank by leverage: which assumptions most change the decision?

**Step 3: Assign Probabilities**
- Reference from session: "Here's what each counselor estimated: [probability ranges]"
- User assigns their own confidence
- Marcus, Munger, Drucker, Jobs, Buffett ranges shown; user reflects on where they sit

**Step 4: Calculate Expected Value**
- EV = Σ(Payoff × Probability) for each scenario
- User notes: Which is most resilient if assumptions are wrong?
- Reference counselor reactions to each other's numbers

**Step 5: Script the Failure**
- Reference from session: "The counselors identified different exit triggers: [list]"
- Marcus: Immediate (principle violation)
- Munger: 90 days (empirical check)
- Drucker: Month 6 (ops gate)
- Jobs: 40% timeline slip
- Buffett: Month 3 (emotional inflection)
- **User commits:** Which will I actually honor?

---

## Quality Gates Before Shipping

- [ ] Trigger pattern is specific (not "any uncertainty")
- [ ] Framework references session (doesn't duplicate counselor work)
- [ ] Each step clearly shows which counselor input informs it
- [ ] Output is concrete + actionable (not just "reflection")
- [ ] Can be completed in 10-15 minutes
- [ ] At least 2-3 disagreement patterns naturally emerge

---

## Three Future Interventions (Sketched)

### Partnership Alignment Check
**Trigger:** Counselors flag value misalignment, conflicting goals, stakeholder tension

**Steps:** Surface goals → Identify value divergences → Stress-test which are fatal → Rank alignment → Commit to checkpoints

**Output:** User's alignment ranking + proceed/no-proceed decision

### Resource Allocation Triage
**Trigger:** Counselors identify constrained resources + competing high-impact opportunities

**Steps:** Map opportunities → Surface trade-offs → Hidden assumptions → Assign sequencing confidence → Commit to priority

**Output:** User's phased roadmap + defer/abandon decision

### Personal Values Alignment
**Trigger:** Counselors surface tension between stated values and proposed choice

**Steps:** List values → Map to choice → Identify trade-offs → Assign value hierarchy → Commit to trade-off

**Output:** User's clarified values hierarchy + conscious trade-off commitment

---

## Implementation Checklist

**System:**
- [ ] Synthesis engine recognizes trigger patterns
- [ ] At synthesis end: "Based on this, you might find [Intervention] helpful. Want to try it?"
- [ ] User can accept/decline (not mandatory)
- [ ] Intervention pulls session data and references it at each step
- [ ] System captures what user produces + changed confidence

**Per Intervention:**
- [ ] Trigger pattern specific and unambiguous
- [ ] All steps reference counselor responses (build on, don't repeat)
- [ ] Counselor integration map shows which input informs which step
- [ ] Output concrete and actionable
- [ ] 10-15 minute completion time
- [ ] Passes quality gates

---

## Skill Location

**Full spec + templates:** `~/.hermes/skills/invisico/invisico-interventions/SKILL.md`

