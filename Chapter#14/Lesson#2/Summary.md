
## 📘 Chapter 14 — Lesson 2 of 4
### Section B: Building Skills + Subagents & Orchestration + MCP Integration + Settings Hierarchy

---

### 🔷 PART A: Building Your Own Skills

---

#### 1. The SKILL.md File — Anatomy of Encoded Expertise

Every skill lives in a **folder**. The folder contains one required file: `SKILL.md`

```
.claude/skills/meeting-notes/
└── SKILL.md    ← This is what you create
```

**The Two Parts of SKILL.md:**

**Part 1 — YAML Frontmatter (The ID Card):**
```yaml
---
name: "meeting-notes"
description: "Transform meeting transcripts or raw notes into structured summaries 
with action items, decisions, and follow-ups. Use when user shares meeting content 
or asks for meeting notes."
---
```

**Part 2 — Markdown Body (The Instructions):**
Everything after the frontmatter — When to Use, Procedure, Output Format, Quality Criteria, Examples.

> 🔑 A skill can be a single markdown file. The simplicity is intentional — **anyone can create one**.

---

#### 2. The Description Field — Your Skill's Activation Trigger ⭐

The `description` in YAML frontmatter is **the most important line you write**. It determines when Claude activates your skill at startup (Level 1 of progressive disclosure).

**Description Quality Guide:**

| Type | Example | Problem |
|---|---|---|
| Too vague | `"Helps with notes"` | "Notes" could mean anything — Claude won't know when to activate |
| Too narrow | `"Summarizes Zoom meeting transcripts from the marketing team"` | Won't activate for Teams calls, non-marketing meetings, or live notes |
| **Good** | `"Transform meeting transcripts or raw notes into structured summaries with action items, decisions, and follow-ups. Use when user shares meeting content or asks for meeting notes."` | States WHAT, lists KEY OUTPUTS, specifies WHEN |

**The Description Formula:**
```
[Action verb] + [input type] + [into/for] + [output type] + [key features].
Use when [trigger conditions].
```

---

#### 3. Fast Way to Create Skills — The Skill-Creator Meta-Skill

Instead of writing SKILL.md manually, use Claude itself:

```
I want to create a skill for [your procedure]. Use the skill-creator to help me build it.
```

The `skill-creator` is a **meta-skill** — a skill that creates other skills. It guides you through understanding your procedure, writing effective descriptions, and generating a complete SKILL.md.

> This is how most people should create skills.

---

#### 4. 6-Section Standard SKILL.md Structure

| Section | What Goes In |
|---|---|
| **When to Use** | Bullet triggers — what user says or requests |
| **Procedure** | Numbered steps Claude follows |
| **Output Format** | How results should be structured |
| **Quality Criteria** | Standards and constraints (specific numbers over vague claims) |
| **Example** | Sample input → output showing the skill in action |

---

#### 5. The Co-Learning Cycle for Skill Refinement

Skills improve through iteration. The three-stage cycle:

| Stage | Role | What Happens |
|---|---|---|
| **AI as Teacher** | Claude reviews your draft | Suggests sections you missed, improvements you didn't think of |
| **You as Teacher** | You specify constraints Claude doesn't know | Team-specific patterns, company policies, style rules |
| **AI as Co-Worker** | You iterate together | Claude offers options, you select based on your real context |

> Skills are reusable IP — they can be shared, versioned in Git, integrated into Custom Agents (Part 6), monetized as vertical AI solutions, and are portable across tools (agentskills.io open standard).

---

### 🔷 PART B: Subagents and Orchestration

---

#### 6. What Is a Subagent?

A subagent is a **specialized AI Agent with its own instructions and isolated context window**. Each subagent is an expert at one type of task.

**The project manager analogy:**
- **Claude Code (main):** Coordinates overall work — the project manager
- **Plan subagent:** Researches codebase and creates multi-step plans — the strategist
- **Explore subagent:** Finds files, searches code, understands structure — the researcher
- **Custom subagents:** You create specialists for your team's specific needs

**View your team with:** `/agents`

---

#### 7. Built-In Agents — Know All Five!

| Agent | Best For | Model |
|---|---|---|
| **Explore** | Finding files, searching code, understanding codebase structure | Haiku (fast) |
| **Plan** | Complex multi-step tasks, creating implementation strategies | Sonnet (smart) |
| **general-purpose** | Multi-step tasks requiring various tools | Inherits current |
| **Bash** | Command execution tasks | Inherits current |
| **claude-code-guide** | Questions about Claude Code itself | Haiku |

---

#### 8. How Subagents Work — The Execution Model

**Critical concept:** A subagent is invoked **ONCE** for a specific goal, completes its work, and **returns results to main Claude Code**.

