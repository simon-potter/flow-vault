---
type: media
title: 'Claude Code Function Hooks: The Best Feature Yet'
date: '2026-08-19'
duration: ~45 minutes
presenter: Theo Browne (T3 Stack)
media_type: video
source_url: 'https://youtu.be/B-YQANvDOq0?is=W9Bj3ymtqtjfMmVr'
ingested_via: 'mcp:put_page'
ingested_at: '2026-09-06T07:41:16.127Z'
source_kind: 'mcp:put_page'
tags:
  - MondayMindBenders
---

# Claude Code Function Hooks: The Best Feature Yet

**Series:** #MondayMindBenders

**Presenter:** Theo Browne (T3 Stack)

**Focus:** Deep dive into Claude Code's new function hooks feature — the most powerful addition to Claude Code, solving existing hook limitations and enabling fine-grained control.

---

## Core Concept

**Function hooks = middleware for Claude Code**

Similar to Express.js middleware, function hooks intercept tool calls and allow you to:
- Rewrite input/output
- Short-circuit execution
- Add custom logic
- Customize UI in real-time
- Maintain persistent state across hooks

---

## Why Function Hooks?

### Problems with existing hooks:
- Can't rewrite prompts
- Can't append context from knowledge bases
- Can't draw UI elements, buttons, status lines
- Can't ask questions
- Can't add/edit tool descriptions
- No memory across hooks/sessions
- Context window degradation: rules fade over time as context fills

### Function hooks solve all of these

---

## Core Capabilities

### 1. **Input/Output Rewriting**
- Intercept tool calls
- Match against regex patterns
- Rewrite commands before execution

**Example:** Replace `npm install` with `pnpm install` to enforce consistent package manager usage

### 2. **Caching & Short-Circuiting**
- Check a store before making requests
- Return cached results if available
- Proceed normally if not cached

**Example:** Prevent re-fetching the same URL by returning cached response

### 3. **Tool Replacement/Interception**
- Override default Claude Code tools
- Route through custom implementations
- Fall back gracefully on failure

**Example:** Override built-in web search with Exa API, fallback to default if Exa fails

### 4. **UI Customization**
- Draw custom rows/panels in Claude Code UI
- Show live data updates
- Display deployment status, build progress, etc.

**Example:** Show Vercel deployment status with stages and elapsed time

### 5. **Persistent State Store**
- **Variable store:** In-memory, scoped per session/turn
- **Durable store:** Persists across sessions and restarts

### 6. **Model Calls Within Hooks**
- Call language models from hooks
- Use `$model` syntax
- Generate summaries, keywords, etc.

### 7. **Ask User & User Input**
- Pause execution and ask for confirmation
- Require approval before dangerous actions
- Validate user before proceeding

---

## Setup

```bash
cloud code enable function hooks=1
```

Then use `/plugin offering` command to generate function hooks through natural language

---

## Real-World Examples

### Example 1: Secret Redaction (Security)

**Goal:** Keep secrets out of session transcript while still using them

**Solution:**
1. Intercept user input
2. Detect high-entropy strings (secrets)
3. Store secret in in-memory variable store
4. Replace with ID in transcript
5. Rewrite tool calls to insert actual secret before execution

**Result:**
- Secrets never appear in transcript
- Secrets can still be used for API calls
- Secure by design (inspired by Infisical Agent Proxy)

### Example 2: Vercel Deploy Status UI

**Goal:** Monitor deployment live in Claude Code UI

**Solution:**
1. Create hook that polls Vercel API
2. Draw custom UI row showing status
3. Update in real-time (queued → building → ready)
4. Show elapsed time
5. Allow hiding/reshowing via button

**Result:** Deployment monitoring built into Claude Code interface

### Example 3: Dry Run Gate

**Goal:** Require dry run before production commands

**Solution:**
1. Block production commands until dry-run command runs
2. Show results first
3. Only allow real commands after approval

**Result:** Safe data analysis workflows

### Example 4: File Size Gate

**Goal:** Prevent massive files (2-3k lines)

**Solution:**
1. On file edit that exceeds 1,000 lines
2. Ask user if refactoring into smaller files is desired
3. Prevent auto-generation of unwieldy files

**Result:** Better code organization by default

### Example 5: Auto-Summary & Text-to-Speech

**Goal:** Get audio summary at end of each turn

**Solution:**
1. On turn end, call Haiku model to summarize
2. Use TTS to speak the summary
3. Use default Apple voice

**Result:** Hands-free status updates

### Example 6: Compliance Audit Trail

**Goal:** Log all Claude Code events for regulated industries (healthcare, payments)

**Solution:**
1. Intercept every event
2. Send to organization's log store
3. Maintain audit trail

**Result:** Regulatory compliance built-in

### Example 7: Email Newsletter Gate

**Goal:** Prevent accidental newsletter sends

**Solution:**
1. Block email send until user confirms via ask()
2. Require user to spend time reviewing
3. Verify approval before sending

**Result:** No accidental broadcasts

---

## Advanced Primitives

### Function Hook Building Blocks:
- **Model calls:** `$model` to invoke language models
- **HTTP calls:** `$http` for API queries
- **Clock:** Measure elapsed time between turns
- **Store:** Persistent state management
- **Ask:** Request user confirmation
- **UI elements:** Draw rows, buttons, panels
- **Tool registration:** Add custom tools
- **Tool overrides:** Replace default tools

---

## Plugin Offering Skill

Built-in skill for generating function hooks:

```bash
/plugin offering
```

Then describe what you want. Examples:
- "Block secrets from entering transcript"
- "Show Vercel deploy status"
- "Ask before editing files over 1000 lines"
- "Speak a summary at end of turn"

The skill generates 300+ lines of production-ready hook code

---

## Key Insights

1. **Deterministic control:** Function hooks give you fine-grained, explicit control over Claude Code behavior
2. **Shareable:** Hooks exist as plugins, easily shared with teams via GitHub
3. **Composable:** Combine multiple hooks for complex workflows
4. **Express.js pattern:** Familiar middleware paradigm for developers
5. **Game changer:** Most powerful Claude Code feature yet (Theo's opinion after testing)

---

## My Favorite Use Cases

1. **Security:** Secret redaction + management
2. **UI customization:** Live monitoring dashboards
3. **Approval gates:** Prevent dangerous operations
4. **Compliance:** Audit trails for regulated industries
5. **Workflow enforcement:** Dry-run gating, file size limits

---

## Migration from cloud.md

**Old approach:** Put rules and requirements in cloud.md
**New approach:** Convert cloud.md rules into well-defined function hooks

**Benefits:**
- Rules are enforced deterministically
- No context window degradation
- Easier to share and version control
- Clearer intent and behavior

---

## Theo's Bonus Content

- Agent Coding School lifetime deal closing (1 week remaining)
- Transitioning to cohort-based model for courses
- New Agent Sandboxing Infrastructure coming soon
- Enterprise training available for teams/organizations

---

## Related

- [[topics/cto|CTO Topic]] — Developer tooling and automation
- Claude Code advanced patterns
- Middleware and hook architectures
