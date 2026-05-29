# ADHD-OS Stack Expansion: Alternatives & Sovereignty

> Detailed research on alternative backends, with recommendations for privacy-first, sovereign, and multi-provider stacks

---

## Part 1: Privacy-First LLM Alternatives

### The Case for Local Reasoning Models

**Problem with closed-source APIs:**
- Data sent to external servers (privacy concern for ADHD notes, personal tasks)
- Cost accumulates with high-volume queries
- Dependency on vendor availability (API outages, rate limits)

**Solution: Open-source reasoning models**
- Run locally via Ollama (no external calls)
- MIT/Apache 2.0 licensed (no licensing costs)
- Equivalent or better reasoning than commercial alternatives

### Recommended Models (2025–2026)

| Model | License | Reasoning | Size | Speed | Sovereignty | ADHD Fit |
|-------|---------|-----------|------|-------|-------------|----------|
| **DeepSeek R1** | MIT | Excellent | 32B/70B | Fast | ✅ Full local | ⭐⭐⭐ Best |
| **Qwen3** | Apache 2.0 | Good | 7B/32B/70B | Very fast | ✅ Full local | ⭐⭐⭐ Best |
| **Phi-4-reasoning** | MIT | Excellent | 14B | Very fast | ✅ Full local | ⭐⭐ Good (specialized) |
| **Mistral 3.1** | Open-weight | Good | 7B/32B | Very fast | ✅ Full local | ⭐⭐ Good |
| **Hermes 4.3** | Apache 2.0 | Good | Various | Fast | ✅ Full local | ⭐⭐ Good |

### Setup: Running Local Models via Ollama

```bash
# Install Ollama (https://ollama.ai)
# Then pull a model:

ollama pull deepseek-r1  # Best reasoning, ~7GB
# or
ollama pull qwen3  # Balanced, ~13GB
# or
ollama pull phi-4  # Lightweight reasoning, ~7GB

# Verify it's running:
curl http://localhost:11434/api/tags | jq '.models | map(.name)'
```

**Integration with ADHD-OS:**
- Replace Claude API calls with local inference
- Zero latency after model loads
- Works offline
- Cost: only your electricity

**Trade-off:** Local models are slower than commercial APIs (5-10s vs. 1-2s), but reasoning quality is comparable. For ADHD workflows, slower local inference beats fast cloud services if privacy is the priority.

**Recommendation:** Start with **Qwen3 (32B)** — best balance of speed + reasoning + resource usage on Mac.

---

## Part 2: Calendar & Time Management Alternatives

### Comparison Matrix

| Service | API | Self-Hosted | CalDAV | Web UI | Mobile | ADHD Fit |
|---------|-----|-------------|--------|--------|--------|----------|
| **Nextcloud Calendar** | ✅ REST + CalDAV | ✅ Yes | ✅ Native | ✅ Excellent | ✅ Mobile | ⭐⭐⭐ Best |
| **Apple Calendar** | ⚠️ CalDAV only | ❌ No | ✅ Native | ⚠️ Limited | ✅ Native | ⭐⭐ Works (friction) |
| **Google Calendar** | ✅ CalDAV + REST | ❌ No | ✅ Native | ✅ Excellent | ✅ Native | ⭐⭐ Current (cloud) |
| **Microsoft Outlook** | ❌ No CalDAV | ❌ No | ❌ No | ✅ Good | ✅ Good | ⭐ Not recommended |
| **Proton Calendar** | ❌ No (requested) | ❌ Cloud | ❌ No | ✅ Good | ✅ Good | ⭐ Not recommended |

### Nextcloud Calendar: The Sovereign Option

**What it is:** Self-hosted calendar server with full API control

**Setup (Docker):**
```bash
docker run -d \
  -v nextcloud_data:/var/www/html \
  -p 8080:80 \
  -e NEXTCLOUD_ADMIN_USER=admin \
  -e NEXTCLOUD_ADMIN_PASSWORD=password \
  nextcloud:latest

# Install Calendar app via Nextcloud web UI
# Access at: http://localhost:8080
```

