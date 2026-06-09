---
type: wiki
title: Hermes Vault Architecture
created_at: '2026-06-09T00:00:00.000Z'
updated_at: '2026-06-09T00:00:00.000Z'
ingested_via: 'mcp:put_page'
ingested_at: '2026-06-09T14:16:18.043Z'
source_kind: 'mcp:put_page'
tags:
  - architecture
  - hermes
  - infrastructure
  - vault
---

# Hermes Vault Architecture

## Layout and Storage Model

The Hermes knowledge base (vault) lives at `/opt/hermes/vault/`. The workspace for messaging and temporary work is at `/opt/hermes/workspace/`. These are two separate filesystem roots.

**Vault structure:**
- `projects/` — project folders (12+ active, each with `_index.md`)
- `sources/` — external content sources
- `people/` — person/entity profiles
- `topics/` — topic-driven knowledge clusters
- `concepts/` — concept stubs and synthesis
- `daily/` — timestamped daily notes
- `processes/` — operational procedures and runbooks
- `wiki/` — reference documentation (this page)
- `companies/` — organization profiles
- `media/` — media assets and references
- `research/` — research papers and findings
- `_meta/` — system metadata
- `_attachments/` — binary assets (PDFs, images, etc.)

## The 2026-06-09 Structural Fix

### The Problem

Earlier today, writes via native file tools (write_file, patch, etc.) were silently landing in `/opt/hermes/workspace/` instead of `/opt/hermes/vault/`, even though the user intended vault writes. The bot appeared to succeed ("✓ saved"), but the operator could not find the pages in later queries. This silent misdirection made it unclear whether the bot was hallucinating success or whether a path resolution issue was at play.

### The Solution

Three changes landed simultaneously:

1. **Symlink bridge** — All 13 vault top-level directories (`projects`, `sources`, `people`, `topics`, `concepts`, `daily`, `processes`, `wiki`, `companies`, `media`, `research`, `_meta`, `_attachments`) are now symlinks from `/opt/hermes/workspace/` pointing back to `/opt/hermes/vault/`. A write to `workspace/projects/foo/` now lands in `vault/projects/foo/` transparently.

2. **Wrapper script** — `/usr/local/bin/gbrain-serve-vault` is the canonical entry point for running `gbrain serve`. It pins the working directory to `/opt/hermes/vault` before invoking gbrain, ensuring the local brain instance always serves from the vault root, never the workspace.

3. **Project folder migration** — All 12 active projects migrated from the sibling-file pattern (`projects/project-name.md`) to the folder + `_index.md` convention (`projects/project-name/_index.md`), matching the Hermes folder-structure convention. This enables hierarchical sub-pages (e.g., `projects/project-name/milestones.md`, `projects/project-name/resources.md`).

## Going-Forward Conventions

### Writing to the Vault

**Prefer `put_page` for vault content.** It triggers gbrain's built-in enrichment pipeline (chunking, embedding, backlink extraction) immediately. When `put_page` is the right tool, use it.

`write_file` works correctly as a fallback for edge cases (e.g., editing generated files, template rendering), but it does not trigger enrichment until the next `gbrain sync` or embed job.

### Entity Structure

**First-class entities** (a project with sub-pages, a person with biography + timeline, a topic with multiple subtopics) belong in a **folder + `_index.md`** structure:

```
vault/projects/invisico/
  _index.md           (main project page, linked as projects/invisico)
  timeline.md         (project milestones)
  resources.md        (links, docs, media)
  team.md             (people involved)

vault/people/alice-example/
  _index.md           (biography, bio)
  timeline.md         (career events)
  takes.md            (beliefs, commitments)

vault/topics/machine-learning/
  _index.md           (overview)
  large-language-models.md
  training-techniques.md
```

This convention allows wikilinks and backlinks to naturally resolve to the `_index.md` when referencing the entity by its folder name.

### Scratch and Temporary Work

Scratch and temporary work always goes to `/opt/hermes/workspace/scratch/`. Never create scratch content under any vault-prefix directory name (e.g., not `vault/scratch/`, not `workspace/projects/scratch/`). The workspace's scratch folder is the canonical dump zone for throwaway experiments, prototypes, and transient notes.

## Diagnostics

### Missing Symlinks

If you ever see a write succeed (tool returns ✓ and a filepath) but a future `gbrain query` or `get_page` call cannot find the content, suspect a **missing symlink**.

**Check:**
```bash
ls -la /opt/hermes/workspace/ | grep ' -> '
```

All 13 top-level vault directories should appear as symlinks (`->`). If one is missing, the write may have landed in a real workspace subdirectory instead of the vault.

**Fix:** Recreate the symlink:
```bash
cd /opt/hermes/workspace
ln -s /opt/hermes/vault/<dir> <dir>
```

Then move any accidentally-written files back to vault:
```bash
mv /opt/hermes/workspace/<dir>/* /opt/hermes/vault/<dir>/
```

## Implementation Details

- **Symlink atomicity:** Symlinks are created at system setup time and checked during `gbrain sync` health phases.
- **gbrain-serve-vault:** Defined in system PATH, invoked by CI/cron jobs and local testing. Always use this entry point, never `gbrain serve` directly from workspace.
- **Project migration:** Completed for all 12 active projects on 2026-06-09. Sibling `.md` files were consolidated into folders with `_index.md` + optional sub-pages.

## References

- [Hermes Vault Operations](wiki/hermes-vault-operations) — day-to-day vault workflow
- [Project Folder Structure](wiki/project-folder-structure) — naming, tagging, and organization conventions
- [Brain Ingestion](wiki/brain-ingestion) — putting content into gbrain correctly
