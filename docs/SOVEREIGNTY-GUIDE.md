# ADHD-OS: Complete Sovereignty Guide

> Step-by-step instructions for running ADHD-OS entirely on your machine with zero external dependencies (except optional Git backup)

---

## The Vision: Full Data Sovereignty

**Current setup** (recommended for most):
- Obsidian vault on your machine ✅
- Claude API (external, cloud)
- Google Calendar (external, cloud)
- Hermes on Discord (external, cloud comms)

**Sovereign setup** (this guide):
- Obsidian vault on your machine ✅
- Local LLM via Ollama (Qwen3/DeepSeek R1) ✅
- Nextcloud Calendar (self-hosted, your server) ✅
- Local agent framework (LangChain) ✅
- Matrix/Element chat (self-hosted, encrypted) ✅
- Email webhooks (optional, for notifications) ✅

**Result:** Everything runs on your hardware. Zero data sent outside your network except:
- Optional Git backup to GitHub (encrypted, you control it)
- Optional email notifications (you choose the provider)

---

## Part 1: Prerequisites

### Hardware
- **Mac Mini M1/M4, Linux, or Windows (WSL2)**
- **Minimum:** 16GB RAM (32GB recommended for local LLM + Nextcloud)
- **Storage:** 50GB free (Nextcloud + models)
- **Internet:** Only for initial setup and optional Git backup

### Software
- **Docker & Docker Compose** (for Nextcloud, Matrix)
- **Ollama** (local LLM serving)
- **Git** (version control, optional backup)
- **Python 3.10+** (for agent framework)
- **Node.js 20+** (optional, for Matrix bot)

### Time Investment
- **Basic setup:** 2-3 hours
- **Full integration:** 4-6 hours
- **Testing & tuning:** 1-2 hours

---

## Part 2: Setup Checklist

### ✅ Phase 1: Core Infrastructure (1.5 hours)

#### Step 1: Install Docker & Compose

**macOS:**
```bash
# Install Docker Desktop (https://www.docker.com/products/docker-desktop)
# Then verify:
docker --version
docker-compose --version
```

**Linux:**
```bash
sudo apt update && sudo apt install -y docker.io docker-compose
sudo usermod -aG docker $USER
# Restart to apply group changes
```

**Windows (WSL2):**
```bash
wsl --install Ubuntu
# Install Docker Desktop for Windows with WSL2 backend
```

#### Step 2: Install Ollama

**macOS:**
```bash
# Download from https://ollama.ai
# Or via Homebrew:
brew install ollama

# Start Ollama service:
ollama serve
```

**Linux:**
```bash
curl -fsSL https://ollama.ai/install.sh | sh
# Start:
ollama serve
```

**Windows (WSL2):**
```bash
# In WSL2 terminal:
curl -fsSL https://ollama.ai/install.sh | sh
ollama serve
```

#### Step 3: Pull a Local Model

**In another terminal:**
```bash
# Option A: Qwen3 (recommended, balanced)
ollama pull qwen3  # ~13GB

# Option B: DeepSeek R1 (better reasoning, slower)
ollama pull deepseek-r1  # ~7GB

# Option C: Phi-4 (lightweight reasoning)
ollama pull phi-4  # ~7GB

# Verify it's running:
curl http://localhost:11434/api/tags | jq '.models'
```

**Expected output:**
```json
{
  "models": [
    {
      "name": "qwen3:latest",
      "modified_time": "2026-05-29T10:00:00Z",
      "size": 13000000000
    }
  ]
}
```

#### Step 4: Create Docker Network (for services to communicate)

```bash
docker network create adhd-os
```

---

### ✅ Phase 2: Self-Hosted Services (2 hours)

#### Step 5: Deploy Nextcloud Calendar (Self-Hosted)

**Create docker-compose.yml:**

```yaml
version: '3.8'

services:
  nextcloud-db:
    image: postgres:15
    container_name: nextcloud-db
    environment:
      POSTGRES_DB: nextcloud
      POSTGRES_USER: nextcloud
      POSTGRES_PASSWORD: your_secure_password  # Change this!
    volumes:
      - nextcloud_db:/var/lib/postgresql/data
    networks:
      - adhd-os
    restart: unless-stopped

  nextcloud:
    image: nextcloud:latest
    container_name: nextcloud
    environment:
      NEXTCLOUD_ADMIN_USER: admin
      NEXTCLOUD_ADMIN_PASSWORD: your_admin_password  # Change this!
      POSTGRES_HOST: nextcloud-db
      POSTGRES_DB: nextcloud
      POSTGRES_USER: nextcloud
      POSTGRES_PASSWORD: your_secure_password
    volumes:
      - nextcloud_data:/var/www/html
    ports:
      - "8080:80"
    networks:
      - adhd-os
    depends_on:
      - nextcloud-db
    restart: unless-stopped

volumes:
  nextcloud_data:
  nextcloud_db:

networks:
  adhd-os:
    external: true
```

