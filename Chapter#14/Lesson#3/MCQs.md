
**📚 Ch.14 Lesson 3 — Hooks, Plugins, Ralph Wiggum Loop, Agent Teams & Cowork**
*Exam L1: P2-GAF1 Prep | 20 Questions | Answers shuffled!*

---

**Q1.** The 'Stop' hook is described as architecturally unique. What makes it special and what is it primarily used for?


🅐 Fires when Claude encounters an error it cannot recover from, allowing custom error-handling scripts to run

🅑 Fires at the end of every tool execution — distinct from PostToolUse because it waits for all parallel tools to complete

🅒 Fires when a user manually presses Ctrl+C, allowing graceful cleanup of partial changes

🅓 Fires when Claude is about to EXIT — it intercepts Claude's normal exit behavior and is the core mechanism behind Ralph Wiggum Loop, reinjecting continuation prompts so Claude keeps working instead of stopping

---

**Q2.** What is the SPECIFIC behavior difference between hook exit code 0 and exit code 2?


🅐 Exit 0 = success, log and proceed; Exit 2 = warning, log and proceed but flag for review; Exit 1 = error, abort and restore

🅑 Exit 0 = approve with no feedback; Exit 2 = approve but display stdout as informational notification

🅒 Exit 0 = hook ran successfully without changes; Exit 2 = hook modified a file, Claude Code should reload it into context

🅓 Exit 0 = allow normal behavior (action proceeds, Claude can stop or idle); Exit 2 = send stdout as feedback AND block/continue the action (reject task completion, keep working, prevent exit)

---

**Q3.** What is the PRECISE architectural difference between a Plugin and a Marketplace?


🅐 A Plugin is a single skill file (.md) with metadata; a Marketplace is a collection of plugins bundled for batch installation

🅑 A Plugin is user-created stored locally; a Marketplace is Anthropic's official distribution channel requiring certification

🅒 A Plugin is a real-time integration using WebSockets; a Marketplace is a static registry of plugin metadata

🅓 A Plugin is a folder containing skills/agents/hooks/MCP configs (like an app); a Marketplace is a catalog listing multiple plugins (like an app store). You install Plugins; you add Marketplaces as discovery sources

---

**Q4.** LSP plugins like typescript-lsp require something beyond just plugin installation. What is this additional requirement?


🅐 A paid Claude Code Pro subscription since real-time language analysis consumes significantly more API tokens

🅑 The target project must be version-controlled with Git since the language server tracks file changes through Git's index

🅒 A separate authentication token from each language's official foundation to access their language server implementations

🅓 The language server BINARY must be installed separately on your system (e.g., typescript-lsp requires typescript-language-server); the plugin provides the Claude Code integration layer but the actual language intelligence comes from the binary

---

**Q5.** In the plugin manifest, what SPECIFICALLY goes inside .claude-plugin/ vs at the root level?


🅐 .claude-plugin/ contains all executable files (Python scripts, bash hooks, compiled binaries); root level has human-readable configs

🅑 .claude-plugin/ contains skills/ and agents/ subdirectories; root level has hooks/ and .mcp.json installed at system level

🅒 .claude-plugin/ contains marketplace.json for distribution PLUS plugin.json, allowing the plugin to serve as both plugin and marketplace

🅓 Only the plugin.json manifest goes inside .claude-plugin/ (name, description, version, author). ALL actual components (skills/, agents/, hooks/hooks.json, .mcp.json) go at the plugin's ROOT level alongside .claude-plugin/

---

**Q6.** Ralph Wiggum Loop is named after a Simpsons character. What philosophical connection does this name establish?


🅐 Ralph Wiggum is known for random, unpredictable behavior — acknowledging that Claude's iteration path cannot be predicted in advance

🅑 Ralph Wiggum is known for following instructions literally without judgment — describing how the loop mechanically executes tasks

🅒 Ralph Wiggum is known for asking for help repeatedly — describing how the loop escalates to human oversight after three consecutive failures

🅓 Ralph Wiggum is known for cheerful persistence despite mistakes — the plugin embodies 'try, fail, learn, repeat'; Claude doesn't give up when a fix doesn't work but keeps attempting corrections with each failed attempt providing context for the next try

---

**Q7.** The embedded promise pattern vs natural tool output — which is RECOMMENDED and why?


🅐 Natural tool output is recommended — tool outputs like '0 problems' are more reliable because they come from deterministic tools, not AI

🅑 Both are equivalent — purely a style choice with no functional difference in reliability

🅒 Embedded promise only for complex tasks with multiple tool outputs; natural for simple single-command tasks

