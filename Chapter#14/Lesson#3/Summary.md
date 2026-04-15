
## 📘 Chapter 14 — Lesson 3 of 4
### Section C: Hooks, Plugins, Ralph Wiggum Loop, Agent Teams + Section D: Claude Cowork

---

### 🔷 PART A: Hooks — Event-Driven Automation

---

#### 1. What Are Hooks?

Hooks are **event-driven automation** triggers that fire at specific points in Claude Code's workflow. They allow you to run custom commands automatically when things happen — without manually intervening.

**Five Hook Event Types:**

| Hook | When It Fires | Use Case |
|---|---|---|
| **PreToolUse** | Before Claude runs any tool | Validate or block an action before it happens |
| **PostToolUse** | After Claude completes a tool | Auto-format, lint, or log after file changes |
| **SessionStart** | When a new session begins | Load environment, check prerequisites |
| **Stop** | When Claude is about to exit/finish | Used by Ralph Wiggum Loop to intercept and continue |
| **TeammateIdle** | When an Agent Team member has no tasks | Assign more work to idle teammates |
| **TaskCompleted** | When a teammate marks a task done | Quality gate before accepting completion |

**Hook exit codes:**
- `exit 0` → Allow the action to proceed normally
- `exit 2` → Send feedback to Claude and block/continue the action

---

### 🔷 PART B: Plugins — Discover and Install

---

#### 2. What Is a Plugin?

A **plugin bundles multiple Claude Code components into one installable package**:

| Component | What It Provides |
|---|---|
| **Skills** | Autonomous capabilities Claude discovers and uses |
| **Commands** | Slash commands (e.g., `/commit-commands:commit`) |
| **Agents** | Specialized subagents for focused tasks |
| **Hooks** | Event automation (format on save, validate on edit) |
| **MCP servers** | External integrations (GitHub, Slack, etc.) |

> Think of plugins as **complete capability packages** — instead of manually setting up skills, hooks, agents, and MCP servers separately, you install one plugin and everything works together.

---

#### 3. Plugin Marketplace — Key Commands

| Command | What It Does |
|---|---|
| `/plugin` | Opens Plugin Manager (Discover, Installed, Marketplaces, Errors tabs) |
| `/plugin install <name>@<marketplace>` | Install a specific plugin directly |
| `/plugin disable <name>@<marketplace>` | Disable without uninstalling |
| `/plugin enable <name>@<marketplace>` | Re-enable a disabled plugin |
| `claude plugin update <name>@<marketplace>` | Update a specific plugin |
| `claude plugin validate ./path-to-plugin` | Validate plugin structure before distributing |
| `/plugin uninstall <name>@<marketplace>` | Completely remove a plugin |
| `/reload-plugins` | Pick up newly installed plugins without restarting |

**Official marketplace:** Anthropic maintains the official plugins repository at `anthropics/claude-plugins-official`.

---

#### 4. Official Marketplace Categories

| Category | Example Plugins | What They Do |
|---|---|---|
| **Code intelligence** | `typescript-lsp`, `pyright-lsp`, `rust-analyzer-lsp`, `gopls-lsp` | Jump to definitions, find references, see type errors (uses Language Server Protocol) |
| **External integrations** | `github`, `gitlab`, `slack`, `linear`, `notion`, `figma` | Connect Claude to services you already use |
| **Development workflows** | `commit-commands`, `pr-review-toolkit`, `plugin-dev` | Git workflows, PR reviews, plugin creation |
| **Output styles** | `explanatory-output-style`, `learning-output-style` | Customize how Claude responds |

> **LSP plugins require the language server binary installed on your system.** For example, `typescript-lsp` requires `typescript-language-server`.

---

#### 5. Plugin Installation Scopes

| Scope | Who Uses It | Where Stored |
|---|---|---|
| **User** | Just you, all projects | `~/.claude/` |
| **Project** | Everyone on this repo | `.claude/settings.json` |
| **Local** | Just you, this repo only | Local settings |

**Recommendation:** Start with User scope for personal tools, Project scope for team standards.

---

#### 6. Plugin Directory Structure

```
my-plugin/
├── .claude-plugin/
│   └── plugin.json          ← Required manifest (4 fields minimum)
├── skills/                  ← Your SKILL.md files
├── agents/                  ← Your subagent definitions
├── hooks/
│   └── hooks.json           ← Hook configurations
├── .mcp.json                ← MCP server configs
└── README.md
```

