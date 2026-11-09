---
title: How Revolut Cut AI Coding Costs 90% With Self-Hosted Open Models
source: https://www.youtube.com/watch?v=Ok6QdZHCcI8
format: video
speaker: David Abitbol, AI Operations, Revolut
channel: AI Engineer
uploaded: "2026-10-29"
duration: "0:11:47"
transcript_format: en-orig
word_count: 1805
tags:
  - "#MondayMindBenders"
  - "#ai-engineering"
  - "#coding-agents"
  - "#llm-optimization"
  - "#cost-reduction"
---

# How Revolut Cut AI Coding Costs 90% With Self-Hosted Open Models

**Source:** https://www.youtube.com/watch?v=Ok6QdZHCcI8  
**Speaker:** David Abitbol, AI Operations at Revolut  
**Channel:** AI Engineer  
**Uploaded:** 2026-10-29  
**Duration:** 0:11:47  
**Format:** Video (auto-generated captions)  
**Word count:** 1805

## Summary

David Abitbol from Revolut shares how they reduced AI coding costs by 90% by self-hosting open-source models (GLM-53) instead of relying on commercial cloud APIs (Anthropic, OpenAI). The company achieved 60–70% improvement in engineering metrics (coding time and lead time) while cutting per-token costs from ~$3/M down to $0.30/M, delivering unlimited AI tokens to 2,000 engineers without budget shock.

Key insight: Lead time improved more than coding time, suggesting the main bottleneck wasn't raw coding speed but context-switching overhead (Jira, email, documentation lookup).

## Key Insights & Highlights

**Adoption Timeline:**
- Jan 2025: Introduced Gemini (10% lead-time, 20% coding-time improvement)
- Feb 2025: Cloud Code (Sonnet 3.7) launched; skepticism due to costs (engineers spending $1k–$10k/month with low ROI)
- April 2026: Self-hosted GLM-51 (60% coding time, 70% lead-time improvement)

**Infrastructure for 2,000 Engineers:**
- Hardware: 56× B200 GPUs needed to host GLM-53 (800B parameters)
- Performance target: **sub-3-second time-to-first-token** (empirical limit; >5s triggers Slack complaints)
- Throughput: 200 TPS is fine; people work asynchronously anyway. After 5pm, can hit 800 TPS when demand is low

**Cost Dynamics:**
- Blended token cost: $0.30/M (1/10th of Anthropic + OpenAI spend)
- Flat billing, zero bill shock, predictable monthly invoicing

**Tuning Parameters (Same GPU Count, 88% Perf Gain):**
- Long context is a scam; 256K tokens is overkill—aim for 256K in practice
- Quantization: FP4 on Blackwell generation; jump from FP4 to FP8 = 40% GPU footprint savings with zero precision loss
- Tensor parallelism: GLM needs TP8 to balance KV cache constraints
- Cache hit ratio: maintain >90% (optimize via spec decoding, sequential pre-fill, PGD)
- Went from: 3 RPS + 10s TTFT → 7 RPS + 1.6s TTFT (same 56 GPUs)

**Production Setup:**
- GLM-53 is text-only; use local router for image recognition (route to Gemini or Luna)
- All endpoints: OpenAI-compatible API (works with Codex, Cloud Code, etc.)
- Alternative vision: Gemini 5G Flash for UI design

**Compliance & Governance (EU Regulated Bank):**
- No data sharing with China—weights are self-hosted on US servers
- Sandbox: Codex Code approval rules prevent autonomous execution (e.g., "allow git but not Gradle")
- Protects against rogue internal actors
- Prompt injection: less of a threat with modern models
- Data privacy: OK as long as data sits in equivalency-framework countries (US, EU, UK, Israel)

## People Mentioned
- David Abitbol — Revolut AI Ops lead
- Implicit: Cloud Code Sonnet 3.7 team (Anthropic)
- Implicit: Gemini team (Google)

## Companies Mentioned
- **Revolut** — digital bank, 80M customers, 45 markets, largest private company in Europe (as of July 2026)
- **Anthropic** — cloud API provider (Claude)
- **OpenAI** — cloud API provider
- **Google** — Gemini model
- **Blackwell** — GPU hardware line (NVIDIA implied)

## Technical Concepts Extracted
- Self-hosted open-source model inference
- GLM-53 (800B parameters, coding-optimized)
- Quantization strategies (FP4, FP8)
- Tensor parallelism
- KV cache optimization
- Spec decoding
- Time-to-first-token (TTFT) as latency metric
- Throughput (tokens per second)
- EU regulatory compliance for AI
- Sandbox-based AI governance