**API Access:**
```bash
# Create calendar via REST API
curl -u admin:password http://localhost:8080/remote.php/dav/calendars/admin/personal/ \
  -X MKCALENDAR \
  -H "Content-Type: application/xml" \
  -d '<?xml version="1.0"?><mkcalendar xmlns="DAV:"><set><prop><displayname>ADHD-OS</displayname></prop></set></mkcalendar>'

# Use CalDAV in your agent/app:
# URL: http://localhost:8080/remote.php/dav/calendars/admin/personal/
# Auth: Basic (admin:password)
```

**Features 2025:**
- Built-in meeting detection and scheduling
- Timezone-aware
- Color-coded calendars
- Integration with Obsidian plugins (if you use CalDAV client)
- Mobile app (via CalDAV sync)

**ADHD Benefit:**
- Full control (runs on your machine)
- No data sent to external services
- API access for agent integration
- Pair with visible time tracking in Obsidian daily notes

### Apple Calendar: Works, But API Friction

**Pros:**
- Native macOS/iOS integration
- Excellent UX (native reminders, notifications)
- Syncs across Apple devices

**Cons:**
- No official REST API (only CalDAV)
- Basic auth is fragile (requires app-specific password)
- Limited programmatic control

**If you use Apple Calendar:**
```bash
# CalDAV URL: https://p12-caldav.icloud.com
# Auth: Basic (Apple ID + 16-char app-specific password)

# Via tsdav (JavaScript/TypeScript library):
npm install tsdav

# Then in your ADHD-OS agent:
import { DAVClient } from 'tsdav';

const client = new DAVClient({
  serverUrl: 'https://p12-caldav.icloud.com',
  credentials: {
    username: 'your-apple-id@icloud.com',
    password: 'xxxx-xxxx-xxxx-xxxx'
  }
});

// Fetch events, create reminders, etc.
```

**Recommendation:** Use Nextcloud if sovereignty is priority. Apple Calendar if you prefer native ecosystem + accept API friction.

---

## Part 3: Agent Frameworks & Orchestration

### Framework Comparison (2025)

| Framework | Maturity | Code | Best For | Community | ADHD Fit |
|-----------|----------|------|----------|-----------|----------|
| **LangChain + LangGraph** | Production (v1.0) | Python/JS | Fine-grained control, custom logic | Very large | ⭐⭐⭐ Best |
| **CrewAI** | Growing (280% adoption 2025) | Python | Role-based agents, predefined workflows | Growing | ⭐⭐⭐ Best (alternative) |
| **AutoGPT** | Prototype | Python | Open-ended exploration | Community | ⭐⭐ Prototyping |
| **n8n** | Mature | Low-code/visual | Team automation, workflows | Large | ⭐⭐ Visual alternative |
| **Make.com** | Mature | No-code | Cloud automation | Large | ⭐ Cloud-only (not sovereign) |

### LangChain + LangGraph: Fine-Grained Control

**Best for:** Custom ADHD-OS agents with specific task routing, context management, tool chains

**Example: ADHD Task Router Agent**

```python
from langgraph.graph import StateGraph
from langchain_community.llms import Ollama  # Local Qwen3
from langchain.tools import tool

# Define tools
@tool
def capture_thought(text: str) -> str:
    """Capture thought to Obsidian inbox"""
    return f"Thought captured: {text}"

@tool
def route_to_kanban(text: str, priority: str) -> str:
    """Route captured thought to Kanban board"""
    return f"Added to Kanban {priority}: {text}"

@tool
def check_time_remaining() -> str:
    """Check time remaining in current task block"""
    # Read from daily note or calendar
    return "2 hours remaining in current task"

# Define agent state
from typing import TypedDict, List

class AgentState(TypedDict):
    messages: List[str]
    current_task: str
    inbox_items: List[str]
    kanban_status: str

# Build agent graph
graph = StateGraph(AgentState)

def agent_logic(state: AgentState):
    """Main agent reasoning loop"""
    model = Ollama(model="qwen3", base_url="http://localhost:11434")
    
    # Decide: capture, route, or continue current task?
    decision = model.invoke(f"""
    You are an ADHD task management agent.
    Current task: {state['current_task']}
    New inbox items: {state['inbox_items']}
    
    Should you:
    1. Capture the new items to inbox
    2. Route them to Kanban (if urgent)
    3. Defer them (continue current task)
    
    Reason through it, then decide.
    """)
    
    return {"messages": [decision]}

graph.add_node("agent", agent_logic)
graph.set_entry_point("agent")

# Run agent
compiled = graph.compile()
result = compiled.invoke({
    "messages": [],
    "current_task": "Writing documentation",
    "inbox_items": ["React 19 perf check", "Call dentist"],
    "kanban_status": "Current: [Writing docs]"
})
```

