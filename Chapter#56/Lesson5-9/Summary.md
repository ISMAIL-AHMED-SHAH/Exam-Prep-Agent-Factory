
## 📘 Chapter 56 — Part C Study Notes: Lessons 5–9
### Memory & Commands | Skills | MCP | Proactive | Voice

---

### 🔷 LESSON 5: Memory & Commands

---

#### 1. The Core Problem — Session Memory Fades

Every conversation session ends and disappears. Anything said conversationally — "I prefer bullet points under 100 words" — is **gone when the session closes**. The agent starts each new session with zero recall of your preferences.

> "There is a difference between saying something in a conversation and writing it to a file."

---

#### 2. The Two Memory Locations ⭐

| Location | What It Stores | When It Loads |
|---|---|---|
| **MEMORY.md** (`~/.openclaw/workspace/MEMORY.md`) | Curated long-term memory: preferences, key decisions, facts | Every single session start |
| **memory/YYYY-MM-DD.md** (`~/.openclaw/workspace/memory/`) | Daily journal logs: session notes, conversation summaries | Today + yesterday at session start |

**Loading summary diagram:**
```
Session starts:
  ├── MEMORY.md          → always loads (curated, long-term)
  ├── memory/today.md    → always loads (today's journal)
  ├── memory/yesterday.md → always loads (yesterday's journal)
  └── memory/older/*.md  → available via memory_search only
```

**Why this design?** Loading every daily log since installation would burn tokens on irrelevant history. The system loads recent context automatically and searches older context on demand.

---

#### 3. How to Save to Memory — Critical Trigger Phrase ⭐

```
Save in memory: I prefer all summaries under 100 words as bullet points.
Never use numbered lists for summaries.
```

**⚠️ Warning:** Using "Remember this:" instead of "Save in memory:" may cause the agent to respond with "Got it!" **without actually writing anything to disk**. Verbal confirmation is NOT proof of a file write.

