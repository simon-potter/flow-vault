---
type: concept
title: 'Hermes Self-Improvement: Operational Summary'
created: 2026-10-28T00:00:00.000Z
source_kind: mcp:put_page
ingested_via: mcp:put_page
ingested_at: '2026-10-28T08:12:49.968Z'
trust_tier: agent_written
tags:
  - hermes
  - operations
  - self-improvement
---

# Hermes Self-Improvement System: Operational Summary

**Setup Complete:** 2026-10-28  
**Status:** 🟢 Ready for first ingestion  
**Owner:** Simon Potter  

---

## What This System Does

Automated feedback loop for continuously improving Hermes:

1. **You find** a Hermes improvement idea (video, article, research)
2. **Agent ingests** the source (transcript, text extraction)
3. **Agent extracts** concrete improvement ideas with AC (Acceptance Criteria)
4. **Agent creates** Kanban tasks (one per improvement)
5. **Implementation agent** executes tasks + reports results
6. **Log tracks** everything: what was ingested, when, outcomes

**Result:** Systematic way to discover, structure, and implement Hermes improvements.

---

## Core Artifacts

### Brain Pages (5 total)

| Page | Purpose | Link |
|------|---------|------|
| Main Overview | Workflow + decision points | `processes/hermes-self-improvement/_index` |
| Extraction Template | Fill this for each source | `processes/hermes-self-improvement/task-extraction-template` |
| Extraction Log | Audit trail + counters | `processes/hermes-self-improvement/extraction-log` |
| Ingested Sources | Folder for all captured media | `processes/hermes-self-improvement/ingested-sources/` |
| This Summary | Quick reference | (this page) |

### Operationalization Skill

**`hermes-self-improvement-intake`** (5-phase intake pipeline)
- Phase 1: Capture & ingest media
- Phase 2: Extract improvements from content
- Phase 3: Create Kanban tasks with AC
- Phase 4: Update extraction log
- Phase 5: Implementation agent executes

### Telegram Auto-Routing

Telegram topic → Brain location mapping:
- **Topic:** `hermes-improvements` (or Hermes Flow thread 1404)
- **Routes to:** `processes/hermes-self-improvement/ingested-sources/`
- **Auto-created:** Extraction pages + Kanban tasks

---

## The Intake Flow (5 Phases)

```
Phase 1: CAPTURE & INGEST
  Input: URL or media file
  Action: Fetch transcript, extract text, store raw
  Output: Brain page with content
  ⭳
  ⭳
Phase 2: EXTRACT IMPROVEMENTS
  Input: Source content
  Action: Identify distinct ideas, fill template
  Output: Extraction page with structured ideas
  ⭳
  ⭳
Phase 3: CREATE KANBAN TASKS
  Input: Extracted improvements
  Action: Quality gate, create task per idea, add AC
  Output: Kanban tasks (ready column)
  ⭳
  ⭳
Phase 4: UPDATE LOG
  Input: Source + extraction + tasks
  Action: Add entry to extraction-log, update counters
  Output: Audit trail + summary notification
  ⭳
  ⭳
Phase 5: IMPLEMENT
  Input: Kanban task + extraction + AC
  Action: Build, test, verify AC
  Output: PR/commit + log update (done)
```

---

## Quick Start (Your First Ingestion)

**Time to complete:** ~2 minutes of action (agent does rest)

### 1. Find a Source

Something about Hermes improvements:
- YouTube: "Hermes Agent tutorial", "Hermes tips", etc.
- Blog: Article about Hermes features or best practices
- GitHub: Issue or discussion about improvements
- Personal: Your own idea about improving Hermes

### 2. Send to Telegram

In thread 1404 (Hermes Flow), send:
```
Improvement: [YouTube link]
```

Or:
```
Hermes idea: [description or link]
```

### 3. Agent Auto-Extracts (~5-10 min)

Check back to see:
- ✅ Brain page created (ingested source + transcript)
- ✅ Extraction page filled (improvements structured)
- ✅ Kanban tasks created (one per improvement)
- ✅ Log updated (entry added)
- ✅ Summary message from agent

### 4. Review Tasks

Go to Kanban `self-improvement` lane:
- See `ready` column with new tasks
- Each task has:
  - Title (improvement name)
  - Body (source link, AC checklist, difficulty, effort)
  - Links (extraction page, source video/article)

### 5. Implement

When ready, implementation agent picks a task:
- Reads extraction page + source + AC
- Builds the improvement
- Tests according to AC
- Moves task to `done`
- Updates log with outcome

---

## Quality Gates (What Gets Extracted)

**The skill auto-applies these gates:**

✅ **EXTRACT if:**
- Idea is specific (not "make it better")
- Idea is actionable (clear steps)
- Idea is in scope (Hermes feature/fix, not external)
- Effort can be estimated

✗ **SKIP if:**
- Too vague
- Outside Hermes (e.g., "change OpenAI's API")
- Already implemented in current version
- Blocked with no clear path

**Example decisions:**
- ✓ "Add native Spotify integration" → Extract
- ✗ "Make Hermes faster" → Skip (vague)
- ✓ "Improve skill discovery search" → Extract
- ✗ "Partner with Google" → Skip (external scope)
- ✣ "Better documentation" → Ask user

---

## Each Improvement Becomes a Kanban Task

