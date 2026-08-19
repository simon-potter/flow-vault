---
type: note
title: Media Ingestion — Monday Mind Benders Videos
ingested_via: 'mcp:put_page'
ingested_at: '2026-08-19T06:58:14.824Z'
source_kind: 'mcp:put_page'
---

# Monday Mind Benders Video Ingestion

## Workflow

When you have a new video to add to the Monday Mind Benders series:

1. **Use the template:** `_meta/templates/monday-mindebenders-video.md`
2. **File location:** `media/videos/monday-mindebenders/<slug>.md`
3. **Tag requirement:** Add `tags: [MondayMindBenders]` to frontmatter
4. **Link to CTO topic:** Include `[[topics/cto|CTO Topic]]` in the Related section

## Auto-Actions on Tag

Once tagged with `#MondayMindBenders`, the video becomes queryable for:

- **Slack posting:** Automated workflow picks up tagged videos and posts to developer channels
- **CTO topic aggregation:** Video links appear in the CTO topic page
- **Developer digests:** Tagged videos roll up into weekly/monthly summaries

## Example

```
File: media/videos/monday-mindebenders/async-rust-patterns.md
Tag: #MondayMindBenders
Action: Auto-post to #engineering-learning Slack channel with title + link
```

## Querying Videos

Find all Monday Mind Benders videos:

```
gbrain query "#MondayMindBenders" --source default
```

Or in conversation:
```
Query the brain for all pages with tag "MondayMindBenders"
```
