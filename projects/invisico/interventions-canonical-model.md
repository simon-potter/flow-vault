---
title: "Invisico Interventions — Canonical Model Reference"
type: reference
created: 2026-08-11
updated: 2026-08-11
source: invisico-repo/docs/intervention-framework/
---

# Invisico Interventions — Canonical Model Reference

## Authoritative Sources

**Use these as canonical whenever speccing new interventions:**

1. `docs/intervention-framework/intervention-model.md` — Conceptual architecture
2. `docs/intervention-framework/capability-ux-model.md` — Implementation pattern  
3. `.claude/skills/intervention-designer/SKILL.md` (when created)
4. `docs/runbooks/design-intervention-from-source.md` (when created)

---

## The Core Model

### What an Intervention IS

A **structured process** that examines a specific problem through a curated selection of **lenses**, synthesizes the resulting **observations** into **insights**, and surfaces **recommendations** the user can act on or carry forward.

**Key properties:**
- **Bounded** — clear entry (trigger or user-invoked) and exit (report saved)
- **Session-local** — inputs scoped to current session; no cross-session state read/write
- **User-confirmed** — nothing computes until user explicitly submits
- **Non-prescriptive** — surfaces costs/risks/signals; doesn't tell user what to decide
- **Lens-composed** — built from reusable, named perspectives

### What a Lens IS

A **structured perspective** that deliberately highlights one aspect of a decision while temporarily ignoring all others.

**Key properties:**
- Asks exactly one kind of question
- Never mixes question types
- Produces exactly one **Observation** per application
- **Reusable** across many interventions
- May be voiced by a counselor (when it maps to their domain)

### The Five Lens Families

#### 1. Resource Lenses
How resources are allocated across the decision's real costs.

| Lens | Question | Output |
|------|----------|--------|
| Time | Committed hours, actual vs contracted | Numeric (hours) |
| Money | Financial cost, opportunity, return | Numeric or directional |
| Attention | Cognitive occupancy, mental presence | Numeric (0–100 units) |
| Energy | Draining vs energizing | Directional |
| Relationships | Impact on key relationships | Qualitative signal |

#### 2. Strategic Lenses
Long-term and systemic thinking about second/third-order effects.

| Lens | Question | Output |
|------|----------|--------|
| Opportunity Cost | What is foreclosed by choosing this? | Named alternatives + cost |
| Compounding | Does this compound over time? | Directional with horizon |
| Optionality | Does this open or close future options? | Opens/closes + named |
| Leverage | Does this multiply output disproportionately? | Directional |
| Second-order consequences | What follows from what follows? | Named sequence |

#### 3. Psychological Lenses
Internal state, self-knowledge, hidden drivers.

| Lens | Question | Output |
|------|----------|--------|
| Fear | What specific fear is driving/blocking this? | Named fear + strength |
| Attachment | Is attachment to past distorting this? | Directional |
| Identity | Does this align with who you're becoming? | Alignment (Low/Med/High) |
| Values | Does this honor your stated values? | Named values + alignment |
| Motivation | Intrinsic or extrinsic? | Directional |
| Emotional load | Emotional weight of carrying open? | Directional signal |

#### 4. Reality Lenses
Testing assumptions, models, picture of the situation.

| Lens | Question | Output |
|------|----------|--------|
| Counterfactual (Relief Test) | If this disappeared, first feeling? | Named feeling |
| Evidence | Actual evidence for key assumption? | Confidence level |
| Devil's Advocate | Strongest case against this? | Named counter-argument |
| Five Whys | Root motivation behind surface decision? | Named root cause |
| Steelman | Most charitable version of opposing view? | Named steelman |
| Falsification | What would make this the wrong choice? | Named falsifier |

#### 5. Temporal Lenses
Different time horizons, each reveals different aspect.

| Lens | Question | Output |
|------|----------|--------|
| Tomorrow | How does this feel the morning after? | Directional signal |
| One year | Where does this leave you in 12 months? | Named state |
| Five years | What trajectory does this set? | Named trajectory |
| Lifetime | Would your best self endorse this? | Yes/no/uncertain |
| Deathbed | Regret saying no more than saying yes? | Directional |
| Legacy | What does this teach people watching? | Named quality |

