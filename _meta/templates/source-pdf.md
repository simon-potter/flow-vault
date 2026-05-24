---
# === IDENTITY ===
type: source
source_type: pdf
source_id: "{{source_id}}"
title: "{{title}}"
aliases: []

# === PDF-SPECIFIC ===
author: "{{author}}"
page_count: "{{page_count}}"
doi: "{{doi}}"

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
  - source/pdf
  - status/processed

# === BACKEND SYNC ===
_backend_meta:
  last_read_hash: "{{content_hash}}"
  last_written_at: "{{processed_at}}"
---

# {{title}}

> [!info] Source
> **Author:** [[people/{{author_slug}}|{{author}}]]
> **Pages:** {{page_count}} | **Published:** {{published_at}}
> **File:** [[_attachments/pdfs/{{filename}}|Open PDF]]

## Abstract / Summary
<!-- AI:BEGIN summary -->
^summary

{{summary}}
<!-- AI:END summary -->

## Key Insights
<!-- AI:BEGIN key-insights -->
^key-insights

{{key_insights}}
<!-- AI:END key-insights -->

## Chapter/Section Notes
<!-- AI:BEGIN sections -->

### Section 1
^section-1

{{section_notes}}
<!-- AI:END sections -->

## Research Perspectives
<!-- AI:BEGIN perspectives -->

### Technical Analysis
^perspective-technical

{{perspective_technical}}

### Critical Evaluation
^perspective-critical

{{perspective_critical}}
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
*Processed: {{processed_at}} | Provider: {{llm_provider}}*
