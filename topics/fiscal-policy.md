---
type: topic
topic_slug: "fiscal-policy"
topic_name: "Fiscal Policy"
aliases:
  - "Fiscal Policy"
created_at: "2026-02-01T07:34:13.035716Z"
updated_at: "2026-02-01T07:34:13.035716Z"
parent_topic: ""
subtopics: []
tags:
  - topic
  - status/active
---

# Fiscal Policy

## Overview
<!-- AI:BEGIN overview -->

{High-level synthesis of this topic across ALL sources}

<!-- AI:END overview -->

## Key Insights
<!-- AI:BEGIN insights -->

- Insight 1 (from [[sources/youtube/...]])
- Insight 2 (from [[sources/pdf/...]])
- Insight 3 (from [[sources/web/...]])

<!-- AI:END insights -->

## Sources

### YouTube Videos
```dataview
TABLE title, channel, processed_at
FROM "sources/youtube"
WHERE contains(string(topics), this.file.name)
SORT processed_at DESC
LIMIT 20
```

### Articles & Papers
```dataview
TABLE title, author, processed_at
FROM "sources/web" OR "sources/pdf"
WHERE contains(string(topics), this.file.name)
SORT processed_at DESC
LIMIT 20
```

> [!note] Dataview Query Explanation
> Uses `contains(string(topics), this.file.name)` because:
> - `topics` is stored as wikilinks in frontmatter
> - `string(topics)` converts to searchable text
> - `this.file.name` is just the filename (e.g., "machine-learning")

## Subtopics

- [[topics/subtopic-1]]
- [[topics/subtopic-2]]

## Related Topics

- [[topics/related-1]]

## Open Questions
<!-- AI:BEGIN questions -->

1. Question emerging from synthesis?
2. Gap in current understanding?

<!-- AI:END questions -->

## My Synthesis
<!-- USER:BEGIN synthesis -->
^synthesis

{Your original thinking and connections go here - this is the VALUE ADD}
{This section is NEVER overwritten by the system}

<!-- USER:END synthesis -->

---
*Created: 2026-02-01T07:34:13.035716Z | Updated: 2026-02-01T07:34:13.035716Z*
