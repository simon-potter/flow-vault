---
type: media
title: How To Build Self-Improving AI Agents with Claude (Stanford's Method)
media_type: video
date: '2026-11-21'
video_id: UUg5oij7ptw
channel: Austin Marchese
duration: '16:44'
source_kind: mcp:put_page
ingested_via: mcp:put_page
ingested_at: '2026-11-23T06:56:40.362Z'
trust_tier: agent_written
tags:
  - agentic-development
  - prompts-included
  - self-improving-systems
  - step-by-step
---

## Video Overview

**Speaker:** Austin Marchese  
**Source:** Stanford AI Course (10+ hours condensed)  
**Topic:** Building self-improving AI agents without fine-tuning  
**Key Innovation:** Four-step system (Generator → Verifier → Coach → Level Selection)  
**Use Case:** Create a self-improving clone of yourself to handle your team's questions

---

## Core Concept: Why AI Agents Self-Improve

**Stanford's Definition:**
> "An AI agent has a goal and will interact with the environment, collect feedback, and use that feedback to correct its steps."

**Plain English:** AI agents use a model, tools, and context to accomplish a goal — not just answer questions.

**Two Ways to Self-Improve:**
1. Retrain the model (fine-tuning) — requires ML expertise
2. **Update what the model reads** (what this video covers) — simpler, business-owner friendly

**Three Ways to Update Context:**
- Improve the tools the agent has
- Improve the context it reads
- Improve the skills it uses

---

## STEP 1: BUILD THE GENERATOR (00:00 - 05:30)

**Purpose:** Create the core agent that does the actual work

**Key Principle:** The more specific and well-defined the job description, the better.

**Example:** Create "Austin GPT" — an AI agent that answers questions exactly how you would.

**Why This Pattern Works:**
- Self-improving systems need verifiable outputs
- Math is easy for AI because answers are verifiable (right/wrong)
- Engineering is easy because you can verify if the output works
- You can verify if an answer matches how YOU would answer (source of truth)

### PROMPT 1: Create Your Personal Agent Generator

```
[PROMPT - Interview yourself to create agent file]

Ask the user (Claude will interview you):
1. What is your job title and primary responsibilities?
2. What are the top 5-10 questions your team asks you most?
3. How do you typically answer these questions?
4. What's your decision-making framework?
5. What constraints or rules do you follow?
6. What tone and style do you use?

Based on responses, Claude generates:
- Agent system prompt
- Instructions for the generator
- Initial context/knowledge
- Tool definitions

Output: agent_generator.txt (the actual agent file)
```

**Action:** Answer questions, receive your personal agent template.

---

## STEP 2: BUILD THE VERIFIER (05:30 - 10:30)

**Problem Solved:** "An agent that creates work can't necessarily tell if the work is good."

**Why Agents Can't Self-Verify:**
- **Self-grading fails:** Agent is biased toward its own output
- **Overconfidence:** One study: agent ran 54 improvement cycles, claimed 54/54 improvements. Reality: 56% of changes were flat or worse.
- **Michael Scott Problem:** Like buying yourself a "World's Best Boss" mug

**Stanford's Quote:**
> "Getting the model to critique itself is harder. Having a consensus of other models critique the model works better because models might be overconfident."

**Solution:** Build a separate read-only agent to verify.

### PART 2A: Create the Answer Key (Evaluation Dataset)

**What it is:** A table mapping inputs → outputs you would provide

**Example:**
```
| Input | Correct Output |
|-------|----------------|
| "Where can I find the checkout link for a customer?" | "Check our build.partner.ai admin portal" |
| "How do I reset my password?" | "Go to Settings → Account → Reset Password" |
| "What's our team's value proposition?" | "We help companies automate customer workflows..." |
```

### PROMPT 2: Extract Your Answer Key from Slack

```
[PROMPT - Extract Q&A from Slack for evaluation dataset]

Connect to Slack API:
1. Find the 20 most common questions your team asked you (search your DMs/channels)
2. Extract the exact answer you gave
3. Format as: Question | Your Exact Answer
4. Create answer_key.md

Output: answer_key.md (20 Q&A pairs, manually reviewed for accuracy)
```

**Critical Note:** This answer key is a **living document**. Every time the agent gets something wrong, it's not a failure — it's a new row to add to the evaluation dataset.

### PART 2B: Build the Verifier Agent

**Job:** Answer the question: "Is this correct or wrong?"

**Rules:**
- Read-only (never edits anything)
- Explains WHY something is wrong
- Doesn't edit answer key, generator, or anything else

### PROMPT 3: Create the Verifier

```
[PROMPT - Build the verifier agent]

You are a strict grading agent. Your job:
1. Read the generator's answer
2. Compare to answer_key.md
3. Score: Correct / Partially Correct / Incorrect
4. Explain WHY (reasoning matters for fixing it)
5. Never edit anything

Example feedback:
- "Incorrect: User asked about checkout link. You mentioned password reset." 
- "Partially correct: Right feature, but outdated URL path."
- "Correct: This matches answer_key row #7 exactly."

Output: Verification report with score + reasoning
```

---

## STEP 3: ADD THE COACH (10:30 - 12:45)

**Problem:** Can the verifier just fix the generator?

**Answer:** No, for two key reasons:
1. **Circular logic:** If verifier grades + fixes, grading becomes meaningless (like grading your own homework)
2. **Gaming the test:** Agent learns to pass the test, not do the job

**Solution:** Third agent = Coach

### How the Coach Works

1. **Reads** what the verifier found
2. **Writes** a candidate version of the agent (next to the original, never replacing it)
3. **Makes ONE change** (isolate variables)
4. **Tests** candidate vs. original
5. **Never touches:** Answer key, verifier, or original generator

### PROMPT 4: Create the Coach Agent

```
[PROMPT - Build the coach agent]

You are a coaching agent. Your job:
1. Read the verifier's feedback
2. Create a NEW candidate version of the agent (candidate_v1.txt)
3. Make ONE change to address the issue
4. Keep original generator.txt unchanged
5. Document what you changed in CHANGELOG.txt

Rules:
- ONE CHANGE PER DRAFT (must isolate variables)
- Never edit answer_key.md or verifier.txt
- Never touch original generator.txt
- Keep versions/ folder with history
- Example change: "Added API documentation to context"
- Example change: "Rewrote system prompt for clarity"
- Example change: "Added new tool definition"

Permissioning:
- Coach CAN read: Verifier feedback, generator, answer key
- Coach CANNOT edit: Verifier, answer key, original generator
- Output files ONLY: candidate_vN.txt, CHANGELOG.txt
```

### Permissioning Structure (System Design)

```
Generator:
  - CAN: Read answer key, see feedback
  - CANNOT: Edit anything
  - FILE: generator.txt (locked in production)

Verifier:
  - CAN: Read generator output, answer key, answer
  - CANNOT: Edit anything
  - FILE: verifier.txt (locked)

Coach:
  - CAN: Read everything
  - CANNOT: Edit answer key, generator, verifier
  - OUTPUT: candidate_vN.txt only (new files, never overwrite)

You (Operator):
  - CAN: Edit all files
  - DECISION: Approve/reject coach's candidate
  - FILE: Promote candidate_vN.txt → generator.txt (manual step)
```

---

## STEP 4: PICK YOUR LEVEL OF AUTONOMY (12:45 - 16:30)

**Mental Model:** Self-improving ≠ "let AI rewrite itself until smart."  
**Reality:** Self-improving = feedback loop where **you design the system** and **decide what AI can change.**

### LEVEL 1: Manual Improvements (You Suggest)

**When:** Day 1, most use cases, low-risk changes

**Flow:**
1. You notice an issue
2. You tell Claude
3. Claude updates the agent

### PROMPT 5: Manual Improvement Command

```
[PROMPT - Direct improvement in conversation]

Use this whenever you spot an issue:

"Based on this conversation, update the [agent/skill] I use so this doesn't happen again."

Example:
"Based on this conversation, I need to add a rule about checking the admin portal first. 
Update the Austin GPT agent so it always checks build.partner.ai before suggesting alternatives."

Claude: Updates generator.txt directly
```

**Effectiveness:** High for quick fixes, good for 90% of use cases.

---

### LEVEL 2: AI Suggests, You Approve (Goldilocks Zone) ⭐ RECOMMENDED

**When:** Anything important, complex decisions, high-risk changes

**Flow:**
1. Generator creates answer
2. Verifier grades it
3. Coach suggests improvement
4. **You review and approve** ← Human in the loop
5. If approved, update generator.txt

### PROMPT 6: Full Self-Improving Loop (Level 2)

```
[PROMPT - Autonomous suggestion with human approval]

1. Run generator against historical outputs where it failed
2. Run verifier to grade each output
3. Run coach to suggest candidate_vN.txt
4. Compare candidate_vN.txt vs generator.txt
5. Report: "Here's what changed and why"
6. Wait for human approval before promoting candidate → generator

Loop:
  for each historical_failure:
    output = generator(historical_failure)
    score = verifier(output, answer_key)
    if score < passing:
      candidate = coach(verifier_feedback)
      candidate_score = verifier(candidate, answer_key)
      if candidate_score > output_score:
        WAIT_FOR_HUMAN_APPROVAL
        if human_approves:
          generator = candidate
        else:
          keep_generator_as_is
```

**Alternative (Simpler):** Use BuildPartner.AI mod that suggests improvements in real-time, you approve/deny in chat.

**Why This is Best:** 
- AI runs continuously (doesn't require you to notice issues)
- You retain final decision (maintain understanding of how agent works)
- Prevents "mysterious auto-changes" that break things
- Keeps agent's behavior predictable

---

### LEVEL 3: Full Autonomy (AI Improves Itself)

**When:** Verifiable pass/fail (code, math, well-defined tests only)

**Warning:** From Zuben @ Weights & Biases:
> "It's really easy to go auto mode, but it doesn't absolve yourself of the thought behind improvements. Auto-looping creates unpredictable outcomes because you don't know what's going on."

### PROMPT 7: Autonomous Self-Improvement Loop (Level 3)

```
[PROMPT - Full autonomy loop]

iteration = 0
while iteration < 10:  # Stop at 10 to save tokens
  output = generator(historical_failures)
  score = verifier(output, answer_key)
  if score == passing:
    BREAK  # Success
  else:
    candidate = coach(verifier_feedback)
    if score(candidate) > score(generator):
      generator = candidate
      iteration += 1
    else:
      BREAK  # No improvement found

if iteration == 10:
  LOG: "Hit iteration limit. Manual review needed."
```

**Recommendation:** Only for technical work with clear pass/fail criteria.

---

## Summary: 4-Step System

| Step | Agent | Job | Output |
|------|-------|-----|--------|
| 1 | Generator | Do the actual work | agent_generator.txt |
| 2 | Verifier | Grade the work (readonly) | Verification report |
| 3 | Coach | Suggest improvements (candidate only) | candidate_vN.txt |
| 4 | (You) | Decide autonomy level | Approval/rejection |

---

## Implementation Checklist

- [ ] **PROMPT 1:** Interview yourself, generate agent_generator.txt
- [ ] **PROMPT 2:** Extract Q&A from Slack, create answer_key.md
- [ ] **PROMPT 3:** Create verifier agent (readonly)
- [ ] **PROMPT 4:** Create coach agent (permissioned candidate writer)
- [ ] **PROMPT 5:** Test manual improvement flow
- [ ] **PROMPT 6:** Set up Level 2 approval loop
- [ ] **Optional:** Level 3 auto-loop for technical work only

---

## Key Warnings

1. **Don't let verifier grade itself** — Creates circular logic
2. **Don't let coach edit generator directly** — Makes version control impossible
3. **Don't auto-loop complex work** — You lose understanding
4. **Answer key is living document** — Add rows as agent fails
5. **Isolate variables** — One change per candidate, or you won't know what helped

---

## For Your Invisico System

**Apply this framework:**
1. **Generator:** Decision-support agent that answers Invisico-specific questions
2. **Verifier:** Compare outputs to your documented decision-making examples
3. **Coach:** Suggest improvements to the agent's reasoning process
4. **Level:** Start at Level 2 (you approve improvements)
5. **Answer Key:** Document 20 real decisions you've made + reasoning

**Result:** Agent that learns your decision patterns, improves over time, stays under your control.
