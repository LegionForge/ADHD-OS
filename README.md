# ADHD-OS: A Sovereign AI Assistant Platform for the ADHD Brain

> Building an **external executive function system** that adapts to how ADHD brains actually work — frictionless capture, modular memory, multi-agent coordination, complete personal ownership.

---

## ⚠️ **IMPORTANT: Read This First**

**[HEALTH-WARNING.md](HEALTH-WARNING.md)** — ADHD-OS is not a medical device and should not replace professional ADHD care. Please read the health disclaimer before using this system.

---

## The Problem

Most productivity systems and AI assistants are built for neurotypical brains. They assume:
- Reliable working memory
- Consistent task initiation
- Low context-switching cost  
- Intrinsic motivation stability

The ADHD brain is wired differently. It's not a discipline problem. It's a **prefrontal cortex architecture problem**:

- **Memory anxiety / FOMO** — Uncaptured thoughts feel lost forever, creating constant mental interruption
- **Task initiation** — The gap between "I should do this" and "I am doing this" is enormous
- **Working memory overload** — Holding multiple project contexts simultaneously causes performance to degrade on all of them
- **Context switching cost** — Interruptions are catastrophically expensive (20+ min re-entry)
- **Impulse control** — Hyperfocus pulls and interesting tangents derail planned work
- **Time blindness** — Difficulty estimating duration and perceiving elapsed time
- **Troubleshooting loops** — Can execute complex sequences without understanding them, leading to hours wasted chasing symptoms instead of root causes

**The solution isn't willpower. It's better infrastructure.**

---

## The Solution: Layered, Sovereign AI Architecture

ADHD-OS is a **modular platform** for building personal AI assistants that:

1. **Prioritize ADHD-specific UX** — frictionless capture, external working memory, loop-breaking
2. **Maintain personal sovereignty** — data stays local, no vendor lock-in, complete ownership
3. **Support multi-agent coordination** — agents work together on complex tasks
4. **Run local-first, cloud-optional** — works offline, hybrid deployment, resilience through redundancy

### Layers

```
┌─────────────────────────────────────────────────────────────┐
│  ADHD UX Layer                                              │
│  (Capture, Priority, Interrupts, Working Memory)            │
│  Obsidian | Notion | OneNote                                │
├─────────────────────────────────────────────────────────────┤
│  Memory Layer                                               │
│  (Long-term, Episodic, Semantic)                            │
│  Letta | Mem0 | OpenBrain | Knowledge Graphs                │
├─────────────────────────────────────────────────────────────┤
│  Agent Layer                                                │
│  (Reasoning, Skill Learning, Orchestration)                 │
│  Hermes Agent | Thoth | OpenClaw | Custom Agents            │
├─────────────────────────────────────────────────────────────┤
│  AI Layer                                                   │
│  (Model Inference)                                          │
│  Claude | Hermes 4.3 | Local Ollama | Other Providers       │
├─────────────────────────────────────────────────────────────┤
│  Infrastructure                                             │
│  (Local Ollama, Sovereign Hosting, Hybrid Cloud/Local)      │
└─────────────────────────────────────────────────────────────┘
```

---

## What's Working Now: The Current Stack

The ADHD-OS platform was designed and validated through real-world use. Here's the proven system:

### 1. **Obsidian** — Persistent External Memory
- **Why:** Every thought, task, project, and reference gets captured immediately. The brain is freed from the anxiety of "I need to remember this"
- **ADHD benefit:** Removes memory anxiety/FOMO. Non-linear linking mirrors how ADHD brains connect ideas (jumping between threads without losing them)
- **Features used:** Kanban boards, Dataview queries, tags, templates, Daily Notes, Frontmatter
- **Data:** Stays on your machine; syncs via Git for safety

