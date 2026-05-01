

# 📚 Chapter 57 — Part G: Study Notes
## Extend Your Claw with MCP (Lessons 1–5)

---

#### 1. The Big Picture ⭐

Chapter 56 taught you to **consume** existing MCP servers. Chapter 57 teaches you to **produce** your own. The goal: give your agent tools that perform real actions in the real world — checking databases, calling APIs, verifying learner progress.

**The workflow:** `mcp-builder` skill → describe in plain English → steer the spec → verify → connect to OpenClaw.

---

#### 2. Lesson 1 — Your Agent Needs Hands ⭐

**The Core Problem:** Your agent has *knowledge* (from training data) but not *ability* (live actions).

> 🧠 **Analogy:** A brilliant logistics consultant who knows every routing algorithm — but when you ask "has container TEMU-4421 cleared customs?" he has to call someone. He has knowledge. He does not have access.

| Concept | What It Means |
|---|---|
| **Knowledge** | What training data provides — timezone offsets, SQL syntax, how databases work *in theory* |
| **Ability** | What a live tool provides — the actual time *right now*, whether *this specific student* completed lesson 3 |

Training data gives the **rule**. A live tool gives the **fact**. No amount of training data replaces a live connection.

**Consumer vs Producer:** ⭐

| Role | What You Do | Responsibility |
|---|---|---|
| **Consumer** | Take an existing MCP server (e.g. `mcp-server-time`), configure your agent to use it | **Configuration** — get the JSON right, restart, verify |
| **Producer** | Create a new MCP server that exposes tools your agent doesn't have yet | **Design** — decide tools, inputs, outputs, build, maintain |

Same protocol both ways. What changes is your responsibility.

**Skill-Driven Build Pattern (5 steps):**
1. Install a skill that gives Claude Code domain expertise
2. Configure CLAUDE.md with project rules
3. Describe what you need in plain language
4. Claude Code builds the implementation
5. You verify the result

*You own the requirements. The agent owns the code.*

---

#### 3. Lesson 2 — Set Up the Workshop ⭐

**Project setup — ~15 minutes, 3 files:**

```bash
mkdir tutorclaw-mcp
cd tutorclaw-mcp
npx skills add https://github.com/anthropics/skills --skill mcp-builder
```

The installer creates `.claude/skills/mcp-builder/` with a `SKILL.md`, `reference/`, and `scripts/` directory.

**The `mcp-builder` skill** gives Claude Code deep knowledge of MCP server structure, proven patterns, edge cases, and SDK best practices. Without it, Claude Code can still write a server, but like a general contractor doing electrical work instead of a licensed electrician.

**CLAUDE.md Rules (4 rules):** ⭐

```
# TutorClaw MCP Server

## Rules
- Use the mcp-builder skill for all MCP work
- Use uv for Python projects
- Follow spec-first development: discuss requirements, output spec, then build
- Use flat Annotated parameters on tools, not Pydantic BaseModel wrappers
```

| Rule | What It Prevents |
|---|---|
| Use mcp-builder skill | Claude Code ignoring the skill and using generic/outdated knowledge |
| Use uv for Python | Claude Code defaulting to pip/poetry when uv is faster and reproducible |
| Spec-first development | Claude Code jumping to code without agreeing on requirements → rework |

Transport and port are **not** in CLAUDE.md yet — added in Lesson 3.

**Final project structure:**
```
tutorclaw-mcp/
├── CLAUDE.md
└── .claude/
    └── skills/
        └── mcp-builder/
            ├── SKILL.md
            ├── reference/
            └── scripts/
```

No code yet. No server. Just the brain before the work.

