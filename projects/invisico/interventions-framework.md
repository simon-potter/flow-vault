---
title: "Invisico Interventions — Specification Framework"
type: reference
created: 2026-08-11
source: invisico-interventions skill
---

# Invisico Interventions: Specification Framework

## What We Built Today

A **framework for specifying structured decision frameworks (Interventions)** that Invisico will use to transform its council of counselors from 5 independent perspectives into a coherent, rigorously applied system.

**AVA/EVA (Expected Value Analysis)** is the reference implementation — showing how "Thinking in Bets" concepts can become a powerful Invisico intervention.

---

## Core Insight

**Interventions are the difference between:**

❌ **Bad:** "Here's what 5 counselors think about your decision"
- Generic advice
- Counselors riffing independently
- Disagreement is accidental, not structural
- User gets 5 perspectives but no framework to act on

✅ **Good:** "Here's how 5 distinct reasoning lenses apply to your specific decision"
- Structured framework applied systematically
- Counselors apply their archetype to the same problem
- Disagreement is built into the framework (it's the point)
- User gets scenario map, probability bands, hidden card inventory, exit ramp plan

---

## The Five-Component Anatomy

Every Invisico Intervention has:

### 1. **Problem Class Definition**
*What type of decision does this address?*
- Must be specific (not "all decisions")
- Must be distinct (different from other interventions)
- Example: "High-stakes irreversible decisions with asymmetric downside, incomplete information, sunk-cost risk"

### 2. **Framework Steps (3-5 phases)**
*What's the procedure the counselors execute?*
- Step 1: Map Scenarios
- Step 2: Surface Hidden Cards
- Step 3: Assign Probabilities
- Step 4: Calculate Expected Value
- Step 5: Script the Failure

Each step: What's the input? Who executes it (user, coordinator, counselor, synthesizer)? What's the output?

### 3. **Counselor Role Map**
*What does each counselor contribute at each step?*

For AVA/EVA:

| Step | Marcus | Munger | Drucker | Jobs | Buffett |
|------|--------|--------|---------|------|---------|
| Map Scenarios | Which test character? | What are the failure modes? | Which require new capabilities? | Which integrate cleanly? | Which matter in 10 years? |
| Surface Hidden Cards | What virtues are you assuming? | What base-rates apply? What exceptions are you betting on? | What operational assumptions are baked in? | What design gaps are you glossing over? | What sunk costs anchor you? |
| Assign Probabilities | 70% if principle held | 45% historical rate | 70% ops feasible, depends on phase 2 | 60% with design priority; 35% bolted-on | Reframing around 10-year regret |
| Calculate EV | If principle violated, no payoff is real | You're underweighting tail risk | Phase 2 failure correlates scenarios A & B | Design integration fails silently by month 6 | This is either a regret anchor or compounding win |
| Script Failure | Immediate exit if principle compromised | Exit at 90-day empirical check | Exit if phase 2 capacity gap by month 6 | Exit if timeline slip >40% | Exit if emotionally locked in by month 3 |

**This is what makes it powerful:** Each counselor has a *different* lens, so they see *different* things. The disagreement is the insight.

### 4. **Disagreement Surface Patterns (2-3 per intervention)**
*Where does the council typically disagree? What does that disagreement reveal?*

For AVA/EVA:

**Pattern A: Probability Divergence**
- Marcus: 70% if principle held
- Munger: 45% (historical base rate)
- Drucker: 70% operationally feasible, but depends on phase 2
- Jobs: 60% with design priority; 35% if bolted on
- Buffett: Not asking about 3-year odds; reframing around 10-year regret odds

**Pattern B: Hidden Assumptions**
- Marcus assumes the team will stay aligned on values
- Munger spots you're betting on a low-probability event X without explicit exit trigger
- Drucker flags the timeline assumes zero operational friction (30% slip is base-rate)
- Jobs sees design complexity is underestimated (integration takes 2x stated effort)
- Buffett warns you have a time-horizon mismatch (optimizing for 3-year exit, but this takes 7)

**Pattern C: Exit Triggers**
- Marcus: Immediate (principle violation)
- Munger: 90 days (empirical check of core assumption)
- Drucker: Month 6 (phase 2 capacity gap)
- Jobs: Timeline slip >40%
- Buffett: Month 3 (emotional attachment inflection point)

**Why this matters:** The user gets to see where they disagree, and that disagreement forces the user to decide: "Which of these signals would actually make me walk away? Which exits are hard vs. theoretical?"

### 5. **Output Specification**
*What does the user get out of a completed intervention?*

For AVA/EVA:
1. **Scenario map** — 4-5 plausible futures with payoffs + counselor annotations
2. **Hidden card inventory** — top 5 assumptions ranked by leverage
3. **Probability bands** — counselor-specific confidence levels, visualized for divergence
4. **EV calculation** — with correlation analysis + counselor critique
5. **Exit ramp plan** — per counselor (trigger + action) + reflection question: "Which of these disagreements would actually change your decision?"

Plus what Invisico captures for tuning:
- Decision class (how did the coordinator identify this as AVA?)
- Counselor confidence divergence (used to improve system prompts)
- User's scripting rigor (signals decision maturity; correlated with good outcomes)
- Follow-up patterns (users who loop to stress-test assumptions make better decisions)

---

## AVA/EVA: The Reference Implementation

**Problem Class:** High-stakes irreversible decisions with asymmetric downside, incomplete information, sunk-cost traps.

**Characteristics:**
- Career moves, M&A, capital investments, personal crossroads
- Multiple plausible futures (scenario-dependent)
- Hidden assumptions (what's assumed vs. what's known)
- Emotional attachment risk (sunk-cost trap, regret trap)
- Time-dependent failure modes (early-exit triggers vs. persist triggers)

**Framework:** Five-step procedure to confront assumptions, assign probabilities, and build exit ramps.

1. **Map Scenarios** (user input + coordinator orchestration)
   - "What are 4-5 plausible outcomes?"
   - "What's the payoff of each?" (not just money — time, reputation, health, relationships)
   - Counselors annotate each scenario through their lens

2. **Surface Hidden Cards** (user input → counselor analysis)
   - "What are you certain about? Assuming? Hoping is true?"
   - Each counselor identifies domain-specific hidden assumptions
   - Rank by leverage (which assumptions most change the decision?)

3. **Assign Probabilities** (counselor phase)
   - Marcus: "Success probability if principle is held? If compromised?"
   - Munger: "Historical failure rate for this *type* of decision?"
   - Drucker: "Operational feasibility by phase?"
   - Jobs: "Design integration difficulty impact?"
   - Buffett: "10-year compounding odds?"

4. **Calculate Expected Value** (algorithmic + synthesis)
   - EV = Σ(Payoff × Probability) for each scenario
   - But note: This is *not* a recommendation engine. It's a rigor check.
   - Synthesis brings counselors back together to react to each other's numbers

5. **Script the Failure** (counselor phase + synthesis)
   - Each counselor specifies: "How will I know this is going wrong? What's my exit trigger?"
   - Marcus: Principle violation (exit: immediate)
   - Munger: Base-rate empirical check (exit at 90 days)
   - Drucker: Phase 2 capacity gap (exit by month 6)
   - Jobs: Design integration slip (exit if >40% overrun)
   - Buffett: Emotional lock-in inflection (exit if committed by month 3)
   - Synthesis asks: "Which of these would actually make you walk away?"

---

## Quality Gates: Before You Ship an Intervention

Validate these before deploying a new intervention:

- **Problem clarity:** Specific, distinct, not "all decisions"
- **Framework rigor:** Procedural steps (not advisory), sequenced (later depends on earlier), reusable (applies to a class), complete (solves the stated problem)
- **Counselor role clarity:** Each has a distinct role (not overlapping), contributes meaningfully in every step, role outputs are different (not versions of same analysis)
- **Disagreement patterns:** At least 2-3 patterns, specific (not vague), emerge naturally (not forced), are valuable (reveal hidden tensions)
- **Output specification:** Outputs are concrete (user can act on them), distinct per counselor, answer the original problem, analytics are meaningful
- **System prompt implications:** Counselor system prompts can be updated to support, no new prompting techniques required, coordinator can identify when this intervention applies, synthesis engine can surface disagreements

---

## Anti-Patterns: Don't Do These

1. **Generic advice disguised as intervention** — Just asking counselors to riff on "what should I do?" without a framework. Bad.

2. **Synthesis that resolves disagreement** — Having counselors disagree then synthesis collapses it to a recommendation. This defeats the whole point.

3. **Too many steps (>5)** — Cognitive load gets too high, users abandon halfway through.

4. **Counselor roles that aren't distinct** — Each counselor doing the same analysis from different data sources. Not distinct lenses.

5. **Vague outputs** — "5 perspectives on your decision" doesn't tell the user what to do. Need concrete outputs: scenario maps, probability bands, exit triggers.

---

## Future Interventions (Sketched)

### Partnership Alignment Check
**Problem:** Multi-party decisions where hidden misalignment causes failure.
**Framework:** Map decision → Surface alignment gaps → Stress test divergences → Assign confidence in alignment → Script misalignment

### Resource Allocation Triage
**Problem:** Constrained resources + competing opportunities. "We can't do all three; which two?"
**Framework:** Map opportunities → Surface trade-offs → Hidden assumptions → Assign confidence in sequencing → Script regret

### Personal Values Alignment
**Problem:** Personal/professional life values in tension.
**Framework:** Map decision → Surface values → Identify conflicts → Assign confidence in alignment → Script regret

---

## Implementation Roadmap

### Phase 1: AVA/EVA (MVP) 
- Coordinator system prompt updated to identify AVA-class problems
- Persona system prompts updated with AVA counselor roles
- Synthesis engine updated to surface disagreement patterns
- Session instrumentation: capture probability bands, hidden cards, exit triggers

### Phase 2: Partnership Alignment Check
- Intervention spec validated with real use cases
- Coordinator learns to recognize alignment problems

### Phase 3: Resource Allocation Triage
- Framework tested with constrained-resource decisions

### Phase 4: Platform Abstraction
- Generic intervention registry (config-driven)
- Intervention selection logic
- Reusable disagreement patterns

---

## Skill Location

**Full specification & implementation details:** `~/.hermes/skills/invisico/invisico-interventions/SKILL.md`

**Use this skill when:**
- Speccing a new Invisico intervention
- Updating AVA/EVA system prompts
- Validating an intervention before shipping
- Designing the intervention selection logic (how coordinator identifies which intervention to run)

