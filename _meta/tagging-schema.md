---
type: note
title: Global Tagging Schema
ingested_via: 'mcp:put_page'
ingested_at: '2026-08-19T06:57:13.338Z'
source_kind: 'mcp:put_page'
---

# Global Tagging Schema

Central registry for all global tags used across the brain for organizing content and triggering actions.

## Video Series Tags

### #MondayMindBenders

**Purpose:** Weekly video series for developer learning and discussion.

**Usage:** Tag videos (typically under `media/videos/`) that are part of the Monday Mind Benders series.

**Action Trigger:** Tagged videos automatically map to the CTO topic and trigger Slack posting to developer channels.

**Format:** Used globally across all media types. Single tag per video sufficient for identification.

**Related:**
- [[topics/cto|CTO Topic]]
- `media/videos/` (filing location)

---

## Tag Conventions

- **Hashtag syntax:** `#CamelCase` for multi-word series names
- **Global scope:** Tags are namespace-free; they cross all source boundaries
- **Automation:** Tags trigger downstream actions (Slack posts, digests, compilations)
- **Queryable:** Use `query` with `tags:MondayMindBenders` to find all tagged items

## Adding New Series Tags

When creating a new global video series:
1. Add entry to this schema
2. Document the purpose and action trigger
3. Link to the corresponding topic (e.g., `topics/cto`)
4. Communicate the tag name to contributors
