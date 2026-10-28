---
type: concept
title: Task Extraction Template
status: template
source_kind: mcp:put_page
ingested_via: mcp:put_page
ingested_at: '2026-10-28T08:05:53.433Z'
trust_tier: agent_written
tags:
  - hermes
  - self-improvement
  - template
---

# Hermes Improvement Task Extraction Template

**Use this template for EVERY ingested source about Hermes improvements.**

Fill it out completely before creating a Kanban task. This ensures structured extraction and prevents vague tasks.

---

## Source Information

**Source Title:** …  
**Source Type:** [Video / Article / GitHub Issue / Community Post / Other]  
**Source URL/Link:** …  
**Date Ingested:** 2026-10-28  
**Creator/Author:** …  
**Duration/Length:** … (video: minutes, article: pages)

**Ingested From:** [Telegram / Web / Shared by User / Other]  
**Transcript/Notes Location:** `processes/hermes-self-improvement/ingested-sources/[slug]/`

---

## Extracted Improvements

### Improvement #1

**Idea Title:** … (short, specific)  
**Category:** [Feature / Bug Fix / Integration / Documentation / Performance / Security / UX/UI / Other]  
**Priority Suggested by Source:** [Critical / High / Medium / Low]  
**Your Assessment:** [Critical / High / Medium / Low]  

**Problem Solved:**  
(What problem does this fix or what need does it address?)

**Current State:**  
(How does Hermes currently handle this? Is there a workaround?)

**Proposed Solution:**  
(Concrete steps or description of the improvement)

**Difficulty to Implement:** [Quick (< 1hr) / Medium (1-4 hrs) / Complex (4+ hrs) / Unknown]

**Dependencies/Blockers:**  
(What would block this? External APIs? Other features?)

**Who Should Own This:**  
(Agent recommendation for implementation)

**Acceptance Criteria (AC):**
- [ ] AC 1: …
- [ ] AC 2: …
- [ ] AC 3: …

**Estimated Effort:** … hours / story points  
**Evidence:** (Quote from source or link to timestamp)

---

### Improvement #2

[Repeat the structure above for each improvement]

---

## Summary

**Total Improvements Extracted:** …  
**Quick Wins (< 1hr):** …  
**Medium Effort (1-4 hrs):** …  
**Complex (4+ hrs):** …  

**Highest Priority:** [Improvement name]  
**Ready to Create Kanban Tasks:** Yes / No / Partially  
**Notes for Implementation Agent:** …

---

## Next Steps

1. **Review this filled template** with Simon
2. **Create Kanban card** for each improvement (one task = one improvement)
3. **Link Kanban card** back to this extraction page
4. **Log in `extraction-log.md`** with date + source + tasks created
5. **Assign to implementation agent** (or set to `ready` for next available)

---

## Example: Completed Extraction

**Source:** YouTube video: "5 Hermes Tips You Didn't Know"  
**Idea:** Add native Spotify integration  
**Current State:** Users manually copy Spotify playlist links  
**Proposed Solution:** Built-in `spotify` skill that plays, searches, queues  
**Difficulty:** Medium (need Spotify API auth + testing)  
**AC:**
- [ ] Spotify API authentication works
- [ ] Can search and play tracks from Hermes chat
- [ ] Skill documented
- [ ] Tested with 3 user workflows

**Effort:** 3 hours