🅓 Embedded promise pattern is recommended — you instruct Claude to output <promise>LINTING_COMPLETE</promise> when done; this gives YOU full control over the exact completion signal, ensures Claude knows explicitly what to output, and works reliably with the static completion promise architecture

---

**Q8.** After 8 Ralph Loop iterations, the same error keeps appearing. Which situation MOST clearly signals time to cancel?


🅐 Iteration count exceeds 50% of max-iterations — statistical analysis shows loops rarely complete at this point

🅑 Claude starts generating longer responses per iteration — indicating a reasoning problem that will eventually self-resolve

🅒 API cost exceeds $10 — the book prescribes this as the hard economic limit for autonomous iteration

🅓 Same error repeats 3+ times — Claude is stuck in a local optimum requiring human judgment; the problem likely needs missing context, an architectural decision, or external dependency resolution that Ralph Loop cannot provide

---

**Q9.** Competing Hypotheses is a poor use case for a single Ralph Loop but perfect for Agent Teams. Why specifically?


🅐 Agent Teams can share a single completion promise across all hypotheses, reducing total iterations needed compared to sequential testing

🅑 Agent Teams allow different models per hypothesis — more powerful for complex reasoning, faster for data lookup — which Ralph Loop's single-model architecture cannot achieve

🅒 Agent Teams can run Ralph Loop on each hypothesis in parallel, multiplying Ralph Loop's power by the number of teammates

🅓 Agent Teams run multiple Claude instances each committed to a DIFFERENT hypothesis who can CHALLENGE each other's findings directly — preventing anchoring bias; a single Ralph Loop would commit to the first plausible explanation and iterate toward confirming it, missing alternative root causes

---

**Q10.** Agent Teams vs subagents — what SPECIFIC communication capability do teammates have that subagents lack?


🅐 Teammates can broadcast messages to ALL teammates simultaneously using a shared channel; subagents can only send private reports to main agent

🅑 Teammates can receive messages from the human user directly; subagents can only be addressed through the main agent as intermediary

🅒 Teammates can read each other's full context windows and conversation histories; subagents operate in complete isolation

🅓 Teammates can send DIRECT messages to EACH OTHER — e.g., market researcher messages financial analyst 'TAM is $2.4B, factor that into your revenue projections'; subagents can only report back to the single main agent with no peer-to-peer communication

---

**Q11.** Task 3 has blockedBy: ['2']. What EXACTLY happens when task 2 completes?


🅐 Task 3 is automatically assigned to the same teammate who completed task 2, ensuring continuity of context

🅑 Task 3 requires explicit lead approval before becoming claimable — the lead must review task 2's outputs as acceptable quality first

🅒 Task 3 sends a notification to the human user requesting confirmation that task 2's results are satisfactory before proceeding

🅓 Task 3 automatically unblocks and becomes available for ANY available teammate to claim from the shared task list — teammates self-coordinate and pick up unblocked tasks without the lead manually assigning them

---

**Q12.** 'Teammates do NOT inherit the lead's conversation history.' What is the SPECIFIC implication and how should developers handle it?


🅐 Teammates start with completely empty context including no access to filesystem or CLAUDE.md — use shared documents to manually share all context

🅑 The limitation only affects the first message — after first exchange, teammates access full conversation history through the shared task file system

🅒 Teammates inherit project-level settings and CLAUDE.md but not conversational context — intended design since conversational context is ephemeral

🅓 Critical project context discussed before teammate creation is invisible to teammates — developers must include essential context explicitly in the spawn prompt for each teammate, OR ensure CLAUDE.md contains necessary background since teammates DO read project context files

---

**Q13.** Delegate Mode (Shift+Tab) — what PRECISELY does it prevent and allow?


🅐 Prevents teammates from making decisions autonomously — all action proposals routed through lead for approval before execution

🅑 Prevents the human user from directly messaging individual teammates — all communication routes through the team lead

🅒 Prevents any single teammate from claiming more than one task at a time — ensuring even parallel distribution

🅓 Prevents the team lead from doing any direct analysis, research, or execution — the lead can ONLY coordinate (create tasks, send messages, review results); all investigation goes to teammates; analogy: you are the project director who defines scope, your team executes, you never write the deliverable

---

**Q14.** Which Agent Teams 'Known Limitation' has the MOST significant operational consequence for long-running complex projects?


🅐 One team per session — limiting to a single active team means parallel workstreams with different compositions must run sequentially

🅑 No nested teams — hierarchical organizational structures requiring multiple management layers need alternative approaches

🅒 Lead is fixed — if the lead's model becomes inadequate for synthesizing complex findings, the session must be restarted