**ADHD-Specific Patterns with LangGraph:**
- **Loop-breaking:** Agent watches for error repetition, suggests diagnosis
- **Hyperfocus protection:** Agent monitors time blocks, suggests breaks
- **Working memory:** Agent maintains session context, writes notes
- **Time blindness:** Agent tracks elapsed time, sends reminders

### CrewAI: Role-Based Agents (Alternative)

**Best for:** If you think in terms of agent *roles* (researcher, writer, reviewer)

```python
from crewai import Agent, Task, Crew

# Define agents as roles
researcher = Agent(
    role="Research Agent",
    goal="Find and synthesize information",
    backstory="You are an expert at deep research and synthesis",
    llm="ollama",  # Use local Ollama
    max_tokens=2000
)

writer = Agent(
    role="Writing Agent",
    goal="Write clear, ADHD-friendly documentation",
    backstory="You are an expert technical writer",
    llm="ollama"
)

# Define tasks (what each agent does)
research_task = Task(
    description="Research the topic: {topic}",
    expected_output="Structured research findings",
    agent=researcher
)

writing_task = Task(
    description="Write documentation based on research",
    expected_output="Clear, well-structured document",
    agent=writer
)

# Crew orchestrates the workflow
crew = Crew(
    agents=[researcher, writer],
    tasks=[research_task, writing_task]
)

result = crew.kickoff(inputs={"topic": "ADHD and working memory"})
```

**ADHD Benefit:** Familiar mental model (like delegating tasks to people). Less low-level control than LangChain, but faster to set up for standard workflows.

---

## Part 4: Communication Channels for Agents

### Comparison Matrix

| Channel | API | Real-Time | Privacy | Sovereignty | ADHD Fit |
|---------|-----|-----------|---------|-------------|----------|
| **Telegram** | ✅ Official | ✅ Webhook | Cloud | ⭐ Good | ⭐⭐⭐ Best |
| **Discord** | ✅ Official | ✅ Websocket | Cloud | ⭐ Good | ⭐⭐⭐ Best (team) |
| **Matrix/Element** | ✅ Official | ✅ Real-time | Self-hosted | ⭐⭐⭐ Excellent | ⭐⭐⭐ Sovereign |
| **Signal** | ⚠️ Unofficial | ✅ Real-time | E2E encrypted | ⭐⭐ Community | ⭐⭐ High-security |
| **Email (Webhooks)** | ✅ Custom | ⚠️ Async | Depends | ⭐ Varies | ⭐⭐ Async notifications |

### Telegram: Stable, Official API

**Setup:**
```bash
# 1. Create bot via BotFather (@BotFather on Telegram)
# 2. Get API token: 123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11

# 3. Run agent bot (Python)
pip install python-telegram-bot

from telegram import Update
from telegram.ext import Application, CommandHandler, MessageHandler, filters

async def start(update: Update, context):
    await update.message.reply_text("ADHD-OS Agent ready. Send me tasks!")

async def handle_message(update: Update, context):
    user_message = update.message.text
    # Route to ADHD-OS agent logic
    response = await adhd_agent(user_message)
    await update.message.reply_text(response)

app = Application.builder().token("YOUR_TOKEN").build()
app.add_handler(CommandHandler("start", start))
app.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, handle_message))

app.run_polling()
```

**ADHD Benefit:**
- Simple, stable API
- No setup required (just send messages)
- Notification-friendly (high reliability)
- Works on any device (cross-platform)

### Matrix/Element: Sovereign & Encrypted

**What it is:** Federated, open-source chat protocol (like email for messaging)

**Self-hosted setup:**
```bash
# 1. Run Synapse (Matrix homeserver) via Docker
docker run -d \
  -v matrix_data:/data \
  -p 8008:8008 \
  -e SYNAPSE_SERVER_NAME=adhd-os.local \
  -e SYNAPSE_REPORT_STATS=no \
  matrixdotorg/synapse:latest

# 2. Access at http://localhost:8008
# 3. Create user for agent bot
# 4. Use matrix-bot-sdk for agent integration
```

