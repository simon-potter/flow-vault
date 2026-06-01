---
type: reference
title: Hermes Perplexity Skills — Implementation Comparison
date: '2026-06-01T00:00:00.000Z'
ingested_via: 'mcp:put_page'
ingested_at: '2026-06-01T07:33:35.203Z'
source_kind: 'mcp:put_page'
tags:
  - comparison
  - hermes
  - implementation
  - perplexity
  - skills
---

# Hermes Perplexity Skills — Implementation Comparison

Quick reference guide for choosing and integrating Perplexity-powered research skills.

## Decision Matrix

### 1. I Want to Verify a Single Academic Claim
**→ Use: `academic-verify`**

| Aspect | Details |
|--------|---------|
| **Skill** | academic-verify |
| **Model** | Perplexity sonar-pro |
| **Cost** | ~$0.04 per claim |
| **Speed** | 5-10 seconds |
| **Activation** | "verify this academic claim" / "check this study" |
| **Output** | Concept page with traced citations |
| **Workflow** | Claim → perplexity-research → Retraction Watch → verified page |
| **Brain Integration** | Checks existing concepts first (brain-first) |

**Example:**
```
User: "Is the Universal and Transferable Adversarial Attacks paper real?"
→ academic-verify → Perplexity finds paper → Traces methodology → 
Confirms replication → Creates concepts/adversarial-attacks-2023 page
```

---

### 2. I Want to Update a Person or Company Page
**→ Use: `enrich`**

| Aspect | Details |
|--------|---------|
| **Skill** | enrich |
| **Model** | Perplexity sonar-pro |
| **Cost** | ~$0.04 per entity |
| **Speed** | 5-10 seconds |
| **Activation** | "enrich this person" / "update company page" |
| **Output** | Updated people/ or companies/ pages with timeline |
| **Workflow** | Get page → call perplexity-research → merge context → update |
| **Brain Integration** | Maintains existing page structure; adds new facts |

**Example:**
```
User: "Who is Sarah Chen?"
→ enrich → Gets any existing brain data on Sarah → 
perplexity-research("what's new about Sarah Chen?") → 
Creates/updates people/sarah-chen page with recent role changes, news
```

---

### 3. I'm Monitoring 20+ Companies for News
**→ Use: `data-research` + Cron Job**

| Aspect | Details |
|--------|---------|
| **Skill** | data-research (can chain with perplexity-research) |
| **Model** | Perplexity sonar (cheaper bulk queries) |
| **Cost** | ~$0.14 per run (20 companies × $0.007) |
| **Speed** | 30-60 seconds per run |
| **Activation** | Via cron job (e.g., Monday 9 AM) |
| **Output** | Tracker pages with structured data + timelines |
| **Workflow** | YAML recipe → perplexity-research per company → extract data |
| **Brain Integration** | Maintains canonical tracker pages |

**Example:**
```
Cron: Every Monday 9 AM
→ For each company in tracker:
    → perplexity-research("new announcements about [company]?")
    → Extract funding/hiring/product updates
    → Add timeline entries
    → Notify user of changes
Cost: ~$0.07/week (10 companies, sonar model)
```

---

### 4. User Just Shared a URL
**→ Use: `idea-ingest`**

| Aspect | Details |
|--------|---------|
| **Skill** | idea-ingest |
| **Model** | Optional perplexity-research (if context needed) |
| **Cost** | $0 base; ~$0.04 if enrichment enabled |
| **Speed** | <1 second (fetch) + optional 5-10s (enrich) |
| **Activation** | User shares URL or says "read this" |
| **Output** | New pages under sources/, people/, concepts/ |
| **Workflow** | Fetch content → create author page → optionally enrich |
| **Brain Integration** | Creates new pages; cross-links |

**Example:**
```
User: "Read this: https://arxiv.org/abs/2406.xxxxx"
→ idea-ingest fetches paper → Creates source page →
Extracts author name → create people/[author] →
(optional) Call enrich on author → Link everything together
```

---

### 5. Raw Article Text Needs Structure
**→ Use: `article-enrichment`**