**Minimum plugin.json manifest:**
```json
{
  "name": "my-skills",
  "description": "My Claude Code skills collection",
  "version": "1.0.0",
  "author": { "name": "Your Name" }
}
```

> ⚠️ Components go at the **root level**, not inside `.claude-plugin/`. The `.claude-plugin/` folder only contains the manifest.

**Plugin vs Marketplace:**

| Concept | What It Is | Analogy |
|---|---|---|
| **Plugin** | A folder with skills, agents, hooks, MCP configs | An app |
| **Marketplace** | A catalog listing multiple plugins | An app store |

---

### 🔷 PART C: Ralph Wiggum Loop — Autonomous Iteration

---

#### 7. The Iteration Fatigue Problem

Without Ralph Loop, you become a **manual feedback loop operator** — running commands, copying output, pasting back to Claude, waiting. This has three hidden costs:
1. Waiting time (idle while Claude processes)
2. Context switching (breaks your flow)
3. Error transcription (copying introduces mistakes)

**Rule of thumb: If you expect more than 10 iterations → Ralph Loop saves time**

| Scenario | Manual Cost | Automation Value |
|---|---|---|
| Simple bug fix (1–3 iterations) | Low (5–10 min) | Not worth it |
| Feature development (5–10 iterations) | Medium (30–60 min) | Maybe worth it |
| Framework upgrade (15–50 iterations) | High (2–4 hours) | Definitely worth it |
| Large refactor (20–100 iterations) | Very high (4–8 hours) | Critical |

---

#### 8. What Is Ralph Wiggum Loop?

**Definition:** A Claude Code plugin that enables **autonomous iteration** — Claude runs a task, checks the result, identifies what needs fixing, makes corrections, and repeats until a completion condition is met, **all without your intervention**.

**Named after:** The Simpsons character Ralph Wiggum — known for cheerful persistence despite mistakes. The plugin embodies "try, fail, learn, repeat."

**Real-World Origin:** Created by Geoffrey Huntley (summer 2025), formalized by Boris Cherny (Anthropic Head of Claude Code) in late 2025. Real production use: 14-hour autonomous upgrade sessions, React v16→v19 migrations.

**Why it's a plugin, not built-in:** Autonomous iteration carries cost and control risks — making it a plugin ensures users opt in deliberately.

---

#### 9. How It Works — The Stop Hook Architecture

**Normal Claude Code Flow:**
```
User: Task → Claude works → Claude finishes → SESSION STOPS (waiting for user)
```

**Ralph Loop Flow with Stop Hook:**
```
User: /ralph-loop task --max-iterations 20 --completion-promise "0 problems"
Claude works → Claude finishes → STOP HOOK INTERCEPTS
→ "Did you see '0 problems'? No? Continue."
→ Claude works again → Claude finishes → STOP HOOK CHECKS AGAIN
→ "Did you see '0 problems'? No? Continue."
→ Claude works → "0 problems. Done."
→ STOP HOOK SEES COMPLETION PROMISE → Allows Claude to stop ✓
```

**The four components:**

| Component | Purpose |
|---|---|
| **Stop Hook** | Intercepts Claude's exit to reinject continuation prompts |
| **Completion Promise** | Text that signals "we're done" (exact string match) |
| **Max Iterations** | Safety limit preventing infinite loops |
| **Loop Prompt** | Template asking Claude to verify results and continue |

---

#### 10. Critical Technical Detail — Completion Promise is STATIC ⭐

The `--completion-promise` is set **ONCE** and **cannot be changed during runtime.**

- ❌ Cannot add a completion promise after starting the loop
- ❌ Cannot modify it mid-loop
- ❌ Cannot have multiple conditions (no "DONE OR SUCCESS")
- ✅ Must get it right at the initial `/ralph-loop` command

> **Why `--max-iterations` is your primary safety net:** Since the completion promise uses fragile exact string matching and cannot be changed during runtime, always rely on `--max-iterations` as your main safety mechanism.

---

#### 11. Embedded Promise Pattern — Recommended Approach ⭐

Instead of relying on unpredictable tool output, embed the completion marker in the task description:

