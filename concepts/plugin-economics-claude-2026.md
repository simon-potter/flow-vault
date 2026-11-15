---
type: concept
title: >-
  You Should Start Selling Plug-ins Now — Building Plugin Economics for
  Claude/ChatGPT
source: https://www.youtube.com/watch?v=rgH2NibyrjY
source_format: video
channel: Devin Kearns
uploaded: '2026-11-13'
duration: '14:41'
words: 3630
source_kind: mcp:put_page
ingested_via: mcp:put_page
ingested_at: '2026-11-15T08:27:16.390Z'
trust_tier: external_untrusted
---

# You Should Start Selling Plug-ins Now

**Source:** [YouTube — Devin Kearns](https://www.youtube.com/watch?v=rgH2NibyrjY)  
**Format:** Video | **Duration:** 14:41 | **Uploaded:** 2026-11-13  
**Transcript:** Raw files saved at `/opt/hermes/workspace/media-raw/youtube-rgH2NibyrjY`

---

## Core Thesis

Building plugins for Claude and ChatGPT is the number one opportunity for builders RIGHT NOW instead of building standalone SaaS products.

**Why?** Claude and ChatGPT are eating the software stack—they're becoming the primary workspace where people work (alongside email and Slack). The distribution is already baked in. The UI is handled by the AI layer. You focus on the integrations and skills that extend what Claude/ChatGPT can do.

---

## Why Plugins vs. Standalone SaaS

### The Trend
- Claude, ChatGPT, and the AI ecosystem are **displacing entire product categories**
  - Google Docs → Claude artifacts
  - Google Workspace → Claude as the default workspace
  - Software CRMs → Claude with integrations
- **No moat advantage for standalone UI:** If your product relies on a separate interface/login, you lose the moment a foundational AI makes that redundant

### The Plugin Advantage
- **No front-end to maintain** — Claude/ChatGPT handle the UI
- **Reduced OpEx** — No customer onboarding calls, fewer logins, less infrastructure overhead
- **Built-in agentic harness** — You don't build a Claude clone; you extend Claude itself
- **Distribution is free** — Distribution comes through the AI platform users already use daily
- **You own the workflow** — What you own is the opinionated, irreducible workflow + the integrations that make it work

---

## The Plugin Structure: 3 Core Components

### 1. **Connections / Integrations**

Anything Claude doesn't have native access to:

- **Proprietary data sources** — LinkedIn, CRM data, email, internal systems
- **Hard-to-integrate platforms** — Ones with strict auth, rate limits, bot detection
- **The scaffolding layer** — You handle auth, rate limits, mode constraints that platforms impose

**Example:** LinkedIn has strict rate limits and bot protections. LinkUp API wraps those constraints so Claude can safely interact with LinkedIn without getting blocked.

**Value:** You make reliable, repeatable access to a hard platform easy for Claude.

### 2. **Skills / Workflows**

Pre-built, opinionated actions Claude can invoke:

- Don't require skills to have value (the integration alone can be enough)
- But skills multiply value by letting Claude immediately use integrations at their full capacity
- Example: LinkUp API has skills for "search connections", "leave comments", "build prospect lists"
- Customer doesn't need to be advanced; they just invoke the skill

**Optional: UI via Onboarding Prompt**
- Even if you don't build a UI, specify the dashboard/artifact UX you want in the onboarding prompt
- Claude creates the artifact; every time a skill runs, the artifact updates
- You get a UI by spec, not by building one

### 3. **Custom Models / Proprietary Functions** (Optional moat)

If you have a proprietary model or specialized capability:

- Bake it into the integration infrastructure as a skill/function
- Example: Fast invoice categorization via a custom JAX model
- The skill calls your model; results update the dashboard artifact
- **This becomes a moat** — Something only you can offer within the Claude ecosystem

---

## Three Real Examples

### 1. **Law OS (Legal Operating System)**

**Integrations:**
- Outlook + Clio (case management system)
- Webhooks for real-time event firing (vs. polling)

**Skills:**
- Document generation
- Case upkeep workflows
- Scheduling
- Sending emails
- Task list management

**Value:** Paralegals and attorneys work inside Claude. Claude has context of their entire Clio system, inbox, calendar. It can generate documents, schedule meetings, manage tasks—all from one interface.

**Unlock:** Massive efficiency for firms that standardize around Claude + this plugin.

---

### 2. **Content OS (Personal/Creator System)**

**Integrations:**
- YouTube analytics
- LinkedIn feed
- Slack (internal ideas)
- Email
- Transcripts of past brainstorms

**Skills:**
- Content research
- Scripting in your voice
- Video editing
- Performance analysis
- Posting / commenting

**Vision:** 
- User brainstorms ideas verbally
- Claude pulls in past conversations, transcripts, Slack threads, YouTube performance data
- Claude identifies patterns in what the creator talks about + what goes viral
- Claude suggests video topics/scripts optimized for both the creator's voice and audience resonance
- Result: Video ideas + scripts ready to post

**Outcome:** Creators work at 10x speed by having Claude as a collaborative AI partner that knows their entire body of work.

---

### 3. **Meeting OS (Organizational Coordination System)**

**Integrations:**
- Calendar
- Gmail
- Slack
- Meeting transcripts

**Skills:**
- Extract actionable tasks from conversations
- Assign tasks automatically
- Update project trackers/CRMs
- Schedule follow-up meetings
- Proactively execute tasks discussed

**Real Example:** Team discusses wanting to reach out to US manufacturers. System:
1. Captures the context (what is Antares? why manufacturers?)
2. Builds a prospect list automatically
3. Sends outreach emails
4. Books meetings on the calendar

**Outcome:** Strategy session happens. System does all the legwork. Next week, calendar is full of booked calls. No busywork required.

---

## Key Insight: Data Origin Matters

The most valuable, actionable data in organizations originates from:

1. **Conversations** — Slack, email, meetings
2. **Transcripts** — Meeting recordings
3. **Documents** — Things people write down
4. **Real-time collaboration data** — The point of origin where ideas are first shared

**If you can capture this data + connect it to Claude + give Claude the skills to act on it → you have a machine that executes work.**

This is not sci-fi. It's happening now.

---

## The Future (2027+)

**Prediction:** Every business will operate with an AI layer as the prime executor of work, especially in white-collar roles.

**For builders right now:**
- Ask: "What unique capability can I give Claude that adds value?"
- Ask: "What skills let Claude take advantage of that capability?"
- **That's your plugin.**

---

## Strategic Takeaway for Simon

Given your Spottmedia portfolio (Invisico, Mediary, Teach Plus, LogiSpot):

1. **Invisico as a plugin** — Could be a Claude skill that runs your counselor logic + returns structured decision frameworks
2. **Mediary as a plugin** — Could be integrations + skills that let Claude query trust state while deciding on vendors/partners
3. **Teach Plus as a plugin** — Could be integrations into course platforms + skills for content generation, grading, student feedback
4. **LogiSpot as plugin infrastructure** — The compliance + security layer underlying the others

The plugin model aligns with your thesis: **AI as wisdom infrastructure**. Plugins let you channel wisdom (your opinionated workflows) through Claude rather than building a separate product.

---

## Related

- [[concepts/ai-side-hustles/top-10-claude-ranked]] — Complementary: Side hustles via Claude
- [[projects/spottmedia-philosophy]] — Strategic alignment with Spottmedia's wisdom-channeling mission