**Agent Integration (JavaScript):**
```javascript
const { MatrixClient, SimpleFsStorageProvider, AutojoinRoomsMixin } = require('matrix-bot-sdk');

const storage = new SimpleFsStorageProvider("./bot.json");
const client = new MatrixClient("http://localhost:8008", "@adhd-agent:adhd-os.local", "password");

client.on("room.message", async (roomId, event) => {
    if (event.content.msgtype !== "m.text") return;
    
    const message = event.content.body;
    const response = await adhd_agent(message);
    
    await client.sendMessage(roomId, {
        msgtype: "m.text",
        body: response
    });
});

await client.start();
```

**ADHD Benefit:**
- Full sovereign control (runs on your machine)
- E2E encryption (privacy)
- Federated (can bridge to other networks)
- Growing adoption in government (35+ countries)

### Email Webhooks: Async Notifications

**New option (2025): AgentMail**

```bash
# AgentMail: Email API for AI agents ($6M seed funding, Mar 2026)
# Allows agents to send/receive emails programmatically

pip install agentmail

from agentmail import EmailAgent

agent = EmailAgent(api_key="your_key")

# Send email from agent
agent.send_email(
    to="your-email@example.com",
    subject="ADHD-OS Reminder: Weekly review due",
    body="It's Friday. Time to review your Kanban board."
)

# Receive webhook when user replies
@agent.on_reply
async def handle_reply(email_content):
    # Process user's email reply as task input
    task = parse_email_as_task(email_content)
    return await adhd_agent(task)
```

**ADHD Benefit:**
- Async (no real-time requirement)
- Universal (works on any email client)
- Integrates all stacks (you keep existing email)
- Searchable archive (important for context)

---

## Part 5: Recommended Stack Configurations

### Configuration 1: Maximum Sovereignty (Private + Local)

**For:** Users who want zero external dependencies

```
Memory:         Obsidian + Git (local)
Calendar:       Nextcloud Calendar (self-hosted)
LLM:            Qwen3/DeepSeek R1 via Ollama (local)
Agent:          LangChain + LangGraph (local Python)
Communication:  Matrix/Element (self-hosted)
Notifications:  Email (self-hosted, or public SMTP)
```

**Setup:** All running on your Mac Mini, no external services except Git backup (GitHub private repo, optional)

**Cost:** ~$0 (just your hardware + electricity)  
**Privacy:** Maximum (nothing leaves your machine except optional Git backup)  
**Latency:** Higher (5-10s for local inference)  
**Maintenance:** Higher (self-hosting requires management)

**ADHD Fit:** ⭐⭐⭐ If you prioritize privacy over convenience

---

### Configuration 2: Balanced (Sovereign + Practical)

**For:** Users who want privacy + reasonable convenience

```
Memory:         Obsidian + Git (local + GitHub backup)
Calendar:       Nextcloud Calendar (self-hosted) OR Apple Calendar (native)
LLM:            Claude API (cloud, trusted provider) + Ollama fallback
Agent:          LangChain (local, Python)
Communication:  Telegram Bot (official API, simple)
Notifications:  Calendar reminders + Telegram messages
```

**Setup:** Mix of local (Obsidian, Ollama for fallback) + trusted cloud (Claude API, Telegram)

**Cost:** ~$5-10/month (Claude API usage)  
**Privacy:** Good (Claude sees task descriptions, but no personal files)  
**Latency:** Fast (1-2s with Claude)  
**Maintenance:** Low (Telegram requires no setup, Nextcloud optional)

**ADHD Fit:** ⭐⭐⭐ Best balance for most users

---

### Configuration 3: Team Collaboration (Shared Stack)

**For:** Multiple humans + agents working together

```
Memory:         Notion (team-friendly, shared)
Calendar:       Google Calendar (shared, calendar views)
LLM:            Claude API (team access via shared account)
Agent:          CrewAI (role-based teams, Hermes Discord bot)
Communication:  Discord (team channel, bot responses visible)
Notifications:  Calendar + Discord
```

**Setup:** Centralized platforms, team members see shared state

**Cost:** Notion ($5-10/user), Claude API usage, Discord (free)  
**Privacy:** Lower (Notion + Google are cloud)  
**Latency:** Fast  
**Maintenance:** Low

**ADHD Fit:** ⭐⭐ Good if team is also ADHD-friendly