**Deploy:**
```bash
docker-compose up -d
# Wait for startup (~1-2 min)
# Access at http://localhost:8080
```

**Configure Calendar:**
1. Log in with admin credentials
2. Go to **Apps** → search "Calendar"
3. Click **Install**
4. Go to **Calendar** app
5. Create calendar: "ADHD-OS"

#### Step 6: Deploy Matrix/Element (Self-Hosted Chat)

**Create matrix-docker-compose.yml:**

```yaml
version: '3.8'

services:
  synapse:
    image: matrixdotorg/synapse:latest
    container_name: matrix-synapse
    environment:
      SYNAPSE_SERVER_NAME: adhd-os.local
      SYNAPSE_REPORT_STATS: 'no'
    volumes:
      - synapse_data:/data
    ports:
      - "8008:8008"
    networks:
      - adhd-os
    restart: unless-stopped

  element:
    image: vectorim/element-web:latest
    container_name: element-web
    volumes:
      - ./element-config.json:/app/config.json
    ports:
      - "8081:80"
    networks:
      - adhd-os
    depends_on:
      - synapse
    restart: unless-stopped

volumes:
  synapse_data:

networks:
  adhd-os:
    external: true
```

**Create element-config.json:**
```json
{
  "default_server_config": {
    "m.homeserver": {
      "base_url": "http://localhost:8008",
      "server_name": "adhd-os.local"
    },
    "m.identity_server": {
      "base_url": "https://vector.im"
    }
  }
}
```

**Deploy:**
```bash
docker-compose -f matrix-docker-compose.yml up -d
# Access web UI at http://localhost:8081
```

**Create account:**
1. Open http://localhost:8081
2. Click **Create account**
3. Username: `adhd-agent`
4. Password: secure password
5. Server: `adhd-os.local`

---

### ✅ Phase 3: Local Agent Framework (1-2 hours)

#### Step 7: Install LangChain + Ollama

```bash
# Create project directory
mkdir adhd-os-agent
cd adhd-os-agent

# Create virtual environment
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install langchain langchain-community python-dotenv
```

#### Step 8: Create ADHD-OS Agent

**Create `adhd_agent.py`:**

```python
import os
from langchain_community.llms import Ollama
from langchain.prompts import PromptTemplate
from langchain.chains import LLMChain

# Initialize Ollama (pointing to local model)
llm = Ollama(
    model="qwen3",  # or "deepseek-r1", "phi-4"
    base_url="http://localhost:11434",
    temperature=0.7
)

# Define system prompt for ADHD-aware agent
system_prompt = """You are an ADHD-OS executive function agent.

Your role:
- Help capture thoughts without judgment
- Route tasks to appropriate locations (Inbox, Current, Waiting, etc.)
- Watch for troubleshooting loops and interrupt with diagnostics
- Provide time-aware reminders and break suggestions
- Support working memory externalization via session notes

ADHD-friendly interaction:
- Be direct and specific (avoid vague advice)
- Validate hyperfocus, don't shame it
- Provide clear next steps (reduce decision-making)
- Check for activation energy barriers
- Use external structure (calendars, checklists, reminders)

When responding:
- Keep responses concise (ADHD working memory is small)
- Offer choices, don't impose
- Assume good intent
- Celebrate small wins
"""

# Create prompt template
prompt = PromptTemplate(
    input_variables=["user_message", "context"],
    template=system_prompt + "\n\nUser context: {context}\n\nUser: {user_message}\n\nADHD-OS Agent:"
)

# Create chain
chain = LLMChain(llm=llm, prompt=prompt)

# Test the agent
def run_agent(user_message, context=""):
    response = chain.run(
        user_message=user_message,
        context=context or "Starting fresh session"
    )
    return response

# Example usage
if __name__ == "__main__":
    # Test capture
    response = run_agent(
        user_message="I just thought of something - need to check React 19 performance",
        context="Currently writing documentation"
    )
    print("Agent response:", response)
    
    # Test loop-breaking
    response = run_agent(
        user_message="I've restarted Docker 3 times and still getting the same error",
        context="Debugging Nextcloud deployment"
    )
    print("Loop-breaker response:", response)
```