| Aspect | Details |
|--------|---------|
| **Skill** | article-enrichment |
| **Model** | Optional perplexity-research for fact-checking |
| **Cost** | $0 base; ~$0.04 if fact-check enabled |
| **Speed** | 1-2 seconds per article |
| **Activation** | "enrich this article" / "enrich brain pages" |
| **Output** | Structured pages under media/articles/ |
| **Workflow** | Parse → summary + quotes + insights + cross-links |
| **Brain Integration** | Transforms dumps into citable content |

**Example:**
```
Input: Raw article text dump in brain page
→ article-enrichment →
Executive Summary + Key Quotes (verbatim) + Insights +
"Why It Matters" section + Cross-references to related pages
```

---

### 6. Diverse Content: Mix of Meetings, Articles, URLs
**→ Use: `ingest` (Meta-Router)**

| Aspect | Details |
|--------|---------|
| **Skill** | ingest |
| **Model** | N/A (routes to specialized skills) |
| **Cost** | Depends on delegated skill |
| **Speed** | Depends on delegated skill |
| **Activation** | "ingest this" / "save this to brain" |
| **Output** | Routed to appropriate skill |
| **Workflow** | Detect type → delegate to idea-ingest/article-enrich/etc |
| **Brain Integration** | Full cross-linking across all types |

**Example:**
```
User: "Ingest these 3 things: [article], [meeting transcript], [tweet]"
→ ingest routes:
  - Article → article-enrichment
  - Meeting → meeting-ingestion
  - Tweet → idea-ingest
All three processed and cross-linked in brain
```

---

## Feature Comparison Table

| Feature | academic-verify | enrich | data-research | idea-ingest | article-enrichment |
|---------|---|---|---|---|---|
| **Perplexity Integration** | ✓ Direct | ✓ Direct | ✓ Optional | ✓ Optional | ✓ Optional |
| **Real-time Updates** | ✓ Yes | ✓ Yes | ✗ Batch | ✓ Yes | ✗ One-time |
| **Citation Verification** | ✓ Yes | ✓ Yes | ✗ No | ✓ Limited | ✓ Yes |
| **Handles Bulk Data** | ✗ No | ✗ No | ✓ Yes | ✗ No | ✓ Yes |
| **Creates New Pages** | ✓ Yes | ✓ Yes | ✓ Yes | ✓ Yes | ✓ Yes |
| **Cross-Links Entities** | ✓ Yes | ✓ Yes | ✓ Yes | ✓ Yes | ✓ Yes |
| **Tracks Timeline** | ✓ Yes | ✓ Yes | ✓ Yes | ✓ Yes | ✗ No |
| **Cost per Use** | ~$0.04 | ~$0.04 | ~$0.007 | $0-0.04 | $0-0.04 |
| **Execution Time** | 5-10s | 5-10s | 30-60s | <1s-10s | 1-2s |

---

## Integration Recipes

### Recipe 1: Daily Research Briefing
```yaml
Trigger: 7 AM daily
Steps:
  1. perplexity-research on monitored topics (using sonar, cheaper)
  2. blogwatcher collects RSS feeds
  3. data-research extracts metrics from tracked companies
  4. Merge all into briefing/ page
Cost: ~$0.02/day (using sonar for bulk queries)
```

### Recipe 2: Weekly Threat Landscape Update
```yaml
Trigger: Monday 2 PM
Input: Your wiki/prompt-injections page
Steps:
  1. academic-verify on latest attack papers
  2. data-research on defense tool releases
  3. Update wiki/prompt-injection-defense-tools
Cost: ~$0.10/week (3-5 verifications + 2-3 data pulls)
```

### Recipe 3: Smart Link Processing
```yaml
Trigger: User shares link
Steps:
  1. idea-ingest fetches content
  2. Calls enrich on mentioned people
  3. Calls article-enrichment if needed
  4. All cross-linked
Cost: ~$0.08-0.12 per interesting link
```

### Recipe 4: Continuous Company Monitoring
```yaml
Trigger: Every Friday 4 PM (20 companies)
Step:
  data-research with parameterized YAML:
    - For each company: "funding OR hiring OR partnerships"
    - Extract structured data
    - Add timeline entries
    - Flag big changes
Cost: ~$0.14/week (sonar queries)
```