### 2. **Claude (via Claude Code)** — Executive Function Prosthetic
- **Why:** Claude can read/write directly to the vault during conversation, providing session-continuous context the ADHD brain would otherwise lose
- **ADHD benefit:** Holds working memory between task switches. Actively watches for troubleshooting loops and interrupts ("⚠️ We're in a loop — let's diagnose first")
- **Interaction:** MCP integration for real-time vault access; thoughts flow directly into notes without copy-paste friction
- **Sovereignty:** Uses Claude API (not web), so all data stays under your control

### 3. **Git + GitHub** — The Safety Net
- **Why:** Auto-commit every 5 minutes; acts as undo buffer and offsite backup
- **ADHD benefit:** Removes anxiety about losing work to impulsive edits or AI mistakes. Reliable restore point if something breaks
- **Private repo:** Backup without cloud vendor lock-in or privacy concerns

### 4. **Google Calendar** — Forcing Function for Time Blindness
- **Why:** Reminders, scheduled reviews, explicit due dates bridge intention and action
- **ADHD benefit:** The calendar is the external clock. Compensates for time blindness and perception distortion

### 5. **Thoth** — Local-First Desktop Agent
- **Why:** Desktop orchestrator with knowledge graph, tool integration (shell, vision, voice, browser), and persistent memory
- **ADHD benefit:** Full-featured local agent with integrated tools, no external dependency
- **Current:** Live and running, primary agent orchestrator

### 6. **Hermes Agent (Phase 2 - Recovering)**
- **Why:** Autonomous agent with skill learning and persistent memory
- **Status:** Currently rebuilding after docker reset (lost memories, no backups)
- **Plan:** Reinstate with Thoth coordination once memories are restored
- **ADHD benefit:** "Set it and forget it" background intelligence, learns and improves

---

## Modularity: Plug and Play Components

### Memory Backends (Swappable)

| System | Best For | Sovereignty | API/Sync | Status |
|--------|----------|-------------|----------|--------|
| **Obsidian** | ADHD UX, non-linear thinking, templates, Kanban | Local files + Git | Yes (via plugins) | ✅ Live |
| **Notion** | Team collaboration, structured databases | Cloud (Notion Inc) | Yes (robust API) | ✅ Alternative |
| **OneNote** | Microsoft ecosystem, sync across devices | Microsoft cloud | Yes (OneNote API) | ✅ Alternative |
| **Proton** | Privacy-first, encrypted vault | Self-hosted/hybrid | Limited (in dev) | 🟡 Emerging |
| **Letta** | Deep memory architecture, multi-tier (core/short/long) | Self-hosted or local | Yes (framework) | 🔄 Phase 2 |
| **Mem0** | Memory management for multi-agent systems | Open source, self-hosted | Yes (SDK) | 🔄 Phase 2 |
| **OpenBrain** | Cognitive architecture patterns, Nate B Jones framework | Custom/research | Research | 🔄 Exploring |

**Current:** Obsidian + Git (fully sovereign, battle-tested for ADHD workflow)  
**Alternatives:** Notion (cloud + API), OneNote (Microsoft), Proton (privacy-first)  
**Roadmap:** Letta + Mem0 for tiered memory, multi-backend support

### Agent Orchestrators (Pluggable)

| System | Architecture | Best For | API | Status |
|--------|--------------|----------|-----|--------|
| **Thoth** | Local-first desktop, knowledge graph + tools | Personal sovereignty, integrated tools (shell, vision, voice, browser) | Development | ✅ **Live** (primary) |
| **Hermes Agent** | Skill learning, ReAct + self-improvement | Learning, workflow automation, persistent memory | Yes | 🔄 Phase 2 (recovering) |
| **OpenClaw** | [Research phase] | TBD | Research | 🔄 Exploring |
| **Crew.ai** | Multi-agent orchestration, role-based teams | Complex workflows, agent delegation | Yes (Python) | 🟡 Alternative |
| **LangChain Agents** | Flexible agent framework, tool integration | Custom agents, RAG patterns | Yes (Python SDK) | 🟡 Alternative |
| **AutoGPT** | Self-improving agent loops | Goal-oriented autonomy | Yes (Docker) | 🟡 Alternative |
| **n8n** | No-code workflow automation | Non-technical automation, integrations | Yes (REST + webhook) | 🟡 Alternative (visual) |
| **Custom Agents** | Your own via LangGraph, Letta, or frameworks | Domain-specific assistants | Custom | Building |