#### Step 9: Create Calendar Integration

**Create `calendar_agent.py`:**

```python
from datetime import datetime, timedelta
from typing import Optional
import requests
from langchain_community.llms import Ollama

class NextcloudCalendar:
    def __init__(self, host: str, user: str, password: str):
        self.host = host
        self.user = user
        self.password = password
        self.base_url = f"{host}/remote.php/dav/calendars/{user}"
        self.auth = (user, password)
    
    def create_event(self, title: str, description: str, duration_minutes: int = 60):
        """Create a calendar event with reminders"""
        start = datetime.now()
        end = start + timedelta(minutes=duration_minutes)
        
        # iCalendar format
        ical = f"""BEGIN:VCALENDAR
VERSION:2.0
PRODID:-//ADHD-OS//Event//EN
BEGIN:VEVENT
UID:{start.isoformat()}
DTSTAMP:{start.isoformat()}
DTSTART:{start.isoformat()}
DTEND:{end.isoformat()}
SUMMARY:{title}
DESCRIPTION:{description}
BEGIN:VALARM
TRIGGER:-PT15M
ACTION:DISPLAY
DESCRIPTION:Reminder
END:VALARM
END:VEVENT
END:VCALENDAR"""
        
        # Create event
        response = requests.put(
            f"{self.base_url}/personal/{title.replace(' ', '_')}.ics",
            data=ical,
            auth=self.auth,
            headers={"Content-Type": "text/calendar"}
        )
        return response.status_code == 201
    
    def list_events(self):
        """List upcoming events"""
        response = requests.get(
            f"{self.base_url}/personal/",
            auth=self.auth
        )
        return response.text

# Usage
calendar = NextcloudCalendar(
    host="http://localhost:8080",
    user="admin",
    password="your_admin_password"
)

# Create time block
calendar.create_event(
    title="Deep Work - Documentation",
    description="ADHD-OS pattern writing with breaks",
    duration_minutes=120
)
```

---

### ✅ Phase 4: Communication & Notifications (30 min)

#### Step 10: Matrix Bot for Agent Responses

**Create `matrix_bot.py`:**

```python
import asyncio
from nio import AsyncClient, RoomMessageText, InviteEvent
from adhd_agent import run_agent

class ADHDOSMatrixBot:
    def __init__(self, homeserver: str, user_id: str, password: str):
        self.client = AsyncClient(homeserver, user_id)
        self.password = password
        self.user_id = user_id
    
    async def login(self):
        await self.client.login(self.password)
        print(f"Logged in as {self.user_id}")
    
    async def handle_message(self, room_id: str, message: str):
        """Process message and respond"""
        # Get context (room name or recent messages)
        context = f"Channel: {room_id}"
        
        # Run agent
        response = run_agent(
            user_message=message,
            context=context
        )
        
        # Send response back
        await self.client.room_send(
            room_id,
            "m.room.message",
            {
                "msgtype": "m.text",
                "body": response
            }
        )
    
    async def sync(self):
        """Listen for messages"""
        self.client.add_event_callback(
            self.handle_message,
            RoomMessageText
        )
        
        await self.client.sync_forever(timeout=30000)

async def main():
    bot = ADHDOSMatrixBot(
        homeserver="http://localhost:8008",
        user_id="@adhd-agent:adhd-os.local",
        password="agent_password"
    )
    
    await bot.login()
    await bot.sync()

if __name__ == "__main__":
    asyncio.run(main())
```

**Run the bot:**
```bash
pip install matrix-client
python matrix_bot.py
```

---

## Part 3: Integration Testing

### ✅ Verify Everything Works

**Test Ollama:**
```bash
curl -X POST http://localhost:11434/api/generate \
  -d '{
    "model": "qwen3",
    "prompt": "What is ADHD executive function?",
    "stream": false
  }' | jq '.response'
```

**Test Nextcloud Calendar:**
```bash
curl -u admin:password http://localhost:8080/remote.php/dav/calendars/admin/personal/ \
  -H "Depth: 1" \
  | grep -o '<d:displayname>[^<]*'
```

**Test Matrix:**
```bash
# Log into http://localhost:8081 with your account
# Create a room
# Send a message (bot should respond if running)
```

**Test Agent:**
```bash
python adhd_agent.py
# Should see response from local Qwen3
```

---

## Part 4: Connect to Obsidian

### Link Nextcloud Calendar to Obsidian

