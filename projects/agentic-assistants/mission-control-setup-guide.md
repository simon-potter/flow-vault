---
type: implementation
title: Mission Control Setup Guide
parent: projects/agentic-assistants
status: active
ingested_via: 'mcp:put_page'
ingested_at: '2026-06-12T05:55:11.182Z'
source_kind: 'mcp:put_page'
---

# Hermes Mission Control: Installation & Usage

**Video Source:** [[hermes-mission-control-video|Hermes Mission Control is INSANE!]]  
**Status:** Production-ready (built into Hermes Agent)  
**Access:** Dashboard running as part of Hermes gateway

## What is Hermes Mission Control?

A **dashboard + execution log viewer** that provides full transparency into AI agent workflows. Instead of seeing only the final answer, you see:

- Every prompt sent
- Every tool call made and its result
- Failures, retries, and model switches
- Memory accessed
- Context compression steps
- The complete journey from task start to finish

This solves the **black box problem** — when agents fail, you can pinpoint exactly which step went wrong instead of guessing.

## Installation

Hermes Mission Control is **built into Hermes Agent**. It's not a separate tool.

### Step 1: Install Hermes Agent

**Quick install (Linux/macOS/WSL):**
```bash
curl -fsSL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh | bash
```

**On Windows:**
```powershell
# Add to PowerShell $PROFILE or run manually:
curl -fsSL https://github.com/NousResearch/hermes-agent/releases/latest/download/hermes-windows-latest.exe -OutFile hermes.exe
# Then move hermes.exe to a folder in PATH
```

**From source (for contributors):**
```bash
git clone https://github.com/NousResearch/hermes-agent.git
cd hermes-agent
python3 -m pip install -e .
hermes setup  # Interactive configuration wizard
```

**Verify installation:**
```bash
hermes --version
hermes doctor  # Check dependencies and config
```

### Step 2: Configure Hermes Agent

Run the interactive setup:
```bash
hermes setup
```

You'll be prompted to:
1. **Choose a model/provider** — OpenRouter (recommended), Anthropic, OpenAI, DeepSeek, Nous Portal, GitHub Copilot, or local models
2. **Set API key(s)** — credentials will be stored in `~/.hermes/.env` (encrypted at rest)
3. **Choose terminal backend** — local (default), Docker, SSH, etc.
4. **Enable tools** — web search, file access, code execution, vision, etc.

**Quick config check:**
```bash
hermes config show
hermes config edit  # Opens config.yaml in $EDITOR
hermes auth list    # Check stored credentials
```

### Step 3: Start the Gateway (Optional, for Messaging Platforms)

Hermes Mission Control works in two ways:

1. **CLI mode** — use Hermes directly in your terminal: `hermes chat`
2. **Gateway mode** — run Hermes as a background service connected to Telegram, Discord, Slack, email, etc.

For **gateway + dashboard access**, start the gateway:

```bash
# Foreground (testing)
hermes gateway run

# Background service (production)
hermes gateway install
hermes gateway start
hermes gateway status
```

Check if running:
```bash
hermes gateway status
# Output: hermes-gateway is running (PID 12345)
```

View logs:
```bash
tail -f ~/.hermes/logs/gateway.log
```

## Using Hermes Mission Control

### Basic Usage: CLI Chat

**Interactive mode (default):**
```bash
hermes
```

Type prompts naturally. Hermes shows:
- Tool calls in real-time
- Results as they arrive
- Any errors or retries
- Final answer

Type `/help` to see commands.

**Single query (one-shot):**
```bash
hermes chat -q "Research SEO trends and summarize in 100 words"
```

### Accessing the Dashboard

**When mission control runs (visual execution log):**

Hermes shows the full execution flow inline in the terminal:

```
>>> Task: "Build a CLI tool for Hermes"

[1] 🔍 Searching web for best CLI frameworks in Python...
    → Found: Click, Typer, Argparse
    
[2] 📖 Reading Click documentation
    → Retrieved 12KB of docs
    
[3] ✍️  Drafting a hello-world CLI
    → Generated 45 lines of Python
    
[4] ✅ Checking code syntax
    → No errors
    
[5] 🎯 Final Answer: "Here's a CLI tool using Click..."
```

Each step is expandable — click or navigate to see full tool input/output, timestamps, and model decisions.

**Web dashboard (if message gateway is active):**

If you're running the gateway (`hermes gateway run`), the dashboard is available at:

```
http://localhost:8000/dashboard
```

This shows:
- Real-time agent execution stream
- All tasks spawned by the gateway
- Kanban board status (if using multi-agent coordination)
- Execution timeline with full audit log

Navigate to this URL in your browser.

### Command Examples

#### 1. Create a Task with Full Visibility

```bash
hermes chat -q "Analyze the top 10 AI startups and write a market report"
```

**What you see:**
- Web searches performed (and results)
- Which sources were read
- How the report was structured
- Any retries or model switches
- Final report

#### 2. Debug a Failed Task

```bash
hermes --continue  # Resume most recent session
```

Look at the execution log:
- **Where did it fail?** Exact step and error message
- **What was the input?** The exact prompt or tool call
- **What was the output?** The error or unexpected result
- **Can you retry just that step?** Yes — modify the prompt and run again

#### 3. Run in Kanban Mode (Multi-Agent)

If you're running multiple Hermes agents coordinating work:

