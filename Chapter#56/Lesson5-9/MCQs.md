

**📘 Ch.56 Lessons 5–9 — Memory, Skills, MCP, Proactive & Voice**
*OpenClaw Personal AI Employee | 20 Questions | Answers shuffled!*

---

**Q1.** Emma's golden rule: 'Verify on disk, not just in chat.' What problem does this address and what are the TWO verification methods?


🅐 File corruption during concurrent session access — verify with 'openclaw memory verify' and restart the gateway

🅑 Memory entries expire after 24 hours unless marked permanent — check 'expires' field and run 'openclaw memory list --permanent'

🅒 Only the first 50 lines of MEMORY.md load per session — count with 'wc -l' and ask which entries loaded at start

🅓 'Remember this:' may produce verbal acknowledgment WITHOUT a file write. Verify with: (1) dashboard tool badge confirming write, and (2) 'cat ~/.openclaw/workspace/MEMORY.md' — verbal confirmation is NOT proof

---

**Q2.** The two memory locations: MEMORY.md and memory/ directory. What is the PRECISE loading behavior for each?


🅐 MEMORY.md loads every session. memory/ loads the LAST 7 DAYS automatically. Entries older than 7 days are permanently deleted

🅑 MEMORY.md loads every session. memory/ loads the current MONTH automatically. Older months are compressed into monthly summaries

🅒 MEMORY.md loads every session. memory/ does NOT auto-load ANY logs — all entries require explicit '/memory search' retrieval

🅓 MEMORY.md loads every session. memory/ loads TODAY's + YESTERDAY's logs automatically. Everything older stays on disk and is retrieved on demand via memory_search — hybrid retrieval combining vector similarity (meaning) and keyword matching (exact terms)

---

**Q3.** Compaction is triggered by long conversations. What EXACTLY happens and why does persistent memory matter because of it?


🅐 Compaction deletes conversation history older than 48 hours; the agent is NOT warned before it happens — persistent memory is the only backup

🅑 Compaction merges daily journal files into a compressed archive every Sunday; the merge can corrupt individual files — MEMORY.md is the backup

🅒 Compaction is triggered when response time exceeds 5 seconds; it clears the MCP tool cache — tools must be re-registered in MEMORY.md

🅓 Gateway compacts OLDER TURNS into summaries to free context space; before compacting, the agent is reminded to save important things to memory files. Session context CAN be summarized away — but MEMORY.md and daily logs survive on disk regardless

---

**Q4.** Slash commands are 'gateway-intercepted.' What does this mean precisely and what is the PRESCRIBED PROOF?


🅐 Commands are processed by a dedicated microservice parallel to the LLM — proof: send /status while a long query is processing and observe both arrive independently

🅑 Commands are validated against an approved whitelist — proof: try sending /delete-all and observe the security error rather than LLM processing

🅒 Commands are cached for 60 seconds — proof: send /status twice and observe the second response is 10x faster

🅓 The command is caught by the GATEWAY before reaching the LLM — zero tokens spent, instant response. Prescribed proof: send '/status' (under 1 second, no thinking indicator) vs ask 'What model are you using?' in natural language (3+ seconds, thinking indicator visible). The timing gap IS the proof

---

**Q5.** ClawHub is described as 'npm for agent capabilities.' What specific npm behaviors does it replicate?


🅐 Dependency resolution, private registries, and semantic versioning (major/minor/patch signals)

🅑 Lockfile generation (skills-lock.json), audit command for vulnerabilities, and workspace monorepo support

🅒 Global vs local installation, peer dependencies, and pre/post install hooks

🅓 Versioning (like npm packages), public publishing (anyone can upload), CLI installation ('openclaw skills install' mirrors 'npm install'), and VECTOR SEARCH (not just keyword matching — find skills by meaning)

---

**Q6.** A Skill has three possible folder components. What are the THREE components and which is the ONLY required one?


