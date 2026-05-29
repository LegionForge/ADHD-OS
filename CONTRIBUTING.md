# Contributing to ADHD-OS

Thank you for your interest in contributing to ADHD-OS. This is a community project, and contributions are welcome in many forms.

---

## Ways to Contribute

### 1. **Share Your Experience**

ADHD brains are wonderfully diverse. What works for one person may not work for another.

- **What works for you?** Share your ADHD-OS workflow, templates, or agent setups
- **What doesn't work?** Tell us what broke or felt clunky
- **[Open an issue](https://github.com/LegionForge/ADHD-OS/issues)** with tag `#experience`

### 2. **Report Bugs**

Found a bug in setup instructions, documentation, or code?

- **[Create an issue](https://github.com/LegionForge/ADHD-OS/issues)** with:
  - What you were trying to do
  - What happened instead
  - Your platform (macOS/Linux/Windows + version)
  - Steps to reproduce

### 3. **Improve Documentation**

Documentation is critical for ADHD-friendly software. Clear, organized docs reduce friction.

- **Setup guide improvements** — Spotted a confusing step? [Submit a PR](https://github.com/LegionForge/ADHD-OS/pulls)
- **Real-world workflow docs** — Document patterns that work (ADHD-PATTERNS.md)
- **Clarify architecture** — Is something unclear in ARCHITECTURE.md?
- **Fix typos** — Yes, even typos matter

### 4. **Build & Share Agents**

Agents are the core of ADHD-OS extensibility.

- **Custom agents** — Build agents for specific workflows (research, debugging, writing, review)
- **Share your agent** — [Open a discussion](https://github.com/LegionForge/ADHD-OS/discussions) or submit a PR with your agent
- **Agent library** — We're building a community library; yours could be in it

**Example agent types we're seeking:**
- Research agent (synthesis, deep dives, fact-checking)
- Code agent (writing, testing, debugging)
- Review agent (quality, security, completeness)
- Writing agent (drafting, editing, tone adjustment)
- Debugging agent (root cause analysis, hypothesis testing)
- Personal knowledge graph agent (entity extraction, relationship inference)

### 5. **Contribute Memory Backends**

ADHD-OS is designed to support multiple memory systems.

- **Letta integration** — Help integrate Letta's tiered memory
- **Mem0 integration** — Add Mem0 for multi-agent memory coordination
- **Custom memory backend** — Build your own memory system

If you're working on this, **please open a discussion first** to align on architecture.

### 6. **Build Thoth/Orchestration Patterns**

Phase 2 exploration involves Thoth and other orchestration frameworks.

- **Thoth integration guide** — How to set up Thoth + Obsidian together
- **LangGraph patterns** — Build complex agent workflows
- **Orchestration examples** — Multi-agent task delegation patterns

### 7. **Create Obsidian Templates**

Non-coders can create and share templates.

- **Daily note templates** — Optimized for ADHD capture patterns
- **Project templates** — Structured project setup for consistency
- **Review templates** — Weekly/monthly/quarterly review formats
- **Kanban templates** — Alternative priority management structures

Share via [discussion](https://github.com/LegionForge/ADHD-OS/discussions) with tag `#templates`

### 8. **Translate & Localize**

Help ADHD-OS reach people in other languages and locales.

- **Translate docs** — README, SETUP, ARCHITECTURE to your language
- **Localize setup** — Adapt commands for your platform/region
- **Cultural adaptations** — ADHD manifests differently across cultures

---

## Contribution Guidelines

### Before You Start

1. **Read [HEALTH-WARNING.md](HEALTH-WARNING.md)** — We take medical disclaimers seriously
2. **Read [LICENSE](LICENSE)** — MIT license + health/liability waiver apply
3. **Read [ARCHITECTURE.md](docs/ARCHITECTURE.md)** — Understand how pieces fit together

### Making a PR

1. **Fork the repo** → make your changes → submit a PR
2. **Clear commit messages:**
   ```
   docs: improve SETUP.md clarity on MCP configuration
   
   - Clarify which API key to use (Anthropic, not OpenAI)
   - Add screenshot of settings screen
   - Add troubleshooting section for common MCP errors
   ```

3. **Describe what & why:**
   - What problem are you solving?
   - Why this approach over alternatives?
   - Any breaking changes or dependencies?

4. **Keep scope focused:**
   - One feature/fix per PR
   - Small is better (easier to review)
   - If large, open an issue first to discuss

### Documentation Standards

- **Clear language** — Explain for someone new to ADHD-OS
- **Avoid jargon** — Or define it when necessary
- **Include examples** — Show concrete usage, not just theory
- **Link liberally** — Help readers navigate related content
- **Test your changes** — Verify setup docs work by following them yourself

### Code Standards

For agents and integrations:

- **Type hints** — Help with IDE autocomplete
- **Docstrings** — Explain what the function does
- **Error messages** — Make them ADHD-friendly (clear, specific, actionable)
- **No telemetry** — ADHD-OS data stays local
- **No required cloud services** — Work offline or with fallbacks

### Licensing

All contributions are under MIT license (see [LICENSE](LICENSE)). By submitting a PR, you agree to license your work under MIT.

---

## Getting Help

### Questions?

- **[GitHub Discussions](https://github.com/LegionForge/ADHD-OS/discussions)** — Ask questions, share ideas
- **[GitHub Issues](https://github.com/LegionForge/ADHD-OS/issues)** — Report bugs, request features
- **Email:** info@legionforge.org — Governance, contribution policy questions

### Not Sure What to Contribute?

Check the [GitHub issues](https://github.com/LegionForge/ADHD-OS/issues) — we tag things by difficulty:

- `#good-first-issue` — Start here if new to the project
- `#help-wanted` — We'd love your expertise here
- `#documentation` — Improve docs (non-code contribution)

---

## Community Standards

ADHD-OS is built by and for people with ADHD. We value:

- **Honesty** — About what works, what doesn't, what you don't understand
- **Neurodiversity** — Different brains, different approaches, all valid
- **No shame** — You don't need to be "productive enough" to contribute
- **Accessibility** — Clear communication, patience, kindness
- **Sovereignty** — Respecting personal data and system autonomy

### Be Kind

People with ADHD face constant criticism. This is a safe space. If someone's approach looks "inefficient" to you, remember: it might be the only way their brain can work. Curiosity over judgment.

---

## Recognition

We recognize contributors through:

- **README contributors section** — Your name/GitHub handle (if you want it)
- **Commit history** — Git immortalizes your work
- **Release notes** — Highlighted features credited to you
- **Community discussions** — Shout-outs for significant contributions

---

## Code of Conduct

This project follows a simple code of conduct:

1. **Be respectful** — Even (especially) when disagreeing
2. **Assume good intent** — People are trying their best
3. **No discrimination** — All neurotypes, genders, orientations, races, abilities welcome
4. **Focus on the work** — Attack ideas, not people
5. **Respect boundaries** — "No" is a complete sentence

Violations can be reported to **info@legionforge.org**

---

## Questions About Contributing?

- **Architecture/design questions?** → Open a [discussion](https://github.com/LegionForge/ADHD-OS/discussions)
- **Bug reports?** → [Open an issue](https://github.com/LegionForge/ADHD-OS/issues)
- **Policy/governance?** → Email info@legionforge.org
- **Just want to chat?** → [Discussions](https://github.com/LegionForge/ADHD-OS/discussions) is the place

---

## Thank You

Thank you for contributing. ADHD-OS is only possible because people like you care about making tools that work for ADHD brains.

Your work matters. 💙

---

**Last Updated:** 2026-05-29
**License:** MIT (see [LICENSE](LICENSE))