---

## Cost Optimization Strategies

### Strategy 1: Model Selection
- **sonar** (~$0.007/q): Bulk monitoring, weekly updates, low-stakes queries
- **sonar-pro** (~$0.04/q): Single claim verification, entity enrichment, urgent research

**Example Cost Savings:**
- Bulk company monitoring (20/week): sonar saves ~80% vs sonar-pro
- Single fact-check: sonar-pro worth the cost for accuracy

### Strategy 2: Batching & Caching
- **Batch queries**: Run 10+ data-research queries in one cron job (cheaper API)
- **Cache results**: Store perplexity-research output; don't re-query same topic within 7 days
- **Savings**: 50-70% reduction in API calls

### Strategy 3: Asynchronous Execution
- **Real-time**: ~$0.04/query (sonar-pro, interactive)
- **Cron jobs**: ~$0.007/query (sonar, batched, off-peak)
- **Savings**: Use async for non-urgent research; save sonar-pro for real-time

### Strategy 4: Brain-First Lookup
- **Query brain before Perplexity**: Avoids duplicate research
- **Only call Perplexity for deltas**: "What changed since [last update]?"
- **Savings**: 30-50% reduction (depends on how often topics change)

---

## Troubleshooting Guide

| Problem | Skill(s) Affected | Root Cause | Fix |
|---------|---|---|---|
| "PERPLEXITY_API_KEY not found" | All | Missing env var | `export PERPLEXITY_API_KEY=pplx-...` |
| API rate limit exceeded | All | Too many queries | Wait 5 min or use sonar (cheaper) |
| Research page not created | enrich, data-research | Permissions or brain down | Check `research/` dir permissions |
| Slow perplexity-research responses | Any | Large context or API latency | Use async jobs; summarize context |
| Citations missing | academic-verify, enrich | Perplexity didn't cite sources | Retry with sonar-pro; check output |
| Outdated info returned | All | Perplexity cache or network lag | Use recency_filter: "day" for fresher results |

---

## Decision Flowchart

```
Start: I need to research something

├─ Single academic claim?
│  └─→ academic-verify ✓
│
├─ Person or company page needs updating?
│  └─→ enrich ✓
│
├─ Monitoring 20+ items?
│  └─→ data-research ✓
│
├─ User just shared a URL?
│  └─→ idea-ingest ✓
│
├─ Raw article text to structure?
│  └─→ article-enrichment ✓
│
├─ Mix of different content types?
│  └─→ ingest (meta-router) ✓
│
└─ Multiple sources, synthesis needed?
   └─→ Combine 2+ skills:
       - idea-ingest + enrich + academic-verify
       - data-research + perplexity-research
       - article-enrichment + enrich
```

---

## Quick Setup

### Step 1: Set Perplexity API Key
```bash
export PERPLEXITY_API_KEY=pplx-<...>
# Verify it's set:
echo $PERPLEXITY_API_KEY
```

### Step 2: Test a Skill
```bash
# Via Hermes agent:
# "verify this academic claim: [study name]"

# Or via CLI (if available):
gbrain submit_agent --prompt "enrich Sarah Chen"
```

### Step 3: Create Your First Automation
```bash
# Example: Weekly company monitoring
hermes cronjob create --name "company-monitor" \
  --schedule "0 9 * * 1" \
  --task "data-research on Anthropic, OpenAI, DeepSeek"
```

---

## Budget Estimate for Active Use

| Usage Level | Queries/Week | Cost/Week | Use Cases |
|---|---|---|---|
| **Light** | 5-10 | ~$0.30 | Weekly research updates |
| **Medium** | 20-40 | ~$1.50 | Daily research + 2-3 monitoring |
| **Heavy** | 80-150 | ~$3-5 | Continuous monitoring 50+ items |

---

## References

- **Perplexity Docs**: https://docs.perplexity.ai/
- **Hermes Skills**: https://hermes-agent.nousresearch.com/docs/skills/
- **GBrain**: https://github.com/garrytan/gbrain
- **This Setup**: See wiki/hermes-perplexity-integration

---

Last updated: 2026-06-01
