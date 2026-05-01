

**📘 Ch.56 Lessons 10–15 — Multi-Agent, Google Workspace, Orchestrate, Gate & NemoClaw**
*OpenClaw Personal AI Employee | 20 Questions | Answers shuffled!*

---

**Q1.** James explains the agent split using his warehouse experience. What was the PRECISE principle behind splitting into two stations?


🅐 About WORKLOAD — too many tasks for one person, divided by task type with same permissions

🅑 About PERSONALITY — different communication styles for different customer types

🅒 About AVAILABILITY — one desk for morning shifts, the other for afternoon shifts

🅓 About PERMISSIONS — both desks were friendly, but only one could release inventory. In OpenClaw: two agents with different workspace configs define what each is ALLOWED TO DO, not just how it talks

---

**Q2.** Which scenario CORRECTLY illustrates the gateway vs workspace config distinction?


🅐 Installing ElevenLabs at workspace level syncs it to all agents automatically. Skills at gateway level are limited to that agent only

🅑 Updating model to Opus in customer-facing workspace upgrades only that agent. Installing a new MCP at gateway level goes only to the default agent

🅒 Configuring a new WhatsApp binding at workspace level restricts messages to that agent. Skills at gateway level are shared by all

🅓 Installing ElevenLabs plugin at GATEWAY level → BOTH agents get voice immediately. Adding finance-skills to ops agent's WORKSPACE → ONLY ops agent gets them. 'Gateway is infrastructure. Workspace is identity.'

---

**Q3.** What is the PRECISE behavior of session cache and how do you force an identity change to take effect immediately?


🅐 Identity changes take effect after a gateway restart — run 'openclaw gateway restart'

🅑 Changes take effect within 60 seconds via background file-watch daemon — no manual action needed

🅒 Changes take effect only when customers close and reopen WhatsApp completely

🅓 Identity changes (SOUL.md, IDENTITY.md) take effect at SESSION BOUNDARIES — not mid-conversation. A customer in an active session keeps the old persona until their session expires. Force immediately with /new. 'The session is the shift. The reassignment takes effect at the boundary.'

---

**Q4.** The book identifies a 'turning point' at Lesson 11 that makes the 'AI Employee' label accurate. What is it?


🅐 Enabling voice (Lesson 9) — the agent communicates through audio, matching how real employees interact

🅑 Adding a second agent (Lesson 10) — for the first time the system has multiple coordinating workers

🅒 Making the agent proactive (Lesson 8) — autonomous initiative distinguishes employee from tool

🅓 Connecting gog (Lesson 11) — for the first time, the agent touches REAL DATA: YOUR inbox, YOUR calendar, YOUR files. 'That is when AI Employee stops being a metaphor.' Every previous lesson operated on data the agent generated itself

---

**Q5.** A developer wants the agent to read emails and check calendar but NEVER send emails or access Drive. What is the EXACT gog command?


🅐 'gog auth add me@gmail.com --services gmail,calendar --no-write'

🅑 'gog auth add me@gmail.com gmail:readonly calendar:readonly' (colon notation for individual scoping)

🅒 'gog auth add me@gmail.com --services gmail,calendar --scope read'

🅓 'gog auth add me@gmail.com --services gmail,calendar --readonly' — the --readonly flag limits BOTH services to read-only, preventing sending emails, creating calendar events, and accepting/declining invitations. Drive excluded by omitting from --services

---

**Q6.** The book warns that even read-only Gmail access has significant security implications. What is the specific risk?


🅐 The agent retains email content in MEMORY.md permanently — configure SOUL.md to prevent saving email content

🅑 Third-party MCP servers can read all emails through gog, bypassing skill restrictions — use NemoClaw only

🅒 Gmail auto-forwards to ~/.openclaw/workspace/ permanently — set 'email.retention.days: 7' in openclaw.json

🅓 The agent can see EVERY email including password reset emails and financial statements. Mitigation: (1) use a DEDICATED TEST GOOGLE ACCOUNT for first setup, not your primary. (2) After connecting, run 'openclaw secrets audit'

---

**Q7.** Free-tier models exhibit a specific failure with sessions_spawn. What exactly happens and why does the book call it 'worse than ignoring'?


🅐 The model spawns subagents with incorrect parameters — consuming credits and producing misleading results that appear valid

🅑 The model spawns then immediately kills the subagent — token costs appear in billing with no useful output

🅒 The model ignores sessions_spawn with no feedback — a generic low-quality response with no error message to diagnose

🅓 The model FABRICATES plausible-sounding refusals — claiming 'permission errors', 'authorization restrictions', 'tool limitations'. These are hallucinations. Worse than ignoring because they make the PLATFORM appear broken, causing developers to debug a working system

---

**Q8.** maxConcurrent=4, 7 customers message simultaneously, each takes 5 seconds. What happens to customer 7?


