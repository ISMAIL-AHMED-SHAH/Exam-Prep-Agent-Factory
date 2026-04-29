
## 📘 Chapter 56 — Part E Study Notes: Lessons 10–15
### Add Second Agent | Google Workspace | Orchestrate | Gate Tools | Deploy | NemoClaw

---

### 🔷 LESSON 10: Add a Second Agent

---

#### 1. Why Split Agents? — The Warehouse Analogy

One agent handling everything is like one person at the front desk handling both customer pickups and inbound shipments. James's warehouse fixed it by splitting into two desks with **different permissions** — not different personalities. Same principle in OpenClaw: the split is about **what each agent is allowed to do**, not how it talks.

---

#### 2. Gateway Config vs Workspace Config ⭐

| | Gateway Config | Workspace Config |
|---|---|---|
| **What it contains** | Plugins, TTS, model settings | SOUL.md, IDENTITY.md, skills, MCP servers |
| **Scope** | Shared across ALL agents | Per-agent only |
| **Implication** | Install a plugin → both agents get it | Edit SOUL.md → only that agent changes |

> "Gateway is infrastructure. Workspace is identity."

---

#### 3. Session Cache — The Shift Boundary ⭐

Identity changes (IDENTITY.md updates) take effect at **session boundaries**, NOT mid-conversation. A customer in an active session keeps the old persona until their session expires. Use `/new` to start a fresh session when testing identity changes.

> James's analogy: "The session is the shift. The identity change is the reassignment. It takes effect at the boundary, not in the middle."

---

#### 4. Routing Rules — Three Levels

| Rule Type | How | Scope |
|---|---|---|
| **Channel-wide binding** | `openclaw agents bind --agent X --bind whatsapp` | ALL messages on that channel go to agent X |
| **Sender-specific binding** | Edit `openclaw.json` directly, add `bindings` array with `peer.id` | Messages from a specific phone number go to agent X |
| **Multi-number** | `openclaw channels login --account personal/business` | Each WhatsApp number gets its own agent |

**Fallback rule:** Unmatched messages always go to the main agent. No message is ever lost.

**Critical flag:** Always use `--workspace` when editing a non-main agent to avoid silently misconfiguring the main agent.

---

### 🔷 LESSON 11: Connecting Google Workspace

---

#### 5. gog — The Google Bridge ⭐

**gog** is a CLI that bridges OpenClaw and Google Workspace. One OAuth setup gives the agent access to Gmail, Calendar, Drive, Contacts, Sheets, Docs, and more. Core command format: `gog gmail`, `gog calendar`, `gog drive`.

**Three services in Lesson 11:**

| Service | What Agent Can Do |
|---|---|
| **Gmail** | Search messages, read threads, send mail, manage labels |
| **Calendar** | List events, create meetings, check availability |
| **Drive** | Search files, upload/download documents, manage permissions |

---

#### 6. Least Privilege — The Critical Security Principle ⭐

Grant only the access the agent actually needs.

```bash
gog auth add me@gmail.com --services gmail,calendar --readonly
```

The `--readonly` flag limits all services to read access. Even read-only Gmail means the agent can see every email including password resets and financial statements.

**What could go wrong with broad access:**
- Read sensitive emails (passwords, financial statements)
- Send emails without your knowledge
- Access confidential Drive documents
- Exfiltrate contacts to external servers

**After connecting any integration:** Run `openclaw secrets audit` — checks for plaintext credentials that should be migrated to SecretRefs.

---

#### 7. The Turning Point

> "Everything before this lesson used data the agent generated itself. This lesson connects it to YOUR inbox, YOUR calendar, YOUR files. That is when 'AI Employee' stops being a metaphor."

**The OAuth Pattern repeats for every SaaS integration:** Register credentials → authorize with CLI → scope permissions. Works the same for Slack, GitHub, Notion, Jira.

---

### 🔷 LESSON 12: Orchestrate Other Agents

---

#### 8. The Model Is the Weakest Link ⭐

Free-tier models exhibit a specific failure: they actively fabricate reasons NOT to use `sessions_spawn`. The model claims "permission issues" or "tool limitations" — these are hallucinations. After 2–3 rounds of insistence, the tool fires.

**Two steps to fix:**
1. Clear the session (`/new`) — old refusal patterns in history cause new refusals
2. Be explicit: "Do you have sessions_spawn? Use it NOW. Spawn a subagent that..."