> 🔧 **Analogy (James's warehouse):** Skill = the manual. CLAUDE.md = the safety checklist. Keys = starting Claude Code.

**Verifying the skill loaded:** Ask Claude Code any MCP question. If the answer is vague (just a paragraph), the skill may not have loaded. Check with `ls .claude/skills/mcp-builder/SKILL.md`, then open a **fresh session** — skills are read on session start, not mid-conversation.

---

#### 4. Lesson 3 — Choose Your Wire ⭐

**The 3 Transport Options** (recap from Ch. 56 Lesson 7, now you must pick one):

| Transport | Scope | Sessions | When to Choose |
|---|---|---|---|
| **stdio** | Local only (same machine) | N/A | Dev tools, local integrations |
| **SSE** | Network | Stateful | Multi-step workflows needing state |
| **streamable-http** | Network | Stateless OR stateful | Default for most production servers |

**The 3 Decision Questions:** ⭐
1. Should the server work only on your laptop, or from anywhere? → Network = streamable-http
2. Should the server track who is calling between requests? → No = stateless
3. Who remembers the conversation? → Agent already does via gateway → server doesn't need to

**Recommended choice: streamable-http, stateless** — used in the rest of this chapter.

> 🏷️ **Analogy:** Stateless is like shipping labels. Every label has the complete destination address. The warehouse doesn't need to remember which dock you used last time. Each package is self-contained.

**Update CLAUDE.md after deciding:**
```
- Use streamable-http stateless transport on port 8000
```

Now CLAUDE.md has 4 rules. Every future Claude Code session in this project reads and follows them.

**Emma's cautionary tale:** She chose "stateful" for a client's inventory system because "sessions sounded professional." Six weeks later — debugging session cleanup timers at 2am, sessions that expired mid-request, memory leaks because cron ran in the wrong timezone. Stateless would have been half the code and none of the bugs.

*Stateless is not always better — but for a tool server where each request is self-contained, it's the obvious fit.*

---

#### 5. Lesson 4 — Spec and Build Your First Tool ⭐⭐

**The Describe-Steer-Verify Cycle** — the chapter's core workflow:

| Step | What Happens |
|---|---|
| **1. Describe** | Send plain-language description to Claude Code — what it accepts, what it returns, and "spec before building" |
| **2. Review Spec** | Claude Code produces a spec (not code yet). You review it. |
| **3. Steer** | Push back if the spec is wrong — sharpen description, add parameters, adjust output |
| **4. Build** | "The spec looks good. Build this." → Claude Code implements, tests, starts server, makes real call, shuts down, reports |

**What to look for in the spec:**

| Element | What to Check |
|---|---|
| Tool name | Clear, lowercase (e.g. `register_learner`) |
| **Tool description** | ⭐ **Most important** — tells agent WHEN to call this tool |
| Input parameters | What it accepts, which are required |
| Output format | What it returns on success and error |

**Why tool description matters most:** ⭐

When an agent has multiple tools, it reads each description to decide which one to call. The description is a **job posting**.

| Quality | Example | Agent Behavior |
|---|---|---|
| **Vague** | "Registers stuff" | Agent doesn't know when to call it — calls it randomly or never |
| **Specific** | "Register a new learner in TutorClaw for the first time. Do NOT call if the learner already has an ID." | Agent picks it exactly right, every time |

**Common steering moves:**
- "Make the tool description more specific..."
- "Add an optional email parameter..."
- "The return should include a timestamp..."

**Build and Verify — Claude Code does all of this automatically:**
1. Runs tests → checks tool logic
2. Starts server → confirms it boots
3. Makes a real tool call → proves end-to-end
4. Shuts server down → reports results
5. Asks if you want MCP Inspector

**MCP Inspector:** Visual tool (`npx @modelcontextprotocol/inspector`) — lets you call tools one at a time and see inputs/outputs. Good for exploring before connecting to OpenClaw.

> ⭐ **Key insight:** "The hardest part was not building. It was knowing what to ask for." — You own the domain knowledge. Claude Code owns the code.

---

#### 6. Lesson 5 — Connect and Test from WhatsApp ⭐

**Same pattern as connecting `mcp-server-time` in Ch. 56 Lesson 7. Different URL.**

**5-step connection sequence:**

```bash
# Terminal 1 — start your server (keep open)
uv run python server.py
# Expected output: Uvicorn running on http://127.0.0.1:8000

# Terminal 2 — connect to OpenClaw
openclaw mcp set tutorclaw '{"url":"http://localhost:8000/mcp","transport":"streamable-http"}'
openclaw gateway restart

# Verify it registered
openclaw mcp list
openclaw mcp show tutorclaw
```

**Then test from WhatsApp:**
- Send: *"Register a new learner named James Chen"*
- Agent recognizes match → calls tool → returns welcome message with UUID learner ID

**Proving the tool actually ran — Tool Badge:** ⭐

A text response alone does NOT prove the tool ran. The agent can fabricate a plausible answer using training data. The **tool badge** in the dashboard is the proof.

The full verified chain:
```
WhatsApp message → Gateway → Agent picks correct tool (via description) 
→ MCP server runs tool → Result returns → WhatsApp response + Tool Badge
```

**Silent failure warning:** If URL is wrong by even one character (missing `/mcp`, wrong port), the connection fails silently. No error in chat. Gateway log is the only diagnostic.

**Emma's debugging story:** "I forgot to restart the gateway after changing the URL. Thirty minutes of debugging. The fix was one command."

---

#### 7. The Full Chapter Pattern ⭐

```
Consumer (Ch. 56) → plug in someone else's server, configure
Producer (Ch. 57) → describe → steer → build → connect → verify
```

**Repeating cycle for every new tool:**
Lesson 2 setup → Lesson 3 transport choice → Lesson 4 Describe-Steer-Verify → Lesson 5 Connect

The MCP protocol is identical whether you built the server or someone else did. The `openclaw mcp set` command works the same for both.

---

#### 📋 Quick Reference Table

| Fact / Number | Detail |
|---|---|
| mcp-builder install command | `npx skills add https://github.com/anthropics/skills --skill mcp-builder` |
| Skill directory created | `.claude/skills/mcp-builder/` (SKILL.md + reference/ + scripts/) |
| CLAUDE.md rule count (end of setup) | 4 rules (skill + uv + spec-first + stateless HTTP port 8000) |
| Recommended transport | streamable-http, **stateless**, port 8000 |
| Spec element that matters most | Tool **description** — tells agent when to call this tool |
| Build-and-verify steps | 5: run tests → start server → real tool call → shut down → report |
| MCP Inspector command | `npx @modelcontextprotocol/inspector` |
| Server start command (Python) | `uv run python server.py` |
| Connect command | `openclaw mcp set <name> '{"url":"http://localhost:8000/mcp","transport":"streamable-http"}'` |
| After connecting | `openclaw gateway restart` |
| Proof tool actually ran | **Tool badge** in dashboard (text response alone is not enough) |
| Silent failure cause | Wrong URL (missing `/mcp`, wrong port) — check gateway log |
| Consumer role | Configuration — get JSON right, restart, verify |
| Producer role | Design — tools, inputs, outputs, build, maintain |
| Knowledge vs Ability | Knowledge = training data (rules). Ability = live tool (facts). |
| Stateless analogy | Shipping labels — every label has the complete address, warehouse doesn't remember past docks |
| Skill analogy | Skill = manual. CLAUDE.md = checklist. Starting Claude Code = keys. |

---
