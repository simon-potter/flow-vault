---
type: research
title: Hermes Community Skills with Perplexity Integration (2026)
date: '2026-06-01T00:00:00.000Z'
ingested_via: 'mcp:put_page'
ingested_at: '2026-06-01T07:26:36.362Z'
source_kind: 'mcp:put_page'
tags:
  - hermes
  - integration
  - perplexity
  - skills
  - web-research
---

# Hermes Community Skills with Perplexity Integration

Comprehensive guide to Perplexity-integrated skills and related research tools available in the Hermes community skill library.

## Core Perplexity Integration

### **perplexity-research** ⭐⭐⭐⭐⭐
- **Location**: `/opt/hermes/.bun/install/global/node_modules/gbrain/skills/perplexity-research/`
- **Status**: Actively maintained, v0.1.0
- **Purpose**: Brain-augmented web research with delta detection
- **Key Features**:
  - Sends brain context to Perplexity API
  - Returns only what's NEW vs. existing brain knowledge
  - Full citation support (every claim cited)
  - Supports Perplexity `sonar-pro` and `sonar` models
  - Recency filtering (hour/day/week/month)
  - Outputs structured research pages under `research/<slug>`

**Activation Triggers:**
- "perplexity research"
- "perplexity-research"
- "what's new about"
- "current state of"
- "web research"
- "what changed about"
- "surface new developments"

**Cost Model:**
- `sonar-pro`: ~$0.04 per query (deep analysis, entity enrichment)
- `sonar`: ~$0.007 per query (quick lookups, bulk monitoring)

**Integration Points:**
- Called by `enrich` skill for entity page updates
- Used in `academic-verify` for citation checking
- Part of `briefing` pipeline for morning updates
- Supports deal/company monitoring via cron jobs

**Requirements:**
- `PERPLEXITY_API_KEY` environment variable
- Internet connectivity for API calls
- Brain context (gbrain pages) to provide research anchors

---

## Skills That Integrate With or Depend On Perplexity Research

### 1. **academic-verify** 🔬
- **Status**: v0.1.0, actively maintained
- **Purpose**: Citation verification through perplexity-research
- **How It Uses Perplexity**: Routes claim validation through perplexity-research, traces publications to methodology and raw data
- **Outputs**: Structured brain pages under `concepts/` with verified citations
- **Triggers**:
  - "verify this academic claim"
  - "check this study"
  - "academic verify"
  - "validate citation"
  - "is this study real"
  - "Retraction Watch"
- **Workflow**:
  1. Accept academic claim
  2. Query brain for prior knowledge
  3. Call perplexity-research for web lookup
  4. Format results with full citations
  5. Cross-reference Retraction Watch, publication databases

### 2. **enrich** 📋
- **Status**: v1.0.0, core skill
- **Purpose**: Tiered entity enrichment for person/company pages
- **How It Uses Perplexity**: Calls perplexity-research when a page needs current web context
- **Workflow**:
  1. Get existing page context
  2. Call perplexity-research for fresh data
  3. Merge with brain knowledge
  4. Update pages with new timeline entries
  5. Cross-link related entities
- **Outputs**: Updated `people/` and `companies/` pages
- **Integration**: Foundational skill called by many downstream workflows

### 3. **data-research** 📊
- **Status**: v1.0.0, mature skill
- **Purpose**: Structured data extraction from web sources
- **How It Complements Perplexity**: 
  - Uses YAML recipes for parameterized searches
  - Can chain with perplexity-research for synthesis
  - Maintains canonical tracker pages
  - Deduplicates across sources
- **Use Cases**:
  - Investor updates
  - Donations tracking
  - Company updates
  - Email-to-structured-data pipelines
- **Outputs**: Tracker pages, timeline entries, raw data archives

### 4. **idea-ingest** 💡
- **Status**: v1.0.0, actively used
- **Purpose**: Ingest links, articles, tweets into brain
- **How It Integrates**:
  - Fetches content from URL
  - Can call perplexity-research for context enrichment
  - Creates author people pages
  - Cross-links sources
- **Triggers**: Whenever user shares a link
- **Outputs**: Pages under `people/`, `concepts/`, `sources/`

