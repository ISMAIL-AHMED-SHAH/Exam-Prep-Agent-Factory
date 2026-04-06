

## 📘 Chapter 14 — Lesson 1 of 4
### Section A: Claude Code Essentials + Section B intro: Skills Concept

---

### 🔷 1. The Claude Code Origin Story — What Actually Happened

**September 2024:** Engineer **Boris Cherny** joined Anthropic and ran an experiment — he gave Claude something it had never had before: **direct access to the filesystem**.

What happened next surprised everyone. When Claude could read files, it didn't just answer better — it *explored*. It naturally read files, followed imports, and understood project structure **without being told to**. The behavior emerged on its own.

This revealed the **"Product Overhang"** — the capability to be a genuine development partner already existed inside Claude. It wasn't waiting for a smarter model. It was waiting for a product that let it actually **see** what developers were working on.

**Dogfooding results (internal launch Nov 2024):**
- **20% adoption on Day 1; 50% by Day 5; 80%+ daily use by May 2025**
- Engineers averaged **5 pull requests/day** (vs 1–2 at typical companies)
- PR throughput jumped **67%** even as the team grew from 2 to 10 people
- Revenue: **$500M+ annual run rate by mid-2025** — almost entirely from word of mouth. **$1B by November 2025**

> 🔑 Key stat: Approximately **90% of Claude Code was written by Claude Code itself** — not because AI became suddenly brilliant, but because filesystem access gave it the context it needed.

---

### 🔷 2. Passive AI vs Agentic AI — The Core Paradigm Shift

| | Passive AI (ChatGPT-style) | Agentic AI (Claude Code) |
|---|---|---|
| How it works | You describe code → AI suggests → You copy-paste → You adapt → You test | AI reads your actual files → proposes specific changes → executes with your approval → runs tests → iterates |
| Analogy | Consultant on the phone — doesn't see your screen | Pair programmer looking directly at your code |
| Memory | Zero — starts fresh every session | Reads filesystem as persistent external memory |
| Verification | Cannot verify its suggestions | Tests its own work, sees errors, fixes mistakes |
| Output | Single response | Loops via OODA until goal is achieved |

**The OODA Loop in Claude Code:**

| Step | What Claude Does |
|---|---|
| **Observe** | Reads the error, scans your files, gathers context |
| **Orient** | Identifies root cause within YOUR stack and patterns |
| **Decide** | Chooses where to look and what approach to take |
| **Act** | Reads files, runs commands, writes code |
| **↩️ Loop** | Corrects if the fix didn't work; repeats until solved |

---

### 🔷 3. The Second Product Overhang — Cowork

Claude Code proved filesystem access unlocks extraordinary capability. But there was a barrier: the **terminal**.

- For developers: terminal is home
- For everyone else: **terminal is a wall**

Anthropic discovered non-technical users who struggled through terminal setup still used Claude Code for organizing files, processing documents, and automating research. So in **January 2026**, Anthropic launched **Cowork** — the same agent architecture and filesystem access paradigm, wrapped in the familiar Claude Desktop interface.

| Aspect | Claude Code | Cowork |
|---|---|---|
| Interface | Terminal / CLI | Desktop App (GUI) |
| Target User | Developers | Knowledge Workers |
| Best For | Building software | Documents, data, organization |
| Foundation | Claude Agent SDK | Claude Agent SDK (same!) |
| Core Capability | Filesystem access + agentic execution | Filesystem access + agentic execution (same!) |

> Both run on the **same Claude Agent SDK**. The only difference is the interface layer.

---

### 🔷 4. The Eight Claude Modes — Know This Map!

Claude in 2026 is not a single tool — it is **8 integrated modes**:

| Mode | What It Does | Where Covered |
|---|---|---|
| **Chat** | Conversational Q&A — where most people start and stay | Prerequisite |
| **Cowork** | AI coworker that works on your actual files on your machine | Section D |
| **Projects** | Save prompts, files, and context in persistent workspace | Chapter 15 |
| **Artifacts** | Interactive apps, dashboards, tools built inside chat | Part 2 |
| **Excel** | Claude inside spreadsheets — reads data, writes formulas, builds charts | Part 3 |
| **Connectors** | Link Claude to Gmail, Drive, Slack, Notion, Figma, 50+ more | Section B (MCP) |
| **Plugins** | Pre-built agent packs for roles — sales, marketing, legal, finance | Section C + Part 3 |
| **Skills** | Reusable task templates giving Claude specialist knowledge | Section B |

> Most people only ever use Chat. This book teaches you to build Digital FTEs using **Cowork, Skills, Plugins, and Connectors**.

---

### 🔷 5. CLAUDE.md — The Persistent Context File

**The problem:** Every Claude Code session starts with **zero context**. LLMs are stateless — they remember nothing between sessions. You'd have to re-explain your entire tech stack, project structure, and coding conventions every time.

**The solution:** `CLAUDE.md` — a Markdown file placed in your project root that Claude Code **automatically loads at the start of EVERY session**.

> Think of it as a **persistent project brief** that travels with your code.

