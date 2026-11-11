---
type: project
title: 'Hermes Agent Writing Workflow: Idea → WordPress Publication'
source_kind: mcp:put_page
ingested_via: mcp:put_page
ingested_at: '2026-11-11T07:35:11.068Z'
trust_tier: agent_written
---

# Hermes Agent Writing Workflow: Idea → WordPress Publication
## Complete Implementation Guide for Simon Potter

**Scope:** End-to-end writing workflow with Hermes as research assistant + editor  
**Output:** WordPress-published articles with editorial visibility and approval gates  
**Visibility:** Kanban board tracking + scheduled daily briefings

---

## Part 1: Architecture Overview

### The Pipeline (What Actually Happens)

```
You capture idea (Telegram/CLI)
  ↓
Hermes logs to memory + Kanban ("Idea" → "Research" column)
  ↓
You request: "Research this angle"
  ↓
Hermes runs Research Agent
  - web_search for sources
  - web_extract for content
  - query brain for existing context
  - creates research memo in vault
  - updates Kanban ("Research" complete)
  ↓
You create outline in vault
  ↓
Hermes updates Kanban (→ "Outline" column)
  ↓
You write draft (100% you, Hermes silent)
  ↓
You submit draft to Hermes
  ↓
Hermes runs Editorial Agent
  - consistency checks
  - citation verification
  - tone alignment
  - returns line-by-line comments (not rewrites)
  ↓
Hermes updates Kanban (→ "Editorial" column)
  ↓
You review notes + revise
  ↓
You submit final draft to Hermes
  ↓
Hermes runs WordPress Publisher Agent
  - creates WordPress draft
  - attaches featured image (optional)
  - sets author + metadata
  - schedules publication date
  ↓
Hermes updates Kanban (→ "WordPress Draft" column)
  ↓
You review in wp-admin, approve or request changes
  ↓
Publish → Kanban moves to "Published"
```

---

## Part 2: Your Kanban Board Structure

### Recommended 7-Column Layout

**Columns (left to right):**
1. **Idea** — Raw ideas, backlog
2. **Research** — Research agent running
3. **Outline** — Outline approved, ready to write
4. **Writing** — You're drafting
5. **Editorial** — Awaiting editorial review
6. **WordPress Draft** — In WordPress, awaiting publish
7. **Published** — Live (archive)

### Per-Card Custom Fields

```yaml
Title: [Article headline]
Description: |
  Thesis: [Your core argument]
  Angle: [Unique perspective]
  Audience: [Who is this for]
  
Custom Fields:
  Topic: [Finance | Tech | Strategy]
  Publish Date: [date picker]
  Status: [auto-sync with column]
  Word Count Goal: [number]
  Brain Slug: [vault page link]
  WordPress URL: [auto-populated]
  
Checklist (Progress):
  □ Idea captured
  □ Research complete
  □ Outline approved
  □ Draft submitted
  □ Editorial reviewed
  □ Revisions done
  □ WordPress draft created
  □ Published
  
Due Dates:
  - Research: [Publish Date - 5 days]
  - Outline: [Publish Date - 4 days]
  - Draft: [Publish Date - 3 days]
  - Final: [Publish Date - 1 day]
  - Publish: [Target Date]
```

---

## Part 3: Required Upgrades & Additions

### MUST-HAVE (Core)

| Component | Current | Action | Type | Effort |
|-----------|---------|--------|------|--------|
| **Kanban Board** | ✓ Built-in | Use native tools | Native | Low |
| **WordPress MCP** | ✗ Missing | Install Respira | Plugin | Medium |
| **Voice Guide** | ✓ Ready | Create in memory | Config | Low |
| **Research Agent** | ✗ Missing | Create skill | Skill | Medium |
| **Editorial Agent** | ✗ Missing | Create skill | Skill | Medium |
| **Publisher Agent** | ✗ Missing | Create skill | Skill | Low |
| **Kanban Automations** | ✗ Missing | YAML config | Config | Medium |
| **Daily Briefing Cron** | ✗ Missing | Create prompt | Cron | Low |
| **Vault Structure** | ✓ Ready | Set up folders | Config | Low |

### NICE-TO-HAVE (Optimization)

| Component | Benefit | Effort |
|-----------|---------|--------|
| **Featured Image Agent** | Visual consistency | High |
| **SEO Agent** | WordPress SEO optimization | High |
| **Social Scheduler** | Multi-channel distribution | Medium |
| **Citation Checker** | URL verification | Medium |
| **Analytics Dashboard** | Performance tracking | High |
| **Ghostwriter Detector** | AI pattern detection | Low |

---

## Part 4: Skills to Create (Detailed Code Specs)

### Skill 1: Research Agent

**Name:** `research-agent`  
**Purpose:** Orchestrate web search + brain query + create research memo