---

## Existing Interventions as Lens Compositions

### Cost of Yes (Reference Implementation)

**Core question:** What is the full price of this decision, beyond contractual terms?

**Lens composition (8 lenses):**
1. Time (Resource)
2. Attention (Resource) — initial
3. Opportunity Cost (Strategic)
4. Attention (Resource) — deeper
5. Momentum (Strategic)
6. Identity alignment (Psychological)
7. Counterfactual/Relief Test (Reality)
8. Future Projection 1 year (Temporal)

**Synthesis contract:** 8 observations combine into cost profile. Dominant observation (highest value, flagged dimension) drives forcing question: "Knowing the full price — [dominant observation] — would you still choose it?"

**Report format:** 8-dimension profile with compact 5-row card for session timeline (top 5 by signal strength).

### Fear (Planned)

**Core question:** What is this fear actually protecting, and is that protection still needed?

**Lens composition (5 lenses):**
1. Fear (Psychological) — named
2. Identity (Psychological)
3. Future Projection 5 years (Temporal)
4. Counterfactual (Reality)
5. Attachment (Psychological)

**Synthesis contract:** Named fear is traced to protective function. Identity lens reveals whether fear guards something real about user's direction. Temporal lens shows whether feared outcome is actually likely. Counterfactual checks whether fear is load-bearing or noise.

---

## Implementation Pattern: elicit → confirm → compute → render → save

```
open capability 
    ↓ POST elicit (LLM #1, context-aware proposal)
form pre-fills 
    ↓ user confirms/edits
    ↓ submit
compute (LLM #2, interpretive output)
    ↓
result rendered by registered view
    ↓ "Save to session"
saved → chronological flow + summary link
```

### Load-Bearing Rules

- **Idempotency declared per capability.** Pure deterministic = idempotent. Interpretive = `idempotent=False`; every invocation recomputes.
- **Untrusted-data serialization.** Session context AND user inputs serialized as delimited strings; prompt instructs model never to follow instructions inside them.
- **Output schema steers model.** Every output field must have a description; schema is the contract, not prose.
- **Runner transaction lifecycle.** Active run committed BEFORE compute runs; no DB transaction held across provider call.
- **Accounting.** Elicit + interpretive computes route through `LlmClient.parse` with call_type, acquire shared LLM semaphore.

### Checklist for New/Upgraded Capability

- [ ] Pure or interpretive? Declare `idempotent` accordingly.
- [ ] Input/output schemas declare `additionalProperties: false` + length bounds.
- [ ] Prompts serialize context/inputs as delimited untrusted data.
- [ ] Proposal rule honored: keys ⊆ properties, values type-checked, abstention legal.
- [ ] Result view registered for (capability_id, schema_version), or deliberate fallback.
- [ ] Live probe matrix entry in `model-metrics.md`.
- [ ] Real-pipeline smoke + operator sign-off recorded in MR.

---

## Key Principles

1. **Every intervention should draw from at least 2 lens families.** Single-family feels narrow.

2. **Observations are the raw material.** Never shown alone without synthesis. Format: `[Lens name]: [value]`

3. **Insights reveal meaning from observations.** They answer "what does this mean?" not "what is this?"

4. **Recommendations are directional.** Two types: action-requiring (→ concrete action) and reflection-only (awareness to carry).

5. **Actions are stored durable.** Via shared durable-output spine. Never auto-generated; user confirms each.

6. **A small library of high-quality lenses composes into many interventions.** 20 lenses → hundreds of interventions.

---

## When Speccing a New Intervention or Lens

**Before writing code:**

1. Identify the **core question** it addresses
2. Select **2-5 lenses** from the 5 families (at least 2 families)
3. Define the **synthesis contract** (how observations combine into insight)
4. Specify the **output format** (what gets saved to session)
5. Design the **elicit proposal** (what pre-fills the form)
6. Map to a **registered result view** (or document fallback)

**Reference:** Cost of Yes and Fear (planned) are your models.