---

### Configuration 4: Hybrid (Recommended for ADHD-OS Phase 1)

**For:** Individual user, proven integrations, future flexibility

```
Memory:         Obsidian (local) + Notion (optional backup)
Calendar:       Google Calendar (current) + Nextcloud (optional sovereign)
LLM:            Claude (primary) + Ollama local fallback
Agent:          Hermes Agent (Discord, proven live)
Communication:  Discord (primary, Hermes bot live)
Notifications:  Calendar + Discord
```

**This is your current stack, with clear upgrade paths.**

**Cost:** ~$3-5/month (Claude API)  
**Privacy:** Good  
**Latency:** Fast  
**Maintenance:** Very low

**ADHD Fit:** ⭐⭐⭐ Current proven setup

---

## Part 6: Integration Guides (Quick Start)

### Adding Nextcloud Calendar (Sovereign Upgrade)

1. **Deploy Nextcloud:**
   ```bash
   docker run -d -v nextcloud_data:/var/www/html -p 8080:80 nextcloud:latest
   ```

2. **Create calendar via Obsidian plugin:**
   - Install plugin: CalDAV Synchronizer
   - Add calendar: `http://localhost:8080/remote.php/dav/calendars/admin/personal/`
   - Sync to local folder in vault

3. **Update SETUP.md:** Add Nextcloud Calendar alternative

4. **Test:** Create event in Nextcloud, verify it syncs to Obsidian

---

### Swapping Claude for Local Qwen3

1. **Pull model:**
   ```bash
   ollama pull qwen3
   ```

2. **Update agent configuration:**
   ```python
   # Before:
   from langchain_anthropic import ChatAnthropic
   llm = ChatAnthropic(model="claude-3-5-sonnet")
   
   # After:
   from langchain_community.llms import Ollama
   llm = Ollama(model="qwen3", base_url="http://localhost:11434")
   ```

3. **Benchmark:** Compare latency/quality vs. Claude

4. **Document:** Update RESEARCH.md with findings

---

### Adding Telegram Bot Communication

1. **Create bot:** Message @BotFather on Telegram, get token

2. **Deploy bot:**
   ```bash
   pip install python-telegram-bot
   # See Part 4 example code
   ```

3. **Connect to Hermes Agent:** Route Telegram messages to agent, respond with results

4. **Test:** Send task to bot, receive response

---

## Part 7: Migration Path (Roadmap)

### Phase 1 (Current ✅)
- Claude + Obsidian + Google Calendar + Discord/Hermes

### Phase 2 (Next - 2-4 weeks)
- Add Nextcloud Calendar (sovereign backup)
- Test local Qwen3 as Claude fallback
- Create integration guide for switching

### Phase 3 (Optional - 1-3 months)
- Full sovereign stack (Nextcloud Calendar + local Qwen3)
- Matrix/Element for team version
- CrewAI for role-based workflow agents

### Phase 4 (Future - 6+ months)
- Letta integration (tiered memory)
- Mem0 for multi-agent coordination
- Community agent library

---

## Resources

### LLMs
- [Ollama](https://ollama.ai) — Local model serving
- [HuggingFace Models](https://huggingface.co/models) — Download open models
- [DeepSeek R1](https://github.com/deepseek-ai/DeepSeek-R1) — GitHub
- [Qwen3 Models](https://huggingface.co/Qwen) — HuggingFace

### Calendars
- [Nextcloud Calendar](https://nextcloud.com/calendar/) — Self-hosted
- [CalDAV Synchronizer](https://obsidian.md/plugins?id=caldav-synchronizer) — Obsidian plugin
- [tsdav](https://github.com/natelindev/tsdav) — TypeScript CalDAV library

### Agents
- [LangChain](https://langchain.com/) — Framework
- [LangGraph](https://langchain-ai.github.io/langgraph/) — State graphs
- [CrewAI](https://www.crewai.com/) — Role-based agents

### Communication
- [Telegram Bot API](https://core.telegram.org/bots/api) — Official docs
- [matrix-bot-sdk](https://github.com/turt2live/matrix-bot-sdk) — Matrix SDK
- [AgentMail](https://www.agentmail.to/) — Email for agents

---

**Last Updated:** 2026-05-29  
**License:** MIT (see [LICENSE](../LICENSE))