🅐 All 7 enter the global lane simultaneously — session lanes are not activated until the global lane is full

🅑 Customers 1-7 queue in individual session lanes processed one at a time sequentially — customer 7 waits ~30 seconds

🅒 Customers 5-7 wait for ALL FOUR of the first wave to complete before any slot opens — customer 7 waits ~10 seconds

🅓 Customers 1-4 start immediately. Customers 5-7 queue. Customer 7 waits ~5 seconds — the time for the FASTEST of the first 4 to finish (not all 4, not 15 seconds). Parallel waves, not sequential processing

---

**Q9.** Why is setting permissionMode CRITICAL before spawning ACP sessions?


🅐 Without it, Claude Code automatically gains root access — can delete system files and access all user directories

🅑 Without it, ACP sessions are billed at 10x standard rate — treated as enterprise API calls

🅒 Without it, output goes to a separate dashboard tab instead of the WhatsApp conversation thread

🅓 ACP sessions are NON-INTERACTIVE — Claude Code cannot ask for permission through WhatsApp mid-task. Without permissionMode: EVERY tool use is denied (ACP_TURN_FAILED: Permission denied). Session spawns but literally cannot do any file reads or command executions

---

**Q10.** The three-tier safety model — what does each tier prevent that the previous tier cannot?


🅐 Tier 1 prevents unauthorized tool use. Tier 2 requires OAuth tokens per external service call. Tier 3 prevents DDoS attacks with rate-limited network namespaces

🅑 Tier 1 prevents customer data exposure. Tier 2 prevents prompt injection by validating messages before the model. Tier 3 prevents memory leaks between sessions

🅒 Tier 1 prevents skill misuse. Tier 2 prevents excessive API spending above a token threshold. Tier 3 prevents data persistence between conversations

🅓 Tier 1 (tool profiles) = binary allow/deny at tool level. Tier 2 (plugin hooks) = human approval before sensitive operations — the tool exists but needs a doorbell ring. Tier 3 (NemoClaw) = API keys in a DIFFERENT PROCESS that the agent physically cannot reach, even if it bypasses Tiers 1 and 2

---

**Q11.** Constraint 5: 'MCP tools bypass before_tool_call hooks.' What is the TECHNICAL reason?


🅐 MCP tools run in a separate process — hooks only intercept in-process calls. Approval gates must be middleware on MCP server endpoints

🅑 MCP tools use OAuth tokens — the hook system only processes tool calls using the agent's API key

🅒 MCP tools are marked 'trusted' in the registry by default — set mcp.trustLevel = 'untrusted' to change this

🅓 MCP tools are APPENDED AFTER hook wrapping during initialization — when the before_tool_call hook registers and wraps the tool registry at startup, MCP tools haven't been added yet. They are never wrapped. 'If something in Chapter 57 calls customers or books appointments, this gate will not protect those operations'

---

**Q12.** 'You will not write the plugin code. You will send a prompt.' What deeper skill principle does this teach?


🅐 Test-driven development — write failing tests first, let agent build implementation that passes them

🅑 Pair programming — you write business logic, agent writes technical implementation, real-time collaboration

🅒 Vibe coding — give general description, let agent figure out details autonomously, trust without over-specifying

🅓 CONSTRAINT-DRIVEN SPECIFICATION — your job is articulating constraints precisely enough that the agent builds correctly on the first attempt. James: 'Writing the purchase order policy took three meetings and legal review. This took five lines and two links. But the thinking was the same: figure out the constraints, write them clearly enough.' The skill is constraint precision, not code writing

---

**Q13.** The book claims: 'promises vs physics.' What does each term represent?


🅐 Promises = SOUL.md rules the agent follows voluntarily. Physics = compiled rule set that cannot be modified at runtime

🅑 Promises = API rate limits enforced by provider quota (circumventable). Physics = rate limits at network level (impossible to bypass)

🅒 Promises = agent must ask permission before each tool use via approval gates. Physics = pre-approved by policy file agent cannot modify

🅓 Promises (Docker Compose) = in-process tool profiles enforce rules within the SAME Node.js runtime as agent — bypass the runtime and rulesfail. Physics (NemoClaw) = API keys in a DIFFERENT POD with NO NETWORK ROUTE from sandbox — the route doesn't exist. 'You cannot steal what is not there'

---

**Q14.** Walk through the EXACT sequence of an inference call in NemoClaw's Privacy Router.


🅐 Agent sends request with SESSION TOKEN → gateway validates → privacy router adds API key → provider → response

🅑 Agent requests API key from router using agent ID → router issues time-limited 60-second token → agent calls provider directly → token expires

🅒 Agent sends request with SANDBOX CERTIFICATE → router verifies certificate → router adds API key → provider → response