**Current:** Thoth (local desktop orchestrator, live) + Claude (via MCP)  
**Recovering:** Hermes Agent (Phase 2 - rebuilding memories post-docker-wipe)  
**Alternatives:** Crew.ai (Python multi-agent), LangChain (flexible), n8n (visual/no-code)  
**Roadmap:** Multi-agent coordination (Thoth + Hermes when ready), OpenClaw exploration

### AI Backends (Provider-Agnostic)

| Provider | Model | Latency | Sovereignty | Cost | Notes |
|----------|-------|---------|-------------|------|-------|
| **Anthropic (Claude)** | Claude 3.5 Sonnet | API (~1-2s) | Your API key | ~$0.003/1k tokens | ✅ Best reasoning |
| **OpenRouter** | 150+ models (Claude, GPT, Llama, etc.) | API (~0.5-1.5s) | Your API key | Highly competitive | ⭐ Super fast aggregator |
| **InceptionLabs** | Various | API (~0.3-0.8s) | Your API key | Competitive | ⭐ Lightning fast inference |
| **Cerebras** | Llama variants, custom | API (~0.2-0.5s) | Your API key | Fastest pricing | ⭐ Fastest on market |
| **OpenAI (ChatGPT)** | GPT-4o, o1 | API (~1-2s) | Via API key | Higher cost | ✅ Alternative reasoning |
| **Local (Ollama)** | Hermes, Llama, Mistral | Instant (GPU/CPU) | Complete (local) | Free (your hardware) | ✅ Full sovereignty |
| **Nous Research** | Hermes 4.3 | API or local | Local available | Free (open source) | ✅ Open-source reasoning |
| **Google** | Gemini | API (~1-2s) | Via API key | Competitive | ✅ Alternative |
| **Meta** | Llama 2/3.1 | Local only | Complete (local) | Free (open source) | ✅ Private alternative |
| **Mistral** | Mistral 7B/Large | Local or API | Local available | Free (local) or paid (API) | ✅ Private alternative |
| **Together AI** | Various (local mirrors) | API (~1-2s) | Your API key | Competitive | 🟡 Privacy-focused API |
| **Replicate** | Various (Llama, Mistral) | API (~1-2s) | Your API key | Pay-per-use | 🟡 Easy model hosting |

**Current:** Claude (Anthropic) + Hermes qwen3.5 (Ollama local)  
**Fast Providers:** OpenRouter (0.5-1.5s), InceptionLabs (0.3-0.8s), Cerebras (0.2-0.5s) — exceptional for real-time ADHD interactions  
**Philosophy:** Use Claude for complex reasoning, fast providers for high-volume tasks, local for sovereignty  
**Sovereign Strategy:** Default local (Ollama) → Claude API → Cerebras/InceptionLabs (speed) → fallback, with zero telemetry requirement

### Calendar & Time Management (Swappable)

| System | Platform | API | Sovereignty | Reminders | Notes |
|--------|----------|-----|-------------|-----------|-------|
| **Google Calendar** | Web/iOS/Android | Yes (CalDAV + REST) | Google cloud | ✅ Rich | ✅ Live |
| **Apple Calendar** | macOS/iOS | Yes (iCal + CalDAV) | Apple cloud | ✅ Native | ✅ Alternative |
| **Microsoft Outlook** | Web/Windows/iOS | Yes (CalDAV + Graph API) | Microsoft cloud | ✅ Rich | ✅ Alternative |
| **Proton Calendar** | Web | Limited (emerging) | Proton (private) | ✅ Basic | 🟡 Privacy-first |
| **Nextcloud Calendar** | Self-hosted | Yes (CalDAV) | Complete (self-hosted) | ✅ Basic | 🟡 Sovereign |
| **Thunderbird Calendar** | Local + sync | Yes (CalDAV support) | Local + optional | ✅ Basic | 🟡 Open-source |