**How context actually works behind the scenes:**

```
You → Claude Code (CLI tool) → AI Model (stateless LLM) → Response back to you
```

The AI model has NO memory between calls. What makes conversations feel continuous:
- Claude Code re-sends the entire conversation history with every new message
- Claude Code treats your **filesystem as external memory**
- `CLAUDE.md` is the orientation guide Claude reads first in every session

```
Stateless LLM + Filesystem Access = Persistent state through your actual files
```

**How to create CLAUDE.md:**
- Use the `/init` command — Claude analyzes your codebase and auto-generates it
- Or ask Claude conversationally to generate it based on what it reads

**6 standard sections in CLAUDE.md:**

| Section | What Goes In |
|---|---|
| **Project Overview** | What does the project do? What problem does it solve? |
| **Technology Stack** | Languages, frameworks, databases, key dependencies |
| **Directory Structure** | Show the layout — where code, tests, migrations live |
| **Coding Conventions** | Style, naming, patterns your team follows |
| **Key Commands** | Run, test, deploy commands |
| **Important Notes** | Gotchas, security considerations, critical constraints |

**Key rules:**
- File must be named exactly `CLAUDE.md` (case-sensitive)
- Must be in project root (same level as `.git`, `package.json`, etc.)
- Keep **under 200 lines** — concise instructions get better adherence
- For larger context, split using `@path/to/file` imports

---

### 🔷 6. Auto Memory — Claude's Own Notes

| System | Who Writes It | Purpose |
|---|---|---|
| **CLAUDE.md** | You | Your instructions, standards, and context for Claude |
| **Auto memory** | Claude | Claude's own notes about what it learned while working |

- Auto memory is **enabled by default**
- Claude saves learnings (build commands, debugging insights, patterns) to `~/.claude/projects/<project>/memory/`
- First 200 lines of memory files load into every session automatically
- You can view with `/memory` command inside Claude Code

---

### 🔷 7. CLAUDE.md vs AGENTS.md — Know the Difference!

| | **CLAUDE.md** | **AGENTS.md** |
|---|---|---|
| Created by | OpenAI → donated to AAIF | Anthropic |
| Scope | **Universal** — works with ALL AI coding agents | **Claude Code specific** — rich Claude features |
| Works with | Claude Code, Cursor, GitHub Copilot, Gemini CLI, Devin, goose, etc. | Claude Code only |
| Adopted by | 60,000+ open-source projects (since Aug 2025) | Your Claude Code projects |

**Best practice — use BOTH:**
```
your-project/
├── CLAUDE.md     ← Rich context for Claude Code (primary tool)
├── AGENTS.md     ← Universal context for ANY AI agent
├── src/
└── ...
```

In your `CLAUDE.md`, simply reference `@AGENTS.md` for shared universal context, then add Claude-specific instructions (Skills, hooks, subagents) separately.

**What goes where:**

| Content | AGENTS.md | CLAUDE.md |
|---|---|---|
| Project overview, tech stack, directory structure | ✅ | Reference @AGENTS.md |
| Coding conventions, key commands | ✅ | Reference @AGENTS.md |
| Claude-specific Skills | ❌ | ✅ |
| MCP server configs, subagent definitions | ❌ | ✅ |
| Hooks configuration | ❌ | ✅ |

---

### 🔷 8. The Three Roles Framework — Applied to CLAUDE.md

Both you AND Claude play three roles when building context together:

| Stage | Role | What Happens |
|---|---|---|
| **Stage 1** | You start | Write a basic draft CLAUDE.md |
| **Stage 2** | AI as Teacher | Claude reviews your draft and tells you what critical sections are missing |
| **Stage 3** | AI as Student | You teach Claude your team's specific constraints (custom auth patterns, company policies, etc.) |
| **Stage 4** | AI as Co-Worker | You iterate together — Claude offers options, you select based on your team's context |

> Result: A CLAUDE.md that's better than either could produce alone.

---

### 🔷 9. The Concept Behind Agent Skills — "Stop Building Agents. Build Skills Instead."

This is the key philosophical shift from **Section B**. Anthropic's conclusion after building Claude Code:

**The equation:**
- **Intelligence** (Claude reasons, analyzes, generates) + **Code** (execution — call APIs, run Python, write files) = **Execution**
- But Intelligence + Code ≠ **Expertise**

> "Agents today have intelligence and capabilities, but not always the expertise needed for real work."

The solution: **Agent Skills** — domain-specific knowledge packages that fill the expertise gap.

**The tax professional analogy (exam favourite!):**
- Who do you want doing your taxes? The 300-IQ mathematical genius who figures it out from first principles? Or the experienced tax professional who knows the patterns, edge cases, and specific procedures?
- **You want the professional** — not because they're smarter, but because they have encoded expertise.
- This is exactly the gap Skills fill. Not more intelligence. Not more execution. Expertise.

---

### 🔷 10. Skills Architecture — How They Work

**Skills = Folders** (intentionally simple)