**Architecture:**
```python
def research_agent(topic, angle, depth="moderate"):
    # Step 1: Brain lookup
    existing = brain.query(angle, limit=5)
    
    # Step 2: Web research
    sources = web_search(angle, limit=10, date_filter="6_months")
    
    # Step 3: Extract content
    research_memo = {}
    for source in sources:
        content = web_extract(source.url)
        research_memo[source.url] = {
            "title": content.title,
            "summary": summarize(content),
            "quotes": extract_quotes(content),
            "relevance": score_relevance(content, angle)
        }
    
    # Step 4: Save to vault
    vault_slug = f"projects/writing/research-{topic_slug}"
    brain.put_page(vault_slug, format_memo(research_memo))
    
    # Step 5: Return to user
    return {
        "status": "complete",
        "sources": len(sources),
        "vault_url": vault_slug
    }
```

**Tools Used:**
- `mcp__gbrain__query` (brain lookup)
- `web_search` (current sources)
- `web_extract` (read sources)
- `mcp__gbrain__put_page` (save memo)

**Trigger:** "Research this angle: {thesis}"

**Output Location:** `projects/writing/research-{slug}.md` (vault)

---

### Skill 2: Editorial Agent

**Name:** `editorial-agent`  
**Purpose:** Review draft, verify citations, check tone consistency, suggest improvements (NOT rewrites)

**Architecture:**
```python
def editorial_agent(draft_text, voice_guide, research_memo):
    checks = []
    
    # Check 1: Citation verification
    claims = extract_factual_claims(draft_text)
    for claim in claims:
        source = find_source_in_research(claim, research_memo)
        if not source:
            checks.append({"type": "unsourced", "line": claim.line, "text": claim.text})
        elif not verify_support(source, claim):
            checks.append({"type": "weak_citation", "line": claim.line})
    
    # Check 2: Internal consistency
    contradictions = find_contradictions(draft_text)
    for c in contradictions:
        checks.append({"type": "contradiction", "lines": c.line_numbers})
    
    # Check 3: Voice alignment
    tone_issues = check_tone(draft_text, voice_guide)
    for issue in tone_issues:
        checks.append({"type": "tone_drift", "line": issue.line})
    
    # Check 4: Weak sentences (suggestions only)
    weak = identify_weak_sentences(draft_text)
    for sentence in weak:
        checks.append({"type": "suggestion", "line": sentence.line, "current": sentence.text})
    
    # Check 5: Flow/structure
    flow_issues = check_transitions(draft_text)
    for issue in flow_issues:
        checks.append({"type": "flow", "line": issue.line})
    
    return format_editorial_report(checks)
```

**Tools Used:**
- `mcp__gbrain__get_page` (read voice guide from memory)
- No brain writes (read-only)

**Trigger:** "Editorial review: {draft_slug}"

**Output:** Structured comment report (inline, not written to vault)

---

### Skill 3: Publisher Agent

**Name:** `publisher-agent`  
**Purpose:** Create WordPress draft, schedule publication (no auto-publish)

**Architecture:**
```python
def publisher_agent(draft_text, title, publish_date, author="Simon Potter"):
    # Step 1: Format for WordPress
    html_content = markdown_to_html(draft_text)
    
    # Step 2: Create WordPress post (as DRAFT)
    post = wordpress.create_post(
        title=title,
        content=html_content,
        status="draft",  # NOT published
        author=author,
        date=publish_date
    )
    
    # Step 3: Return preview + edit link
    return {
        "status": "draft_created",
        "wordpress_id": post.id,
        "edit_url": post.edit_url,
        "preview_url": post.preview_url,
        "scheduled": publish_date,
        "next_step": "Review in wp-admin and click Publish"
    }
```

**Tools Used:**
- `respira` (WordPress MCP)

**Trigger:** "Publish to WordPress: {draft_slug}"

**Output:** WordPress post ID + edit link

**Critical:** NEVER auto-publish. Always require human approval in wp-admin.

---

## Part 5: Configuration Files (YAML)

### 5.1 WordPress MCP Setup

**File:** `~/.hermes/config.yaml`

```yaml
mcp_servers:
  respira:
    # Option A: Local (using NPX)
    command: "npx"
    args: ["-y", "respira-mcp"]
    env:
      RESPIRA_SITE_URL: "https://your-site.com"
      RESPIRA_AUTH: "oauth"
    
    # Option B: Remote (if you have endpoint)
    # url: "https://your-site.com/wp-json/respira/v1/mcp"
    # auth: oauth
```

**Then test:**
```bash
hermes mcp login respira
hermes ask "List the pages on my WordPress site"
```

### 5.2 Kanban Automations

**File:** `~/.hermes/config.yaml`