**Structure:**
```
Title: [Improvement Name]
Body:
  Source: [Link to ingested video/article]
  Extraction: [Link to extraction page]
  Problem: [Why this matters]
  Solution: [What to build]
  Difficulty: [Quick / Medium / Complex]
  Effort: [2 hours / 5 hours / etc.]
  
  Acceptance Criteria:
    [ ] AC 1: ...
    [ ] AC 2: ...
    [ ] AC 3: ...

Assignee: [Implementation agent or open]
Status: ready (→ in-progress → done)
Priority: [Critical / High / Medium / Low]
```

**Example:**
```
Title: Add native Spotify integration
Difficulty: Medium (3 hours)
AC:
  [ ] Spotify API auth works with Hermes config
  [ ] Users can search & play tracks from chat
  [ ] Skill documented with examples
  [ ] Works with 3 test playlists
Source: [YouTube video link]
Extraction: [extraction page link]
```

---

## Extraction Log: Tracking Everything

**Live audit trail at:** `processes/hermes-self-improvement/extraction-log`

**Each entry records:**
```
Date: 2026-10-28
Source Title: "5 Hermes Hacks"
Source URL: [YouTube link]
Extraction Page: [link]
Improvements Found: 5
Kanban Tasks Created: [task IDs]
Status: Ready for Implementation
Notes: [any blockers or context]
```

**Counters at top update as you ingest:**
- Total sources ingested
- Total improvements extracted
- Total Kanban tasks created
- Tasks completed
- Average effort per task

---

## Workflow in Action

**Scenario: YouTube video "Hermes Advanced Features"**

1. **You:** Send link in Telegram
   ```
   Improvement: https://youtube.com/watch?v=abc123
   ```

2. **Agent (Phase 1):** Ingests
   - Fetches video transcript via yt-dlp-flow
   - Creates: `processes/hermes-self-improvement/ingested-sources/video-abc123/`
   - Stores raw .vtt transcript

3. **Agent (Phase 2):** Extracts
   - Reads: "Add Spotify, improve UI, fix bugs, add versioning"
   - Creates: `.../video-abc123/extraction` page
   - Fills template for each idea:
     - "Add Spotify integration" (Medium, 3hrs)
     - "Improve skill search" (Quick, 1hr)
     - "Auto-save configs" (Complex, 6hrs)
     - "Skill versioning" (Complex, 8hrs)

4. **Agent (Phase 3):** Creates tasks
   - HERMES-105: Spotify integration → Kanban
   - HERMES-106: Skill search UI → Kanban
   - HERMES-107: Auto-save configs → Kanban
   - HERMES-108: Versioning system → Kanban

5. **Agent (Phase 4):** Updates log
   ```
   Date: 2026-10-28
   Source: "Hermes Advanced Features" (15 min video)
   Improvements: 4
   Tasks: HERMES-105, HERMES-106, HERMES-107, HERMES-108
   Status: Ready for Implementation
   ```

6. **You:** See summary
   ```
   Ingested: "Hermes Advanced Features"
   Extracted 4 improvements, created 4 tasks
   Ready in Kanban self-improvement lane
   ```

7. **Implementation Agent:** Picks HERMES-106 (Quick)
   - Implements skill search UI improvements
   - Tests AC
   - Creates PR
   - Moves task to done
   - Log updated: "Status: Done | PR: #456"

---

## Why This Works

**Structured feedback loop:**
- Every improvement is captured (not lost)
- Every improvement is analyzed (quality gates applied)
- Every improvement becomes actionable work (Kanban tasks)
- Every improvement is tracked (extraction log)
- Every improvement is measured (done/not-done)

**For continuous improvement:**
- Feedback from videos, articles, community becomes tasks
- Tasks are specific (not vague)
- Tasks have AC (concrete + measurable)
- Tasks are prioritized (difficulty, impact)
- Tasks are tracked (audit trail)
- Outcomes are recorded (log updated)

**Self-improving system:**
- More sources ingested → more ideas discovered
- More ideas extracted → more improvements implemented
- More improvements implemented → Hermes gets better
- System learns what works → AC refinement, task patterns

---

## Files You Need to Know

**Read these:**
- `processes/hermes-self-improvement/_index` — Full process overview
- `processes/hermes-self-improvement/task-extraction-template` — What to fill out
- `processes/hermes-self-improvement/extraction-log` — Live tracking

**The skill:**
- `~/.hermes/skills/hermes-self-improvement-intake/SKILL.md` — Workflow operationalization

**Telegram routing:**
- `~/.hermes/skills/knowledge-management/telegram-topic-routing/references/telegram-topic-mapping.md` — Topic → project mapping

---

## What Happens Next

1. **You send first improvement source** (video/article/idea)
2. **Agent ingests + extracts** (brain pages created)
3. **Kanban tasks appear** (ready for implementation)
4. **Implementation agent** picks tasks + builds
5. **Extraction log grows** (audit trail)
6. **Hermes improves** (feedback loop in action)

---

## Status

✅ System setup complete  
✅ Brain structure created  
✅ Skill operationalized  
✅ Telegram routing configured  
✅ Ready for first ingestion  

**Next:** Send first Hermes improvement source via Telegram.

---

**Created:** 2026-10-28  
**Owner:** Simon Potter  
**Status:** Active, awaiting first ingestion
