# ADHD-OS: Setup & Installation Guide

> Complete walkthrough for setting up ADHD-OS from scratch
> **Time:** 45-90 minutes depending on platform and optional components
> **Difficulty:** Beginner-friendly (no coding required for basic setup)

---

## ⚠️ Before You Start

**Read [HEALTH-WARNING.md](../HEALTH-WARNING.md) first.** ADHD-OS is not a medical device and should not replace professional ADHD care.

---

## Requirements

### Hardware
- **Computer:** Mac (M1+), Linux, or Windows 10+ (with WSL2)
- **RAM:** 16GB minimum (32GB recommended if running Ollama locally)
- **Storage:** 20GB free (includes Ollama models)
- **Internet:** For cloud AI providers; local-only setup also possible

### Software (to be installed)
- **Git** — Version control (free)
- **Obsidian** — Note-taking app (free for personal use)
- **Ollama** — Local LLM inference (free, optional)
- **Node.js 20+** — For Hermes Agent (optional)

### Accounts (optional but recommended)
- **Anthropic API key** — For Claude access (~$0.003 per 1K tokens)
- **GitHub account** — For backup/version control (free tier fine)
- **Google account** — For Calendar integration (optional)

---

## Part 1: Essential Setup (30 min)

### 1.1 Install Git

**macOS (Homebrew):**
```bash
brew install git
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```

**Windows (WSL2):**
```bash
sudo apt update
sudo apt install git
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```

**Linux:**
```bash
sudo apt install git  # Debian/Ubuntu
# or
sudo dnf install git  # Fedora/RHEL
```

### 1.2 Clone the ADHD-OS Repository

```bash
git clone https://github.com/LegionForge/ADHD-OS.git
cd ADHD-OS
```

### 1.3 Install Obsidian