### 5. **article-enrichment** 📰
- **Status**: v0.1.0, specialized
- **Purpose**: Transform raw article text into structured brain pages
- **How It Works**:
  - Extracts executive summary
  - Preserves verbatim quotes
  - Identifies key insights
  - Can integrate perplexity-research for fact-checking
- **Outputs**: Structured pages under `media/articles/`
- **Conventions**: Follows quality.md citation rules

### 6. **ingest** 🔀
- **Status**: Mature, routing dispatcher
- **Purpose**: Meta-skill that routes content to specialized ingestion skills
- **How It Integrates**:
  - Detects input type (meeting, article, media, conversation)
  - Delegates to appropriate ingestion skill
  - Each downstream skill can use perplexity-research
- **Triggers**:
  - "ingest this"
  - "save this to brain"
  - "process this meeting"

---

## Related Research Skills (Non-Perplexity but Complementary)

### 7. **arxiv** 📚
- **Purpose**: Search and ingest academic papers
- **Complements Perplexity**: Can feed papers into academic-verify workflow

### 8. **blogwatcher** 📰
- **Purpose**: Monitor blogs and RSS/Atom feeds
- **Use Case**: Continuous monitoring; surfaces sources for perplexity-research

### 9. **llm-wiki** 🧠
- **Purpose**: Build/query interlinked markdown knowledge bases
- **Use Case**: Karpathy's LLM Wiki integration

### 10. **polymarket** 📈
- **Purpose**: Query prediction markets (Polymarket API)
- **Complements**: Can validate market-based claims via perplexity-research

---

## Recommended Integration Patterns

### Pattern 1: Entity Enrichment Pipeline
```
Link shared → idea-ingest → extract entities → 
enrich (calls perplexity-research) → 
brain pages updated with citations
```

### Pattern 2: Academic Verification
```
Claim encountered → academic-verify → 
perplexity-research (web lookup) → 
Retraction Watch check → verified concept page
```

### Pattern 3: Daily Briefing
```
Monitored companies/deals → perplexity-research 
(what's new?) → blogwatcher (RSS sources) → 
briefing synthesis with citations
```

### Pattern 4: Deal/Company Monitoring (Cron)
```
Every Monday 9 AM → perplexity-research 
(what changed about [company]?) → 
data-research (extract metrics) → 
timeline updates + notifications
```

### Pattern 5: Idea-to-Analysis
```
User: "Read this [URL]" → idea-ingest → 
article-enrichment → cross-link entities → 
call enrich on mentioned people/companies → 
perplexity-research for fresh context
```

---

## Setup & Configuration

