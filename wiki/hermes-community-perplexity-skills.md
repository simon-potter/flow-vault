---
title: Hermes Community Skills Integrating Perplexity & Web Research
type: research
date: 2026-06-01
tags: [hermes, perplexity, skills, web-research, automation]
related: [wiki/prompt-injection-defense-tools, wiki/known-prompt-injections]
---

# Hermes Community Skills Integrating Perplexity & Web Research

Comprehensive catalog of available Hermes/GBrain skills that integrate with Perplexity API and advanced web research workflows for knowledge synthesis and entity enrichment.

## Core Perplexity Integration Skills

### 1. **perplexity-research** ⭐ (PRIMARY)
**Location**: `/opt/hermes/.bun/install/global/node_modules/gbrain/skills/perplexity-research/`

**Purpose**: Brain-augmented web research. Combines existing brain knowledge with Perplexity's web search and synthesis.

**Key Features**:
- Sends brain context to Perplexity so it knows what you already know
- Returns NEW developments vs existing brain knowledge (delta search)
- Citation-based results with verifiable sources
- Brain-first approach: avoids re-narrating settled fact
- Recency filtering: hour | day | week | month options
- Structured research page output under `research/<slug>.md`

**Triggers**:
```
- "perplexity research"
- "perplexity-research"
- "what's new about [topic]"
- "current state of [topic]"
- "web research"
- "what changed about [topic]"
- "surface new developments"
```

**API Models Available**:
| Model | Cost | Use Case |
|-------|------|----------|
| sonar-pro | ~$0.04/query | Deep analysis, entity enrichment, deal research |
| sonar | ~$0.007/query | Quick lookups, bulk monitoring, briefing pipelines |

**Environment Requirements**:
```bash
PERPLEXITY_API_KEY=<your-api-key>
# Optional: set in ~/.gbrain/.env
```

**Output Format**:
```markdown
---
title: "[Topic] — Research [YYYY-MM-DD]"
type: research
date: YYYY-MM-DD
brain_context_slugs: [pages whose context was sent]
recency_filter: [hour|day|week|month|none]
---

# Key New Developments
What's changed since brain last updated

# Confirming Signals
Web evidence validating existing brain knowledge

# Contradictions or Updates
Things that conflict with the brain

# Recommended Brain Updates
Specific page updates suggested based on research

# Citations
[Source title](URL) — accessed YYYY-MM-DD
```

**Integration Patterns**:
1. **Entity Enrichment** — Called by `enrich` skill to add current web context to person/company pages
2. **Deal Monitoring (Cron)** — Weekly news pulls per company with change detection
3. **Morning Briefing** — Replaces raw web_fetch calls to avoid re-narrating known facts
4. **Academic Claim Verification** — Wrapped by `academic-verify` skill