**Install CalDAV plugin:**
1. In Obsidian → Settings → Community plugins → Browse
2. Search "CalDAV Synchronizer"
3. Install and enable
4. Configure:
   - URL: `http://localhost:8080/remote.php/dav/calendars/admin/personal/`
   - Username: `admin`
   - Password: your password
   - Sync folder: `Calendar` (in vault)

**Result:** Calendar events sync to Obsidian, visible in daily notes.

### Link Agent to Obsidian

**Create `obsidian_agent.py`:**

```python
import json
from pathlib import Path
from adhd_agent import run_agent

class ObsidianAgent:
    def __init__(self, vault_path: str):
        self.vault = Path(vault_path)
    
    def capture_to_inbox(self, thought: str):
        """Add thought to daily inbox"""
        daily_note = self.vault / "Daily Notes" / "Today.md"
        
        if not daily_note.exists():
            daily_note.write_text("# Daily Note\n\n## Inbox\n")
        
        content = daily_note.read_text()
        content += f"- {thought}\n"
        daily_note.write_text(content)
    
    def write_session_note(self, title: str, summary: str):
        """Write session note for context restore"""
        session_file = self.vault / "Daily Notes" / f"Session_{title}.md"
        
        note = f"""# Session: {title}

## Summary
{summary}

## Key Decisions
- (add decisions here)

## Blockers
- (add blockers here)

## What's Next
1. (next step)
2. (next step)
"""
        session_file.write_text(note)

# Usage
agent = ObsidianAgent(vault_path="/path/to/vault")

response = run_agent("I need to remember to check React 19 performance")
agent.capture_to_inbox(response)

agent.write_session_note(
    "Documentation Writing",
    "Completed ADHD patterns 1-3, next: time blindness patterns"
)
```

---

## Part 5: Backup & Maintenance

### Optional: Git Backup to GitHub

**Why:** Even with full sovereignty, backups protect against hardware failure

**Setup:**
```bash
# Create private GitHub repo: adhd-os-vault

cd ~/Documents/adhd-os-vault
git init
git remote add origin https://github.com/YOUR_USERNAME/adhd-os-vault.git

# Add to .gitignore (never commit credentials):
echo ".env" >> .gitignore
echo "secrets/" >> .gitignore
echo "node_modules/" >> .gitignore

# Commit and push
git add .
git commit -m "Initial ADHD-OS vault backup"
git push -u origin main

# Set up auto-commit (every 5 min):
# (See SETUP.md for git hook instructions)
```

### Docker Maintenance

**Backup volumes:**
```bash
# Backup Nextcloud data
docker run --rm \
  -v nextcloud_data:/data \
  -v /backup:/backup \
  alpine tar czf /backup/nextcloud-backup.tar.gz -C /data .

# Backup Matrix data
docker run --rm \
  -v synapse_data:/data \
  -v /backup:/backup \
  alpine tar czf /backup/synapse-backup.tar.gz -C /data .
```

**Update containers:**
```bash
docker-compose pull
docker-compose up -d --remove-orphans
```

---

## Part 6: Performance & Optimization

### Local LLM Tuning

**For faster responses (trade off quality):**
```python
# Use smaller model
llm = Ollama(model="phi-4", ...)  # ~3-5s per query

# Or increase CPU threads
ollama run qwen3 --num-thread 8
```

**For better quality (slower):**
```python
# Use larger model
llm = Ollama(model="deepseek-r1", ...)  # ~10-15s per query

# Or increase context window
llm = Ollama(model="qwen3", num_ctx=4096)
```

### Nextcloud Optimization

**Enable caching:**
```bash
# Edit docker-compose.yml
environment:
  REDIS_HOST: redis
  REDIS_PORT: 6379

# Add Redis service
  redis:
    image: redis:alpine
    container_name: nextcloud-redis
    networks:
      - adhd-os
```

### Memory Management

**Check resource usage:**
```bash
# Monitor Docker containers
docker stats

# Typical consumption:
# Nextcloud: 300-500MB
# Matrix: 200-300MB
# Ollama + model: 8-16GB (depends on model size)
```

---

## Part 7: Troubleshooting

### Ollama Not Responding

```bash
# Check if service is running
ps aux | grep ollama

# Restart service
ollama serve

# Test connection
curl http://localhost:11434/api/tags
```

### Nextcloud Calendar Sync Issues

```bash
# Check logs
docker logs nextcloud

# Verify CalDAV endpoint
curl -u admin:password \
  http://localhost:8080/remote.php/dav/calendars/admin/personal/ \
  -H "Depth: 1"
```

### Matrix Bot Not Responding

