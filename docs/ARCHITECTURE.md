# ADHD-OS: Technical Architecture

> Deep-dive into how ADHD-OS layers compose, how data flows, and where to extend or modify the system

---

## System Architecture Overview

```
┌─────────────────────────────────────────────────────────────────────────┐
│ User (ADHD Brain)                                                       │
└────────────────────────┬────────────────────────────────────────────────┘
                         │ (Thoughts, capture, commands)
                         ▼
┌─────────────────────────────────────────────────────────────────────────┐
│ ADHD UX Layer — Obsidian Vault (Local First)                            │
├─────────────────────────────────────────────────────────────────────────┤
│ • Daily Notes (capture inbox)                                           │
│ • Kanban board (priority/status management)                             │
│ • Projects, Templates, Reference materials                              │
│ • Tags, Dataview queries (flexible organization)                        │
│ • Auto-sync via Git (every 5 min)                                       │
│                                                                         │
│ Data: markdown files in filesystem (~/.adhd-os-vault/)                  │
│ Sync: Git push to GitHub (private repo) every 5 minutes                 │
└────────────────────────┬────────────────────────────────────────────────┘
                         │ (MCP read/write via Claude Code)
                         ▼
┌─────────────────────────────────────────────────────────────────────────┐
│ Memory Layer — Obsidian + Optional Letta/Mem0                           │
├─────────────────────────────────────────────────────────────────────────┤
│ Obsidian (Current, Phase 1):                                            │
│ • Persistent vault as long-term memory                                  │
│ • Dataview queries as semantic search                                   │
│ • Tags & backlinks as associative retrieval                             │
│                                                                         │
│ Letta (Phase 2, Planned):                                               │
│ • Core memory: personality, constants, user preferences                 │
│ • Short-term: current session context                                   │
│ • Long-term: episodic (what happened) + semantic (concepts/knowledge)   │
│ • Bounded context window within agent's active memory                   │
│                                                                         │
│ Mem0 (Phase 3, Planned):                                                │
│ • Cross-agent memory coordination                                       │
│ • Shared facts across multiple agents                                   │
│ • Memory eviction policy (what to remember vs forget)                   │
│                                                                         │
│ Data: Markdown (Obsidian) + JSON/vector DB (Letta) + distributed (Mem0)│
│ Retrieval: Full-text search (Obsidian) → semantic/graph (Letta/Mem0)   │
└────────────────────────┬────────────────────────────────────────────────┘
                         │ (Agent queries memory, stores decisions)
                         ▼
┌─────────────────────────────────────────────────────────────────────────┐
│ Agent Orchestration Layer — Hermes/Thoth/Custom                         │
├─────────────────────────────────────────────────────────────────────────┤
│ Hermes Agent (Current, Phase 1):                                        │
│ • Autonomous agent on separate hardware (Dylan's Mac)                   │
│ • Skill learning: converts workflows → reusable skills                  │
│ • ReAct + tool calling (can access shell, files, APIs)                  │
│ • Persistent state & memory between sessions                            │
│ • Discord interface for casual interaction                              │
│                                                                         │
│ Thoth (Phase 2, Planned):                                               │
│ • Local-first desktop orchestrator                                      │
│ • Knowledge graph (10 entity types, 67 relations)                       │
│ • Tool integrations: shell, vision, voice, browser automation           │
│ • Fallback model selection based on capabilities                        │
│                                                                         │
│ OpenClaw (Phase 3, Planned):                                            │
│ • Alternative orchestration framework                                   │
│ • TBD: collaborative agents, complex workflows                          │
│                                                                         │
│ Custom Agents (Extensible):                                             │
│ • Research agent (synthesis, deep dives)                                │
│ • Code agent (writing, testing, debugging)                              │
│ • Review agent (quality, security, completeness)                        │
│ • Executor agent (runs approved commands)                               │
│                                                                         │
│ Data: Agent state (JSON), skill library (serialized workflows)          │
│ Communication: Claude API, LangGraph, custom protocols                  │
└────────────────────────┬────────────────────────────────────────────────┘
                         │ (Requests models, runs inference)
                         ▼
┌─────────────────────────────────────────────────────────────────────────┐
│ AI Backend Layer — Model Inference                                      │
├─────────────────────────────────────────────────────────────────────────┤
│ Provider Options:                                                       │
│                                                                         │
│ Cloud Providers:                                                        │
│ • Anthropic (Claude) — ~1-2s latency, 0.003/1K tokens                 │
│ • OpenAI (GPT-4o) — ~1-2s latency, higher cost                         │
│ • Google (Gemini) — ~1-2s latency, competitive cost                    │
│                                                                         │
│ Local Providers:                                                        │
│ • Ollama (local inference) — instant latency, free, your hardware       │
│ • LM Studio — alternative local inference engine                        │
│                                                                         │
│ Selection Strategy:                                                     │
│ • Default: Claude (best reasoning, reliable)                            │
│ • High-volume: Hermes local (cost, latency)                            │
│ • Fallback chain: Claude → OpenAI → local Ollama                        │
│                                                                         │
│ Data: Model weights (12B-70B params, stored locally or cloud)          │
│ Input/Output: Tokens, streaming or batch                                │
└────────────────────────┬────────────────────────────────────────────────┘
                         │ (Infrastructure, compute)
                         ▼
┌─────────────────────────────────────────────────────────────────────────┐
│ Infrastructure Layer — Compute, Storage, Networking                     │
├─────────────────────────────────────────────────────────────────────────┤
│ Compute:                                                                │
│ • Local: Your Mac/Linux machine (primary)                               │
│ • Remote: Separate Mac Mini or Linux box (Hermes Agent, always-on)     │
│                                                                         │
│ Storage:                                                                │
│ • Local: /Users/username/Documents/adhd-os-vault/ (git repo)           │
│ • Offsite: GitHub private repo (backup, version history)               │
│ • Cloud (optional): S3/GCS for long-term archive (Phase 2)             │
│                                                                         │
│ Networking:                                                             │
│ • LAN: Internal communication between machines (SSH, MCP)              │
│ • Internet: API calls to Claude, Calendar, optional cloud storage       │
│ • VPN (optional): For hybrid work, remote access                        │
│                                                                         │
│ Sovereignty Guarantees:                                                 │
│ • Data at rest: AES-256 encryption (optional, full-disk)               │
│ • Data in transit: TLS 1.3 (to cloud APIs only)                        │
│ • No telemetry: Hermes/Ollama have zero tracking                        │
│ • GDPR-friendly: All raw data stays local; can delete vault anytime    │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## Data Flow Diagram

### Scenario 1: Simple Capture → Response

```
User Types Thought
    │
    ▼