> "The model is always the weakest link. Everything else is infrastructure."

---

#### 9. Two Delegation Patterns ⭐

| Pattern | Behavior | When to Use |
|---|---|---|
| **sessions_spawn** | Blocking — waits for result before responding | Need full answer before replying |
| **sessions_yield** | Async — replies immediately "I'll get back to you" | Matches WhatsApp conversational cadence; 14-second pauses feel wrong |

**Nested orchestration:** Enable with `openclaw config set agents.defaults.subagents.maxSpawnDepth 2`. Track flows with `openclaw tasks flow list`.

---

#### 10. The Two-Layer Concurrency Model ⭐

| Layer | Scope | maxConcurrent | Behavior |
|---|---|---|---|
| **Session lane** | Per-customer | 1 | Messages from same customer process sequentially (prevents race conditions) |
| **Global lane** | Shared | 4 (default) | Up to 4 different customers processed in parallel |

**The math (exam favourite):**
- 5 customers message simultaneously → 4 start immediately, 1 queues
- Customer 5 waits ≈ 3–8 seconds (time for fastest of first 4 to finish)
- 7 customers with maxConcurrent=4, 5 seconds each → customers 1–4 start, 5–7 queue ~5 seconds

**No cross-contamination:** Session lanes are completely isolated. Customer A's context is NEVER visible during Customer B's agent turn.

---

#### 11. ACP — Control Claude Code from WhatsApp ⭐

**ACP (Agent Client Protocol):** How OpenClaw controls external coding agents (Claude Code, Codex, Cursor, Gemini CLI).

```bash
# Enable ACP plugin
openclaw config set plugins.entries.acpx.enabled true
openclaw config set acp.enabled true
openclaw config set plugins.entries.acpx.config.permissionMode approve-reads

# Spawn Claude Code session from WhatsApp
/acp spawn claude --bind here

# Send it work
/acp steer Summarize the README.md in my current project

# Check and close
/acp status
/acp close
```

**Three permission modes:**

| Mode | Allows |
|---|---|
| `approve-reads` | Read files, list directories. Block writes/exec |
| `approve-all` | Read, write, execute commands |
| `deny-all` | Block everything (testing only) |

**Critical:** ACP sessions are NOT sandboxed — Claude Code spawned via ACP has the same filesystem access as Claude Code in your terminal.

**Wait for spawn confirmation before sending /acp steer** — sending before ready causes `ACP_SESSION_INIT_FAILED`.

---

### 🔷 LESSON 13: Gate Your Agent's Tools

---

#### 12. Three-Tier Safety Model ⭐

| Tier | Mechanism | Level | Prevents |
|---|---|---|---|
| **1** | Tool profiles (coding/messaging/minimal) | In-process, same Node.js runtime | Agent accessing unauthorized tools |
| **2** | Plugin hooks with `requireApproval` | In-process, plugin intercepts before execution | Sensitive operations without operator approval |
| **3** | NemoClaw sandboxing | Out-of-process, kernel-level | API key exfiltration, network escape |

> Tool profiles = door lock (open/closed). Plugin hooks = doorbell (anyone can knock, you decide to open).

---

#### 13. Six Plugin Constraints — Silent Failures ⭐

Plugins that violate these **compile, load, and silently do nothing**:

| # | Constraint | Wrong | Right |
|---|---|---|---|
| 1 | Hook system | `api.registerHook()` (legacy) | `api.on()` (typed, works) |
| 2 | Registration | `plugins.load.paths` alone | Also need `plugins.entries.<id>.enabled = true` |
| 3 | Hook name | Required in legacy only | `api.on()` doesn't need it |
| 4 | Tool name | `"bash"` (display name) | `"exec"` (internal name) |
| 5 | MCP bypass | Expect hooks to gate MCP | MCP tools bypass `before_tool_call` hooks entirely |
| 6 | Approval routing | Plugin returns `requireApproval` alone | Also need `approvals.plugin` in openclaw.json |

**Three approval decisions:**
- `allow-once` — this call runs, future calls still ask
- `allow-always` — this and all future calls proceed without asking
- `deny` — blocked, agent receives denial

**Default timeout:** 120 seconds. `timeoutBehavior: "deny"` = fail closed.

---

#### 14. Constraint-Driven Specification

The lesson's meta-lesson: you don't write plugin code — you write constraints. The agent reads the constraints + reference URL, builds the plugin, registers it, and verifies the load.

