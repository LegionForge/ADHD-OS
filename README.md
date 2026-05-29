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

### 5. **Hermes Agent (Discord Bot)** — Background Intelligence
- **Why:** Autonomous agent running on separate hardware (Dylan's Mac Mini) with persistent memory
- **ADHD benefit:** "Set it and forget it" intelligence working in background without requiring conscious initiation
- **Current:** v0.13.0 live on Discord, ~103s response latency, running locally via Ollama (qwen3.5)

---

## Modularity: Plug and Play Components

### Memory Backends (Swappable)

| System | Best For | Sovereignty |
|--------|----------|-------------|
| **Obsidian** | ADHD UX, non-linear thinking, templates, Kanban | Local files + Git |
| **Notion** | Team collaboration, structured databases | Cloud (Notion Inc), integrations via API |
| **OneNote** | Microsoft ecosystem, sync across devices | Microsoft cloud |
| **Letta** | Deep memory architecture, multi-tier (core/short/long) | Self-hosted or local |
| **Mem0** | Memory management for multi-agent systems | Open source, self-hosted |
| **OpenBrain** | Cognitive architecture patterns, Nate B Jones framework | Research/custom |

**Current:** Obsidian + Git (fully sovereign, battle-tested for ADHD workflow)  
**Roadmap:** Letta integration for tier-based memory, Mem0 for multi-agent coordination

### Agent Orchestrators (Pluggable)

| System | Architecture | Best For | Status |
|--------|--------------|----------|--------|
| **Hermes Agent** | Skill learning, ReAct + self-improvement | Learning from interactions, workflow automation | Live (v0.13.0) |
| **Thoth** | Local-first desktop app, knowledge graph + tools | Personal sovereignty, integrated tools (shell, vision, voice) | Exploring |
| **OpenClaw** | [Research phase] | TBD | Exploring |
| **Custom Agents** | Your own via LangGraph, Letta, or frameworks | Domain-specific assistants | Building |

**Current:** Hermes Agent (Discord) + Claude (via MCP)  
**Roadmap:** Thoth for local orchestration, multi-agent task delegation

### AI Backends (Provider-Agnostic)

| Provider | Model | Latency | Sovereignty | Cost |
|----------|-------|---------|-------------|------|
| **Anthropic (Claude)** | Claude 3.5 Sonnet | API (~1-2s) | Your API key | ~$0.003/1k tokens |
| **Local (Ollama)** | Hermes, Llama, Mistral | Instant (GPU/CPU) | Complete (local inference) | Free (your hardware) |
| **Nous Research** | Hermes 4.3 | API or local | Local option available | Free (open source) |
| **OpenAI** | GPT-4o | API (~1-2s) | Via API key | Higher cost |
| **Google** | Gemini | API | Via API key | Competitive |

**Current:** Claude (Anthropic) + Hermes qwen3.5 (Ollama local)  
**Philosophy:** Use Claude for complex reasoning, local Hermes for low-latency tasks, fallback to OpenAI if needed

### Security & Sovereignty Strategy

- **Data stays local first** — Obsidian vault on your machine, Git as backup
- **No telemetry** — Hermes Agent runs with zero cloud tracking
- **API keys, not passwords** — Control which services can access what
- **Hybrid cloud/local** — Critical paths local (Obsidian, Ollama), integrations to cloud (Claude API) as needed
- **Version control** — Everything in Git, including agent state (via Letta's `.af` format when adopted)

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

### Phase 1 (Current ✅)
- [x] Obsidian capture + Kanban + templates
- [x] Claude MCP integration (vault read/write)
- [x] Git auto-commit + backup
- [x] Hermes Agent (Discord bot, local inference)
- [x] Calendar integration

### Phase 2 (In Progress 🟢)
- [ ] **Thoth Integration** — Local-first desktop orchestrator with knowledge graph memory
  - [ ] Multi-model support (Claude, Hermes, others)
  - [ ] Tool integrations (shell, browser automation, vision)
  - [ ] Personal knowledge graph as alternative memory backend
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

### Quick Links

→ **[docs/SETUP.md](docs/SETUP.md)** — Complete step-by-step installation guide

→ **[docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)** — Technical deep-dive on how all the pieces work

→ **[HEALTH-WARNING.md](HEALTH-WARNING.md)** — Important disclaimer (read first!)

→ **[LICENSE](LICENSE)** — MIT license + comprehensive health/liability waiver

---

## Philosophy

ADHD-OS is built on a few non-negotiable principles:

1. **ADHD UX first** — If it requires willpower or "just try harder," it won't work. Infrastructure must be frictionless.
2. **Sovereignty** — Your data, your machine, your rules. No vendor lock-in or forced cloud dependency.
3. **Honest about limitations** — This is not a cure. It's not a replacement for medication or therapy. It's infrastructure that works *alongside* those.
4. **Modular** — You should be able to swap memory backends, AI providers, and orchestrators without rebuilding everything.
5. **Reliable** — The system should work offline, fail gracefully, and never lose your data.

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
