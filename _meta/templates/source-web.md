---
# === IDENTITY ===
type: source
source_type: web
source_id: "web:{{url_hash}}"
title: "{{title}}"
aliases: []

# === WEB-SPECIFIC ===
domain: "{{domain}}"
author: "{{author}}"

# === METADATA ===
url: "{{url}}"
created_at: "{{created_at}}"
processed_at: "{{processed_at}}"
published_at: "{{published_at}}"
language: "en"
llm_provider: "claude"

# === LINKING (wikilink format for Dataview) ===
topics: []
people: []
projects: []
related: []

# === STATUS ===
tags:
  - source/web
  - status/processed

# === BACKEND SYNC ===
_backend_meta:
  last_read_hash: "{{content_hash}}"
  last_written_at: "{{processed_at}}"
---

# {{title}}

> [!info] Source
> **Author:** [[people/{{author_slug}}|{{author}}]] | **Site:** {{domain}}
> **Published:** {{published_at}}
> **URL:** [Original Article]({{url}})

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

## Notable Quotes
<!-- AI:BEGIN quotes -->
^quotes

{{notable_quotes}}
<!-- AI:END quotes -->

## Research Perspectives
<!-- AI:BEGIN perspectives -->

### Technical Analysis
^perspective-technical

{{perspective_technical}}

### Practical Applications
^perspective-practical

{{perspective_practical}}
<!-- AI:END perspectives -->

## Follow-Up Questions
<!-- AI:BEGIN questions -->
^questions

{{follow_up_questions}}
<!-- AI:END questions -->

## Topics

{{topic_links}}

## My Notes
<!-- USER:BEGIN notes -->
^notes

{Your personal notes and insights go here - this section is NEVER overwritten by the system}

<!-- USER:END notes -->

---
*Captured: {{created_at}} | Processed: {{processed_at}}*