```
.claude/skills/
├── meeting-notes/          ← Each skill is a folder
│   ├── SKILL.md            ← Main instructions (loaded on-demand)
│   └── templates/          ← Supporting files (loaded if needed)
│       └── standup.md
├── code-review/
│   ├── SKILL.md
│   └── checklist.md
└── blog-planner/
    └── SKILL.md
```

**Three-level progressive disclosure (prevents context overload):**

| Level | What Loads | When | Tokens |
|---|---|---|---|
| **Level 1** | Name + short description | Always (at startup) | ~100 tokens per skill |
| **Level 2** | Full SKILL.md instructions | When Claude decides skill is relevant | < 5K tokens |
| **Level 3** | Supporting files, scripts, docs | Only when executing the skill | On demand |

> Like a smartphone — 100 apps installed but only the ones you tap actually run. Skills stay dormant until needed → enables hundreds of skills without overwhelming context.

---

### 🔷 11. Three Sources of Skills

| Source | Description | Examples |
|---|---|---|
| **Bundled** | Built into Claude Code — available immediately | `/batch`, `/debug`, `/loop`, `/simplify`, `/claude-api` |
| **Foundational** | Basic capabilities that extend what Claude can do | Create Word docs, PowerPoint, Excel, PDFs |
| **Partner Skills** | Help Claude work with specific software/services | Browserbase (browser automation), Notion (workspace research) |
| **Enterprise/Custom** | Created by organizations for their specific needs | Company coding style, internal documentation standards, org-specific workflows |

**Key bundled slash commands to know:**

| Command | What It Does |
|---|---|
| `/init` | Generates CLAUDE.md by analyzing your codebase |
| `/batch <instruction>` | Orchestrates large-scale changes across codebase in parallel |
| `/debug [description]` | Troubleshoots current session by reading the debug log |
| `/loop [interval] <prompt>` | Runs a prompt repeatedly on an interval |
| `/simplify [focus]` | Reviews recently changed files for quality issues |
| `/memory` | Shows which CLAUDE.md files are loaded; lets you browse memory |

---

### 🔷 12. Skills Are Universal — Not Just for Coding

Skills work for ANY domain because code is the **universal interface to the digital world**:

| Domain | Example Skills |
|---|---|
| Finance | Quarterly report formatting, audit procedures, compliance checklists |
| Legal | Contract review workflow, clause analysis, due diligence procedures |
| Marketing | Brand voice guidelines, campaign brief templates |
| Healthcare | Clinical documentation standards, patient communication templates |
| Recruiting | Candidate evaluation criteria, interview question frameworks |
| Education | Lesson plan structure, assessment rubrics |

> You don't need to be a programmer to create or use skills. You need **domain expertise** and the willingness to document your procedures clearly.

---

### 🔷 13. Skills as Strategic Assets — The 4 Key Properties

| Property | Manual Prompting | Agent Skills |
|---|---|---|
| Reliability | Ad-hoc, best effort | Deterministic, script-backed |
| Token Cost | Pay for "rules" in every conversation | Load rules only when triggered |
| Asset Type | Disposable conversation | **Reusable, scalable IP** |
| Integration | Requires human copy-paste | **API-ready via Agent SDKs** |

**Skills can be:**
- **Shared** with your team (everyone benefits)
- **Versioned** in Git (track improvements)
- **Integrated** into Custom Agents (Part 6)
- **Monetized** as part of vertical AI solutions
- **Portable** — follow the open Agent Skills standard at agentskills.io; work across Claude Code, OpenAI Codex, goose, and other compatible tools

---

### 🔷 14. The Stack Analogy (Exam Favourite!)

| Layer | Computing | AI Equivalent |
|---|---|---|
| **Processor** | Requires massive investment; immense potential | Foundation Models (Claude, GPT, Gemini) |
| **Operating System** | Made processors valuable by orchestrating processes | Agent Runtimes (Claude Code) |
| **Applications** | Millions of developers encode domain expertise here | **Agent Skills** ← This is where YOU create value |

> "A few companies build processors and operating systems. But millions of developers build software that encodes domain expertise. **This is the layer that opens for everyone.**"

---

### 🔷 15. Code vs Cowork — Decision Framework

**Simple rule: Code for code. Cowork for documents.**

| Use Claude Code when... | Use Claude Cowork when... |
|---|---|
| Writing software code | Working with documents |
| Running tests or builds | Organizing files and folders |
| Using version control (git) | Processing spreadsheets |
| Debugging or profiling | Creating presentations |
| Managing dependencies | Analyzing PDFs and reports |
| Comfortable with terminals | Prefer visual interfaces |

**Skills work across BOTH interfaces** — if you create a skill for "financial report analysis," you can use it in Claude Code when processing data programmatically AND in Cowork when generating reports from spreadsheets.

**The Convergence Path:** Claude Code now runs in VS Code, JetBrains, a standalone desktop app, a web browser, and iOS. The boundary between "Code" (terminal) and "Cowork" (desktop) is blurring. Focus on agentic reasoning patterns and skill design — these transfer across all surfaces.