```bash
/ralph-loop "Fix all ESLint errors in the project:
- Run ESLint on all files
- Fix each error
- Re-run ESLint to verify
Output <promise>LINTING_COMPLETE</promise> when all errors resolved." \
--max-iterations 20 \
--completion-promise "LINTING_COMPLETE"
```

**Why this works better:**
- You control the exact completion signal
- Claude explicitly knows what to output when complete
- More reliable than depending on tool output format

---

#### 12. Good vs Poor Ralph Loop Use Cases ⭐

| Good Use Cases | Why |
|---|---|
| Framework upgrades (React v16→v19) | Build errors give clear feedback, completion is objective |
| Test-driven refactoring | Tests provide immediate verification |
| Linting/Type error resolution | Compiler output is deterministic |
| Deployment debugging | HTTP status provides clear success signal |

| Poor Use Cases | Why |
|---|---|
| Tasks requiring human judgment | Strategy, aesthetics, business priorities need human input |
| Exploratory research | No clear completion criteria |
| Creative work | Quality is subjective |
| Multi-goal tasks ("Fix bugs AND add features AND write docs") | No single completion signal |
| Tasks requiring external input (waiting for API keys) | Loop will stall |

> **The Golden Rule:** Ralph Loop excels when success is **objective, verifiable, and deterministic** — measurable by tools, not human judgment.

---

#### 13. Safety Rules — Cost Management

Real-world Ralph Loop costs:
- 14-hour upgrade session: ~$50–100 in API costs
- 30-iteration React migration: ~$30–40
- 80-iteration refactor: ~$80–150

**5 Cost Protection Rules:**
1. Always set `--max-iterations` (never run without a limit)
2. Start conservative — use lower limits first, increase if needed
3. Monitor spending — check Claude Code usage dashboard during long loops
4. Use incremental approach — break large tasks into smaller loops
5. Test on small scope first — run on one module before entire codebase

**When to cancel (`/cancel-ralph`):** Same error repeats 3+ times; Claude starts making unrelated changes; external dependency issue.

---

### 🔷 PART D: Agent Teams — Coordinating Multiple Claude Sessions

---

#### 14. Subagents vs Agent Teams — The Key Distinction ⭐

| | Subagents (Lesson 11) | Agent Teams |
|---|---|---|
| What they are | Fire-and-forget workers that report back to a single caller | Fully independent Claude Code instances that coordinate through a shared task list and direct messaging |
| Communication | One direction: report back to main agent | Bidirectional: teammates can message EACH OTHER directly |
| Context | Isolated per subagent | Each teammate has its own independent context window |
| Coordination | Via main agent orchestration | Self-coordinate via shared task list |

**The decision rule:** If teammates need to talk to each other, use teams. If they just report back, use subagents.

---

#### 15. Enabling Agent Teams

Agent Teams is an **experimental feature** requiring Claude Code v2.1.32 or later:

```json
{
  "env": {
    "CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1"
  }
}
```

**Two display modes:**
- **in-process** (default): all teammates run inside your main terminal; use Shift+Up/Down to select and message teammates
- **split panes**: each teammate gets its own pane; requires `tmux` or iTerm2; NOT supported in VS Code integrated terminal, Windows Terminal, or Ghostty

---

#### 16. How Agent Teams Work — Key Mechanics ⭐

**Navigation shortcuts:**
- `Ctrl+T` → View the shared task list
- `Shift+Up/Down` → Switch view between team lead and teammates
- `Shift+Tab` → Toggle Delegate Mode (ON/OFF)

**Task file structure** (stored in `~/.claude/tasks/*/`):
```json
{
  "id": "1",
  "subject": "Research market size and growth trends",
  "owner": "market-researcher",
  "status": "in_progress",
  "blocks": ["3"],        ← Tasks that wait for this one
  "blockedBy": []         ← Dependencies that must complete first
}
```

**The `blocks`/`blockedBy` dependency graph:** A task with unresolved `blockedBy` entries cannot be claimed until those dependencies complete — tasks unblock automatically.

---

#### 17. Team Control Methods