```
You → Main Claude Code → Launches Subagent → Subagent works
                                               (isolated context)
                               ↓
                    Subagent completes → Returns results
                               ↓
              Control returns to Main Claude Code → You
```

**Two ways to invoke subagents:**

| Method | How |
|---|---|
| **Automatic** | Claude Code decides when to delegate based on task complexity and request type |
| **Explicit** | Type "Use the Plan subagent to..." or type `@` and pick from typeahead menu |

> `@-mention` invocation **guarantees** that specific subagent runs — unlike automatic delegation which may not trigger.

---

#### 9. Parallel Power — Multiple Agents at Once

You can invoke **multiple subagents in a single prompt**:

```
Use Explore to find all test files in this project, AND use Plan to suggest 
a testing strategy for the gaps you find.
```

Both subagents launch simultaneously, work in isolated contexts, and results combine into a single response. This is **orchestration** — coordinating multiple specialists toward a goal.

---

#### 10. Why Isolated Context Windows Matter

**Without subagents (one AI doing everything):**
- Research fills context with notes → later tasks get contaminated by earlier research → Claude confuses research notes with your pitch

**With subagents:**
- Research subagent returns clean summary → Main Claude context stays clean → Planning subagent works with fresh focus

> Like a team meeting: the researcher presents findings, then leaves. The strategist creates a plan with fresh focus. Nobody juggles everything at once.

---

#### 11. Custom Subagent File Structure

Subagents live at:
- **Project-level:** `.claude/agents/` (this project only)
- **User-level:** `~/.claude/agents/` (all your projects)

Example agent file (`.claude/agents/code-reviewer.md`):
```markdown
---
name: code-reviewer
description: Reviews code for bugs and suggests improvements
model: sonnet
---

# Code Review Instructions
1. Check for bugs and edge cases
2. Suggest performance improvements
3. Note any security concerns
4. Recommend cleaner patterns
```

**Model field options:** `sonnet`, `opus`, `haiku`, full model ID (e.g., `claude-sonnet-4-6`), or `inherit` (uses whatever model the main conversation uses). When omitted, subagents inherit current model by default.

---

#### 12. Skills vs Subagents — Decision Framework ⭐ (Exam favourite!)

| Factor | Choose Skill | Choose Subagent |
|---|---|---|
| **Invocation** | Automatic OR explicit by name | Explicit only (you invoke) |
| **Context** | Shared with main conversation | Isolated context window |
| **Complexity** | Lightweight, single-focus | Multi-step, complex workflows |
| **Guarantee** | Flexible (auto-triggers or invoke by name) | Hard invocation (always runs) |
| **Best for** | Repeated patterns, formatting, procedures | Audits, refactoring, comprehensive analysis |

**Simple rule:**
- Use skill when: "I want Claude to automatically do this whenever it's relevant"
- Use subagent when: "I need guaranteed execution with isolated context for this complex task"

**Examples:**
- Meeting notes formatting → **Skill** (happens often, simple, automatic)
- Comprehensive security audit → **Subagent** (complex, needs isolation, guaranteed execution)

---

### 🔷 PART C: MCP Integration

---

#### 13. The Core Mental Model — MCP as Phone Directory

**Without MCP:** Claude Code can only see files on your computer. It's a brilliant assistant confined to your office.

**With MCP:** You give Claude a **phone directory** of approved external contacts — a web browser expert, a documentation specialist, a database consultant. Claude can call the right expert safely when needed.

> "MCP is that phone directory — connecting Claude Code to external tools and data sources in a standardized, safe way."

---

#### 14. Skills + MCP = Expertise + Connectivity ⭐

| Component | Role | Analogy |
|---|---|---|
| **Skills** | The "How-To" — expertise packs | Teaching Claude a specific workflow |
| **MCP** | The "With-What" — data pipes | Connecting skills to live data |

**Without MCP:** Agent knows HOW but can't reach the data.
**Without Skills:** Agent can reach data but doesn't know your reporting standards.
**With both:** Queries database (MCP) + analyzes using your procedures (Skill) + produces reports matching your standards.

---

#### 15. What MCP Unlocks — Before/After Table

| Task | Without MCP | With MCP |
|---|---|---|
| Browse Amazon | Can't — you do the shopping | Playwright MCP: Claude navigates, extracts prices/reviews, summarizes |
| Check latest docs | Uses training data (outdated, may hallucinate) | Context7 MCP: Fetches current docs, real examples, live citations |
| Query production database | Can't — you run queries, paste results | Database MCP: Claude executes queries safely, analyzes results |
| Post to Slack | Can't — you copy-paste manually | Slack MCP: Claude sends messages, threads, reactions automatically |
| Analyze GitHub repo | Can't — you clone locally | GitHub MCP: Claude clones, analyzes, answers questions about code |

---

#### 16. MCP Tool Search — Context Efficiency ⭐

