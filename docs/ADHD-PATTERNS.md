# ADHD-OS: Real Workflows for Real ADHD Brains

> Concrete patterns for using ADHD-OS to solve specific ADHD problems. These come from real experience, not theory.

---

## Pattern 1: Frictionless Capture (The Inbox Dump)

**Problem:** Your brain fires thoughts constantly. If you don't capture them *right now*, they vanish — but stopping to organize them derails your current task. Result: context switch, activation energy spike, hyperfocus broken.

**Solution:** Ultra-low-friction capture. One step. No decision-making.

### The Workflow

**Setup (one-time, 5 min):**
1. Create a Quick Capture shortcut in Obsidian (plugin: QuickAdd)
2. Bind it to a keyboard shortcut: `Cmd+Shift+I` (capture Inbox)
3. Template: Just the thought, no metadata
   ```
   - {input} ({timestamp})
   ```

**During the day:**

```
You're deep in coding. Random thought: "I should check if React 19 has better memo performance"

Instead of: "Let me open a browser and research" (loses hyperfocus)

Press: Cmd+Shift+I
Type: "React 19 memo perf check"
Press: Enter

[Thought captured, 2 seconds, brain can let go]
```

**Triage (5 min, once daily):**
Open Daily Note → Inbox section → Review captured thoughts:
- ✅ Add to current project? → Move to Projects/ProjectName.md
- ✅ Add to Kanban? → Move to Kanban Current or Inception
- ❌ Not useful right now? → Delete
- ⏳ Might be useful later? → Move to Reference folder

### Why It Works

**Neuroscience:** ADHD brains experience "memory anxiety / FOMO" — the fear that an uncaptured thought is a lost thought. This anxiety interrupts constantly. By capturing, you tell your brain: "It's safe. You don't have to remember it."

**Friction:** Every step between thought and capture = risk of not capturing. One keystroke, one field. That's it.

**Async triage:** You capture in hyperfocus; you triage when hyperfocus ends (naturally, not forced). Two separate cognitive tasks.

### Example: Real Capture Session

```
[You're writing documentation. Hyperfocus active.]

Brain fires: "Wait, do we have a security.md for the API?"
Cmd+Shift+I → "Check security.md for API endpoints" → ✓

Brain fires: "Mom's birthday is next week"
Cmd+Shift+I → "Mom birthday - card + gift" → ✓

Brain fires: "The Obsidian backlinks feature could help with reference linking"
Cmd+Shift+I → "Explore Obsidian backlinks for cross-project refs" → ✓

[Still hyperfocused, still writing, but 3 thoughts safely captured]

[Later, during daily triage:]
- "Mom birthday" → Move to Personal projects
- "Obsidian backlinks" → Move to ADHD-OS Inception (future exploration)
- "security.md" → Move to Projects/ADHD-OS, add to Kanban
```

---

## Pattern 2: Working Memory Externalization (Session Notes for Re-entry)

**Problem:** You're working on something complex. A notification (or ADHD hyperfocus shift) pulls you away. You lose the mental model. Re-entering costs 20+ minutes of reconstruction.

**Solution:** Claude writes a "session note" — a checkpoint of *where you were, what you decided, what's next*. Re-entry: read the note in 2 minutes.

### The Workflow

**During session (with Claude):**
```
You: "Help me design a new agent framework for ADHD-OS"

Claude: [discusses, suggests, explores options]

You: "I need to step away now, but I'll continue this tomorrow"

Claude: "I'll write a session note capturing where we are"

Claude writes to: Daily Notes/2026-05-29-session-llm-agent-design.md
```

**Session note template (Claude auto-fills):**
```markdown
# Session: LLM Agent Design for ADHD-OS
**Date:** 2026-05-29  
**Duration:** 45 minutes  
**Status:** 🔄 In progress

## What We Discussed
- Three agent architectures: ReAct, Reflection, Plan-Execute
- Chose Reflection (self-correcting, low latency vs ReAct)
- Integration point: Hermes Agent layer

## Key Decisions
1. ✅ Use Claude's tool_use for agent decisions
2. ✅ Async execution (agent runs independently, returns results)
3. ❓ TBD: How to handle state between agent calls (Letta vs custom)

## Blockers / Open Questions
- How does Letta's memory layer fit with Obsidian vault? (Need to research)
- Do we need agent persistence, or just skill library? (Clarify scope)

## What's Next
1. Research Letta architecture + test with toy agent
2. Design state management layer
3. Integration test: Hermes Agent ↔ Obsidian via MCP

## Links
- [[ADHD-OS Architecture]] — system overview
- [[Hermes Agent]] — current agent framework
- Reference: LangGraph ReAct pattern
```