1. Download from [obsidian.md](https://obsidian.md)
2. Install for your platform
3. **Create a new vault:**
   - Open Obsidian
   - Click "Create new vault"
   - Name it `adhd-os-vault` (or your choice)
   - Choose a local directory (e.g., `~/Documents/adhd-os-vault`)
   - Click "Create"

### 1.4 Initialize Git in Your Vault

```bash
cd ~/Documents/adhd-os-vault  # Or wherever you created the vault
git init
git config user.name "Your Name"
git config user.email "your-email@example.com"
```

### 1.5 Set Up Auto-Commit (macOS/Linux)

Create a Git post-commit hook to auto-commit every 5 minutes:

**Create the hook file:**
```bash
cat > ~/Documents/adhd-os-vault/.git/hooks/post-commit << 'EOF'
#!/bin/bash
# Auto-commit every 5 minutes
(sleep 300; cd "$(git rev-parse --show-toplevel)" && git add -A && git commit -m "auto: vault update" 2>/dev/null) &
EOF

chmod +x ~/Documents/adhd-os-vault/.git/hooks/post-commit
```

**Windows (WSL2):**
Use the same command in WSL2 terminal.

---

## Part 2: Obsidian Configuration (15 min)

### 2.1 Create Vault Structure

In Obsidian, create these folders:

```
.
├── 📁 Daily Notes/
├── 📁 Projects/
├── 📁 Tasks/
├── 📁 Reference/
├── 📁 Templates/
└── 📁 Archive/
```

Right-click in Obsidian file explorer → New folder

### 2.2 Enable Core Plugins

**Settings → Core plugins → Enable:**
- ✅ Daily Notes
- ✅ Templates
- ✅ Backlinks
- ✅ Tag Pane
- ✅ File Explorer
- ✅ Outline

### 2.3 Install Community Plugins

**Settings → Community plugins → Search & install:**

| Plugin | Purpose |
|--------|---------|
| **Kanban** | Visual Kanban board for task management |
| **Dataview** | Query and display vault data |
| **Calendar** | Calendar view for Daily Notes |
| **Periodic Notes** | Weekly/Monthly/Quarterly notes |
| **Multi-tag** | Better tag management |
| **Templater** | Advanced template system |
| **QuickAdd** | Quick capture (keyboard shortcuts for new notes) |

After installing, enable each plugin in Settings → Community plugins

### 2.4 Configure Daily Notes

**Settings → Daily Notes:**
- Date format: `YYYY-MM-DD`
- Template location: `Templates/Daily Note`
- Folder: `Daily Notes`

### 2.5 Create Note Templates

**Create `Templates/Daily Note.md`:**
```markdown
# Daily Note — [[{{date:YYYY-MM-DD}}]]

## ✅ Priority (1-3 items max)
- [ ] 

## 🧠 Inbox (capture throughout day)
- 

## 📊 Kanban
Link to your main Kanban board or embed it

## 📝 Session Notes
*Notes from Claude/AI sessions*

## 🎯 Tomorrow's Focus
*What's your one thing tomorrow?*

---
tags: #daily
```

**Create `Templates/Project.md`:**
```markdown
# Project: {{title}}

**Status:** 🟢 Active / 🟡 On Hold / 🔴 Blocked / ✅ Complete

**Goal:** 
*One sentence: what does success look like?*

**Why:** 
*Why does this matter?*

**Next Action:** 
*What's the very next step?*

**Blockers:** 
- 

**Resources:** 
- 

---
tags: #project
```

### 2.6 Create Main Kanban Board

**Create `Projects/Kanban.md`:**
```markdown
# ADHD-OS Kanban

## Inbox
- New items go here
- They get triaged daily

## 🎯 Current
- Item 1 (limited to 1-3)

## ⏳ Inception/Ongoing
- Hyperfocus items
- Tangents (explicitly allowed)

## 🚧 In Progress
- Active work

## ⏸️ Waiting
- Blocked on external input

## ✅ Done
- Weekly review

---
`

```dataview
task from ""
group by status
```
```

---

## Part 3: Claude MCP Setup (20 min)

### 3.1 Get Anthropic API Key

1. Go to [console.anthropic.com](https://console.anthropic.com)
2. Sign up or log in
3. Create an API key
4. Copy the key (keep it secret!)

### 3.2 Install Claude Code (CLI or Desktop)

**Option A: CLI (Recommended)**
```bash
# macOS
brew install anthropic/claude/claude-code

# Linux/Windows (WSL2)
npm install -g @anthropic-ai/claude-code
```

**Option B: Desktop App**
- Download from [claude.com/claude-code](https://claude.com/claude-code)

### 3.3 Configure Claude Code with Your Vault

Create a `.claude/settings.local.json` in your vault:

```json
{
  "vault_path": "~/Documents/adhd-os-vault",
  "mcp_config": {
    "obsidian": {
      "vault_dir": "~/Documents/adhd-os-vault"
    }
  },
  "permissions": {
    "read_obsidian": true,
    "write_obsidian": true,
    "read_git": true,
    "write_git": true
  }
}
```

### 3.4 Test Claude MCP Connection

Start Claude Code in your vault directory:
```bash
cd ~/Documents/adhd-os-vault
claude-code
```

In the chat, try:
```
Can you list my Recent notes?
```

If you see your vault files listed, MCP is working! ✅

---

## Part 4: Optional — Local AI with Ollama (15 min)

### 4.1 Install Ollama

1. Download from [ollama.ai](https://ollama.ai)
2. Install for your platform
3. Run: `ollama serve`

### 4.2 Pull a Model

In another terminal:
```bash
# Hermes (recommended for ADHD-OS, ~7GB)
ollama pull hermes:latest

# Or lightweight alternative
ollama pull mistral:latest

# Check what's installed
ollama list
```

### 4.3 Test Local Inference

```bash
curl http://localhost:11434/api/generate -d '{
  "model": "hermes",
  "prompt": "What is ADHD?",
  "stream": false
}'
```

If you get a response, Ollama is working! ✅

---

## Part 5: Optional — Hermes Agent (25 min)

### 5.1 Install Node.js

**macOS:**
```bash
brew install node@20
```

**Linux:**
```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs
```

**Windows (WSL2):**
```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs
```

### 5.2 Install Hermes Agent

```bash
npm install -g hermes-agent
```

### 5.3 Initialize Hermes Agent

```bash
hermes init
# Follow prompts:
# - Memory backend: Obsidian (or Letta if installed)
# - Model: hermes (local via Ollama)
# - Vault path: ~/Documents/adhd-os-vault
# - Auto-start: yes
```

### 5.4 Verify Hermes is Running

```bash
hermes status
# Should show: ✅ Running on port 8080
```

---

## Part 6: Google Calendar Integration (Optional, 10 min)

### 6.1 Enable Google Calendar Access

1. Go to [console.cloud.google.com](https://console.cloud.google.com)
2. Create a new project: `adhd-os`
3. Enable Google Calendar API
4. Create OAuth 2.0 credentials (Desktop app)
5. Download JSON credentials

### 6.2 Connect to Obsidian

1. In Obsidian, install plugin: **Google Calendar**
2. Paste your credentials JSON
3. Authenticate with Google account
4. Authorize ADHD-OS access to Calendar

---

## Verification Checklist

Run this to verify everything is working:

```bash
#!/bin/bash
echo "=== ADHD-OS Setup Verification ==="

