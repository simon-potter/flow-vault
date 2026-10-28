---
type: concept
title: Extraction Log
status: active
source_kind: mcp:put_page
ingested_via: mcp:put_page
ingested_at: '2026-10-28T08:06:03.362Z'
trust_tier: agent_written
tags:
  - audit-trail
  - hermes
  - self-improvement
---

# Hermes Self-Improvement: Extraction Log

**Purpose:** Audit trail of all ingested sources, extracted improvements, and tasks created.

**Updated:** 2026-10-28  
**Total Sources Ingested:** 0  
**Total Improvements Extracted:** 0  
**Total Kanban Tasks Created:** 0  

---

## Log Entries

### Entry Template

```
**Date:** YYYY-MM-DD  
**Source Title:** [Video/Article/Issue name]  
**Source URL:** [link]  
**Ingestion Method:** [Media-Ingest / Manual]  
**Extraction Page:** [Link to extraction template filled out]  
**Improvements Found:** N  
**Kanban Tasks Created:** [Link task IDs]  
**Status:** Pending / Ready for Implementation / In Progress / Done  
**Notes:** [Any blockers, questions, or context]  
```

---

## Current Queue

*No ingestions yet. When you send the first improvement source via Telegram, it will appear here.*

---

## Completed Extractions

*Will track completed ingestions here.*

---

## Statistics

| Metric | Count |
|--------|-------|
| Total sources ingested | 0 |
| Average improvements per source | — |
| Tasks created | 0 |
| Tasks completed | 0 |
| Avg effort per task | — |

---

## How to Add an Entry

1. **After ingesting a source:** Fill the extraction template (see `task-extraction-template.md`)
2. **Create Kanban tasks** for each improvement
3. **Add an entry to this log** with:
   - Date, source title, extraction page link
   - Number of improvements + task IDs
   - Status (Pending / Ready / In Progress / Done)
4. **Update stats** at the top

---

## Implementation Agent Checklist

When picking a task from Kanban:
- [ ] Read the extraction page for context
- [ ] Read the linked source (video transcript, article, etc.)
- [ ] Understand the AC (Acceptance Criteria)
- [ ] Implement the improvement
- [ ] Test according to AC
- [ ] Update log: change status to "Done"
- [ ] Report back to Simon with outcome