Obsidian Daily Note (Markdown)
    │
    ├─→ Auto-save to disk
    │
    ├─→ Git commit (every 5 min)
    │
    └─→ (Optional) Sync to GitHub backup
```

### Scenario 2: Claude MCP Session

```
User: "Help me prioritize my Kanban"
    │
    ▼
Claude Code (CLI/Desktop)
    │
    ├─→ MCP Read: Kanban.md
    │   ├─→ Reads from vault on disk
    │   ├─→ Parses markdown
    │   └─→ Returns structure to Claude
    │
    ├─→ (Claude analyzes)
    │
    ├─→ MCP Write: Session Notes
    │   ├─→ Creates timestamped file
    │   ├─→ Writes decision + rationale
    │   └─→ Saves to disk
    │
    └─→ Git Auto-commit
        └─→ Captures new session note

[Claude session ends]
    │
    ▼
Next session: User reads session note → context restored
```

### Scenario 3: Hermes Agent Background Task

```
User: "/remind me to review papers tomorrow"
    │
    ▼
Hermes Agent (on separate machine)
    │
    ├─→ Parses command → stores as task
    │
    ├─→ At scheduled time, retrieves task
    │
    ├─→ Inference: Claude/Ollama
    │   └─→ Generates reminder message
    │
    ├─→ Optional: Updates Obsidian via MCP
    │   └─→ Writes to vault: "Papers review reminder"
    │
    └─→ Returns to Discord
        └─→ "Reminder: time to review papers"
        
