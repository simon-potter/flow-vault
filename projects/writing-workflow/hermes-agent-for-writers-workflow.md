---
type: project
title: 'Using Hermes Agent for Your Writing Workflow: Idea to Production'
source_kind: mcp:put_page
ingested_via: mcp:put_page
ingested_at: '2026-11-11T07:28:25.588Z'
trust_tier: agent_written
---

# Using Hermes Agent for Your Writing Workflow: Idea to Production

**Your Role:** Writer + Director (you write; Hermes researches and edits)  
**Hermes Role:** Research assistant + editorial partner (never the author)

---

## Your Workflow Architecture

Based on current best practices (2026) and Hermes-specific capabilities:

```
Idea capture → Research + context → Outline → You write → Hermes edits → Publish
```

### Stage 1: Idea Capture (You)
**What you do:**
- Capture raw ideas immediately (voice notes, bullet points, rambling)
- Use a tool that timestamps and preserves exact phrasing (Whisper Flow, Apple Notes, or even a Telegram note to Hermes)
- Don't structure yet—just capture the thought before it evaporates

**Why this matters:**  
Ideas are most authentic in raw form. Polishing them too early kills the original insight.

**Hermes role:** *Waiting to receive*. Set up a Telegram channel or email where you can dump ideas. Hermes can log them with timestamps into persistent memory.

---

### Stage 2: Research + Background (Hermes)
**What Hermes does (you request it):**
- Takes your raw idea/thesis
- Searches for conflicting viewpoints, supporting evidence, recent data
- Finds comparable articles/precedents
- Creates an annotated bibliography or research memo
- Flags gaps or weak points you should address
- Returns findings organized by your outline points (if you have one)

**Quality gate:**  
You verify citations. AI hallucinations are common—check that sources actually exist and say what Hermes claims.

**Hermes setup for this stage:**
- Use `query` (brain) to check if you've written about related topics before
- Use `web_search` + `web_extract` to gather current sources
- Organize findings in a markdown file or vault page (e.g., `projects/[yourproject]/research-[topic].md`)
- Return structured memo with: source, relevance, quotable passage, potential counterargument

---

