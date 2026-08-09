---
type: source
title: YouTube eWkZlS5JMD4 — unavailable (removed)
url: 'https://youtu.be/eWkZlS5JMD4'
format: youtube
status: unavailable
checked: '2026-08-09'
video_id: eWkZlS5JMD4
ingested_via: put_page
ingested_at: '2026-08-09T08:32:27.667Z'
source_kind: put_page
tags:
  - tombstone
  - unavailable
  - youtube
---

# YouTube eWkZlS5JMD4 — unavailable (removed)

**URL:** https://youtu.be/eWkZlS5JMD4
**Status:** ❌ Not retrievable
**Last checked:** 2026-08-09

## Why this page exists

A tombstone, so this video is not silently re-queued for ingestion again.

Requested for ingestion on 2026-06-24 as gbrain import job #3. That job never ran — no
worker consumed it, and its payload shape (`{url, format, source_slug}`) is not one the
builtin `import` handler accepts. Job cancelled 2026-08-09.
[Source: compiled from gbrain minion_jobs table, 2026-08-09]

## Why it cannot be ingested

YouTube returns:

> Video unavailable. It was removed following a copyright removal request by
> The Java Community BV

[Source: yt-dlp-flow via Decodo, 2026-08-09]

No transcript or metadata is obtainable. Retried across rotated Decodo egress IPs; the
removal is upstream, not an anti-bot block.

## ⚠️ Correction — previous metadata on this page was fabricated

This page previously read *"Simon Potter - Security/Threat Analysis Video"* with
**Creator: Simon Potter**, and section headers about "threat vectors relevant to Invisico".
None of that was verified against the video. The only hard evidence about the video's
identity is the copyright claimant, **The Java Community BV**, which suggests Java
conference or community content rather than anything authored by Simon Potter.

The fabricated attribution has been removed. If you know what this video actually was, the
page can be corrected; otherwise it stays a tombstone.
[Source: User request 2026-08-09; YouTube removal notice via yt-dlp-flow 2026-08-09]

## See also

- [[concepts/thinking-in-bets]] — sibling video from the same batch of stuck jobs