**Next session (re-entry):**
```
You: "I'm back on the agent design work"

[Read yesterday's session note in 2 min]

Brain has context restored. No 20-minute reconstruction needed.

You: "Claude, based on yesterday's session note, let's start by researching Letta"
```

### Why It Works

**Neuroscience:** Working memory in ADHD brains degrades when context switches. But *reading* (external, stable) restores context much faster than *reconstructing* (internal, fragile).

**Async triage:** The session note is Claude's work, not yours. No activation energy needed.

**Persistence:** Session notes stay in vault (Git backup). You can return days or weeks later and still understand the context.

### Example: Real Session Note

```markdown
# Session: ADHD-OS Publishing Roadmap
**Date:** 2026-05-29  
**Duration:** 2.5 hours

## What We Did
- Created comprehensive README for ADHD-OS platform
- Synthesized modular architecture: 5 layers (ADHD UX → Memory → Agent → AI → Infrastructure)
- Wrote HEALTH-WARNING.md with medical disclaimers
- Drafted LICENSE with medical non-liability boilerplate
- Started SETUP.md installation guide

## Key Decisions Made
1. ✅ ADHD UX is the priority (not modularity or sovereignty)
2. ✅ Platform description includes current system (Obsidian + Claude + Git) AND future roadmap (Thoth, Letta, Mem0)
3. ✅ Health disclaimer is prominent (HEALTH-WARNING.md reads first)
4. ✅ All docs use accessible language (no assumed jargon)

## What We Discovered
- Research shows Thoth + Letta + Mem0 composable architecture is strong pattern
- Synthesizing ADHD problem → infrastructure solution is the coherent narrative
- Medical/liability disclaimers for ADHD tools are critical (and missing in most projects)

## Blockers / Open Questions
- How much of Phase 2 (Thoth/Letta integration) to document now vs. later?
- Should template vault be published as separate repo or included here?

## What's Next
1. ✅ Finish SETUP.md with verification checklist
2. ✅ Complete ARCHITECTURE.md with technical deep-dive
3. ✅ Create CONTRIBUTING.md
4. 🔄 Draft ADHD-PATTERNS.md (concrete workflows)
5. Research section (effectiveness, studies, community perspectives)
6. Template vault (preconfigured Obsidian)

## Files Created
- README.md ✅
- HEALTH-WARNING.md ✅
- LICENSE ✅
- docs/SETUP.md ✅
- docs/ARCHITECTURE.md ✅
- CONTRIBUTING.md ✅

## Decision for Next Session
- Start ADHD-PATTERNS.md with real workflows
- Collate research on ADHD + AI effectiveness
- Decide: publish Phase 1 now or wait for ADHD-PATTERNS + research?
```

---

## Pattern 3: Loop-Breaking (The Watchdog Pattern)

**Problem:** You're troubleshooting something. Same error appears 3 times, but you keep trying the same fix. You're pattern-matching without understanding. 30 minutes wasted chasing symptoms instead of root causes.

**Solution:** Claude actively watches for loop signatures and interrupts with escalating directness.

### The Workflow

**Setup (configure Claude):**
Give Claude explicit instructions:
```
You are my loop-breaking watchdog. During troubleshooting, watch for these signatures:

1. After 10-15 min on same problem (no progress):
   Interrupt gently: "Can we verify our assumption about what's happening?"

2. After 20+ min of same problem:
   Warning: "⚠️ We might be in a loop. Let's diagnose first."

3. Same error appears 2+ times without diagnosis:
   Direct: "⚠️ We've seen this error twice without understanding it. 
   Before trying another fix, let's figure out what's actually broken."

4. Same command/action tried 3+ times:
   Strong interrupt: "⚠️ STOP. This approach isn't working. 
   Let's step back and figure out the actual problem."

Your role: External prefrontal cortex. Break the loop before it wastes hours.
```

