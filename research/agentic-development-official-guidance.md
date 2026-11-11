---
type: concept
title: >-
  Agentic Development: Official Guidance from Anthropic, OpenAI, GitHub &
  Industry Leaders
date: '2026-11-11'
source_kind: mcp:put_page
ingested_via: mcp:put_page
ingested_at: '2026-11-11T13:57:33.404Z'
trust_tier: agent_written
tags:
  - agentic-development
  - industry-standards
  - official-guidance
  - thought-leaders
---

## Overview

These are the **official methodologies** endorsed by Anthropic, OpenAI, GitHub, and established thought leaders. High-credibility sources with production deployments.

---

## 1. **Anthropic: Claude Code + Agent SDK** ⭐ Official Standard

**Official Source:** https://code.claude.com/docs/en/how-claude-code-works.md

**Published by:** Anthropic (the company that created Claude)

### The Core Loop

All agentic work follows this loop:

```
Gather Context → Take Action → Verify Results → Repeat
```

### Best Practices from Anthropic

**Source:** https://claude.com/resources/articles/building-agents-with-the-claude-agent-sdk

1. **Delegate, don't dictate** — Give context and direction, let Claude figure out details
2. **Gather Context Effectively** — Let agent search/fetch context dynamically
3. **Verify Work Continuously** — Tests/linters at every step, real feedback
4. **Externalize State** — Use repos, files, docs as externalized state
5. **Iterate on Tool Design** — If agent fails, improve the tools available to it

---

## 2. **OpenAI: Codex — Long-Horizon Agentic Tasks**

**Official Source:** https://developers.openai.com/blog/run-long-horizon-tasks-with-codex

**Key Shift:** This is not just "models got smarter." Agents can stay coherent for LONGER, completing larger chunks of work end-to-end.

### Codex Loop (Production Pattern)

```
1. Plan
2. Edit code
3. Run tools (tests/build/lint)
4. Observe results
5. Repair failures
6. Update docs/status
7. Repeat
```

### Best Practices for Long-Horizon Work

1. **Spec File** (externalized intent)
   - Write target + constraints as markdown
   - Agent revisits repeatedly

2. **Plans.md** (checkpointed milestones)
   - Break into completion steps with AC
   - Agent verifies each step

3. **Implement.md** (runbook)
   - How agent should operate
   - Enforces discipline

4. **Continuous Verification**
   - Tests/lint/typecheck at every step

5. **Live Status Log**
   - documentation.md keeps run inspectable
   - Enables mid-course corrections

### Case Study: 25-Hour Codex Run

Codex ran a blank repo for 25 hours (13M tokens, ~30k lines) building a full design tool, stayed coherent entire time, verified continuously.

---

## 3. **GitHub: Agentic Engineering Workflow** ⭐ Practical Framework

**Official Source:** https://github.blog/ai-and-ml/github-copilot/beyond-code-generation-a-developers-guide-to-agentic-engineering/

**Problem:** Coding got 400% faster. PRs now spend 441% longer in review. Agents need to help the entire workflow, not just coding.

### The 4-Phase Workflow

#### **Phase 1: Plan**
- Copilot pulls scattered context into one place
- Team discusses tradeoffs
- Creates GitHub Issues with AC + plan
- **Output:** Reviewable plan, explicit AC

#### **Phase 2: Build**
- Agents work on isolated copies of repo
- No shared working tree conflicts
- Iterate: code → build → test → fix
- **Output:** Clean diff, implementer notes

#### **Phase 3: Verify**
- Copilot reviews against team standards
- GitHub Code Quality catches lint before human review
- Async code review (4 hour SLA)
- **Output:** Quality-gated PR

#### **Phase 4: Observe**
- After release, Copilot connects dashboards/commits
- Documents findings, creates follow-ups
- Lessons inform next cycle
- **Output:** Production insights

---

## 4. **Jesse Vincent: Superpowers Framework** ⭐ Industry Thought Leader

**Authority:** Creator of Request Tracker; CEO of Prime Radiant (AI research lab)