**The problem:** Each MCP server has tool definitions that consume context tokens:
- Playwright MCP: ~5,000–8,000 tokens
- Context7 MCP: ~3,000–5,000 tokens
- GitHub MCP: ~8,000–12,000 tokens
- **5 servers = 25,000–40,000 tokens before you ask a single question**

**The solution (since January 2026, Claude Code 2.1.7+):** MCP Tool Search — automatic lazy loading.

| Setting | Behaviour |
|---|---|
| `ENABLE_TOOL_SEARCH=auto` | Activates when MCP tools exceed 10% of context (default) |
| `ENABLE_TOOL_SEARCH=auto:5` | Activates at 5% threshold |
| `ENABLE_TOOL_SEARCH=true` | Always on |
| `ENABLE_TOOL_SEARCH=false` | Legacy — loads all tools upfront |

**Result: ~85% automatic reduction in MCP overhead**. Most users don't need to configure this — it works automatically.

---

#### 17. When NOT to Use MCP — 4 Guardrails

| Don't Use MCP For | Why | Better Approach |
|---|---|---|
| **Private/sensitive data** (company financials, SSH credentials) | Security risk — MCP connects to internet | Use local file access or environment variables |
| **High-frequency queries** (1000+ queries/second) | MCP adds latency per call (network + Claude reasoning) | Use direct database connections |
| **Untrusted MCP servers** | Malicious server could read your files, access your tokens | Only use servers from Anthropic official list, modelcontextprotocol.io, verified npm packages |
| **Before understanding basics** | Security model must be understood first | Master Playwright and Context7 first; build custom MCPs in Part 7 |

---

#### 18. The Three Pillars of AI-Native Development ⭐

This is the book's synthesis of Sections A and B:

```
CLAUDE.md  → Claude knows YOUR PROJECT  (context)
   ↓
Skills     → Claude knows YOUR PROCEDURES  (expertise)
   ↓
MCP        → Claude knows THE WORLD'S TOOLS  (reach)
   ↓
Result: A Digital FTE that understands your goals, knows how you work, 
and can access any external system safely
```

> "Without CLAUDE.md, Claude is generic. Without Skills, Claude repeats itself. Without MCP, Claude is blind to the outside world. With all three, Claude becomes truly autonomous."

> **Context + Procedures + Access = Digital FTE**

---

### 🔷 PART D: Settings Hierarchy

---

#### 19. Three Settings Levels — Know All Three!

| Level | File Location | Scope | When to Use |
|---|---|---|---|
| **User (Most General)** | `~/.claude/settings.json` | ALL your projects on this machine | Personal preferences, coding style, workflow defaults |
| **Project (Middle)** | `.claude/settings.json` (inside project) | Just this project | Team standards, project-specific customizations |
| **Local (Most Specific)** | `.claude/settings.local.json` (inside project) | This project on your machine only (NOT shared with team) | Temporary overrides, personal experiments, machine-specific |

**Precedence rule (most specific wins):**
```
Local > Project > User
```

> Full enterprise chain: **Managed > CLI args > Local > Project > User**
> (Managed = deployed by IT teams, cannot be overridden)

**Which files go in `.gitignore`?**
- `.claude/settings.json` → **Commit to Git** (share with team)
- `.claude/settings.local.json` → **Add to .gitignore** (keep personal)

---

#### 20. Permission Modes — From Manual to Autonomous ⭐

| Mode | What Happens | Best For |
|---|---|---|
| **default** | Claude asks permission before EVERY tool use | Learning, sensitive projects, exploring new codebase |
| **acceptEdits** | Claude reads and edits files freely; still asks for Bash commands | Active daily development |
| **auto** | Safety classifier screens each action; safe = proceeds, risky = blocked | Long-running tasks, multi-hour refactoring (released March 2026) |
| **bypassPermissions** | Claude runs everything without asking | CI/CD pipelines, containers (no human present) |

- Toggle between modes during session: **Shift+Tab**
- Enable auto mode: `claude --enable-auto-mode` or Settings > Claude Code

**Auto Mode (March 2026):**
- Safe actions (reading files, running tests, editing code) → proceed automatically
- Risky actions (mass file deletion, accessing credentials, destructive commands) → blocked
- Works with both Sonnet 4.6 and Opus 4.6

---

#### 21. Quick Reference — Key Commands

| Command | What It Does |
|---|---|
| `/agents` | View all available subagents; create new ones |
| `/config` | Opens interactive settings menu (no manual JSON editing) |
| `/memory` | Shows which CLAUDE.md files are loaded; browse Auto Memory |
| `claude mcp add --transport stdio <name> <command>` | Add an MCP server |
| `claude mcp list` | See all installed MCP servers |
| `Shift+Tab` | Cycle between permission modes |

---