**During troubleshooting (with Claude):**

```
You: "Docker container won't start. Getting 'bind: address already in use' error"

Claude: [helps you investigate]

[After 15 min, same error, you're trying to restart again]

Claude: "Hold on. We've tried restarting 3 times. 
Instead of restarting again, let's diagnose: What's actually using port 8080?

Run: lsof -i :8080

Then we'll know what to stop."

You: [runs command, sees it's an old Ollama process]
"Ah! Old Ollama still running"

[Root cause found in seconds instead of wasted on symptom-chasing]
```

### Why It Works

**Neuroscience:** ADHD brains can execute complex sequences (following instructions, running commands) while the executive function that would catch "wait, this doesn't make sense" is already deep in hyperfocus. The brain is pattern-matching, not reasoning.

**External interrupt:** When you're in the loop, you can't see the loop. An external partner (Claude) can.

**Escalating directness:** Gentle nudge → warning → direct interrupt. Respects autonomy while breaking loops before they consume hours.

### Example: Real Loop-Breaking

```
[You're debugging a Flask app]

You: "API endpoint returns 500. Let me restart Flask"
[Restarts]
"Still 500. Let me restart Ollama"
[Restarts]
"Still 500. Let me update dependencies"
[pip install -U]
"Still 500."

Claude: "🛑 We've done restart-restart-update three times. 
The error isn't changing.

Before we try anything else, let's look at the actual error message.
What does the Flask log say? (Not 'restart', just look at logs)"

You: [checks logs]
"Oh! 'NameError: name 'client' is not defined' — I didn't initialize the Ollama client"

[Problem diagnosed in 30 seconds. Actual fix: 1 line of code]
```

---

## Pattern 4: Time Blindness Compensation (Calendar + Blocking)

**Problem:** You lose track of time. Tasks take 3x longer than you think. Deadlines surprise you. You can't estimate "how long will this take?"

**Solution:** Explicit calendar blocks + reminders + visible time elapsed

### The Workflow