**Framework:** Superpowers — 500k+ installs, top 50 GitHub repos in AI-assisted development

**Featured:** O'Reilly + Tim O'Reilly ("Superpowers: meta-skills for how agents think")

### Core Philosophy

**Key Insight:** "Claude tries to rationalize skipping structured processes. Superpowers encodes discipline so agents can't ignore instructions."

### Skills (Reusable Workflows)

```
Brainstorming  → Socratic dialogue to clarify intent
Writing Plans  → Break into tasks with AC
Executing      → Run plan with review checkpoints
TDD            → Write tests before code
Debugging      → Systematic diagnosis
Review         → Validate against requirements
Verify         → Run tests before "done"
```

### Discrete Phases (Don't Let Agents Skip Ahead)

1. **Brainstorming** — Clarify what you REALLY want (can take hours)
2. **Planning** — Detailed task breakdown with context
3. **Execution** — Subagent-driven with isolated context

### Quality Loops

```
1. Spec Review (1st pass) — Implement everything asked?
2. Spec Review (2nd pass) — Fresh agent (catches different errors)
3. Code Quality Review — Separate fresh agent
4. Repeat until approval
```

### Why Fresh Agents Each Time

Each agent's hallucinations are different. Second opinion catches errors first agent missed.

---

## 5. **Sarah Drasner: The Agentic Web** ⭐ Strategic Vision

**Authority:** Distinguished Engineer at Google; Area Tech Lead for AI and Web Ecosystem

**Conference:** Keynote at AGNTCon + MCPCon North America 2026

**Topic:** Web is transitioning from human-navigated to agent-navigated. Requires new interaction patterns (WebMCP, MCP) and security models.

---

## Consensus Across All Authorities

✅ **Tests/Verification are CONTINUOUS, not afterthought**

✅ **Externalize State** — Repo, files, docs, status logs help agents maintain clarity

✅ **Steerability > Autonomy** — Agent works unattended but you can interrupt anytime

✅ **Skills/Runbooks Encode Methodology** — Not long prompts, but reusable workflows

✅ **Git Worktrees for Parallelism** — Each agent gets isolated checkout, no merge conflicts

✅ **Multiple Review Passes** — Spec review → code quality → fresh verification

✅ **TDD + Red-Green-Refactor** — Tests LOCKED, code must pass unchanged

---

## For Your 4-Person Team: Reading Order

1. **Anthropic's Claude Code docs** — Build your mental model of the agent loop
   - https://code.claude.com/docs/en/how-claude-code-works.md

2. **Jesse Vincent + Tim O'Reilly** — Understand how to encode methodology
   - https://www.oreilly.com/live-events/give-your-agents-superpowers-jesse-vincent-live-with-tim-oreilly/0642572444747/

3. **OpenAI's long-horizon task guide** — See full end-to-end workflow (spec + plans + runbook)
   - https://developers.openai.com/blog/run-long-horizon-tasks-with-codex

4. **GitHub's 4-phase workflow** — Adapt to your team's process
   - https://github.blog/ai-and-ml/github-copilot/beyond-code-generation-a-developers-guide-to-agentic-engineering/

---

## Direct Links (All Authoritative)

| Source | Link |
|---|---|
| Anthropic (Official Loop) | https://code.claude.com/docs/en/how-claude-code-works.md |
| Anthropic (Best Practices) | https://claude.com/resources/articles/building-agents-with-the-claude-agent-sdk |
| OpenAI (Long-Horizon) | https://developers.openai.com/blog/run-long-horizon-tasks-with-codex |
| GitHub (Team Workflow) | https://github.blog/ai-and-ml/github-copilot/beyond-code-generation-a-developers-guide-to-agentic-engineering/ |
| Jesse Vincent (Video) | https://www.oreilly.com/live-events/give-your-agents-superpowers-jesse-vincent-live-with-tim-oreilly/0642572444747/ |
| Jesse Vincent (Podcast) | https://www.heavybit.com/library/podcasts/open-source-ready/ep-36-managing-ai-coding-agents-with-jesse-vincent |