> "The skill is specifying constraints precisely enough that the agent builds correctly on the first attempt."

---

### 🔷 LESSON 15: Isolate with NemoClaw

---

#### 15. The Core Problem with Docker Compose

API keys live as environment variables inside the container — in the same process as the agent. Tool profiles are in-process checks in the same Node.js runtime. If an attacker bypasses the runtime via a native module vulnerability or V8 exploit, tool profiles are irrelevant and keys are exposed.

> "The agent promises to follow the rules" (Docker Compose) vs "The agent physically cannot break the rules" (NemoClaw).

---

#### 16. What NemoClaw Is ⭐

```
NemoClaw = OpenClaw + OpenShell + Privacy Router + Policy Engine
```

Not a new product. Not a fork. One install command. Runs as a K3s (lightweight Kubernetes) cluster inside a single Docker container with four pods.

---

#### 17. The 4-Pod Architecture ⭐

| Pod | Purpose | Has API Keys? | Has Agent? |
|---|---|---|---|
| **Gateway** | Channel adapters, auth, routing, Control UI | No | No |
| **Sandbox** | OpenClaw runtime, agent loop, tools, skills | **NO** | **YES** |
| **Privacy Router** | API key vault, provider fallback, rate limiting | **YES** | No |
| **Policy Engine** | Landlock (fs), seccomp (syscalls), netns (network) | No | No |

**Critical insight:** No arrow carries API keys into the Sandbox.

---

#### 18. The Privacy Router — How It Eliminates the Key Attack Surface ⭐

1. Agent sends request to `inference.local:8080` with model name but **NO API key**
2. Request crosses network namespace boundary (sandbox → router pod)
3. Privacy router looks up provider and API key
4. Router adds `Authorization` header with real key
5. Router forwards to actual provider (api.anthropic.com)
6. Response comes back clean (no auth headers)
7. Agent receives standard model response

The agent **never sees its own API key**. Even with full root access in the sandbox, `printenv` shows no keys, config files show only `inference.local`, and network traffic contains no credentials.

---

#### 19. Kernel-Level Enforcement

| Primitive | What It Does |
|---|---|
| **Landlock** | Restricts filesystem access — sandbox can only read/write its own workspace |
| **seccomp** | Restricts system calls — no `ptrace`, no mount, no raw sockets |
| **Network namespaces** | Removes route to api.anthropic.com — route doesn't exist in sandbox's network stack |

---

#### 20. When to Upgrade from Docker Compose ⭐

| Signal | Meaning |
|---|---|
| Customer asks "where are API keys stored?" | Need better answer than "environment variable" |
| Second operator joins | They shouldn't have direct key access |
| Compliance audit requires evidence | Default-deny network policy IS audit evidence |
| Serving paying customers | $10/month is a liability decision, not a cost decision |

**Cost delta:** Docker Compose ~$66/month vs NemoClaw ~$76/month ($10 difference).

**NemoClaw minimum specs:** 4 vCPU, 8 GB RAM.

**Alpha status:** v0.1.0. Crash recovery is manual. No sandbox image caching (1142 MiB push per sandbox creation). Log aggregation is split across four pods.

---

### 🔷 QUICK REFERENCE — Lessons 10–15

| Fact | Detail |
|---|---|
| Gateway config scope | Shared across ALL agents |
| Workspace config scope | Per-agent only |
| Session cache behavior | Changes take effect at session boundary, not mid-session |
| gog install command (macOS) | `brew install gogcli` |
| gog verify command | `gog auth list` |
| After gog integration | `openclaw secrets audit` |
| maxConcurrent default | 4 |
| Session lane concurrency | 1 per customer (sequential) |
| 5 customers, maxConcurrent=4 | Customer 5 waits ~3–8 seconds |
| ACP permission mode recommended | `approve-reads` to start |
| Tool name (display vs internal) | bash (display) vs exec (internal) |
| Approval timeout default | 120 seconds |
| MCP tools and hooks | MCP tools BYPASS before_tool_call hooks |
| NemoClaw formula | OpenClaw + OpenShell + Privacy Router + Policy Engine |
| NemoClaw deployment | K3s cluster inside single Docker container |
| Privacy router endpoint | `inference.local:8080` |
| NemoClaw cost delta | ~$10/month more than Docker Compose |
| NemoClaw minimum specs | 4 vCPU, 8 GB RAM |
| NemoClaw version | v0.1.0 (alpha) |
| OpenShell version | v0.0.16 |

---