[Workflow saved as skill for next time]
```

### Scenario 4: Multi-Agent Orchestration (Phase 3)

```
User: "Research how to set up a Postgres database for the ADHD-OS project"
    │
    ▼
Orchestrator Agent (Thoth/Hermes)
    │
    ├─→ Route to Research Agent
    │   ├─→ Queries knowledge graph
    │   ├─→ Calls web search tools
    │   └─→ Synthesizes findings → vault
    │
    ├─→ Route to Code Agent
    │   ├─→ Receives research summary
    │   ├─→ Generates setup scripts
    │   └─→ Tests in sandbox
    │
    ├─→ Route to Review Agent
    │   ├─→ Checks security (no hardcoded secrets)
    │   ├─→ Validates instructions
    │   └─→ Approves for execution
    │
    ├─→ Update Memory (Mem0)
    │   └─→ Store fact: "Postgres setup for ADHD-OS uses X approach"
    │
    └─→ Return final artifact to user
        └─→ "Here's your database setup guide"
```

---

## API Boundaries & Integration Points

### 1. Obsidian ↔ Git

**Integration:** Auto-commit via Git hooks

```bash
# Hook: post-save in Obsidian
.obsidian/plugins/obsidian-git/...
  └─→ On file save, triggers: git add -A && git commit -m "auto: vault update"