🅐 SKILL.md (required), config.json (optional — permissions/access controls), tests/ (optional — marketplace verification)

🅑 SKILL.md (required — instructions only), tools.json (optional — MCP connections), examples/ (optional — sample conversations)

🅒 SKILL.md (required), prompts/ (optional — dynamic prompt templates), data/ (optional — static reference data CSV/JSON)

🅓 SKILL.md (REQUIRED — YAML frontmatter + markdown instructions), scripts/ (optional — executable code: Python/Bash/JavaScript), references/ (optional — documentation read on demand). 'A skill can be a single markdown file. The simplicity is intentional.'

---

**Q7.** What is the SINGLE most important cross-ecosystem insight about the bundle plugin format (.claude-plugin/)?


🅐 The bundle format is the same used by Cursor and GitHub Copilot — any IDE plugin works in OpenClaw as a bundle

🅑 The bundle format is a subset of npm — any npm package with a plugin.json manifest qualifies as an OpenClaw bundle plugin

🅒 The bundle format is proposed by AAIF — all member tools will eventually support it, making bundles the safest long-term investment

🅓 The .claude-plugin/ format is the SAME format used by Claude Code and Cowork — any Claude plugin works in OpenClaw as a bundle, opening the entire Claude plugin ecosystem without code conversion

---

**Q8.** The escalation path: Skill → MCP → Plugin. What is the SPECIFIC decision criterion for EACH escalation step?


🅐 Escalate Skill→MCP when SKILL.md exceeds 200 lines. Escalate MCP→Plugin when more than 5 MCP servers need coordination

🅑 Escalate Skill→MCP when data exceeds 10MB. Escalate MCP→Plugin when MCP response latency exceeds 2 seconds

🅒 Escalate Skill→MCP when the task requires state persistence beyond MEMORY.md. Escalate MCP→Plugin when multiple agents must share the same MCP server