🅓 No session resumption — if a teammate crashes or session restarts, in-process teammates cannot be recovered and the team must be recreated from scratch; any interruption (network loss, system restart) destroys all teammate context and work state permanently

---

**Q15.** In Workflow 4 (Research Synthesis of 65 documents), which TWO Cowork patterns are MOST critical for trustworthy results?


🅐 'Propose, Then Execute' AND 'Handle Variation' — approval before processing and adapting to different document formats

🅑 'Handle Variation' AND 'Propose, Then Execute' — inconsistent formatting and structural approval before deep processing

🅒 'Explore First' AND 'Propose, Then Execute' — scanning titles to plan, then outline approval before reading full content

🅓 'Explore First' (Claude actually reads all 65 documents before synthesizing, not just scanning titles) AND 'Report Results' (source attribution and citations for each extracted insight enabling the developer to verify accuracy and cross-reference originals)

---

**Q16.** Cowork Connectors vs MCP — what IS the relationship?


🅐 Connectors are a separate higher-level protocol built ON TOP of MCP — adding authentication, rate limiting, and data transformation layers

🅑 Connectors use REST APIs directly rather than MCP, making them more compatible with existing enterprise systems

🅒 Connectors are pre-built Anthropic-certified integrations while MCP connections are community-built — distinction is about quality assurance

🅓 Connectors ARE MCP connections — the same underlying Model Context Protocol — but presented through Cowork's more accessible GUI interface; what Claude Code calls 'MCP servers' Cowork calls 'Connectors' to make the concept accessible to knowledge workers who may not know what MCP means

---

**Q17.** The book says Cowork 'makes tasks feasible that you'd otherwise skip or do poorly.' What does this SPECIFICALLY mean?


🅐 Cowork can perform tasks physically impossible for humans — reading 65 documents truly simultaneously in parallel

🅑 Cowork enables tasks that require capabilities humans don't have — perfect recall or exact calculations without rounding errors

🅒 Cowork allows non-experts to complete tasks previously requiring specialized skills — democratizing technical capabilities

🅓 Many valuable tasks (organizing Downloads, synthesizing 65 documents, generating formatted reports from CSV) don't get done manually because the time cost exceeds the perceived benefit — Cowork makes these feasible by reducing the effort barrier, enabling higher-quality work that previously went undone

---

**Q18.** Ralph Wiggum Loop's connection to the Digital FTE vision — what specific parallel does the book draw?


🅐 Ralph Loop demonstrates the 'cost-per-outcome' pricing model — clients pay only when the loop completes, not per iteration

🅑 Ralph Loop demonstrates the need for 'vertical expertise' — generic loops are less effective than domain-specific loops, validating why domain specialists create better Digital FTEs

🅒 Ralph Loop demonstrates the 'Three Pillars' (CLAUDE.md + Skills + MCP) in action across each iteration

🅓 Ralph Loop demonstrates 'autonomous execution' — the core Digital FTE capability: start with a goal, work independently, self-correct when errors occur, signal when human judgment is needed; the same pattern powers autonomous sales agents, customer support agents, and DevOps agents in production

---

**Q19.** 'Sequential investigation suffers from anchoring; parallel debate eliminates it.' What IS anchoring bias and why does parallel debate eliminate it?


🅐 Anchoring = investigator becomes anchored to initial data sources found in first search, missing contradicting sources found later; parallel teams start with different search strategies

🅑 Anchoring = investigator anchors conclusion to client's stated hypothesis rather than following evidence; anonymous investigators aren't influenced by knowing client expectations

🅒 Anchoring = investigator's conclusion anchors to when they complete analysis, missing later information; simultaneous completion means all evidence available to all investigators

🅓 Anchoring = finding the first plausible explanation and stopping — not exploring alternatives; parallel debate eliminates it because four investigators committed to DIFFERENT theories actively try to disprove each other's findings; the hypothesis that survives cross-challenge is most likely correct

---

**Q20.** A developer needs GitHub integration for Claude Code. What is the COMPLETE workflow according to the book's 'check what exists before building from scratch' principle?


🅐 Visit modelcontextprotocol.io → copy GitHub MCP server command → run 'claude mcp add' → create a GitHub skill to teach Claude how to use it effectively

🅑 Create a .mcp.json file with GitHub API credentials → run 'claude mcp add' → create hooks.json for automation → test each component individually

🅒 Visit github.com/anthropics/claude-plugins-official → fork the github plugin → modify for your team's workflow → install from your fork

🅓 Run /plugin → Discover tab → find 'github' under External Integrations → install (or /plugin install github@claude-plugins-official directly) → the plugin automatically configures MCP, bundled skills, and automation hooks — no manual setup needed