```yaml
kanban:
  board_id: "default"  # Your Hermes Kanban
  automations:
    
    # When card moves to Research column
    - trigger: column_enter
      column: "Research"
      action: notify
      message: "Research started. Hermes will gather sources."
    
    # When card in Research >3 days
    - trigger: time_in_column
      column: "Research"
      days: 3
      action: notify
      message: "Research on {{card.title}} >3 days. Blocker?"
    
    # When card moves to Editorial
    - trigger: column_enter
      column: "Editorial"
      action: notify
      message: "Draft received. Running editorial review..."
    
    # When card moves to WordPress
    - trigger: column_enter
      column: "WordPress Draft"
      action: notify
      message: "WordPress draft created. Review in wp-admin."
    
    # When published (detected via webhook)
    - trigger: wordpress_published
      action: column_move
      to_column: "Published"
      add_label: "#live"
```

### 5.3 Daily Briefing Cron

**File:** `~/.hermes/cron/editorial-briefing.yaml`

```yaml
name: "daily-editorial-briefing"
schedule: "0 8 * * *"  # 8:00 AM every day
task:
  type: "report"
  template: |
    📊 **Editorial Status** — {{date}}
    
    **Kanban Summary:**
    • Idea: {{count.idea}} cards
    • Research: {{count.research}} ({{overdue.research}} overdue)
    • Outline: {{count.outline}}
    • Writing: {{count.writing}}
    • Editorial: {{count.editorial}} ({{overdue.editorial}} awaiting review)
    • WordPress: {{count.wordpress}}
    • Published: {{count.published}} (this month)
    
    **Today's Action:**
    {{action_items}}
    
    **Overdue Items:**
    {{if overdue.any}}
    • {{overdue.items}}
    {{endif}}
  output: "telegram"  # or email
  frequency: "daily"
```

---

## Part 6: Installation Checklist

### Phase 1: Foundation (Week 1)
- [ ] Set up Kanban board with 7 columns
- [ ] Add custom fields (Topic, Publish Date, Brain Slug, Word Count)
- [ ] Create voice guide (collect 3-5 best articles)
- [ ] Save voice guide to Hermes memory
- [ ] Set up vault folder: `projects/writing/`

### Phase 2: WordPress Integration (Week 2)
- [ ] Install Respira MCP
- [ ] Test WordPress connection
- [ ] Create one test post in WordPress via Hermes

### Phase 3: Research Agent (Week 3)
- [ ] Create `research-agent` skill (using code from Part 4)
- [ ] Test on one article idea
- [ ] Refine based on output

### Phase 4: Editorial Agent (Week 4)
- [ ] Create `editorial-agent` skill
- [ ] Refine voice guide based on testing
- [ ] Test editorial review on draft

### Phase 5: Publisher Agent (Week 5)
- [ ] Create `publisher-agent` skill
- [ ] Test WordPress draft creation
- [ ] Add Kanban automations
- [ ] Set up daily briefing cron

### Phase 6: Full Workflow Test (Week 6)
- [ ] Run complete workflow: idea → research → outline → write → editorial → wordpress → publish
- [ ] Measure: time per stage, revision rounds
- [ ] Optimize prompts based on results

---

## Part 7: Best Practices (Industry References)

### Research Workflow
**Source:** Gregory S. McNeal, "AI-Amplified Cognition" (2026)
- Start with brain lookup (existing context)
- Web search for fresh sources
- Manually verify top 3 sources
- Create annotated bibliography *before* outline

### Editorial Workflow
**Source:** Scientific Writing Skills (SFETNI/2026) + Hermes 3000 (2026)
- All editorial gates are BLOCKING (no silent passes)
- Citation verification is human responsibility
- Separate tone review from citation check
- Never auto-rewrite; suggest only

### Kanban/Visibility
**Source:** Zapier, ClickUp Reporters, Purple Editorial (2026)
- 7-stage pipeline for visibility
- Custom fields carry deadline data
- Automations move cards (not manual)
- Track metrics: time per stage, revision rounds, missed deadlines

### WordPress Integration
**Source:** Respira Press + WPEngine (2026)
- Create as DRAFT, never auto-publish
- Use Respira MCP for native WordPress access
- Require human approval in wp-admin before going live
- Save snapshots for undo capability

### Multi-Agent Orchestration
**Source:** Taskade AI, PaperOrchestrator (2026)
- Sequential handoffs (Research → Writer → Editor → Publisher)
- Shared context between agents
- Each agent's output = next agent's input
- Human approval at critical gates

---

## Summary

**End-to-End Workflow:**
```
Idea (you) → Research (Hermes) → Outline (you) → Write (you) →
Editorial (Hermes) → Revise (you) → WordPress (Hermes) →
Publish (you) → Archive
```

**Visibility:** Kanban + Daily Briefing shows progress at every stage

**Quality Gates:**
1. Outline approval (before writing)
2. Editorial review (before revision)
3. WordPress approval (before publishing)

**What You Get:**
- Faster output (research + editing automated)
- Authentic voice (you write 100%)
- Auditable trail (Kanban + brain)
- Repeatable process (same workflow every article)

---

**Next Step:** Which would you like to start with—Kanban setup, WordPress integration, or skill creation?