### Prerequisites
1. **PERPLEXITY_API_KEY** environment variable set
2. Valid Perplexity API credentials (sign up at https://www.perplexity.ai/api)
3. Hermes with gbrain integration enabled
4. At least one brain page to provide context

### Environment Setup
```bash
# Set in your .env or systemd service
export PERPLEXITY_API_KEY="pplx-xxxxxxxxxxxxx"

# Verify connectivity
hermes skill view perplexity-research

# Test call (if using with cli)
gbrain submit_agent --prompt "What's new in LLM security?"
```

### Cost Optimization Tips
1. **Use `sonar` for bulk monitoring** (~$0.007/query)
2. **Use `sonar-pro` for deep analysis** (~$0.04/query)
3. **Cache results**: Store research output in brain to avoid re-queries
4. **Batch queries**: Run perplexity-research in cron jobs during off-peak hours
5. **Set recency_filter**: Limit to `week` or `month` for older topics (saves API calls)

---

## Known Limitations & Workarounds

### Limitation 1: No Direct Perplexity Integration in Hermes Core
- **Issue**: perplexity-research is a gbrain skill, not a native Hermes tool
- **Workaround**: Use through skill invocation or delegate_task with skill loading
- **Status**: This is by design (gbrain handles brain persistence, Hermes handles agents)

### Limitation 2: Context Window Size
- **Issue**: Very long brain pages might exceed Perplexity API limits
- **Workaround**: Summarize brain context before sending to Perplexity
- **Mitigation**: The skill auto-chunks large contexts

### Limitation 3: Latency
- **Issue**: Perplexity API calls add 2-10 second latency
- **Workaround**: Use for async cron jobs, not real-time chat
- **Alternative**: Cache results; reuse recent research

### Limitation 4: API Rate Limits
- **Issue**: Perplexity has rate limits (~10 req/min on standard tier)
- **Workaround**: Space out queries; use sonar for bulk work
- **Monitoring**: Check API dashboard for quota usage

---

## Comparison: When to Use Each Skill

| Need | Skill | Cost | Speed | Freshness |
|------|-------|------|-------|-----------|
| Fact-check a single claim | `academic-verify` | ~$0.04 | 5-10s | Live web |
| Update person/company page | `enrich` | ~$0.04 | 5-10s | Live web |
| Monitor 50+ companies weekly | `data-research` + cron | ~$0.35/week | Batch | Day-old |
| Save a URL quickly | `idea-ingest` | $0 | <1s | Local only |
| Build investor tracker | `data-research` | $0.01-0.02 ea | Batch | As-needed |
| Verify academic claims | `academic-verify` | ~$0.04 ea | 5-10s | Live web |

---

## Community Contributions & Roadmap

### Potential Enhancements (Not Yet Implemented)
1. **Multi-source research**: Chain perplexity-research with arxiv, blogwatcher for cross-source synthesis
2. **Caching layer**: Persist research results to avoid re-queries on identical topics
3. **Custom prompts**: Allow users to define custom research templates via YAML
4. **Fact-checking automation**: Systematic verification of brain claims vs. web reality
5. **Conflict detection**: Flag contradictions between brain pages and latest research
6. **Attribution graphs**: Trace claims back to sources with citation chains

### How to Contribute
1. **Report bugs**: Create issues at [hermes-agent GitHub](https://github.com/nousresearch/hermes-agent)
2. **Add skills**: Follow SKILL.md conventions and submit PRs
3. **Share patterns**: Document your integration workflows for community reuse
4. **Improve docs**: Help expand skill documentation with examples

---

## Quick Start: Using Perplexity-Research with Your Brain

### Example 1: Verify a Prompt Injection Defense Tool
```
User: "Is Guardrails AI still maintained in 2026?"

Steps:
1. Hermes loads perplexity-research skill
2. Searches brain for existing Guardrails info
3. Calls Perplexity: "What's new about Guardrails AI since [date]?"
4. Returns: "Still maintained, v1.3+ released June 2026, GitHub stars 8k+"
5. Updates brain/research page with findings + citations
```

### Example 2: Monitor a Company
```
User: (via cron job) Weekly perplexity-research on "Anthropic 2026 updates"

Steps:
1. Brain context: [All existing Anthropic knowledge]
2. Perplexity query: "What changed about Anthropic since last week?"
3. Results: New model releases, hiring, funding, partnerships
4. Timeline entries created
5. Existing Anthropic page updated
6. Notification sent to user
```

### Example 3: Enrich an Imported Article
```
User shares: https://arxiv.org/abs/2406.xxxxx

Steps:
1. idea-ingest fetches article
2. article-enrichment structures it
3. Extracts author → create people page
4. enrich skill calls perplexity-research on author
5. Final output: Linked, enriched article with author context + citations
```

---

## Troubleshooting

### Error: "PERPLEXITY_API_KEY not found"
- **Fix**: Set environment variable before running hermes
- **Command**: `export PERPLEXITY_API_KEY="pplx-xxxxx"` then `hermes serve`

### Error: "API rate limit exceeded"
- **Fix**: Wait 5 minutes or upgrade Perplexity plan
- **Workaround**: Use `sonar` model instead of `sonar-pro`

### Error: "Research page not created"
- **Fix**: Check brain permissions and `research/` directory exists
- **Command**: `gbrain get research/test-page` to verify write access

### Slow responses from perplexity-research
- **Cause**: Large brain context or API latency
- **Fix**: Use async cron jobs; don't expect <5s results
- **Optimization**: Summarize brain context before sending

---

## References & Resources

- **Perplexity Docs**: https://docs.perplexity.ai/
- **Hermes Agent**: https://hermes-agent.nousresearch.com/docs
- **GBrain Skills**: `/opt/hermes/.bun/install/global/node_modules/gbrain/skills/`
- **Skill SKILL.md Format**: https://hermes-agent.nousresearch.com/docs/skills/authoring

---

## Last Updated
2026-06-01

This is a living document. Check the Hermes community and gbrain repositories for the latest skill updates and community contributions.