**Anti-Patterns to Avoid**:
- ❌ Sending NO brain context (then it's just a web search — use `web_fetch` instead)
- ❌ Truncating brain context (the whole point is "knows what you know")
- ❌ Discarding citations (every claim must have a URL)
- ❌ Skipping cross-linking of entities mentioned

---

### 2. **academic-verify**
**Location**: `/opt/hermes/.bun/install/global/node_modules/gbrain/skills/academic-verify/`

**Purpose**: Verify research claims and academic citations by tracing them through publication → methodology → raw data → replication.

**Key Features**:
- Routes through `perplexity-research` for web lookup
- Checks existing brain pages first (brain-first approach)
- Traces claims to source data, not just author's characterization
- Detects retracted or disputed studies
- Formats results as citation-checked brain pages
- Writes to `concepts/` directory

**Triggers**:
```
- "verify this academic claim"
- "check this study"
- "academic verify"
- "validate citation"
- "is this study real"
- "Retraction Watch"
```

**Workflow**:
1. Extract claim from user input
2. Query brain for existing page on this study
3. If not found, call `perplexity-research` for current info
4. Verify via:
   - Original publication source
   - Citation count and recency
   - Retraction Watch lookup
   - Independent replication status
5. Write findings to `concepts/[study-name].md`

**Example Use**:
```
User: "Verify the claim that X reduces Y by 50%"
→ academic-verify traces to original paper
→ Checks if study was replicated
→ Flags if retracted or in dispute
→ Returns citation-checked verdict
```

---

## Supporting Research & Enrichment Skills

### 3. **enrich**
**Location**: `/opt/hermes/.bun/install/global/node_modules/gbrain/skills/enrich/`

**Purpose**: Enriches brain pages with tiered enrichment protocol. Creates and updates person/company pages with compiled truth, timeline, and cross-links.

**Key Features**:
- Tiered enrichment: stub → linked → detailed
- Often calls `perplexity-research` for current web context
- Creates person/company pages with timelines
- Cross-links related entities
- Maintains "compiled truth" across sources
- Writes to `people/`, `companies/` directories

**Triggers**:
```
- "enrich"
- "create person page"
- "update company page"
- "who is this person"
- "look up this company"
```

**Workflow**:
1. Brain-first lookup: check if page exists
2. If exists: update with new information
3. If not: create new page with available data
4. Call `perplexity-research` for "current state" of entity
5. Add timeline entries for major events
6. Cross-link to other entities

---

### 4. **data-research**
**Location**: `/opt/hermes/.bun/install/global/node_modules/gbrain/skills/data-research/`

**Purpose**: Structured data research: search sources, extract structured data, archive raw sources, maintain canonical tracker pages.

**Key Features**:
- Parameterized via YAML recipes
- Email-to-structured-data pipelines
- Investor updates, donations, company updates tracking
- Maintains canonical tracker pages
- Deduplication across sources
- Raw data archival with `put_raw_data`

**Triggers**:
```
- "research"
- "track"
- "extract from email"
- "investor updates"
- "donations"
- "build a tracker"
- "data dig"
```

**Complements perplexity-research**:
- `perplexity-research` = web synthesis + citations
- `data-research` = structured extraction + tracking
- Use together for: entity monitoring with both qualitative (Perplexity) + quantitative (data-research) signals

---

### 5. **idea-ingest**
**Location**: `/opt/hermes/.bun/install/global/node_modules/gbrain/skills/idea-ingest/`

**Purpose**: Ingests links, articles, tweets, and ideas into the brain. Fetches content, saves with analysis, creates author person pages, cross-links.

**Key Features**:
- Detects content type from URL/input
- Fetches full content (web_fetch, media extraction)
- Automatically creates author person pages
- Extracts and stores insights
- Cross-links to related concepts
- Writes to `people/`, `concepts/`, `sources/` directories

**Triggers**:
```
- Shares a link or URL
- "read this"
- "save this"
- "think about this"
- "put this in brain"
```

**Workflow**:
1. User shares link/content
2. Detect type (article, tweet, PDF, video, etc.)
3. Fetch full content
4. Extract key insights and quotes
5. Create/update author person page
6. Save to appropriate directory with analysis
7. Cross-link to related pages

---

### 6. **article-enrichment**
**Location**: `/opt/hermes/.bun/install/global/node_modules/gbrain/skills/article-enrichment/`

**Purpose**: Transforms raw article text dumps into structured pages with executive summary, verbatim quotes, key insights, why-it-matters, and cross-references.

**Key Features**:
- Converts walls-of-text → quotable, actionable pages
- Executive summaries with key takeaways
- Verbatim quotes with attribution
- "Why this matters" contextual framing
- Cross-references to related topics
- Writes to `media/articles/` directory

**Triggers**:
```
- "enrich this article"
- "enrich the article"
- "batch enrich"
- "enrich pass"
- "make brain pages useful"
```

**Works with**:
- `idea-ingest` (after ingesting raw content)
- `article-enrichment` (transforms to structured form)
- Results: Highly useful, cross-linked brain pages

---

### 7. **ingest** (Router Skill)
**Location**: `/opt/hermes/.bun/install/global/node_modules/gbrain/skills/ingest/`

**Purpose**: Routes content to specialized ingestion skills. Detects input type and delegates appropriately.

**Key Features**:
- Detects: meetings, articles, media, documents, conversations
- Routes to appropriate specialist skill
- Coordinates across `idea-ingest`, `article-enrichment`, `media-ingest`, etc.
- Single entry point for "save this to brain"

**Triggers**:
```
- "ingest this"
- "save this to brain"
- "process this meeting"
```

**Routing Decision Tree**:
```
ingest (router)
├─→ idea-ingest (links, tweets, articles)
├─→ article-enrichment (raw text → structured)
├─→ media-ingest (video, audio, PDF)
├─→ meeting-ingestion (transcripts)
└─→ voice-note-ingest (voice memos)
```

---

## Complementary Research Skills

### 8. **capture**
**Location**: `/opt/hermes/.bun/install/global/node_modules/gbrain/skills/capture/`

**Purpose**: Save any thought or content into the brain via one CLI command.

**Use Case**: Quick capture before deeper enrichment:
```bash
hermes capture "Quick note about X"  # Creates scratch page
hermes capture "https://article.com" # Queues for ingestion
```

---

### 9. **perplexity-research-adjacent Skills**

#### **briefing**
- Combines multiple `perplexity-research` calls for morning briefing
- Provides synthesis of new developments across topics
- Filters known facts to surface genuinely new information

#### **cold-start**
- Day-one data bootstrapping for new brain
- Uses `perplexity-research` to quickly populate initial knowledge
- Sequences multiple Perplexity queries efficiently

#### **concept-synthesis**
- Deduplicates raw concept stubs into tiered structure
- Uses Perplexity results as input
- Creates "canonical truth" from multiple sources

---

## Integration Architecture

### Skill Dependency Graph

```
perplexity-research (Core)
├─→ academic-verify (claims verification)
├─→ enrich (entity enrichment)
├─→ data-research (structured + Perplexity synthesis)
├─→ briefing (aggregated research)
└─→ concept-synthesis (deduplication)

idea-ingest
├─→ article-enrichment (structuring)
└─→ enrich (author pages)

ingest (Router)
├─→ idea-ingest
├─→ media-ingest
├─→ meeting-ingestion
└─→ voice-note-ingest
```

### Recommended Workflow Sequences

**Scenario 1: Research a Person**
```
1. User: "Who is this person?"
2. enrich (calls perplexity-research internally)
3. Result: Enriched person/[slug].md with current role, timeline
```

**Scenario 2: Fact-Check a Claim**
```
1. User: "Verify that X"
2. academic-verify
3. Calls: perplexity-research + Retraction Watch
4. Result: Citation-checked concepts/[claim].md
```

**Scenario 3: Monitor a Company**
```
1. Schedule: Weekly via cron
2. enrich or perplexity-research on companies/[slug]
3. Result: companies/[slug].md with new developments, timeline updates
```

**Scenario 4: Save and Synthesize an Article**
```
1. User: "Save this article"
2. ingest (detects it's an article)
3. Routes to: idea-ingest
4. Then: article-enrichment (on demand)
5. Result: Structured media/articles/[slug].md with quotes, insights
```

**Scenario 5: Verify + Enrich an Entity**
```
1. User: "Check if this company is still active"
2. enrich (calls perplexity-research)
3. perplexity-research fetches current status
4. Result: companies/[slug].md with "Company Status: Active" timeline entry
```

---

## API & Configuration

### Perplexity API Setup

**1. Get API Key**:
```bash
# Sign up at https://www.perplexity.ai/
# Generate API key from dashboard
```

**2. Set Environment Variable**:
```bash
export PERPLEXITY_API_KEY="your-key-here"
# Or in ~/.gbrain/.env
echo "PERPLEXITY_API_KEY=..." >> ~/.gbrain/.env
```

**3. Test Connection**:
```bash
curl -X POST https://api.perplexity.ai/chat/completions \
  -H "Authorization: Bearer $PERPLEXITY_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "sonar-pro",
    "messages": [{
      "role": "user",
      "content": "What is Perplexity?"
    }]
  }'
```

### Cost Estimation

| Scenario | Queries/Month | Model | Cost |
|----------|---------------|-------|------|
| Daily briefing | 30 | sonar | $0.21 |
| Weekly company monitoring (10 companies) | 40 | sonar-pro | $1.60 |
| Research tasks (ad-hoc) | 50 | sonar-pro | $2.00 |
| **Total typical usage** | ~120 | Mix | **~$5-10/mo** |

---

## Skill Maintenance Status (2026-06-01)

| Skill | Repo | Last Update | Status | Maintenance |
|-------|------|-------------|--------|-------------|
| perplexity-research | gbrain | 2026-05-23 | ✅ Active | ⭐⭐⭐⭐⭐ |
| academic-verify | gbrain | 2026-05-23 | ✅ Active | ⭐⭐⭐⭐ |
| enrich | gbrain | 2026-05-23 | ✅ Active | ⭐⭐⭐⭐⭐ |
| data-research | gbrain | 2026-05-23 | ✅ Active | ⭐⭐⭐⭐⭐ |
| idea-ingest | gbrain | 2026-05-23 | ✅ Active | ⭐⭐⭐⭐⭐ |
| article-enrichment | gbrain | 2026-05-23 | ✅ Active | ⭐⭐⭐⭐ |
| ingest | gbrain | 2026-05-23 | ✅ Active | ⭐⭐⭐⭐⭐ |

---

## Quick Start Guide

### Step 1: Install/Verify Perplexity Skill
```bash
# Already included in Hermes/GBrain
skill_view perplexity-research
```

### Step 2: Set API Key
```bash
export PERPLEXITY_API_KEY="your-api-key"
# Verify with: echo $PERPLEXITY_API_KEY
```

### Step 3: Run a Test Research Query
```bash
# Via Hermes:
hermes "Use perplexity research to find what's new about AI safety regulations in 2026"

# Via GBrain CLI:
gbrain think "What's new in AI safety?" --take
```

### Step 4: Review Output
- Check `research/` directory in your brain
- Pages include citations, new developments, contradictions
- Cross-links automatically added to related entities

---

## Advanced Patterns

### Pattern 1: Continuous Entity Monitoring
```yaml
# cron job running weekly
schedule: "0 9 * * 1"  # Monday 9am
skill: enrich
params:
  entities: ["companies/acme", "people/founder-bob"]
  force_perplexity: true
```

### Pattern 2: Citation Verification Pipeline
```
New article → idea-ingest → extract claims → academic-verify for each claim → flagged contradictions in feed
```

### Pattern 3: Briefing Synthesis
```
perplexity-research (5 queries, recency: day)
→ aggregate results by topic
→ deduplicate with brain
→ output: morning briefing page
```

### Pattern 4: Multi-Source Data Fusion
```
perplexity-research (qualitative)
+ data-research (structured)
+ enrich (timeline)
→ unified entity view
```

---

## Troubleshooting

| Issue | Cause | Solution |
|-------|-------|----------|
| "PERPLEXITY_API_KEY not found" | Environment variable not set | `export PERPLEXITY_API_KEY=...` |
| High API costs | Using sonar-pro for bulk tasks | Switch to `sonar` for monitoring |
| Duplicate research pages | Running perplexity-research twice on same topic | Check existing `research/` pages first |
| Citations not appearing | Using older API version | Update GBrain: `hermes update` |

---

## References

- **Perplexity API Docs**: https://docs.perplexity.ai/
- **GBrain Skills Registry**: `/opt/hermes/.bun/install/global/node_modules/gbrain/skills/`
- **Convention**: `skills/_brain-filing-rules.md` (where to file output)
- **Quality Standards**: `skills/conventions/quality.md` (citation requirements)

---

## Related Skills (Non-Perplexity)

- **web-search**: Basic keyword search (lighter than Perplexity)
- **arxiv**: Academic paper search (Google Scholar-like)
- **blogwatcher**: RSS/Atom feed monitoring
- **polymarket**: Prediction market data
- **llm-wiki**: Interlinked markdown KB building

---

## Last Updated
**2026-06-01**

**Note**: This is a living document. Perplexity API frequently updates models and pricing. Check [Perplexity docs](https://docs.perplexity.ai/) for latest models and costs before deploying production workflows.