🅓 Escalate Skill→MCP when the agent needs real EXTERNAL ACCESS (not just knowledge — a skill teaches but can't connect to live data). Escalate MCP→Plugin when the agent needs to MODIFY GATEWAY BEHAVIOR (add channels, voice, routing). Try bundle plugin before native TypeScript

---

**Q9.** MCP silent failure — what EXACTLY happens when an MCP server fails and what is the ONLY diagnostic?


🅐 A red 'Tool unavailable' error banner appears in WhatsApp; the only place to see technical details is the gateway log

🅑 The agent replies 'I'm having trouble accessing that tool' and retries 3 times; the only place to see retry history is the gateway log

🅒 The gateway automatically switches to the nearest compatible MCP server; the only place to see the fallback is the gateway log

🅓 The agent responds NORMALLY using training data — NO error in chat, NO warning, NO indicator. The response LOOKS correct; only the tools are missing. The ONLY diagnostic is the gateway log at ~/.openclaw/logs/gateway.log

---

**Q10.** Gateway-level vs workspace-level MCP config — what is the PRECISE architectural distinction?


🅐 Gateway-level is permanent (requires restart); workspace-level is temporary (takes effect immediately). Use gateway for production; workspace for experiments

🅑 Gateway-level is shared across all users of the same OpenClaw installation; workspace-level is private to one user. Use gateway for organizational tools

🅒 Gateway-level allows all 3 transports (stdio, SSE, streamable-http); workspace-level allows only stdio. Use gateway for remote servers

🅓 Gateway-level ('openclaw config set mcp.servers.*') stores in openclaw.json → shared across ALL AGENTS. Workspace-level (.mcp.json in workspace) → scoped to the ONE AGENT whose workspace contains it. Use workspace-level when different agents need different tool sets

---

**Q11.** Emma: 'Everything before this lesson was a chatbot with features. After this lesson, it is a Personal AI Employee.' What SPECIFIC capability crosses this line?


🅐 The agent can now maintain context across multiple simultaneous WhatsApp conversations — shared awareness across all active chats

🅑 The agent can now access external APIs via MCP servers — real-time data instead of just training data (Lesson 7 capability)

🅒 The agent can now maintain persistent memory across sessions via MEMORY.md — remembering preferences across days (Lesson 5 capability)

🅓 The agent acts WITHOUT being prompted — heartbeats fire at regular intervals, cron jobs at exact times, triggering the agent to check, decide, and act entirely on its own schedule. Like a coordinator who checks the supplier inbox before the morning meeting without being told to

---

**Q12.** The book presents specific cost math for heartbeat vs cron jobs. What are the EXACT numbers?


🅐 5 cron jobs × 2/hour × 24hrs = 240 turns. 5 heartbeat items × 2/hour × 24hrs = 240 turns. Cost is the same; heartbeats offer batching quality benefits only

🅑 5 cron jobs at 30-min intervals = 5 × 48 = 240 runs/day at $0.02 each = $4.80/day. 1 heartbeat = 48 × $0.02 = $0.96/day. 80% cost reduction

🅒 5 cron jobs at 1-hour intervals = 5 × 24 = 120 turns/day. 1 heartbeat at 30-min intervals = 48 turns/day. 60% reduction — heartbeats only beat crons at high-frequency

🅓 5 cron jobs at 30-min intervals: 5 × 2 × 24 = 240 agent turns/day. 1 heartbeat with 5 items: 1 × 2 × 24 = 48 agent turns/day. 80% reduction. Principle: heartbeats BATCH multiple checks into ONE wake-up cycle; each cron requires a dedicated full agent turn

---

**Q13.** The HEARTBEAT_OK suppression mechanism — what EXACTLY does the gateway do when it receives a response containing this token?


🅐 Replaces HEARTBEAT_OK with empty string and delivers remaining content labeled '[heartbeat]' so you can track that the check ran

🅑 Forwards the token to a monitoring dashboard recording run history but delivers nothing to WhatsApp

🅒 Deletes the conversation turn entirely, freeing context space for future heartbeat turns

🅓 Scans for HEARTBEAT_OK token → strips it → checks if REMAINING content is ≤ 300 chars (ackMaxChars) → if yes, SILENTLY DROPS the entire message — nothing reaches your phone. When agent has something to report, it OMITS the token → gateway delivers as alert

---

**Q14.** Quiet hours must be enforced at TWO levels. What is the critical reason BOTH are required?


🅐 Level 1 handles customer-facing channels; Level 2 handles internal channels — different compliance rules per channel type require separate enforcement

🅑 Level 1 is temporary (cleared by /reset); Level 2 persists across restarts — using only prompt-level creates a security gap after every reset

🅒 Level 1 uses user's timezone from MEMORY.md; Level 2 uses server's system clock — timezone mismatches require both to agree before sending

🅓 Level 1 (prompt — HEARTBEAT.md instructions) depends on the MODEL OBEYING — it might not. Level 2 (infrastructure — activeHours config) prevents heartbeats at the GATEWAY level regardless of model behavior. 'Defense in depth: the model might ignore prompt instructions, but it cannot override the config'

---

**Q15.** Which TTS provider is recommended for first setup, what makes it uniquely accessible, and what audio format do ALL FOUR providers produce?


🅐 OpenAI TTS — already in most users' free tier via existing API keys. All four produce MP3 which WhatsApp auto-converts to voice note format

🅑 ElevenLabs — free tier provides 10,000 chars/month, enough for several testing days. All four produce WAV which the gateway transcodes to OGG

🅒 MiniMax — only provider with a WhatsApp-specific endpoint. The other three produce generic audio that loses quality during re-encoding

🅓 Microsoft Edge TTS — NO API key, NO signup, completely FREE (uses the Edge browser Read Aloud backend). All four produce Opus-encoded OGG at 48kHz, 64kbps — WhatsApp's native push-to-talk format, so replies appear as playable voice notes, not file attachments

---

**Q16.** Which TTS mode is recommended for PRODUCTION and why is 'always' explicitly NOT a production setting?


🅐 'tagged' is recommended — best UX because the agent chooses per-message. 'always' fails because it sends audio even during quiet hours

🅑 'off' is recommended for most deployments — voice notes consume 3x more tokens. 'always' violates regulatory text-based audit trail requirements

🅒 'always' with 1,500-char limit IS recommended — the limit auto-skips short confirmations. The book specifically recommends 'always' for reliable cross-model voice output

🅓 'inbound' is the recommended production mode — matches customer's modality automatically (text→text, voice→voice), no SOUL.md config needed. 'always' degrades UX: 'Done.' becomes a voice note, reference numbers can't be copied from audio, links can't be clicked when spoken

---

**Q17.** The book identifies a specific technical issue with 'tagged' mode. What is the issue and what is the reliable production alternative?


🅐 'tagged' mode doubles token cost because the model must reason about modality for every message. Alternative: 'inbound' offloads the decision to the gateway

🅑 'tagged' mode only works with OpenAI TTS and ElevenLabs — Microsoft Edge TTS doesn't support tag-based activation. Alternative: 'inbound' works with all providers

🅒 'tagged' mode is incompatible with HEARTBEAT.md delivery — [[tts]] tags are ignored in heartbeat alerts. Alternative: dedicated cron jobs for voice alerts

🅓 The [[tts]] markers sometimes appear as LITERAL TEXT in chat rather than triggering synthesis — a rendering/interception bug where the model outputs the tag but the gateway doesn't always process it. Reliable production alternative: 'inbound' — handles modality at the gateway level, no marker insertion needed

---

**Q18.** The Modality Design Principle: what are the TWO content types that MOST strongly require TEXT (not voice)?


🅐 Long-form explanations and detailed summaries — content over 500 words loses coherence when listened to and requires re-reading

🅑 Technical instructions and code samples — code cannot be meaningfully conveyed via audio and must be displayed for implementation

🅒 Questions and clarifying prompts — users can't review the question while composing a typed response to audio

🅓 Reference numbers and LINKS — reference numbers cannot be copied from audio, and links cannot be clicked when spoken. 'Anything containing numbers or links the user might need to copy' — the fundamental problem is irreversibility: once spoken, users cannot interact with the content

---

**Q19.** The book introduces three memory engine options. What are the THREE engines, what does each ADD, and when should you upgrade?


🅐 SQLite (default), PostgreSQL (multi-user concurrent access for teams), Redis (in-memory cache for low-latency high-frequency queries)

🅑 SQLite (default), Pinecone (cloud vector DB for 10,000+ entries), LangChain Memory (compatibility with ChromaDB, Weaviate)

🅒 SQLite (default), Elasticsearch (full-text search with facets), GraphQL Memory (structured relational memory queries)

🅓 SQLite with vector + keyword search (built-in default, handles personal setups), QMD (local sidecar — adds RERANKING + indexes ENTIRE PROJECT DIRECTORIES beyond workspace), Honcho (AI-native — BUILDS USER PROFILES AUTOMATICALLY from conversations + works across MULTIPLE AGENTS)

---

**Q20.** James explains why he chose MCP over a skill or plugin for the timezone tool. What was his reasoning and what principle does it illustrate?


🅐 Timezone data changes frequently (DST, political changes) — a SKILL.md would need constant updates; live connection prevents staleness

🅑 Timezone queries are high-frequency — MCP caches responses while a skill triggers a full LLM call each time; efficiency is the principle

🅒 Timezone conversion involves math that LLMs hallucinate — a dedicated computational tool provides numerical precision; reliability is the principle

🅓 'The agent already KNOWS about timezones — it doesn't need more knowledge. It needs ACCESS to something that checks a live clock.' His analogy: 'We didn't rewrite the shipping dashboard. We connected an external service.' Principle: apply the escalation path — knowledge = skill, external access = MCP

---

