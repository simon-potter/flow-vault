---
# === IDENTITY ===
type: source
source_type: youtube
source_id: "youtube:{{video_id}}"
title: "{{title}}"
aliases:
  - "{{short_title}}"

# === YOUTUBE-SPECIFIC ===
video_id: "{{video_id}}"
channel: "{{channel}}"
channel_slug: "{{channel_slug}}"
duration: "{{duration}}"

# === METADATA ===
url: "{{url}}"
created_at: "{{created_at}}"
processed_at: "{{processed_at}}"
published_at: "{{published_at}}"
language: "en"
llm_provider: "claude"

# === LINKING (wikilink format for Dataview) ===
topics: []
people:
  - "[[{{channel_slug}}]]"
projects: []
related: []

# === STATUS ===
tags:
  - source/youtube
  - status/processed

# === BACKEND SYNC ===
_backend_meta:
  last_read_hash: "{{content_hash}}"
  last_written_at: "{{processed_at}}"
---

# {{title}}

> [!info] Source
> **Channel:** [[people/{{channel_slug}}|{{channel}}]]
> **Duration:** {{duration}} | **Published:** {{published_at}}
> **URL:** [Watch on YouTube]({{url}})

## Summary
<!-- AI:BEGIN summary -->
^summary

{{summary}}
<!-- AI:END summary -->

## Key Insights
<!-- AI:BEGIN key-insights -->
^key-insights

{{key_insights}}
<!-- AI:END key-insights -->

## Research Perspectives
<!-- AI:BEGIN perspectives -->

### Technical Analysis
^perspective-technical

{{perspective_technical}}

### Practical Applications
^perspective-practical

{{perspective_practical}}

### Critical Evaluation
^perspective-critical

{{perspective_critical}}

### Exploratory Directions
^perspective-exploratory

{{perspective_exploratory}}
<!-- AI:END perspectives -->

## Follow-Up Questions
<!-- AI:BEGIN questions -->
^questions

{{follow_up_questions}}
<!-- AI:END questions -->

## Research Outline
<!-- AI:BEGIN outline -->
^outline

{{research_outline}}
<!-- AI:END outline -->

## Transcript
<!-- AI:BEGIN transcript -->

<details>
<summary>Timestamped Transcript (click to expand)</summary>

{{timestamped_transcript}}

</details>
<!-- AI:END transcript -->

## Topics

{{topic_links}}

## My Notes
<!-- USER:BEGIN notes -->
^notes

{Your personal notes and insights go here - this section is NEVER overwritten by the system}

<!-- USER:END notes -->

---
*Processed: {{processed_at}} | Provider: {{llm_provider}}*