# Git
echo "✓ Git:" $(git --version)

# Obsidian (check vault exists)
if [ -d ~/Documents/adhd-os-vault ]; then
  echo "✓ Obsidian vault found"
else
  echo "✗ Obsidian vault NOT found"
fi

# Ollama
if pgrep -x "ollama" > /dev/null; then
  echo "✓ Ollama running"
  curl -s http://localhost:11434/api/tags | jq '.models | length' | xargs -I {} echo "  {} models available"
else
  echo "⚠ Ollama not running (optional)"
fi

# Hermes Agent
if pgrep -x "hermes" > /dev/null; then
  echo "✓ Hermes Agent running"
else
  echo "⚠ Hermes Agent not running (optional)"
fi

# Claude Code
if command -v claude-code &> /dev/null; then
  echo "✓ Claude Code installed"
else
  echo "✗ Claude Code NOT found"
fi

echo ""
echo "=== Setup Status ==="
echo "Essential: Git ✓, Obsidian ✓, Claude Code ✓"
echo "Optional: Ollama, Hermes Agent, Google Calendar"
```

---

## First Session: Getting Started

### 1. Open Daily Note

In Obsidian, create today's daily note:
- Click "Create new Daily Note" (or Calendar → today)
- It should use your Daily Note template

### 2. Capture Something

In the Inbox section, add a thought or task:
```
- Set up ADHD-OS (move to Current → In Progress when ready)
- Review Kanban board weekly (move to Waiting for next review)
```

### 3. Triage to Kanban

Move important items to your Kanban board:
```
## Current
- [ ] Complete ADHD-OS setup

## Inception/Ongoing
- [ ] Explore Thoth integration (future phase)
```

### 4. Create First Project Note

Open your first project:
```
# Project: Learn ADHD-OS

**Status:** 🟢 Active

**Goal:** Understand how to use ADHD-OS for daily work

**Next Action:** Create a Daily Note template and test capture workflow

**Blockers:** None
```

### 5. Start Claude Code Session

```bash
cd ~/Documents/adhd-os-vault
claude-code
```

In Claude:
```
Can you help me review my ADHD-OS setup? 
Here's my vault structure: [Claude will read it via MCP]
```

Claude can now read and write to your vault directly!

---

## Troubleshooting

### Obsidian vault not syncing
- Check: Is Git running? (`git status` in vault directory)
- Check: Do you have write permissions? (`ls -la .git`)
- Solution: Re-init Git and add files manually

### Claude Code can't read Obsidian
- Check: Is MCP configured? (verify `settings.local.json`)
- Check: Is vault path correct?
- Solution: Restart Claude Code after config changes

### Ollama models are slow
- Check: Is GPU detected? (`ollama info`)
- Solution: Run smaller model (mistral instead of hermes)
- Fallback: Use Claude API (cloud-based, faster but requires internet)

### Hermes Agent won't start
- Check: Node.js version: `node --version` (should be 20+)
- Check: Ollama running: `ollama status`
- Solution: `hermes restart`

---

## Next Steps

Now that you're set up:

1. **Read [ARCHITECTURE.md](ARCHITECTURE.md)** — Understand how the pieces fit together
2. **Review [../README.md](../README.md)** — Core philosophy and ADHD-specific patterns
3. **Create your first Kanban** — Start capturing and prioritizing
4. **Set up auto-commit** — Let Git back up your work automatically
5. **Explore integrations** — Calendar, Claude MCP, optional Ollama/Hermes

---

## Support & Questions

- **Setup issues?** Check Troubleshooting section above
- **Want to contribute?** See [CONTRIBUTING.md](../CONTRIBUTING.md)
- **Health concerns?** Re-read [HEALTH-WARNING.md](../HEALTH-WARNING.md)
- **Technical deep-dive?** See [ARCHITECTURE.md](ARCHITECTURE.md)

---

**Last Updated:** 2026-05-29
**License:** MIT (see [LICENSE](../LICENSE))
