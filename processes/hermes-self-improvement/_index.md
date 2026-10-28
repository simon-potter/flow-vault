---
type: process
title: Hermes Self-Improvement System
status: active
created: 2026-10-28T00:00:00.000Z
last_updated: 2026-10-28T00:00:00.000Z
linked_projects:
  - agentic-assistants
source_kind: mcp:put_page
ingested_via: mcp:put_page
ingested_at: '2026-10-28T08:01:48.781Z'
trust_tier: agent_written
tags:
  - automation
  - hermes
  - process
  - self-improvement
---

# Hermes Self-Improvement System

**Purpose:** A living feedback loop that captures Hermes improvement ideas from videos, articles, research, and community suggestions — then systematically extracts actionable improvements into Kanban tasks for implementation.

**Owner:** Simon Potter  
**Status:** 🟢 Active (2026-10-28)  
**Last Updated:** 2026-10-28

---

## Overview: The Feedback-to-Action Pipeline

This process runs in 5 phases:

### Phase 1: Capture
When you find a video, article, or suggestion about improving Hermes:
- Link or upload it to `ingested-sources/`
- Use media-ingest skill to transcribe/extract content
- Store raw source for provenance

### Phase 2: Extract
From each ingested source:
- Identify **all improvement ideas** mentioned
- Extract concrete suggestions (not vague notions)
- Note implementation difficulty (quick/medium/complex)
- Identify dependencies or blockers

### Phase 3: Structure
For each improvement:
- Fill out the task extraction template (see `task-extraction-template.md`)
- Classify by category (feature, fix, integration, documentation, etc.)
- Determine feasibility and effort
- Create Kanban task with AC

### Phase 4: Track
Each extracted improvement becomes a Kanban card:
- Status: `suggested` → `ready` → `in-progress` → `done`
- Linked back to source
- Assigned to an implementation agent
- Tracked in extraction-log.md

### Phase 5: Implement & Feedback
Implementation agent:
- Executes the task
- Documents changes
- Tests improvements
- Reports back to brain

---

## Key Decision Points

### When to Create a Task

✓ **Create a task if:**
- The suggestion is specific and actionable
- It improves Hermes for the user's workflow
- It doesn't duplicate existing Hermes features
- Effort can be estimated (hours, not days)

✗ **Skip if:**
- Too vague ("make it better")
- Outside Hermes scope (e.g., "change OpenAI's API")
- Already implemented in current version
- Blocked on external dependency without clear path

### Task Priority Routing

**🔴 Critical (implement now):**
- Fixes for broken core features
- Security/stability issues
- User-blocking bugs

**🟡 High (next sprint):**
- Significant usability improvements
- Performance optimizations
- Missing integrations for common workflows

**🟢 Medium (backlog):**
- Nice-to-have features
- Polish/UX improvements
- Documentation/learning enhancements

**⚪ Low (nice-to-have):**
- Future ideas
- Nice-to-have optimizations
- Long-term roadmap items

---

## Ingested Sources Log

See **`ingested-sources/`** folder for all captured media + extracted notes.

See **`extraction-log.md`** for audit trail of what was ingested, when, and which tasks were created.

---

## How to Use This System

### As Simon (Capture & Suggest)

1. **Find a video/article/idea about Hermes improvements**
   - Could be a YouTube tutorial, GitHub issue, community forum, etc.
   
2. **Send it via Telegram** (in thread 1404 / Hermes Flow topic)
   - Agent auto-routes to `processes/hermes-self-improvement/ingested-sources/`
   - Media-ingest creates a brain page with transcript + summary
   
3. **Agent extracts improvements**
   - Fills task template
   - Creates Kanban cards
   - Logs in extraction-log.md

4. **You review & approve** (optional)
   - Accept suggested tasks
   - Reprioritize
   - Add context

### As Implementation Agent

1. **Monitor Kanban lane:** `self-improvement`
2. **Pick task from `ready` column**
3. **Read source + AC**
4. **Execute**
5. **Report: success / blocker / needs-clarification**
6. **Update extraction-log.md with outcome**

---

## Related Skills

- **media-ingest** — Capture videos, PDFs, articles
- **document-to-action-items** — Extract structured tasks
- **brain-ops** — Brain workflow (lookup before creating)
- **filing-rules-hierarchy** — Content routing

---

## Template Files

- `task-extraction-template.md` — Structure for each improvement idea
- `extraction-log.md` — Audit trail (what was ingested, when, outcomes)

---

## Current Improvements Tracked

See `extraction-log.md` for live tracking.

**Quick links:**
- [All Ingested Sources](processes/hermes-self-improvement/ingested-sources/)