### Stage 3: Outline (You + Hermes)
**What you do:**
- Take Hermes's research memo
- Decide the argument structure (your unique angle, not AI's)
- Create outline with: thesis, main points, supporting evidence, counterarguments

**What Hermes does (optional):**
- If you want, Hermes can suggest outline variations (3-5 different structures)
- You pick which feels right, then modify it
- Hermes then annotates each outline point with "which research supports this" so you don't hunt later

**Hermes setup:**
- Outline lives in a vault page: `projects/[yourproject]/outline-[title].md`
- Hermes tags it with research citations inline so you can click through
- Create a checklist version so you can tick off sections as you write

---

### Stage 4: You Write (100% You)
**What you do:**
- Open the outline
- Write each section in your voice, at your pace
- You own every sentence, every claim, every comma
- Hermes is *not* drafting. You are.

**Why:**  
Your voice is irreplaceable. The authenticity comes from you writing, not AI. This is non-negotiable.

**Hermes role:** *Silent*. Hermes waits. When you hit a section that needs a specific quote or statistic, you ask Hermes to fetch it (it's already in the research memo). That's the only interaction during this stage.

---

### Stage 5: Editorial Pass (Hermes)
**What Hermes does:**
Once you've written the full draft, Hermes runs:

1. **Consistency check**
   - Does your voice stay consistent across sections?
   - Any contradictions in claims?
   - Any repeated phrasing that should vary?

2. **Citation verification**
   - Does every factual claim in your draft trace back to research?
   - Are citations accurate (Hermes cross-checks against the original sources)
   - Flag anything that needs a source

3. **Structure/flow review**
   - Do transitions work?
   - Is the argument clear to a first-time reader?
   - Any sections that feel off or underexplained?

4. **Tone alignment**
   - Does the draft match your established voice/style?
   - Catch corporate jargon you might not want, redundancy, passive voice where active would work
   - Suggest rewrites of specific sentences (not full paragraphs)

**Output format:**  
Hermes returns:
- Line-by-line comments (not rewrites)
- Suggested rewrites for specific weak sentences
- Flag: "This claim needs a source" with line numbers
- Flag: "This contradicts what you said in Section 2"
- Positive flag: "This argument is strong because..."

**You review and decide:**  
You accept, reject, or modify each suggestion. Hermes doesn't touch your draft—you do.

**Hermes setup for editorial:**
```
Hermes editorial prompt:
"Read this draft as an editor who knows the author's voice and the research.
- Identify unsourced claims
- Flag contradictions
- Suggest rewrites only for sentences that are unclear, repetitive, or weak
- Do NOT rewrite paragraphs
- Do NOT change voice or tone
- Return as line-by-line comments with [EDITORIAL NOTE] tags"
```

---

### Stage 6: You Revise (100% You)
**What you do:**
- Read Hermes's notes
- Decide which suggestions to take
- Rewrite your own sentences
- Verify citations if Hermes flagged them
- Polish any weak sections

---

### Stage 7: Final Check (Hermes)
**What Hermes does:**
- One final pass: any errors in the revised draft?
- Spot-check citations one more time
- Confirm tone consistency
- Quick check: does the headline/intro accurately reflect the content?

---

## Technical Setup (Hermes-Specific)

### Persistent Memory
Store these in Hermes memory so it doesn't forget across sessions:

```markdown
# Your writing voice/style guide
- [3-5 of your best articles]
- Word: [tone] (e.g., "conversational, opinionated, direct")
- Don't sound like: [AI patterns to avoid]
- Audience: [who you're writing for]
- Topics you care about: [your beats]
```

Then when you request an editorial pass, Hermes refers to this.

### Vault Organization
```
projects/
  [yourproject]/
    ideas/
      raw-[date].md          ← Capture stage
    research/
      research-[topic].md    ← Research memo from Hermes
    outline/
      outline-[title].md     ← Your outline
    drafts/
      draft-[title]-v1.md    ← Your writing
      draft-[title]-v2.md    ← After Hermes edits
    published/
      [title].md             ← Final version
```

### Scheduled Briefing (Optional)
If you want, set up a cron job:
```
10:00pm daily → "Summarize today's writing progress and ideas captured"
```

This keeps you aware of what you've logged without being intrusive.

---

## What NOT to Delegate to Hermes

✗ **Do NOT let Hermes:**
- Write sections for you (even as a "first draft to edit")
- Choose your article's angle or thesis
- Make claims you haven't verified
- Publish without your explicit approval
- Auto-revise your text
- Decide what's true

✓ **DO use Hermes for:**
- Finding sources
- Organizing research
- Flagging inconsistencies
- Suggesting sentence rewrites (not paragraph rewrites)
- Catching typos and grammar
- Verifying citations exist
- Reminding you what you've written before (memory)

---

## Quality Checkpoints (Human-in-the-Loop)

Based on scientific manuscript best practices (because stakes are high when your reputation is on the line):

| Stage | Checkpoint | Who Decides |
|-------|-----------|------------|
| Idea captured | Is this worth writing? | **You** |
| Research gathered | Are these sources credible? Do they support the angle? | **You** |
| Outline approved | Is this the right argument structure? | **You** |
| Draft complete | Does every claim in my draft have a source? | **You** (Hermes flags, you verify) |
| Editorial notes received | Which suggestions do I accept? | **You** |
| Final version | Am I comfortable putting my name on this? | **You** |
| Published | This is going live under my byline | **You** (not Hermes) |

---

## Comparison: Your Workflow vs. Common AI-Writing Mistakes

| Mistake | What Goes Wrong | Your Approach |
|---------|-----------------|---------------|
| "AI writes everything" | You lose voice; reader trust evaporates | You write; Hermes edits |
| "Publish AI draft as-is" | Hallucinated citations; factual errors | You verify every claim |
| "Use one model for everything" | Mediocre at all tasks | Hermes routes: web search for research, language model for editing |
| "No persistence between sessions" | You repeat context; Hermes forgets | Persistent memory + vault |
| "Autopilot editorial" | Edits miss your voice; suggestions are generic | Hermes knows your style + suggests, not rewrites |

---

## Why This Works (Evidence from 2026 Best Practices)

**83% of writers don't publish AI content as-is.** Why? Because:
- AI drafts lack authenticity
- Citations need verification
- Voice doesn't ring true unless the human writes it
- Errors compound when humans trust automation

**The winning pattern (Gregory S. McNeal, AI Amplified Cognition):**
1. Capture ideas in your own words
2. Use AI to research and structure
3. Human writes the actual draft
4. AI catches errors and inconsistencies
5. Human revises and decides
6. Human verifies citations before publishing

**Result:** Faster output than writing alone, authentic voice, credible sources, reader trust intact.

---

## Implementation Roadmap for You

### Week 1: Set Up
- [ ] Create vault folders for your project
- [ ] Write your "voice guide" and save to Hermes memory
- [ ] Test idea capture (Telegram to Hermes, or daily voice note)

### Week 2: Test Research Stage
- [ ] Pick one article idea
- [ ] Ask Hermes: "Research this angle. Find 5-10 sources. Create an annotated bibliography."
- [ ] Verify one source manually
- [ ] Keep research memo in vault

### Week 3: Full Workflow
- [ ] Write the full outline
- [ ] Write the article (100% you)
- [ ] Submit draft to Hermes editorial
- [ ] Revise based on notes
- [ ] Publish

### Week 4+: Iterate
- [ ] Track what editorial notes you keep vs. reject
- [ ] Update your voice guide with patterns
- [ ] Optimize Hermes editorial prompts based on what works

---

## The Philosophy

**Hermes is your research department + copy editor in one.**  
It doesn't have opinions about what you should write. It helps you write *better* what you already decided to write.

**You remain the author.** Every claim, every word, every decision is yours. Hermes assists; you direct.

**Authenticity scales.** The more you write, the better Hermes gets at understanding your voice (persistent memory). The faster you work (research + editing offloaded), the more you can write.

This is the opposite of "AI writes for you". It's "AI clears the desk so you can write."
