

**📚 Ch.14 Lesson 2 — Building Skills, Subagents, MCP & Settings Hierarchy**
*Exam L1: P2-GAF1 Prep | 20 Questions | Answers shuffled!*

---

**Q1.** The description field in SKILL.md's YAML frontmatter — why does the book call it 'the most important line you write'?

🅐 It appears as a tooltip in Claude Code's interface helping users know when to manually invoke the skill
🅑 It's used by agentskills.io marketplace to categorize and index your skill for community discovery
🅒 It's compiled into binary activation rules requiring exact regex pattern matching to trigger
🅓 It's the skill's activation trigger — Claude scans descriptions at startup (Level 1 of progressive disclosure) to decide which skills apply; vague descriptions mean Claude won't know when to activate

---

**Q2.** Which description MOST correctly applies the book's Description Formula?

🅐 'Blog planning skill for content creators who need structured outlines and headline generation'
🅑 'Use this when you want to plan a blog post. It helps with outlines and headlines.'
🅒 'A comprehensive blog planning tool that integrates with your content calendar, generates SEO-optimized headlines, creates audience-targeted outlines, and drafts introductions in your brand voice'
🅓 'Plan blog posts with topic research, outline creation, headline variations, and introduction drafts. Use when user asks to plan, outline, or write blog content' — states action verb, key outputs, and trigger conditions

---

**Q3.** The 'skill-creator' is described as a meta-skill. What does this mean?

🅐 It's Anthropic's internal tool for creating official partner skills — individuals request skills via the agentskills.io portal
🅑 It's a VS Code extension providing a GUI wizard for building SKILL.md files with YAML syntax validation
🅒 It's a subagent that auto-triggers when Claude Code detects you're doing a task repeatedly
🅓 It's a skill that creates other skills — guiding you through procedure analysis, description writing, and SKILL.md generation; using Claude itself to create skills produces better results than writing manually

---

**Q4.** After using a skill three times and noticing generic outputs, what does the Co-Learning Cycle prescribe?

🅐 Delete and rebuild from scratch using the skill-creator since iterating on a flawed skill compounds errors
🅑 Submit to agentskills.io community forum for peer review by external domain experts
🅒 Add more specific regex patterns to the description to force more frequent activation
🅓 Use AI as Teacher → You as Teacher → Co-Worker iteration: ask Claude to review and suggest improvements, specify your domain constraints, then iterate together until the skill matches your real workflow

---

**Q5.** What happens to control flow AFTER a subagent completes its work?

🅐 The subagent becomes the new primary agent replacing main Claude Code for subsequent interactions
🅑 The subagent remains running as a persistent background listener available without re-invocation
🅒 The subagent's isolated context window merges into main Claude Code's context
🅓 Control returns to main Claude Code — the subagent completes its task, returns results, and you interact with main Claude Code again; subagents are one-shot workers not persistent processes

---

**Q6.** What is the SPECIFIC advantage of @-mention invocation over natural language requests for subagents?

🅐 @-mention is faster by ~200-400ms as it bypasses Claude Code's decision-making layer
🅑 @-mention gives the subagent elevated permissions to access protected files that normal delegation restricts
🅒 @-mention creates a persistent connection allowing the subagent to be recalled without re-initialization
🅓 @-mention guarantees the specific subagent runs — natural language requests rely on Claude's automatic delegation which may or may not trigger the intended agent depending on task interpretation

---

**Q7.** The Explore subagent uses Haiku while Plan uses Sonnet. What principle does this demonstrate?

🅐 All subagents must use different models to prevent context contamination between isolated windows
🅑 Haiku is for read-only tasks while Sonnet is for write operations — a security principle
🅒 The assignment is temporary during beta; all subagents will use Sonnet for consistency after release
🅓 Different tasks warrant different model capabilities — Explore does fast file scanning (speed matters), Plan creates complex multi-step strategies (reasoning depth matters); matching model to task optimizes performance and cost

---

**Q8.** A developer needs a comprehensive security audit across a 50,000-line codebase. Skill or Subagent?