```

**Data Format:** Markdown files

**Frequency:** Every file save (typically ~5 min via cron)

**Rollback:** `git revert <commit>` restores any state

### 2. Obsidian ↔ Claude MCP

**Protocol:** Model Context Protocol (stdio-based)

```json
{
  "method": "obsidian:read_file",
  "params": {
    "path": "Projects/ADHD-OS.md"
  }
}
```

**Authentication:** Local file access (no API key needed)

**Rate Limit:** None (local calls)

**Use Cases:**
- Claude reads current context (Kanban, daily notes, projects)
- Claude writes session notes, decisions, analysis
- Claude updates Kanban based on conversation

### 3. Hermes Agent ↔ Obsidian (via MCP)

**Transport:** SSH tunnel (LAN) or VPN (remote)

```
Hermes Agent (Dylan's Mac)
    │
    ├─→ SSH: ~/.hermes/mcp-connector
    │   └─→ Obsidian vault (JP's Mac)
    │
    └─→ Read/Write operations
        ├─→ Update task status
        ├─→ Log completed workflows
        └─→ Query memory for context
```

**Authentication:** SSH key (no passwords)

**Latency:** ~50ms (LAN) or ~200ms (internet)

### 4. Agent ↔ AI Backend

**Option A: Cloud (Claude API)**
```python
import anthropic

client = anthropic.Anthropic(api_key="sk-...")
response = client.messages.create(
    model="claude-3-5-sonnet",
    max_tokens=2000,
    messages=[
        {"role": "user", "content": "analyze my Kanban"}
    ]
)
```

**Rate Limit:** ~100 req/min (Anthropic free tier)

**Cost:** ~$0.003 per 1K input tokens

**Option B: Local (Ollama)**
```python
import requests

response = requests.post(
    "http://localhost:11434/api/generate",
    json={
        "model": "hermes",
        "prompt": "analyze my Kanban",
        "stream": False
    }
)
```

**Rate Limit:** None (local)

**Cost:** Free (your hardware)

**Latency:** Instant (GPU) to ~10s (CPU)

### 5. Calendar ↔ Google Calendar API

**Protocol:** OAuth 2.0 (Obsidian plugin handles this)

```json
GET https://www.googleapis.com/calendar/v3/calendars/primary/events
Authorization: Bearer {access_token}
```

**Use Cases:**
- Obsidian reads upcoming events
- Obsidian displays calendar view
- Scheduled review reminders

---

## Extensibility Points

### 1. Custom Agents

Add a new agent type in `/agents/`:

```python
# agents/my_agent.py
from hermes.agent import BaseAgent

class MyAgent(BaseAgent):
    def initialize(self):
        self.capabilities = ["web_search", "file_write"]
    
    def process(self, task):
        # Your logic here
        return result
```

### 2. Memory Backends

Implement the Memory interface:

```python
class MyMemory:
    def store(self, entity, relation, target):
        # Store to your backend (Letta, Mem0, custom DB)
        pass
    
    def recall(self, query, limit=10):
        # Return relevant memories
        pass
```

### 3. Tool Integrations

Add tools to Hermes Agent:

```python
from hermes.tools import Tool

class MyTool(Tool):
    name = "my_tool"
    description = "What this tool does"
    
    def execute(self, **kwargs):
        # Your implementation
        return result
```

### 4. Model Providers

Implement provider interface:

```python
class MyProvider:
    def __init__(self, api_key=None):
        self.api_key = api_key
    
    def infer(self, prompt, max_tokens=2000):
        # Call your model
        return response
```

---

## Security Model

### Data at Rest

**Local Storage (Primary):**
- Obsidian vault on your machine
- Protected by filesystem permissions (macOS: chmod 700)
- Optional: Full-disk encryption (macOS: FileVault)

**Offsite Backup:**
- GitHub private repo (encrypted by GitHub)
- No encryption key needed (repo is private)
- Only accessible with your GitHub account

### Data in Transit

**Local Network (LAN):**
- MCP calls: SSH tunnel (no TLS needed, LAN is local)
- Hermes ↔ Obsidian: SSH with public key auth

**Internet (Cloud APIs):**
- Claude API: TLS 1.3 to api.anthropic.com
- Google Calendar: OAuth 2.0 with credential exchange
- GitHub: SSH or HTTPS (your choice)

**No Telemetry:**
- Hermes Agent: zero cloud tracking
- Ollama: no phone-home requests
- Obsidian: only what you explicitly sync

### Threat Model

| Threat | Mitigation |
|--------|-----------|
| **Data loss** | Git + GitHub backup (version history) |
| **Ransomware** | Offline backup on external drive (periodic) |
| **Cloud vendor lock-in** | Local-first + git = portable anytime |
| **Account compromise** | SSH keys (not passwords), 2FA on GitHub |
| **Man-in-the-middle** | TLS for cloud APIs, SSH for local LAN |
| **Unauthorized access** | Filesystem permissions + GitHub private repo |

---

## Performance Characteristics

### Latency

| Operation | Latency | Bottleneck |
|-----------|---------|-----------|
| Obsidian read (local) | <10ms | Disk I/O |
| Claude API call | 1-5s | Network + inference |
| Ollama local inference | instant-10s | GPU utilization |
| Hermes Agent (LAN) | ~50ms | SSH overhead |
| Hermes Agent (internet) | 100-500ms | Network latency |

### Storage

| Component | Size |
|-----------|------|
| Obsidian vault (1 year) | ~500MB (text) |
| Ollama models (1-3) | 5-20GB |
| Git history (full) | ~1GB |
| Hermes skills library | ~100MB |

### Scalability

| Metric | Limit | Solution |
|--------|-------|----------|
| Daily notes (archive) | 10,000+ | Move to Archive folder, Git compaction |
| Kanban items | 500+ | Use filters, Dataview queries |
| Claude context | 100K tokens | Session notes management |
| Concurrent agents | 3-5 | Orchestration queue, scheduling |

---

## Deployment Architectures

### Architecture 1: Single Machine (Recommended for Start)

```
Your Mac/Linux
├── Obsidian vault (local)
├── Ollama (optional, local inference)
├── Claude Code (optional, cloud inference)
└── Git backup → GitHub
```

**Pros:** Simple, no network setup, fully local

**Cons:** Hermes Agent on same machine = resource contention

---

### Architecture 2: Dual Machine (Current Production)

```
Your Machine (JP's Mac)          Other Machine (Dylan's Mac)
├── Obsidian vault               ├── Hermes Agent (always-on)
├── Claude Code                  ├── Ollama (inference)
└── Git (local)                  └── MCP connector (SSH)
    │                                 │
    └─────────────────────────────────┘
              Git sync (GitHub)
              MCP calls (SSH tunnel)
```

**Pros:** Hermes runs 24/7, no resource contention, distributed

**Cons:** Network setup required, SSH management

---

### Architecture 3: Hybrid Cloud/Local (Future)

```
Your Machine                    Cloud (AWS/DigitalOcean)
├── Obsidian (local)            ├── Hermes Agent replica
├── Ollama (local, fast)         ├── Letta memory service
└── Claude Code                  ├── Thoth orchestrator
                                 └── Long-term backup
```

**Pros:** High availability, geographic redundancy, scalable

**Cons:** Cloud costs, more complex setup

---

## Version & Compatibility

| Component | Current | Min Required | Notes |
|-----------|---------|--------------|-------|
| Obsidian | 1.5+ | 1.3 | Plugins require 1.5+ |
| Node.js | 20 LTS | 18 | For Hermes Agent |
| Git | 2.30+ | 2.20 | Standard features |
| Ollama | 0.24+ | 0.20 | Model library updates |
| Claude | Sonnet 3.5 | 3.0 | Recommend 3.5+ for reasoning |
| Hermes 4.3 | 0.13.0 | 0.10.0 | Skill learning since 0.10 |

---

## Debugging & Troubleshooting

### Enable Logging

```bash
# Obsidian logs
~/.obsidian/plugins/obsidian-git/git.log

# Hermes logs
~/.hermes/logs/

# Claude Code logs
~/.claude/logs/
```

### Health Check Script

```bash
#!/bin/bash
echo "=== ADHD-OS Health Check ==="

# Git
echo "Git status: $(git log -1 --pretty=%B)"

# Obsidian sync
echo "Vault size: $(du -sh ~/Documents/adhd-os-vault)"

# Ollama
if pgrep ollama > /dev/null; then
  echo "Ollama: running"
  curl -s http://localhost:11434/api/tags | jq '.models | map(.name)'
fi

# Hermes
if pgrep hermes > /dev/null; then
  echo "Hermes: running on port 8080"
fi

# Claude
if command -v claude-code &> /dev/null; then
  echo "Claude Code: installed"
fi
```

---

## Testing

### Unit Tests (Agents)

```bash
cd ~/path/to/hermes-agent
npm test
```

### Integration Tests (Obsidian ↔ Claude)

```bash
# Create test note, verify Claude can read it
# Write test output, verify it syncs via Git
```

### E2E Tests (Full workflow)

```bash
# 1. Capture thought in Obsidian
# 2. Claude processes it
# 3. Hermes Agent executes result
# 4. Git commits all changes
# 5. Verify in GitHub
```

---

## Future: Roadmap Architecture Changes

### Phase 2: Knowledge Graph

Add Thoth's knowledge graph as alternative memory backend:

```
Obsidian (flat documents)
    ↓ (sync via MCP)
Thoth Knowledge Graph
    ├─ Entity extraction (person, place, concept)
    ├─ Relation inference (Person → works on → Project)
    └─ Semantic search (find "similar projects")
```

### Phase 3: Distributed Agents

Multi-agent orchestration with Mem0 shared memory:

```
Orchestrator Agent
├── Research Agent (queries knowledge graph)
├── Code Agent (writes code, stores in vault)
├── Review Agent (checks quality, security)
└── Executor Agent (runs approved commands)

All agents share: Mem0 (facts, learnings, decisions)
```

### Phase 4: High Availability

Replicated Hermes agents across multiple machines + cloud fallback:

```
Local Hermes (primary) → Cloud Hermes (backup)
Local Ollama (primary) → Claude API (fallback)
GitHub backup (always-on)
```

---

**Last Updated:** 2026-05-29
**License:** MIT (see [LICENSE](../LICENSE))