🅓 1. Agent calls inference.local:8080 with model name, NO API KEY. 2. Crosses network namespace boundary to router pod. 3. Router looks up real key. 4. Router adds Authorization header. 5. Forwards to api.anthropic.com. 6. Response comes back STRIPPED of auth headers. 7. Agent receives clean response. Agent never sees its own API key

---

**Q15.** The Policy Engine uses three kernel-level mechanisms. What does each restrict?


🅐 Landlock = memory access. seccomp = CPU usage. Network namespaces = bandwidth limits

🅑 Landlock = process creation. seccomp = file permissions. Network namespaces = DNS resolution

🅒 Landlock = user permissions (non-root). seccomp = inter-process communication. Network namespaces = port access

🅓 Landlock = FILESYSTEM ACCESS (sandbox reads/writes only its own workspace). seccomp = SYSTEM CALLS (no ptrace, no mount, no raw sockets). Network namespaces = ROUTING (the route to api.anthropic.com literally doesn't exist in sandbox's network stack — structural impossibility, not interception)

---

**Q16.** What is the core principle underlying ALL NemoClaw upgrade triggers?


🅐 SCALE — when traffic consistently exceeds 4 concurrent sessions and K3s enables horizontal scaling

🅑 FEATURE REQUIREMENTS — when you need multi-agent coordination that Docker Compose cannot support

🅒 UPTIME — when you need 99.9% SLA; K3s provides automatic pod restart and load distribution

🅓 TRUST MODEL CHANGE — not scale. When a second operator joins, when customers' data becomes your liability, when compliance requires audit evidence. '$10/month is a LIABILITY decision, not a cost decision.' Docker Compose is fine when operator = user = trusting relationship

---

**Q17.** What specific limitations exist in NemoClaw v0.1.0 (alpha)?


🅐 Max 2 agents per deployment; voice (TTS) not supported in sandbox; skills cannot update without full sandbox recreation; gog incompatible with privacy router isolation

🅑 Requires dedicated server (no shared VPS); $150/month minimum from K3s licensing; MCP re-registration required after every restart; WhatsApp pairing breaks on every update

🅒 MEMORY.md not shared between sandbox and gateway pods; heartbeats disabled by default in sandbox; privacy router only supports Anthropic API; max 2 concurrent sessions

🅓 (1) Crash recovery is MANUAL — K3s recreation needed; Docker Compose with restart:unless-stopped is MORE resilient. (2) No sandbox image caching — 1142 MiB push per sandbox creation (3-7 minutes). (3) Split log aggregation — separate kubectl logs per pod. (4) Documentation gaps (cgroup v2 issue not in setup steps)

---

**Q18.** Sender-specific bindings vs channel-wide bindings — which wins and what determines priority?


🅐 Channel-wide wins — evaluated first in routing chain. Sender-specific only applies when no channel-wide binding exists

🅑 The binding FIRST in the array wins — array order determines priority. Place most important binding at top

🅒 Both fire simultaneously — OpenClaw uses whichever agent responds faster. Lower latency = winning route

🅓 Sender-specific (peer phone number match) ALWAYS WINS over channel-wide. Array order does NOT determine priority — SPECIFICITY determines precedence. Practical use: all WhatsApp → helper-agent (channel-wide), EXCEPT your personal number → main (sender-specific)

---

**Q19.** What prevents Customer A's context from being visible during Customer B's agent turn?


🅐 NemoClaw sandbox isolation — each customer session runs in a separate container with its own memory space

🅑 The maxConcurrent=1 per session lane — only 1 message processes at a time per customer, preventing overlap

🅒 Each customer's MEMORY.md is encrypted with their session ID — data is unreadable without the correct key

🅓 The SESSION SYSTEM from Lesson 2 — completely separate from the concurrency model. Global lane controls HOW MANY run simultaneously (concurrency). Session system controls WHAT EACH SESSION SEES (isolation). These are ORTHOGONAL systems. 'Isolation is handled by the session system from Lesson 2'

---

**Q20.** The approval gate has three decisions. What is the EXACT behavior of each and what happens on timeout?


🅐 allow-once = runs + suppresses next 5 prompts. allow-always = permission for current session only. deny = blocks + disables tool 10 minutes. Timeout = runs automatically (fail open)

🅑 allow-once = runs + logs for audit review. allow-always = permission for current calendar day only. deny = blocks + sends alert to gateway log. Timeout = runs after 60-second grace period

🅒 allow-once = grants approval for all calls using same tool (exec) for rest of session. allow-always = marks tool as trusted in TOOLS.md permanently. deny = blocks + removes tool from profile. Timeout = prompts again before blocking

🅓 allow-once = ONE-TIME PASS only, all future calls still require approval. allow-always = PERMANENT permission for all future calls from this plugin. deny = this call blocked, agent gets denial. Timeout (120s default, timeoutBehavior:'deny') = automatic BLOCK, FAIL CLOSED — same result as deny. 'The tool does not run.'