**Verification rule (Emma's golden rule):** "Verify on disk, not just in chat."
```bash
cat ~/.openclaw/workspace/MEMORY.md
```

**Proof of write:** The OpenClaw dashboard shows a **tool badge** next to the agent's response confirming a file write operation. No tool badge = preference was NOT saved.

---

#### 4. memory_search — Finding Older Notes

When the agent needs something from logs older than yesterday, it uses `memory_search` — **hybrid retrieval** combining:
- **Vector similarity** (matches meaning, even when wording differs)
- **Keyword matching** (matches exact terms)

---

#### 5. Compaction — When Long Conversations Get Compressed

When a conversation runs too long, the **gateway compacts** older turns into a summary to free context space. Before compacting, the agent is automatically reminded to save important things to memory files.

- MEMORY.md and daily logs survive compaction
- Session context can be summarized away at any time
- Trigger manually with `/compact` if conversations feel sluggish

---

#### 6. Slash Commands — The Gateway Bypass ⭐

Slash commands are **intercepted by the gateway** before the model ever sees them. Zero tokens spent, instant response.

| Command | What It Does |
|---|---|
| `/help` | Lists available commands |
| `/status` | Shows model, session state, diagnostics |
| `/model <n>` | Switches model mid-conversation |
| `/reset` | Fresh session (clears conversation, KEEPS memory) |
| `/compact` | Summarizes older turns to free context space |
| `/commands` | Lists all available slash commands |

**Speed proof:** `/status` returns in under a second. Asking "What model are you using?" in natural language takes 3+ seconds with a thinking indicator. That speed gap IS the proof that slash commands bypass the model entirely.

> James's analogy: "The walkie-talkie. Direct channel. No interpretation needed. You do not ask the walkie-talkie to think about your request."

**Three memory engine options:**
1. **SQLite with vector + keyword search** — the built-in default; handles most personal setups
2. **QMD** — local search sidecar with reranking; can index entire project directories
3. **Honcho** — AI-native memory service that builds user profiles automatically from conversations; works across multiple agents

---

### 🔷 LESSON 6: Install Skills & Discover the Ecosystem

---

#### 7. ClawHub — The Skill Marketplace

**ClawHub** (`clawhub.ai`) is described as "the skill dock for sharp agents" — the public registry for Agent Skills bundles. Think of it as **npm for agent capabilities**.

Key features:
- Anyone can upload skills, version them like npm packages
- Searchable with **vector search** (not just keywords)
- Dangerous code detection — critical findings fail **closed** (install blocked, not just warned) as of v2026.3.31

**Key commands:**
```bash
openclaw skills search booking      # Search ClawHub
openclaw skills install service-booking  # Install a skill
openclaw skills list                # List installed skills
openclaw skills update --all        # Update all skills
```

⚠️ **Gateway restart required after installing a skill** — skills are snapshotted when a session starts.

---

#### 8. What Is a Skill (in OpenClaw)? ⭐

A skill is a **folder** containing a `SKILL.md` file that teaches the agent how to handle a specific task.

```
skill-name/
├── SKILL.md          # Required: metadata + instructions
├── scripts/          # Optional: executable code (Python, Bash, JS)
└── references/       # Optional: documentation loaded on demand
```

**Three components:**
- `SKILL.md` — the instructions (YAML frontmatter + markdown)
- `scripts/` — executable code the agent runs as part of the workflow
- `references/` — additional documentation read on demand

The **Agent Skills specification** (`agentskills.io`) is cross-platform — the same SKILL.md format works in **OpenClaw, Claude Code, and other agent platforms**.

**Progressive disclosure:** Only name and description load at startup (~light on tokens). Full instructions load only when the skill activates.

---

#### 9. The Plugin Ecosystem — Already Installed

Run this to see what you already have:
```bash
openclaw plugins list --verbose
```

**Three bundled plugin categories:**

| Category | Loaded by Default | Disabled by Default |
|---|---|---|
| **Model providers** | Google, Anthropic, OpenAI, DeepSeek, Mistral, Ollama, NVIDIA | Groq |
| **Channels** | WhatsApp | Discord, Telegram, Slack, Signal, Matrix, IRC, Line, MS Teams |
| **Utilities** | Browser, DuckDuckGo, Memory Core, Talk Voice | ElevenLabs, Brave, Firecrawl, OpenShell Sandbox |

**Plugin output fields:**
- `loaded` / `disabled` — whether the plugin is active
- `format` — `openclaw` (native TypeScript) or `bundle` (file-based)
- `origin` — `bundled` means it shipped with your install
- `providers` — which provider names it registers
- `error` — why it is disabled

---

#### 10. Two Plugin Formats ⭐

| | Native (`openclaw`) | Bundle (`.claude-plugin/`) |
|---|---|---|
| **Contains** | `openclaw.plugin.json` + TypeScript | Markdown skills + JSON commands + MCP connectors |
| **Code required?** | Yes | No |
| **Runs where** | Inside the gateway process | Loaded as file-based extensions |
| **Used for** | Channels, model providers, voice, gateway hooks | Domain workflows, knowledge packages |
| **Example** | WhatsApp adapter, Brave search | Productivity plugin, finance plugin |

> **Key insight:** The `.claude-plugin/` format is the SAME one Claude Code and Cowork use. Any Claude plugin works in OpenClaw as a bundle.

**Two open-source bundle collections:**
- Anthropic: `github.com/anthropics/knowledge-work-plugins` (productivity, sales, marketing, legal, finance, etc.)
- Panaversity: `github.com/panaversity/agentfactory-business-plugins` (Islamic finance, banking, legal operations)

---

#### 11. The Extension Decision Tree + Escalation Path ⭐

| Your agent needs to... | Extension type | Code required? |
|---|---|---|
| **Know** something new | Skill (SKILL.md) | No |
| **Access** an external service/API | MCP server | JSON config only |
| **Gain** a new gateway capability | Plugin (bundle first, native if needed) | Depends |

**The Escalation Path:**
```
Start here → Skill (SKILL.md, no code)
        ↓ not enough?
             → MCP server (JSON config, Lesson 7)
        ↓ not enough?
             → Plugin: bundle first (no code), native if needed
```

> "Most agent needs are skills. If you do need a plugin, try a bundle plugin first. Native plugins are for platform developers extending the gateway itself."

---

### 🔷 LESSON 7: Connect External Tools (MCP)

---

#### 12. The Two Config Levels for MCP ⭐

| Level | How | Scope |
|---|---|---|
| **Gateway-level** | `openclaw config set mcp.servers.*` | Shared across ALL agents |
| **Workspace-level** | `.mcp.json` in the workspace directory | Scoped to ONE agent only |

Use workspace-level when different agents need different tool sets.

---

#### 13. The Three MCP Transport Options ⭐

| Your Server | Transport | Config Key |
|---|---|---|
| Local (npm package, Python script) | **stdio** | `command` + `args` |
| Remote (HTTP Server-Sent Events) | **SSE** | `url` (default for URL-based) |
| Remote (HTTP streaming) | **streamable-http** | `url` + `"transport":"streamable-http"` |

**Connecting the time MCP server (first example):**
```bash
openclaw config set mcp.servers.time '{"command":"uvx","args":["mcp-server-time"]}'
openclaw gateway restart
```

Tools provided: `get_current_time` and `convert_time` (IANA timezone format: `Asia/Tokyo`, `America/New_York`).

---

#### 14. Silent Failure — OpenClaw's Most Counterintuitive Behavior ⭐

When an MCP server fails to start, **the agent answers normally using training data** — no error in chat, no indication anything went wrong.

**The ONLY diagnostic is the gateway log:**
```bash
tail -20 ~/.openclaw/logs/gateway.log
```

| Common Cause | What Log Shows | Fix |
|---|---|---|
| Wrong package name | Non-zero exit code | Verify exact package name |
| Missing runtime | "uvx: command not found" | Install uv or Node.js |
| Remote server unreachable | Connection timeout | Verify URL and server is running |
| Gateway not restarted | Old config still active | Run `openclaw gateway restart` |

> Emma: "I spent twenty minutes on my first one. Kept restarting the gateway, thinking it was a config syntax problem. The actual cause was a typo in the package name. The log is always the first place to look."

---

#### 15. MCP Management Commands

```bash
openclaw mcp list              # See all configured MCP servers
openclaw mcp show time         # See details for one server
openclaw mcp set time '{...}'  # Add or update
openclaw mcp unset time        # Remove a server
```

**Verify MCP tools appeared:** Dashboard → Agents → Tools (shows skills and MCP tools separately).

---

### 🔷 LESSON 8: Make It Proactive

---

#### 16. The Line That Separates Chatbot from AI Employee ⭐

> "This is the line. Everything before this lesson was a chatbot with features. After this lesson, it is a Personal AI Employee."

Before Lesson 8: the agent only responds when you type.
After Lesson 8: the agent acts on its own schedule.

---

#### 17. Heartbeats vs Cron Jobs ⭐

| Aspect | Heartbeat | Cron |
|---|---|---|
| **Timing** | Approximate (30-min intervals default) | Exact (cron expression) |
| **Batching** | Yes (multiple items, one API call) | No (one job = one run) |
| **Token cost** | Low (one turn, many checks) | Full (one turn per job) |
| **Use case** | "Check if anything needs attention" | "Deliver this at exactly 9:00 AM" |
| **Silence when nothing found** | Yes (HEARTBEAT_OK) | No |

---

#### 18. The Cost Math — Critical Exam Fact ⭐

**5 separate cron jobs at 30-minute intervals:**
- 5 jobs × 2 runs/hour × 24 hours = **240 agent turns per day**

**1 heartbeat with 5 checklist items:**
- 1 heartbeat × 2 runs/hour × 24 hours = **48 agent turns per day**

**Result: 80% fewer API calls for the same work.** Use heartbeats for batched periodic checks. Use crons only when exact timing is required.

---

#### 19. HEARTBEAT.md — The Checklist File ⭐

- Lives at `~/.openclaw/workspace/HEARTBEAT.md`
- Default state: **empty** (just comments) = heartbeat runs are **skipped entirely** — no API call, no tokens spent
- Activated by adding checklist items

**The HEARTBEAT_OK suppression token:**
- When the agent finds nothing to report, it replies with the exact string `HEARTBEAT_OK`
- The gateway scans for this token, strips it, and checks if remaining content ≤ 300 characters (`ackMaxChars`)
- If so: **message is silently dropped** — nothing reaches your phone
- When something needs attention: agent omits the token, gateway delivers the alert

> "Silent heartbeats are not wasted computation. They are proof that the agent is alive, watching, and has nothing to report."

---

#### 20. Heartbeat Config Commands

```bash
openclaw config set agents.defaults.heartbeat.every 1m    # Test interval
openclaw config set agents.defaults.heartbeat.target last  # Route to last active chat
openclaw config set agents.defaults.heartbeat.every 30m   # Production interval
openclaw gateway restart
```

**Owner/Operator separation:**
- **Agent owns WHAT to check** (HEARTBEAT.md content)
- **Operator controls HOW OFTEN and WHERE** (gateway config)

---

#### 21. Quiet Hours — Defense in Depth ⭐

Two layers, both required:

**Layer 1 — Prompt level (HEARTBEAT.md):**
```
## Quiet Hours
- Do NOT send customer messages before 8am or after 9pm
```
(Model may ignore this)

**Layer 2 — Infrastructure level (config):**
```bash
openclaw config set agents.defaults.heartbeat.activeHours.start "08:00"
openclaw config set agents.defaults.heartbeat.activeHours.end "21:00"
openclaw config set agents.defaults.heartbeat.activeHours.timezone "America/New_York"
```
(Gateway skips heartbeat entirely outside this window — no model call, no tokens, no risk)

> "Defense in depth means multiple layers, each independently sufficient, so that a single failure does not cascade."

---

#### 22. The Full Agent OS Mental Model (Expanded) ⭐

| OS Concept | OpenClaw Equivalent |
|---|---|
| Kernel | Gateway |
| Process scheduler | Heartbeat + Cron |
| Process table | Task ledger (`openclaw tasks list`) |
| File system | Workspace files |
| Cron daemon | HEARTBEAT.md + cron jobs |
| Process memory | Sessions |
| Device drivers | Plugins |
| Shared libraries | Skills |
| System calls | Tool profiles |
| IPC / Networking | Channels |
| User accounts | Pairing + session isolation |

---

### 🔷 LESSON 9: Give It a Voice

---

#### 23. Four TTS Providers ⭐

| Provider | API Key | Quality | Cost | Voices |
|---|---|---|---|---|
| **Microsoft Edge** | None | Good | **Free** | 300+ neural |
| **OpenAI TTS** | OPENAI_API_KEY | Excellent | ~$15/M chars | 6 |
| **ElevenLabs** | ELEVENLABS_API_KEY | Premium | Free tier available | Thousands |
| **MiniMax** | MINIMAX_API_KEY | Good | Free tier available | Multiple |

All providers produce **Opus-encoded OGG audio (48kHz, 64kbps)** — the exact format WhatsApp uses for push-to-talk voice messages. Replies appear as playable voice notes, not file attachments.

**Start with Microsoft Edge** (no API key, free, proves the pipeline).

---

#### 24. The Four TTS Modes ⭐

| Mode | Who Decides | Behavior | Use Case |
|---|---|---|---|
| `off` | Nobody | Text only (default) | Safe default |
| `always` | Config | Every reply → voice note | Testing only |
| `inbound` | Customer | Voice ↔ voice, text ↔ text | **Smart production default** |
| `tagged` | The Agent | TTS fires only when agent includes `[[tts]]` | Best UX (when working) |

**Why `always` gets annoying:** Every reply becomes audio. "Done." becomes a voice note. A reference number the user needs to copy becomes a voice note. `always` proves the pipeline — it is not a production setting.

**Why `inbound` is the smart default:** The agent automatically matches the customer's modality. Send text → get text. Send voice note → get voice note. No SOUL.md configuration needed.

**The `tagged` mode caveat:** The `[[tts]]` tags sometimes appear as literal text in chat instead of triggering synthesis. Until resolved, `inbound` is the reliable production choice.

---

#### 25. Enable Voice (3 Commands) ⭐

```bash
openclaw config set messages.tts.auto always
openclaw config set messages.tts.provider microsoft
openclaw config set plugins.entries.microsoft.enabled true
openclaw gateway restart
```

**Verify before testing:**
```
/tts status
```
Should show: `State: enabled`, `Provider: microsoft (configured)`.

**The 1,500-character limit:** Replies longer than 1,500 characters are auto-summarized or skipped. Adjust with `/tts limit 3000`.

---

#### 26. The Modality Design Principle

| Voice Works Best For | Text Works Best For |
|---|---|
| Descriptions, summaries | Reference numbers, links, codes |
| Emotional, persuasive content | Lists the customer needs to copy |
| Hands-busy users (driving) | Short confirmations |
| Long-form explanations | Search-friendly content |

> In `tagged` mode: "The agent becomes the UX designer." In `inbound` mode: "The gateway handles it automatically."

---

### 🔷 QUICK REFERENCE TABLE — Lessons 5–9 Key Facts

| Fact | Detail |
|---|---|
| Save to memory trigger | "Save in memory:" (not "Remember this:") |
| Memory verification command | `cat ~/.openclaw/workspace/MEMORY.md` |
| Proof of memory write | Tool badge in dashboard |
| Older memory retrieval | `memory_search` (vector + keyword hybrid) |
| Compaction trigger command | `/compact` |
| Model switching command | `/model <name>` |
| Reset session (keeps memory) | `/reset` |
| ClawHub URL | `clawhub.ai` |
| Skill install command | `openclaw skills install <name>` |
| After skill install requirement | `openclaw gateway restart` |
| Plugin list command | `openclaw plugins list --verbose` |
| Default memory engine | SQLite with vector + keyword search |
| MCP silent failure diagnostic | Gateway log (`~/.openclaw/logs/gateway.log`) |
| MCP verify tool command | Dashboard → Agents → Tools |
| Heartbeat default interval | 30 minutes |
| Test heartbeat interval | 1 minute |
| Heartbeat suppression token | `HEARTBEAT_OK` |
| Heartbeat cost vs 5 crons | 80% fewer API calls |
| 5 heartbeat items/day turns | 48 |
| 5 separate crons/day turns | 240 |
| TTS audio format | Opus-encoded OGG (48kHz, 64kbps) |
| TTS character limit | 1,500 (adjustable with `/tts limit`) |
| Free TTS provider | Microsoft Edge (no API key) |
| Production TTS mode | `inbound` |