| Method | How | What It Does |
|---|---|---|
| **Delegate Mode** | Shift+Tab | Prevents lead from doing analysis directly — lead can ONLY coordinate, never execute analysis |
| **Plan Approval** | In task description | Teammate presents approach for review before billing time; you approve or reject with feedback |
| **Direct Messages** | Shift+Up/Down → type | Redirect a specific teammate mid-task without disturbing others |
| **Task Dependencies** | `blocks`/`blockedBy` in task files | Sequential workflows where each stage feeds the next |
| **Shared Documents** | Write to shared files | All teammates contribute to the same output file; lead synthesizes |

---

#### 18. Known Agent Team Limitations ⭐

| Limitation | What It Means |
|---|---|
| **No session resumption** | If a teammate crashes or session restarts, in-process teammates cannot be recovered — must recreate the team |
| **One team per session** | A Claude Code session supports a single active team at a time |
| **No nested teams** | A teammate cannot itself create sub-teams |
| **Lead is fixed** | The lead agent is set at team creation and cannot be changed mid-session |
| **Permissions set at spawn** | Each teammate inherits permission level when created; cannot escalate later |
| **Teammates don't inherit lead's history** | Must include critical context in spawn prompt OR ensure CLAUDE.md covers it |

---

#### 19. Three Agent Team Patterns ⭐

| Pattern | Use When | Example |
|---|---|---|
| **Parallel Investigation** | Multiple angles on same question simultaneously | Market researcher + Competitive analyst + Financial analyst all investigating the same opportunity |
| **Pipeline Build** | Sequential dependencies where each stage feeds the next | Market research → Positioning → Marketing plan → Financial projection |
| **Competing Hypotheses** | Root cause is unclear; prevents anchoring bias | Four teammates each investigating a different theory; the hypothesis that survives debate is most likely correct |

> **Why Competing Hypotheses works:** A single investigator finds one plausible explanation and stops looking. With independent investigators who can challenge each other, the surviving hypothesis is far more likely to be the real root cause.

---

#### 20. Agent Team Cost Consideration

Agent teams use more tokens than subagents because each teammate maintains its own full context window plus inter-agent messages. A 3-agent team might cost 3–5x what a single-agent session costs.

**Best practice:** Use the strongest model for the lead (synthesis), efficient models for teammates (research).

---

### 🔷 PART E: Claude Cowork — Practical Workflows

---

#### 21. What Cowork Can Actually Do — 4 Key Workflows

Cowork transforms knowledge work from hours of manual clicking to minutes of conversation:

| Workflow | Manual Time | Cowork Time | Speedup |
|---|---|---|---|
| **Downloads folder organization** | 2 hours (often never done) | 5 minutes | 24x faster, actually done |
| **Batch video conversion (50 files)** | 8 hours manual | 10 minutes | 48x faster |
| **Weekly finance report from CSV** | 2 hours every Monday | 5 minutes | 24x time savings |
| **Research synthesis (65 documents)** | 3+ days | 30 minutes | 144x faster |

---

#### 22. Cowork Workflow Patterns — 4 Universal Patterns

| Pattern | What It Means |
|---|---|
| **Explore First** | Claude begins by scanning/understanding what it's working with before acting |
| **Propose, Then Execute** | Claude shows you what it will do → you confirm → it proceeds (prevents mistakes) |
| **Handle Variation** | Real-world files are messy; Claude adapts its approach based on what it finds |
| **Report Results** | Claude provides transparency: files processed, changes made, errors encountered |

---

#### 23. Cowork Plugins & Connectors

**Cowork has 50+ connectors** for external services (Gmail, Drive, Slack, Notion, Figma, and more). In Cowork, MCP connections are called **Connectors** — same underlying protocol, more accessible interface for non-technical users.

**Built-in Document Skills — Cowork natively handles:**
- Word documents (`.docx`)
- Excel spreadsheets (`.xlsx`)
- PowerPoint presentations (`.pptx`)
- PDF files (`.pdf`)

These are the same document Skills from the AAIF standard — accessible through Cowork's GUI without any setup.

---

#### 24. Cowork Common Pitfalls

| Pitfall | Fix |
|---|---|
| **Vague instructions** | "Clean up folder" → "Organize files by type into: documents, images, archives, installers" |
| **Skipping approval review** | Always review what Claude proposes before execution, especially for deletions |
| **No backup strategy** | Before major operations, ensure important data is backed up first |
| **Overly complex initial requests** | Start simple and build complexity gradually |

