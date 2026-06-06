---
type: process
title: Project Inventory Sync
ingested_via: 'mcp:put_page'
ingested_at: '2026-06-06T12:32:27.405Z'
source_kind: 'mcp:put_page'
tags:
  - active
  - projects
  - sync
---

# Project Inventory Sync Process

Tracks project drift across three systems: **Dropbox**, **Notion**, and **Brain Vault** (Gbrain).

## Current State (2026-06-06)

| Source | Total | Synced | Only Here |
|--------|-------|--------|-----------|
| Dropbox | 38 | 14 | 24 |
| Notion | 18 | 14 | 4 |
| Brain Vault | 6 | 0 | 6 (new) |

### Dropbox Projects (38 total)
Located in `/Projects` folder. Last sync: 2026-06-06.

**Synced with Notion (14):**
- Academy Plus, Boox, CarePilot, CGIAR, Deep Tutor, Digital Deluxe, EdenWines, ExchangewireLabs, FCTO, Fellowers, First Party Capital, First Party Studio, HonkMedia, Madbugger, Mad Tech Money, Matt, Mei-in-a-box, Mneumonically, Propad, Purestak, PyFiddles, SweetDWiliams, VerticalContent, wcventures

**Dropbox-Only (24):**
- Boox, CarePilot, CGIAR, Deep Tutor, Digital Deluxe, EdenWines, ExchangewireLabs, FCTO, Fellowers, First Party Capital, First Party Studio, HonkMedia, Madbugger, Mad Tech Money, Matt, Mei-in-a-box, Mneumonically, Propad, Purestak, PyFiddles, SweetDWiliams, ValiPath, VerticalContent, wcventures

### Notion Database Projects (18 total)
Notion database ID: `d71ebc28aafb43c19053e8c21050d3eb` (display) / `fdae218e-27af-42ba-a5c0-4d496c7a52ff` (query endpoint).
Query endpoint: `/v1/data_sources/fdae218e-27af-42ba-a5c0-4d496c7a52ff/query`

**Synced with Dropbox (14):** Same as above.

**Notion-Only (4):**
- Kwiziq, PromptStack, PropAd, SweetDWiliams

### Brain Vault Projects (6 total - NEW)
Located in `/vault/projects/` directory.

**Newly Added (2026-06-06):**
- [projects/invisico]
- [projects/mediary]
- [projects/spottmedia]
- [projects/olddog-ai]
- [projects/teachplus]
- [projects/academy-plus]

All marked as active and awaiting enrichment.

## Sync Runbook

### How to Run the Full Sync

```bash
doppler run -- bash /opt/hermes/.hermes/skills/knowledge-management/project-inventory-sync/scripts/sync-projects.sh
```

**Expected output:**
- Dropbox project count
- Notion project count
- Overlap count (synced)
- Drift breakdown (Dropbox-only + Notion-only)
- JSON output with full comparison (use `--json` flag)

**Exit code:** 0 = no drift detected, 1 = drift exists (expected while systems are out of sync)

### Critical Gotchas (DO NOT SKIP)

1. **Credential Masking Breaks Bash Syntax**
   - Hermes `write_file` tool masks `${DROP...EN}` inline as `***`, breaking curl syntax
   - Solution: Write scripts with real variable names, run via `doppler run --` to inject at runtime
   - Example: `curl -H "Authorization: Bearer ${DROPBOX_ACCESS_TOKEN}" ...`

2. **Dropbox `.tag` Field is Literal (Not a jq Path)**
   - API response includes field literally named `.tag` (with dot)
   - Wrong: `select(.tag=="folder")`
   - Correct: `select(.\".tag\"==\"folder")`
   - This single bug was returning 0 projects until fixed

3. **Doppler Variable Names Must Match Exactly**
   - `DROPBOX_ACCESS_TOKEN` (not `DROPBOX_TOKEN`)
   - `NOTION_API_KEY` (not `NOTION_KEY`)
   - Mismatches fail silently with 0 results

4. **Notion Query Endpoint is Data Source ID, Not Database ID**
   - Database display ID: `d71ebc28aafb43c19053e8c21050d3eb`
   - Query endpoint ID: `fdae218e-27af-42ba-a5c0-4d496c7a52ff`
   - Wrong: `/v1/databases/{id}/query`
   - Correct: `/v1/data_sources/{id}/query`

## Future Work

- [ ] Add 24 Dropbox-only projects to Notion (manual review first)
- [ ] Verify/archive 4 Notion-only projects
- [ ] Enrich Brain Vault project pages with links to Dropbox/Notion
- [ ] Set up weekly cron job for automated drift detection
- [ ] Email drift reports when changes detected

## Tools & Commands

**Brain Vault (Gbrain):**
- Create project: `mcp_gbrain_put_page(slug="projects/<name>")`
- List all projects: `mcp_gbrain_list_pages(type="project")`
- Search: `mcp_gbrain_query("project name")`

**Dropbox API:**
- Endpoint: `/2/files/list_folder` (requires `DROPBOX_ACCESS_TOKEN`)
- Returns: recursive folder list with `.tag` field (literal dot in key name)

**Notion API:**
- Endpoint: `/v1/data_sources/{id}/query` (requires `NOTION_API_KEY`)
- Use data-source endpoint (not database endpoint) for actual query results

**Skill Location:**
`/opt/hermes/.hermes/skills/knowledge-management/project-inventory-sync/`
- `SKILL.md` — Complete documentation
- `scripts/sync-projects.sh` — Production script
- `references/verified-api-patterns-2026-06-06.md` — Test results + runbook

[Source: User & Project Sync Automation, 2026-06-06]