**Current:** Google Calendar (proven integrations, rich reminders)  
**Sovereign alternatives:** Nextcloud (self-hosted), Apple Calendar (device-native), Proton (privacy-first)  
**Recommendation:** Pair with ADHD-PATTERNS calendar blocking (visible time tracking in daily notes)

### Communication Channels (Multi-Modal)

| Channel | API | Status | Best For | Notes |
|---------|-----|--------|----------|-------|
| **Discord** | Yes (bot framework) | ✅ Live | Hermes Agent bot, team collaboration | Rich integrations |
| **Slack** | Yes (webhook + API) | ✅ Alternative | Team/org workflow, bot integration | Enterprise-friendly |
| **Signal** | Limited (REST API community) | 🟡 Research | Private messaging, encrypted | Privacy-first but limited API |
| **Telegram** | Yes (Bot API) | ✅ Alternative | Bot integration, simpler than Discord | Good for casual users |
| **SMS** | Yes (Twilio, MessageBird) | ✅ Alternative | Low-bandwidth reminders | Cost-based (per message) |
| **Email** | Yes (SMTP/IMAP) | ✅ Fallback | Capture, notifications, archive | Universal but slower |
| **Matrix/Element** | Yes (REST API) | 🔄 Emerging | Federated, encrypted, open-source | Decentralized alternative |

**Current:** Discord (Hermes bot live, rich ecosystem)  
**Alternatives:** Slack (team-friendly), Telegram (simple), Signal (private)  
**Hybrid approach:** Discord primary, SMS for critical reminders, email for archiving

### Security & Sovereignty Strategy