🅐 A Skill — security audits are repeated patterns that should be consistently applied, encoding procedures ensures same quality criteria every time
🅑 Either works equally — purely personal preference since both can access the same files and return the same quality
🅒 A Skill — Skills can reference external MCP servers for security databases while Subagents are limited to local files
🅓 A Subagent — complex multi-step workflow requiring isolated context (findings shouldn't contaminate other work), guaranteed execution (must run fully), and too large for a skill's shared context window

---

**Q9.** The book uses a 'phone directory' analogy for MCP. Which aspect does it MOST precisely map to?

🅐 The phone directory maps to AGENTS.md — just as a phone directory lists contacts, AGENTS.md tells agents what capabilities are available in the project
🅑 The phone directory maps to the SKILL.md description — just as a directory entry briefly describes who to call, a skill description tells Claude when to activate
🅒 The phone directory maps to progressive disclosure — just as a directory gives only name and number (not the full conversation), progressive disclosure only loads skill names at startup
🅓 The phone directory gives Claude a list of approved external specialists it can contact safely — standardized, safe access to the outside world with each MCP server representing an approved external connection

---

**Q10.** MCP Tool Search (Claude Code 2.1.7+, January 2026) — what problem does it solve and what is the default threshold?

🅐 Solves security — scans tool definitions for malicious patterns; default: quarantine any tool with 50+ parameters
🅑 Solves latency — pre-loads commonly used tools based on project history; activates when Claude Code starts
🅒 Solves compatibility — normalizes definitions from different MCP server versions; activates when 3+ servers are installed
🅓 Solves context overhead — lazy loading so definitions only load when needed; default threshold = auto (activates when MCP tools exceed 10% of context); achieves ~85% automatic token reduction

---

**Q11.** A developer wants to use MCP with a high-frequency trading database updating 500 times per second. Which guardrail applies?

🅐 Don't use MCP for sensitive financial data — trading databases contain proprietary information that should never be exposed via MCP's external connection model
🅑 Don't use MCP before understanding the security model — trading databases require HIPAA-level certification MCP servers don't provide
🅒 Don't use untrusted MCP servers — trading database MCPs aren't on Anthropic's official list and haven't been certified
🅓 Don't use MCP for real-time high-frequency queries — MCP adds latency per call (network + Claude reasoning); 500 updates/second is architecturally mismatched; use direct connections for high-frequency data, MCP for ~10 queries/minute analytical access

---

**Q12.** The 'Three Pillars of AI-Native Development' formula — which is MOST accurate?

🅐 Specifications (CLAUDE.md) + Automation (Skills) + Integration (MCP) = Custom Agent replacing human workers
🅑 Documentation (CLAUDE.md) + Templates (Skills) + APIs (MCP) = AI assistant answering questions accurately
🅒 Memory (CLAUDE.md) + Intelligence (Skills) + Speed (MCP) = AI system processing queries faster than manual research
🅓 Context (CLAUDE.md — Claude knows your project) + Procedures (Skills — Claude knows your workflows) + Access (MCP — Claude knows the world's tools) = Digital FTE that understands your goals, knows how you work, and can access any external system safely

---

**Q13.** A team wants to prevent Claude Code from reading .env files for ALL team members. Which settings level?

🅐 User settings (~/.claude/settings.json) — applies to all projects each team member works on, broader protection
🅑 Local settings (.claude/settings.local.json) — lets each member apply it on their own machine without enforcing on CI/CD
🅒 Enterprise managed settings — security-critical constraints require IT department deployment so they can't be overridden
🅓 Project settings (.claude/settings.json) — committed to Git and shared with the team, adding 'permissions.deny: ["Read(./.env)"]' ensures every team member automatically gets this constraint when they pull

---

**Q14.** User has 'Concise' at User level, 'Explanatory' at Project level, no Local settings. They create Local with 'Verbose'. What's active? What happens when they delete Local?

🅐 With Local: 'Verbose'. After deleting: 'Concise' (Claude falls back to most general User level)
🅑 With Local: all three merge and most recently updated wins; after deleting: reverts to last-committed Project settings
🅒 With Local: 'Verbose' for new sessions only; existing sessions retain 'Explanatory' until restarted
🅓 With Local: 'Verbose' (Local wins). After deleting Local: 'Explanatory' (Project wins). User-level 'Concise' is never active in this project because Project always overrides it unless Local is set differently

---

**Q15.** Which permission mode was released in March 2026 and what makes it distinctly different from the others?

🅐 bypassPermissions — released March 2026 — allows all commands without confirmation, safe for CI/CD pipelines with no human present
🅑 acceptEdits — released March 2026 — automatically accepts all file edits while still requiring confirmation for Bash commands
🅒 default — released March 2026 — introduced the permission model where Claude asks before every tool use, replacing previous unrestricted access
🅓 Auto mode — released March 2026 — uses a safety classifier evaluating each tool call: safe actions (reading files, running tests) proceed automatically, risky actions (mass deletion, accessing credentials) are blocked; sits between 'ask every time' and 'skip all checks' using AI-based risk assessment

---

**Q16.** Why should .claude/settings.json be committed to Git but .claude/settings.local.json should be in .gitignore?

🅐 settings.json is read-only after commit so it must be in Git for updates via PRs; settings.local.json is writable by Claude Code at runtime causing constant Git conflicts
🅑 settings.json contains only safe public configuration; settings.local.json may contain sensitive data like API keys that should never be committed
🅒 settings.json affects Claude Code at the model level and must be identical across environments for reproducibility; settings.local.json only affects UI preferences
🅓 settings.json contains team-agreed standards that should be shared and enforced consistently (security policies, project conventions); settings.local.json contains personal experiments and machine-specific settings that should stay private to each developer

---

**Q17.** A healthcare professional wants to encode HIPAA-compliant patient communication templates as a skill. What IS the actual requirement for skill creation?

🅐 Basic Python or JavaScript to write supporting scripts validating HIPAA compliance rules since SKILL.md alone cannot enforce regulatory requirements
🅑 Claude Code installation and terminal familiarity since skills must be created and tested in Claude Code's CLI environment
🅒 An Anthropic API key with healthcare tier access since HIPAA-compliant skills require special certification
🅓 Domain expertise and willingness to articulate procedures clearly — the SKILL.md format (Markdown with YAML frontmatter) is accessible to anyone who can write structured text; the healthcare professional's HIPAA knowledge IS the valuable asset

---

**Q18.** What SPECIFIC problem emerges when researching competitors AND drafting a pitch WITHOUT subagents?

🅐 Token exhaustion — research fills the context window completely before pitch drafting can begin, causing a context overflow error
🅑 Model confusion — using the same model for both analytical research and creative writing causes Claude to switch cognitive modes producing poor output
🅒 Permission escalation — research requires read permissions and drafting requires write permissions; combining both causes unauthorized permission requests
🅓 Context contamination — research notes fill shared context window; when Claude drafts the pitch it may confuse research findings with pitch content, mixing competitor weaknesses into value propositions or losing analytical distance

---

**Q19.** Context7 MCP vs Playwright MCP — what is Context7's PRIMARY function that distinguishes it?

🅐 Context7 manages context for long sessions — it summarizes and compresses conversation history when the context window approaches its limit
🅑 Context7 indexes local project files creating a searchable semantic database while Playwright accesses external websites
🅒 Context7 manages the seven types of context (CLAUDE.md, Auto Memory, Skills, Subagents, MCP, Settings, Chat History) providing a unified dashboard
🅓 Context7 fetches up-to-date official documentation from live sources solving Claude's training data staleness problem — while Playwright navigates and interacts with web pages, Context7 specifically provides current library docs, best practices, and official references with citations

---

**Q20.** The full five-level precedence chain includes 'Managed' settings. When do developers encounter them and what makes them unique?

🅐 Managed settings are Anthropic-deployed updates to Claude Code's default behaviors automatically propagating to all installations as recommended best practices
🅑 Managed settings are created by the project's designated 'settings manager' role who has exclusive write access others cannot modify
🅒 Managed settings are settings approved through a formal change request process, distinguished from experimental settings not yet approved for production
🅓 Managed settings are deployed by IT teams in enterprise environments and CANNOT be overridden by any developer — they sit at the highest precedence level above all others (Managed > CLI args > Local > Project > User), enforcing organizational security policies and compliance requirements

---