**Setup:**
1. Add all tasks to Google Calendar (not optional for time-blind ADHD)
2. Set duration estimates (even if they're wrong)
3. Add 15-min buffer before each task (context switching, setup)
4. Create recurring reminders (every morning, mid-day, evening)

**Pattern: Task Blocking**

```
Task: "Write ADHD-OS documentation"

Don't estimate: "I'll do it this week"
Do estimate: "30 min capture patterns, 45 min research, 60 min architecture review"

Calendar blocks:
- Thu 2pm-2:30pm: ADHD-PATTERNS capture
- Thu 3pm-3:45pm: ADHD-PATTERNS research
- Thu 4pm-5pm: Architecture review
- (4 hours = full task, but broken into calendar blocks)

Reminders:
- 15 min before each block: "Starting ADHD-PATTERNS work in 15 min"
- End of block: "Time's up. Save progress."
```

**Pattern: Time Visibility**

In your Daily Note, add elapsed time tracking:
```markdown
## Today's Time Blocks

- ⏰ **2:00-2:30 ADHD-PATTERNS capture** ← Currently here (5 min in)
- ⏳ **3:00-3:45 Research** 
- ⏳ **4:00-5:00 Review**

## Elapsed Time
- So far today: 2 hours 15 min
- Scheduled ahead: 2 hours 15 min
- **Available today: ~30 min** (end of day at 5:30pm)
```

**Pattern: Time Auditing (Weekly)**
```
Every Friday, 5 min review:
- What did I estimate vs. actual?
- Tasks that ran over (adjust estimates up)
- Tasks I skipped (why? too long? low priority? activation barrier?)

Example:
- Estimated "write docs" at 1 hour → actual 3 hours (new estimate: 3 hours)
- Estimated "code review" at 30 min → actual 15 min (keep at 30 min, buffer is fine)
```

### Why It Works

**Neuroscience:** ADHD brains have "time blindness" — difficulty perceiving elapsed time and estimating duration. The solution isn't "try harder to estimate." It's external time tracking.

**Visibility:** Calendar makes invisible time visible. Reminders externalize the clock your brain doesn't have.

**Progressive refinement:** First estimates are wrong. That's okay. Each week, you get better because you have data.

### Example: Time Blocking in Action

```
Monday morning:
You estimate: "I'll write the ADHD-PATTERNS doc today. Should take 2-3 hours tops."

You create calendar blocks:
- 9am-10am: Patterns intro + capture pattern
- 10:15am-11:30am: Working memory pattern
- (lunch)
- 1pm-2pm: Loop-breaking pattern
- 2:15pm-3:15pm: Time blindness pattern
- 3:30pm-4:30pm: Review + polish

By 11am: You've written 2 patterns. Right on schedule.
At 11:30am: Reminder goes off. "Time's up. Save."
By 1pm: You've showered, eaten, reset. Back for next block.

Each block: ~45 min work + 15 min break/setup

Result: 5 hours of scheduled blocks completed by 4:30pm.
Actual doc time spent: 5 hours (close to estimate).
Quality: Better, because you had breaks (your brain resets).
```

---

## Pattern 5: Inbox Triage (The Weekly Cleanup)

**Problem:** Inbox overflows. 200 items. You don't know where to start. Activation energy spike → avoidance → more guilt.

**Solution:** Systematic, time-bounded triage. 20 minutes. Everything triaged.

### The Workflow

**Weekly Triage (Friday, 20 min):**

1. **Collect** (5 min) — Open Daily Notes from the week, grab all Inbox items
2. **Categorize** (10 min) — Each item gets one decision:
   - ✅ **Current** — This is my priority (max 3 items, move to Kanban)
   - 🔄 **Inception** — Hyperfocus item or future tangent (keeps it safe, not a failure)
   - 📋 **Waiting** — Blocked on someone else (move to Waiting column)
   - 📚 **Reference** — Good to know, but not actionable now (move to Reference folder)
   - ❌ **Delete** — Not useful anymore (with permission to discard guiltlessly)
3. **Archive** (5 min) — Move Inbox section to Archive/2026-Week-22 for history

**Triage decision tree:**
```
Item: "Research Letta integration"

Q: Can I act on it now? → No (Obsidian not set up for testing)
Q: Do I want to act on it this week? → No (lower priority)
Q: Could this be useful later? → Yes
Q: Is it a genuine interest (not guilt)? → Yes

Decision: → Move to ADHD-OS Inception section (hyperfocus item when ready)
```

### Why It Works

**Neuroscience:** Decision paralysis (executive dysfunction) makes triage feel overwhelming. Time-bounding (20 min) removes the "I need to decide forever" anxiety. "I have 20 minutes, then I'm done" = manageable.

**Permission to discard:** ADHD brains often capture thoughts out of fear ("what if I forget"). Triage gives permission to delete guilt-free because you made a conscious decision.

**Asynchronous processing:** Inbox happens *during* work. Triage happens *after* work. Two separate cognitive tasks, separated by time.

### Example: Real Triage Session

```
Friday, 3pm. You have 20 minutes.

Inbox items this week:
- "Check React 19 memo perf" → Research (Inception)
- "Mom's birthday gift" → Personal/Current
- "Update npm packages" → Code (Current)
- "Learn Letta" → ADHD-OS (Inception)
- "Write that blog post" → Writing (Waiting - need feedback from JP first)
- "Reorganize vault structure" → Infrastructure (Reference - future cleanup)
- "Try new Obsidian theme" → Delete (not important)

[6 decisions in ~2 min each, 20 min total]

Kanban updated with Current items.
Inception has safe parking for hyperfocus tangents.
Waiting has blockers.
Reference has ideas for later.
Inbox: empty.

Brain: "Great, you're organized for next week."
```

---

## Pattern 6: Hyperfocus Management (Bottling & Preventing Burnout)

**Problem:** You enter hyperfocus. You forget to eat, sleep, move. You burn out. After hyperfocus: crash, guilt, exhaustion.

**Solution:** Bottle hyperfocus (let it happen, don't fight it) with guardrails (breaks, hydration, end-time).

### The Workflow

**Before hyperfocus (prevention):**
```
Recognize when hyperfocus is starting:
- You've been working for 90+ min without a break
- You're ignoring hunger, time, surroundings
- You're in a flow state (good thing! don't kill it)

Set guardrails:
1. Water bottle + snacks within reach
2. Calendar reminder for "break time" in 90 min
3. Calendar reminder for "end work" at a hard stop
4. Phone on do-not-disturb (protect focus)
```

**During hyperfocus (protect it):**
```
✅ DO:
- Let it happen
- Write notes quickly (don't break focus)
- Accept that time is invisible
- Trust the guardrails

❌ DON'T:
- Check messages/Slack
- "Just one more thing"
- Feel guilty about ignoring other tasks
- Force yourself to stop early
```

**After hyperfocus (recovery):**
```
Hyperfocus ends (naturally, or guardrail triggers)

Immediate:
- Eat (you forgot)
- Move (you've been sitting 3 hours)
- Rest (brain is tired, even if you don't feel it)

Recovery session (next day):
- Move accomplishment from Inception to Current (in Kanban)
- Claude writes session note (what you did, what's next)
- Celebrate it (hyperfocus is a superpower, not a failure)

Don't crash yourself:
- DON'T start another task immediately
- DO take 30-60 min of low-activation work (email, comms, admin)
```

### Why It Works

**Neuroscience:** Hyperfocus is a gift, not a problem. ADHD brains enter deep flow states that neurotypical brains envy. The problem isn't hyperfocus — it's the *cost* (burnout, ignoring needs).

**Bottling, not killing:** The worst thing you can do is fight hyperfocus. Bottling it (letting it happen with guardrails) preserves the benefit while preventing the harm.

**Permission structure:** Hyperfocus comes with guilt ("I should be doing other things"). Explicit permission (this is legitimate work) removes the guilt.

### Example: Real Hyperfocus Session

```
Thursday, 2pm. You sit down to code.

Guardrails set:
- Water + snacks on desk
- Calendar: "Break" at 3:30pm
- Calendar: "Dinner" at 6:30pm
- Phone: do-not-disturb

2:00-3:30pm: Hyperfocus. You code. It flows.

3:30pm: Calendar reminder. You ignore it (hyperfocus)

4:30pm: You realize you haven't moved in 2.5 hours
"Water + snack break" (5 min)

Back to focus 4:35-6:30pm: More coding

6:30pm: Calendar reminder. Dinner time. Hard stop.

[You've been hyperfocused 4.5 hours, produced amazing code]

That evening:
- Eat (actually eat, not snack)
- Move (walk around block)
- Rest (light TV, no more work)

Next day, session note:
"Hyperfocus session Thu 2-6:30pm. Completed X, Y, Z features. 
Quality: excellent. Next: testing and integration."

Kanban updated. Work credited. No guilt.
```

---

## Pattern 7: Context Switching Recovery (The Re-entry Protocol)

**Problem:** Your spouse asks a question. A notification pings. You get pulled away from deep work. Re-entering the mental model takes 20+ minutes. You lose the afternoon.

**Solution:** Explicit re-entry protocol. Read a note. Brain restores context.

### The Workflow

**Before going deep:**
Before you start focused work, create a "context checkpoint":

```markdown
# Context: Hermes Agent Design Session

**Current focus:** Designing agent memory persistence layer

**Where I am:** 
- Just finished researching Letta architecture
- About to design how agent state saves to Obsidian

**Mental model (keep this in head):**
- Agent = stateful object (remembers past interactions)
- State = (persona, memories, skills, current task)
- Storage = Obsidian vault (via MCP)
- Problem: How to serialize state without losing context?

**Next steps if interrupted:**
1. Read this checkpoint
2. Look at the code/design I was working on
3. Claude can help me re-orient: "Hey, I was working on agent state serialization"

**Links:**
- [[Hermes Agent]] — overall architecture
- [[Letta Research]] — how Letta does it
- /code/hermes-agent/agent.ts — file I was editing
```

**When interrupted:**
- **Step 1:** Save current work (auto-save helps)
- **Step 2:** Leave the context checkpoint open
- **Step 3:** Handle the interruption
- **Step 4 (re-entry):** Read the checkpoint (2 min). Brain restores ~70% of context.

**With Claude (ideal):**
```
You: "I was interrupted. Let me get back into focus."

Claude: [reads your context checkpoint, looks at your code/notes]

Claude: "You were designing how agent state persists to Obsidian. 
You'd finished researching Letta (which uses a tiered memory model). 
The next step is figuring out serialization format. 
Want to continue from there?"

You: "Yes, exactly where I was"

[Full re-entry in 2 min instead of 20]
```

### Why It Works

**Neuroscience:** Context switching is expensive for ADHD brains. But *reading* context (external) is much cheaper than *remembering* it (internal memory, fragile in ADHD).

**Checkpoint as lifeline:** When you re-enter, you don't reconstruct from scratch. You read the checkpoint, look at your partial work, and Claude orients you.

**Asynchronous restoration:** You don't need to keep context in your head during the interruption. The checkpoint holds it.

### Example: Real Interruption & Re-entry

```
[You're deep in writing code, 2:30pm, in flow]

Spouse: "Did you feed the dog?"

[Context lost. You're thinking about dog, not code]

You: [quickly save file]

File: hermes-agent.ts (half-finished)
Checkpoint note: "Designing memory serialization. Next: JSON format vs binary"

You: [go feed dog, 5 min task]

You: [come back, 3pm]

Brain: "Wait, what was I doing?"

You: [read checkpoint in 30 sec]

Claude session:
You: "I'm back on the agent design. Let me remind us where we were"

Claude: "Memory serialization. You were deciding between JSON and binary. 
JSON is debuggable, binary is efficient. 
Given ADHD-OS values transparency (Obsidian vault), JSON makes sense. 
Where do you want to go next?"

You: [back in flow, no reconstruction needed]

[You've lost ~5 min to dog, but not the 20 min to context reconstruction]
```

---

## Pattern 8: Decision Fatigue Prevention (Pre-Decided Defaults)

**Problem:** Every day brings small decisions. "Should I work on X or Y? Should I use Claude or local Ollama? Should I take a break now or later?" Decision fatigue kills you by 3pm.

**Solution:** Pre-decide. Document defaults. Decisions are already made.

### The Workflow

**Setup (30 min, one-time):**

Create a file: `Personal/Defaults.md`

```markdown
# My ADHD-OS Defaults

## Work Priorities (in order)
1. Deep work (code, writing, design) — default morning (9am-12pm)
2. Admin/comms (email, Slack, reviews) — default afternoon (1-3pm)
3. Learning/exploration — default when hyperfocus strikes (don't force it)

## Which AI to Use (by task type)
- **Complex reasoning:** Claude (default, best quality)
- **High volume:** Local Hermes (cost, latency)
- **Coding:** Claude (testing, edge cases)
- **Brainstorming:** Claude (creativity + reasoning)

## When to Take Breaks
- Every 90 min automatically (calendar reminder, non-negotiable)
- If hyperfocus happens, use guardrails instead
- If stuck for 20 min, take 10 min break

## What to Do When Stuck
1. First: Take a 10 min break (walk, water, move)
2. Then: Call in Claude to pair on it
3. If still stuck 30 min later: Switch tasks (deferrable? defer. blocking? escalate)

## Morning Routine (15 min)
1. Read Daily Note from yesterday (5 min)
2. Review Kanban priorities (2 min)
3. Plan today in calendar (check time blocks) (3 min)
4. Coffee + think (5 min)
5. Start with #1 priority

## When Hyperfocus Hits
Allow it. Set guardrails. Don't feel guilty.

## End of Day (5 min)
- Log what you did
- Note any blockers for tomorrow
- Triage any new Inbox items
- Close laptop
```

**Using defaults:**
```
Morning: You open Defaults.md → "First priority is deep work, Claude for reasoning"
Decision made. No fatigue.

Afternoon: "Stuck on a design decision"
Check Defaults → "Call in Claude to pair on it"
Decision made. Action taken.

Thursday: Hyperfocus kicks in
Check Defaults → "Allow it. Set guardrails. Don't feel guilty."
Decision made. You work without guilt.
```

### Why It Works

**Neuroscience:** ADHD brains have limited executive resources. Every decision uses resources. Pre-deciding burns resources once, not repeatedly.

**Reduces activation energy:** Instead of "Should I do X?", it's "X is the default. Do X."

**Gives permission:** Defaults include permission structures ("When hyperfocus hits, allow it"). This removes guilt.

### Example: Real Defaults in Action

```
Monday 8:30am:
Brain: "What should I work on today?"

Without defaults: Decision paralysis, 30 min lost researching options

With defaults: "Check Defaults.md"
- Morning = deep work
- Priority = ADHD-PATTERNS documentation
- AI to use = Claude
- Task blocking = 9am-12pm

Decision made instantly. Start at 9am.
No fatigue. Brain energy conserved.

2pm, stuck on time blindness pattern:
Brain: "Should I keep coding or take a break?"

Check Defaults → "Every 90 min, break automatically"
(It's been 92 min)

Decision made. Take break. No deliberation.

3:30pm, hyperfocus kicks in on something fun:
Brain: "Should I keep going or stick to the plan?"

Check Defaults → "Allow it. Set guardrails. Don't feel guilty."

Decision made. Hyperfocus protected, guardrails set.
No guilt. No second-guessing.
```

---

## Anti-Patterns (What NOT to Do)

### ❌ "Perfect Capture"
Trying to organize thoughts *while* capturing them.

**Why it fails:** Adds activation energy. You lose the thought while trying to categorize it.

**Better:** Capture messy. Triage later.

---

### ❌ "The Omniscient Daily Review"
Reviewing everything (all projects, all tags, all notes) every day.

**Why it fails:** ADHD brains get overwhelmed by choice. Analysis paralysis.

**Better:** Review one thing: today's calendar blocks and Inbox items. That's it.

---

### ❌ "Motivation-Driven Task Initiation"
Waiting until you feel like it to start a task.

**Why it fails:** Motivation is unstable in ADHD. You'll wait forever.

**Better:** Calendar block (decision already made). Start at the block time, not when you feel motivated.

---

### ❌ "Willpower-Based Discipline"
"I'll just focus harder / work later / skip lunch to compensate"

**Why it fails:** Willpower is an ADHD-brain myth. You'll burn out.

**Better:** Infrastructure (guardrails, defaults, breaks). Let the system do the work.

---

### ❌ "Binary Task Status"
Tasks are either "not started" or "done."

**Why it fails:** ADHD tasks are often partial, blocked, or in-progress-but-paused. Binary status creates guilt.

**Better:** Kanban with 6-7 columns (Inbox, Current, Inception, Waiting, In Progress, Done, Archive). Partial progress is visible and valid.

---

### ❌ "The Perfect Plan"
Trying to plan the entire week/month/quarter before starting.

**Why it fails:** Plans change. ADHD brains are fluid. Detailed plans create rigidity and failure-feelings.

**Better:** Plan today. Decide tomorrow based on what happened today. Flexible, rolling planning.

---

## Summary: Core Principles

These patterns all work because they follow a few core ADHD-friendly principles:

1. **Reduce activation energy** — Make the right thing easy; friction kills action
2. **Externalize cognitive load** — Don't hold it in your head; put it in the system
3. **Permission structures** — "You're allowed to hyperfocus / take a break / change plans"
4. **Async triage** — Capture when the brain is hot, organize when it's cool
5. **Visible progress** — Track what you do; brain needs concrete evidence of accomplishment
6. **Default decisions** — Pre-decide. Reuse decisions. Conserve executive resources.
7. **Recovery buffers** — Breaks, session notes, checkpoints. Expect context switches; recover fast.

---

## Next Steps

- **Pick one pattern** to try this week (suggest: Frictionless Capture)
- **Set it up** (5-15 min setup, usually one-time)
- **Use it for 3 days** (let it become automatic)
- **Adjust** based on what your ADHD brain actually needs
- **Add another pattern** when you're ready

Not all patterns work for everyone. That's okay. ADHD brains are diverse. Use what works for you. Discard what doesn't.

---

**Last Updated:** 2026-05-29
**License:** MIT (see [LICENSE](../LICENSE))