- **Data stays local first** — Obsidian vault on your machine, Git as backup
- **No telemetry** — Hermes Agent runs with zero cloud tracking
- **API keys, not passwords** — Control which services can access what
- **Hybrid cloud/local** — Critical paths local (Obsidian, Ollama), integrations to cloud (Claude API) as needed
- **Version control** — Everything in Git, including agent state (via Letta's `.af` format when adopted)
- **Provider flexibility** — No vendor lock-in; swap memories, AI, calendars, and comms without rebuilding

---

## ADHD-Specific Features

### 1. **Ubiquitous Capture** (Obsidian Daily Notes + Claude MCP)
- New thought appears while deep in another task?
- Type `!cap <thought>` → Claude writes it to Inbox section → Brain can let go
- Claude interrupts only if truly urgent; non-urgent items go to Kanban for later review
- **Why it works:** Removes the "if I don't act on this now, it's lost" anxiety

### 2. **Working Memory Externalization** (Obsidian + Session Notes)
- Every session with Claude produces a timestamped note capturing:
  - What was the goal
  - What was decided
  - What's blocked and why
  - What's next
- Return after context switch? Read the note instead of reconstructing from memory
- **Why it works:** Re-entry takes 2 min (reading) instead of 20 min (reconstruction)

### 3. **Kanban as Priority Management** (Obsidian + Dataview)
- **Inbox** → New captures waiting triage
- **Inception/Ongoing** → Hyperfocus items and tangents (explicitly allowed, not a failure)
- **Current** → What you're actually working on (ruthlessly limited to 1-3 items)
- **Waiting** → Blocked on external input
- **Done** → Completed (weekly review)
- **Why it works:** Externalizes priority without requiring constant re-evaluation. Hyperfocus is a *feature*, not a bug — the Kanban captures it safely

### 4. **Troubleshooting Loop Breaker** (Claude Watchdog)
- **Problem:** ADHD brains can execute complex sequences without understanding, leading to hours wasted
- **Solution:** Claude actively watches for loop signatures:
  - Same error appears 2+ times → Interrupt: "⚠️ We're pattern-matching without understanding. Let's diagnose first."
  - Restarting same thing 3+ times → Direct: "⚠️ STOP. This isn't working. Let's check the actual problem."
  - 15+ min on one problem → Pause: "Can we verify our assumptions about what's happening?"
- **Why it works:** External interrupt partner breaks the loop when prefrontal cortex is already deep in hyperfocus

### 5. **Time Blindness Compensation** (Calendar + Reminders)
- Scheduled reviews (weekly, monthly, quarterly)
- Explicit time blocks for task estimation ("this will take ~2 hours")
- Reminders for time-sensitive items
- **Why it works:** The system tracks time; the brain doesn't have to

---

## Roadmap & Exploration

### Phase 1 (Current ✅) — Validated and Live

**Primary Development Platform:**
- [x] Obsidian capture + Kanban + templates
- [x] Claude MCP integration (vault read/write)
- [x] Git auto-commit + backup
- [x] **Thoth agent** (VALIDATED LIVE, local-first desktop orchestrator) — Current primary
- [x] Calendar integration
- [x] Fast inference options (OpenRouter, InceptionLabs, Cerebras for real-time)

> **Note:** Phase 1 validation focuses on Thoth as the proven agent orchestrator. Hermes has NOT been validated in Phase 1 and is secondary.

### Phase 2 (In Progress 🟢)

**Thoth (Primary — Already Live):**
- [x] **Thoth** — Local-first desktop orchestrator with knowledge graph memory (Live, validated)
  - [x] Multi-model support (Claude, Hermes, fast providers)
  - [x] Tool integrations (shell, browser automation, vision)
  - [x] Personal knowledge graph for memory

**Hermes Agent (Secondary — In Recovery):**
- [ ] **Hermes Agent Recovery** — Rebuilding memories post-docker-reset
  - [ ] Reinstate Hermes with memory persistence
  - [ ] Validate Hermes in Phase 2
  - [ ] Coordinate with Thoth for multi-agent workflows
- [ ] **Letta Framework** — Tiered memory architecture
  - [ ] Core memory (personality, constants)
  - [ ] Short-term (current session context)
  - [ ] Long-term (episodic, semantic)
  - [ ] Integration with Obsidian Kanban
- [ ] **Skill Learning** — Hermes Agent converts workflows into reusable skills
  - [ ] Common patterns (research, debug, write, review)
  - [ ] Skill library with auto-improvement

### Phase 3 (Planned)
- [ ] **Multi-Agent Coordination** — Agents delegate to each other
  - [ ] Research agent → finds and synthesizes information
  - [ ] Code agent → writes and tests
  - [ ] Review agent → checks quality and security
  - [ ] Orchestrator → routes tasks and manages context
- [ ] **Mem0** — Cross-agent memory management and persistence
- [ ] **OpenBrain Integration** — Cognitive architecture patterns
- [ ] **Provider Flexibility** — Swap Claude for Hermes, Gemini, or local models seamlessly
- [ ] **High Availability** — Fallback to local inference if cloud APIs are down

### Phase 4 (Aspirational)
- [ ] Custom agent templates for specific workflows (research, debugging, writing)
- [ ] Community sharing of agents, skills, and Kanban templates
- [ ] Mobile companion (capture on phone, process on desktop)
- [ ] Real-time collaboration (multiple humans + agents on shared Kanban)

---

## Getting Started

### Prerequisites
- **Computer:** Mac, Linux, or Windows (WSL2) with 16GB+ RAM
- **Software:** Git, Obsidian (free), Node.js 20+ (optional)
- **Accounts:** Anthropic API key (for Claude, ~$0.003/1K tokens) — optional but recommended
- **Time:** 45-90 minutes for full setup

### Documentation

**Getting Started:**
- **[docs/SETUP.md](docs/SETUP.md)** — Installation guide (45-90 min, all platforms)
- **[docs/ADHD-PATTERNS.md](docs/ADHD-PATTERNS.md)** — 8 real workflows for ADHD brains

**Technical:**
- **[docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)** — System architecture, data flow, extensibility
- **[docs/RESEARCH.md](docs/RESEARCH.md)** — Evidence base (29 sources, neuroscience + AI)
- **[docs/STACK-EXPANSION.md](docs/STACK-EXPANSION.md)** — Alternatives for every layer (memory, AI, calendar, agents, comms)

**Advanced:**
- **[docs/SOVEREIGNTY-GUIDE.md](docs/SOVEREIGNTY-GUIDE.md)** — Complete self-hosted stack (Nextcloud + Ollama + Matrix)

**Legal:**
- **[HEALTH-WARNING.md](HEALTH-WARNING.md)** — Health disclaimer (read first!)
- **[LICENSE](LICENSE)** — MIT license + health/liability waiver
- **[CONTRIBUTING.md](CONTRIBUTING.md)** — Community contribution guidelines

---

## Philosophy

ADHD-OS is built on a few non-negotiable principles:

1. **ADHD UX first** — If it requires willpower or "just try harder," it won't work. Infrastructure must be frictionless.
2. **Sovereignty** — Your data, your machine, your rules. No vendor lock-in or forced cloud dependency.
3. **Honest about limitations** — This is not a cure. It's not a replacement for medication or therapy. It's infrastructure that works *alongside* those.
4. **Modular** — You should be able to swap memory backends, AI providers, and orchestrators without rebuilding everything.
5. **Reliable** — The system should work offline, fail gracefully, and never lose your data.

---

## Community & Discussions

**GitHub Discussions** are open for:
- **Use Cases** — Share what works for your ADHD brain
- **Integrations** — Ask about alternatives (Notion, Nextcloud, local models, etc.)
- **Patterns** — Show custom workflows and agents
- **Help** — Get setup assistance and troubleshooting
- **Roadmap** — Discuss Phase 2 priorities and features

**[Open Discussions →](https://github.com/LegionForge/ADHD-OS/discussions)**

---

## Contributing

ADHD-OS is open source because this infrastructure should be available to everyone. We're looking for:

- **Your use cases** — What works for *your* ADHD brain? What doesn't?
- **Agent implementations** — Custom agents for specific workflows (research, debugging, writing, etc.)
- **Memory backend integrations** — Letta, Mem0, OpenBrain, others
- **Orchestration patterns** — How should agents work together?
- **Documentation** — Setup guides, troubleshooting, patterns that work

[See CONTRIBUTING.md](CONTRIBUTING.md)

---

## Resources & References

- [ADHD Neurochemistry Basics](https://www.adhdcentre.co.uk/what-is-adhd/) — Understanding the prefrontal cortex architecture
- [Obsidian](https://obsidian.md) — Local-first knowledge base
- [Hermes Agent](https://hermes-agent.org/) — Self-learning autonomous agent framework
- [Thoth](https://github.com/siddsachar/Thoth) — Local-first AI assistant with knowledge graph
- [Letta](https://github.com/letta-ai/letta) — Stateful AI agents with tiered memory
- [Mem0](https://mem0.ai/) — Memory management for AI agents
- [OpenBrain](https://github.com/nate-jones-ai/openbrain) — Cognitive architecture framework
- [Claude API Documentation](https://docs.anthropic.com/)
- [MCP Protocol](https://modelcontextprotocol.io/)

---

## License

MIT — See [LICENSE](LICENSE)

---

## Acknowledgments

- **Obsidian community** — For proving non-linear thinking works
- **Nous Research** — For building Hermes Agent as open source
- **Claude team** — For MCP and making AI assistants genuinely useful
- **ADHD community** — For the radical honesty about how different our brains are wired

---

**Built with 💙 by someone with ADHD who got tired of productivity systems designed for someone else's brain.**