```bash
hermes kanban list        # See all tasks
hermes kanban show TASK   # Inspect a task's execution + comments
```

Each task shows its complete journey, tool calls, and audit trail.

#### 4. Schedule a Recurring Task with Monitoring

```bash
hermes cron create "0 9 * * *" -p "Analyze overnight analytics and send summary"
```

Check saved runs:
```bash
hermes cron runs JOBID    # See all runs and their execution logs
```

Click any run to see the full mission control log.

## Key Features of Mission Control

### 1. **Full Execution Transparency**

See every decision the agent made:
- Prompts → LLM responses → tool calls → results → next prompt
- All model switches and why they happened
- All approvals (if human-in-the-loop is enabled)
- Memory retrieval and facts used

### 2. **Debugging & Root Cause Analysis**

When something goes wrong:
```
❌ Task failed at step 5:
   - Tool: web_search
   - Query: "OpenAI Q3 results"
   - Error: Search returned 0 results
   - Action: Agent retried with different keywords
```

Fix it faster because you know **exactly where** it broke.

### 3. **Pattern Detection**

Over time, you'll spot:
- Agents using the wrong tool repeatedly
- Unnecessary model switches (performance waste)
- Missed opportunities for caching/memory
- Specific prompts that cause failures

Example:
```
Agent made 12 web_search calls in this task,
but your memory already had 8 of those answers.
Suggestion: Improve memory retrieval prompt.
```

### 4. **Audit Trail**

Every execution is logged with:
- Timestamp
- Model used + cost
- Tools called
- Human approvals (if enabled)
- Final output

Useful for compliance, debugging, and optimization.

## Slash Commands (In Mission Control)

During an active chat session, use these to navigate the execution log:

```
/help                  Show all commands
/config                View current Hermes config
/model [name]          Show or change model
/tools                 Manage which tools are enabled
/skills list           Browse available skills
/retry                 Resend last message
/undo                  Undo last exchange
/rollback [N]          Restore a checkpoint
/agents                Show running tasks/agents
/goal [text]           Set a goal for Hermes to work on
```

## Configuration: Tuning Mission Control

Most settings are in `~/.hermes/config.yaml`:

```yaml
# Show full execution trace (vs. just the answer)
display:
  show_tool_calls: true
  tool_progress: true    # Real-time updates as tools run
  show_reasoning: true   # Show agent's thinking

# Logging
logging:
  level: info            # info | debug | warn | error
  save_transcripts: true # Save session history

# Approvals (human-in-the-loop for risky commands)
approvals:
  mode: manual           # manual | smart | off
```

**Change settings live:**
```bash
hermes config set display.show_tool_calls true
hermes /reset  # Restart session to apply
```

## Troubleshooting

### Mission Control Not Showing

**Problem:** You see only the final answer, not the execution log.

**Solution:**
```bash
hermes config set display.show_tool_calls true
hermes /reset
```

Then try again.

### Gateway Dashboard Not Loading

**Problem:** `http://localhost:8000/dashboard` returns 404.

**Solution:**
```bash
# Check if gateway is running
hermes gateway status

# If not running, start it
hermes gateway start

# Check logs for errors
tail -30 ~/.hermes/logs/gateway.log
```

### Tool Calls Not Appearing

**Problem:** Agent ran tools, but you don't see them in the log.

**Solution:**
```bash
# Enable verbose mode
hermes -v  # or /verbose in-session

# Or change config
hermes config set display.verbose full
```

### Agent Failing at Same Step

**Problem:** Task always fails at step 3 (e.g., parsing web results).

**Solution:**
1. Run in mission control mode to see the exact error
2. Read the tool output (the web results or API response)
3. Check if the tool call was correct or if the response was unexpected
4. Fix the prompt or add a validation step

Example debug query:
```bash
hermes chat -q "Debug this web search failure: when I search for 'AI companies', the agent fails to parse results. Why?"
```

## Integration with Your Projects

Link mission control logs to your agentic-assistants project:

**Add to any agent task:**
```bash
# Before running a task, enable logging
hermes --pass-session-id

# After task completes, save the execution log
hermes sessions export /tmp/session.jsonl
# or view it in the dashboard
hermes sessions browse
```

## Next Steps

1. **Install Hermes:** `curl -fsSL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh | bash`
2. **Run setup:** `hermes setup`
3. **Start using:** `hermes chat`
4. **Explore tools:** `hermes tools list` then enable what you need
5. **Set up gateway (optional):** `hermes gateway install && hermes gateway start`

## Resources

- **Official Docs:** https://hermes-agent.nousresearch.com/docs/
- **GitHub:** https://github.com/NousResearch/hermes-agent
- **CLI Reference:** `hermes --help` or https://hermes-agent.nousresearch.com/docs/reference/cli-commands
- **Skill Catalog:** `hermes skills browse` or https://hermes-agent.nousresearch.com/docs/reference/skills-catalog
- **Provider Setup:** `hermes model` or https://hermes-agent.nousresearch.com/docs/integrations/providers
- **Gateway/Messaging:** https://hermes-agent.nousresearch.com/docs/user-guide/messaging/

---

**Related Pages:**
- [[hermes-mission-control-video|Video: Hermes Mission Control is INSANE!]]
- [[tools-and-platforms|Tools & Platforms]] — Full Hermes ecosystem overview
- [[use-cases-and-improvements|Use Cases & Improvements]] — Real applications and roadmap