```bash
# Check logs
docker logs matrix-synapse

# Verify bot is running
ps aux | grep matrix_bot

# Check Matrix server is accessible
curl http://localhost:8008/_matrix/client/versions
```

---

## Part 8: Scaling & Expansion

### Add More Agents

Create specialized agents for different workflows:

```python
# Research agent
research_agent = ADHDOSAgent(
    model="qwen3",
    system_prompt="You are a research assistant focused on synthesis..."
)

# Code agent
code_agent = ADHDOSAgent(
    model="phi-4",  # Good for coding
    system_prompt="You are an expert programmer..."
)

# Writing agent
writing_agent = ADHDOSAgent(
    model="qwen3",
    system_prompt="You are an expert writer..."
)
```

### Multi-Machine Setup

Run services on separate machines:

```
Mac Mini #1 (JP):
- Obsidian vault
- Local Ollama (Qwen3)
- LangChain agent

Mac Mini #2 (Server):
- Nextcloud Calendar
- Matrix/Element server
- Agent bots (Matrix, Discord alternative)

Benefits:
- Dedicated hardware for each service
- Always-on infrastructure (server machine)
- Distributed, resilient system
```

---

## Part 9: Security Considerations

### Secure Credentials

**Use environment variables, not hardcoded:**

```bash
# Create .env file (add to .gitignore)
NEXTCLOUD_ADMIN_PASSWORD=your_secure_password
MATRIX_PASSWORD=your_secure_password
OLLAMA_BASE_URL=http://localhost:11434

# Load in Python
from dotenv import load_dotenv
import os

load_dotenv()
nc_password = os.getenv("NEXTCLOUD_ADMIN_PASSWORD")
```

### Firewall Rules

**Only expose ports you need:**

```bash
# Close external access to internal services
# Only expose if accessing from other machines on LAN
# Example: UFW (macOS alternative: pfctl)

sudo ufw allow from 192.168.1.0/24 to any port 8080  # Nextcloud (LAN only)
sudo ufw allow from 192.168.1.0/24 to any port 8008  # Matrix (LAN only)
```

### Encryption at Rest

**Optional: Full-disk encryption**

```bash
# macOS: FileVault
# Linux: LUKS
# Windows: BitLocker
```

---

## Reference: All Commands Quick List

```bash
# Start infrastructure
docker network create adhd-os
docker-compose up -d  # Nextcloud
docker-compose -f matrix-docker-compose.yml up -d  # Matrix
ollama serve  # Ollama (separate terminal)

# Test services
curl http://localhost:11434/api/tags  # Ollama
curl http://localhost:8080  # Nextcloud
curl http://localhost:8081  # Matrix
curl http://localhost:8008/_matrix/client/versions  # Matrix server

# Run agents
python adhd_agent.py
python matrix_bot.py

# Backup
tar czf backup.tar.gz /path/to/vault
docker exec nextcloud tar czf /backup.tar.gz /var/www/html

# Logs
docker logs nextcloud
docker logs matrix-synapse
ps aux | grep ollama
```

---

## Cost Analysis: Sovereignty vs. Cloud

### Sovereign Setup (This Guide)

**One-time costs:**
- Hardware (if buying new Mac Mini): $800-1200
- Time to set up: 5-10 hours

**Ongoing costs:**
- Electricity: ~$30-50/month (continuous server)
- Internet: Already have
- Backups: Free (GitHub, or paid cloud storage if desired)

**Total first year:** ~$800-1200 + electricity

---

### Cloud Setup (Current ADHD-OS)

**One-time costs:**
- Setup time: 30-45 min

**Ongoing costs:**
- Claude API: $3-10/month (usage-based)
- Google Calendar: Free
- Discord: Free
- GitHub: Free (private repo)
- Optional: Notion ($5-10/user), other services

**Total first year:** ~$36-120 + hardware (if buying)

---

## Recommendation

**For most users:** Stick with current cloud setup (Claude + Google Calendar). It's simpler, cheaper, and well-integrated.

**For privacy-first users:** Follow this guide. Sovereignty is worth the overhead.

**For hybrid:** Start with cloud, gradually add self-hosted services (Nextcloud Calendar first, local Ollama second).

---

**Last Updated:** 2026-05-29  
**License:** MIT (see [LICENSE](../LICENSE))

**Next Steps:**
1. Follow Part 2 (Phase 1-4) for step-by-step deployment
2. Test each service (Part 3)
3. Integrate with Obsidian (Part 4)
4. Monitor and maintain (Part 5)

**Questions?** Open a discussion on GitHub.
