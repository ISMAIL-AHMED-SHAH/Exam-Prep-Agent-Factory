**📚 Ch.14 Lesson 1 — Claude Code Origin, CLAUDE.md & Skills Concept**
*Exam L1: P2-GAF1 Prep | 20 Questions!*

---

**Q1.** What did Anthropic call the 'Product Overhang' discovered by Boris Cherny in September 2024?

🅐 Claude's reasoning improved with larger context windows, revealing suppressed capability

🅑 Claude's coding benchmarks jumped 40% when given real-time internet access

🅒 Claude's accuracy improved dramatically with structured prompt templates

🅓 The capability to be a genuine development partner already existed inside Claude — it didn't need to become smarter, it needed filesystem access to unlock behavior that emerged without explicit instruction

---

**Q2.** Which set of dogfooding metrics from Anthropic MOST accurately reflects Claude Code's internal results?

🅐 30% Day 1, 70% Day 5, 95%+ by launch; 3 PRs/day; throughput doubled with constant team size

🅑 20% Day 1, 50% Day 5, 80%+ by May 2025 launch; engineers averaged 5 PRs/day vs typical 1-2; PR throughput jumped 67% as team grew from 2 to 10

🅒 10% Day 1, 40% by Day 10, 60% by launch; 8 PRs/day; throughput tripled as team halved

🅓 50% Day 1, 80% by Day 3, 100% within a week; 10 PRs/day; 200% throughput increase

---

**Q3.** 'About 90% of Claude Code was written by Claude Code itself.' What does the book say this demonstrates?

🅐 That foundation models have reached human-level intelligence and can fully replace software engineers

🅑 That Claude Code's training data was primarily its own previous outputs — a self-improving feedback loop

🅒 That agentic AI always outperforms human developers given sufficient compute resources

🅓 Not that AI became suddenly brilliant, but that the agentic model gives it the access it needs — when AI can read code, run tests, and iterate, it becomes capable of complex work

---

**Q4.** The book distinguishes passive AI from agentic AI using a specific analogy. Which is MOST accurate?

🅐 Passive AI is a junior developer following exact instructions; agentic AI is a senior developer making autonomous decisions without checking with you

🅑 Passive AI is a search engine; agentic AI is a recommendation engine that proactively suggests content based on behavioral patterns

🅒 Passive AI is a calculator performing operations you specify; agentic AI is a spreadsheet that automatically recalculates dependent cells

🅓 Passive AI is a consultant on the phone who doesn't see your screen — generic advice; agentic AI is a pair programmer looking directly at your code — reads files, proposes specific changes, runs tests, iterates

---

**Q5.** In Claude Code's OODA Loop, what is the SPECIFIC function of the 'Orient' step when debugging?

🅐 Claude searches training data for similar errors and retrieves the most statistically common solution

🅑 Claude generates five alternative hypotheses and ranks them by probability for the developer to choose

🅒 Claude orients the terminal output to display error messages in a more structured parseable format

🅓 Claude identifies the root cause within the context of YOUR specific tech stack, existing patterns, and project constraints — framing the problem in your actual environment before deciding where to look

---

**Q6.** What SPECIFIC observation at Anthropic triggered the development of Cowork (the Second Product Overhang)?

🅐 Enterprise clients demanded a GUI after the terminal interface failed security audits in regulated industries

🅑 Market research showed 80% of potential users were knowledge workers who had never used a terminal

🅒 Developer productivity metrics showed terminal interfaces were 30% slower for document-heavy workflows

🅓 Non-technical users who struggled through terminal setup were still using Claude Code for organizing files, processing documents, and automating research — revealing the value was in agentic filesystem access, not the terminal

---

**Q7.** Which combination of modes does the book say SPECIFICALLY enables building Digital FTEs?

🅐 Only Chat and Projects — Chat handles reasoning, Projects provides persistent memory across sessions

🅑 Excel, Artifacts, and Chat — data processing, output generation, and workflow coordination

🅒 Only Cowork and Connectors — agentic execution and external data access

🅓 Skills, Connectors, Plugins, and Cowork/Code — composing Skills, wiring Connectors, packaging Plugins, deploying through Cowork or Claude Code — the four professional-grade modes that turn domain expertise into Digital FTEs

---

**Q8.** How does Claude Code create the ILLUSION of conversation continuity when LLMs are actually stateless?

🅐 Claude Code stores history in a local SQLite database and injects relevant past exchanges using semantic similarity search

🅑 Claude Code uses a persistent server-side session that maintains model state between requests

🅒 Claude Code compresses conversation history using a summarization model that creates an ever-growing context summary file

🅓 Claude Code re-sends the entire conversation history bundled with every new message — so when you send message #3, it secretly sends #1+#2+#3 together to the stateless LLM which reads the full bundle fresh each time

---

**Q9.** What is the book's CORE insight about why filesystem access solves the LLM statelessness problem for coding work?

🅐 Filesystem access allows Claude Code to write conversation logs to disk, creating a persistent memory system

🅑 Filesystem access enables Claude Code to sync with cloud storage, creating shared memory across machines

🅒 Filesystem access lets Claude Code modify its own system prompt between sessions by reading a configuration file

🅓 Your code files already contain your project's state — instead of describing your project to Claude, Claude reads it directly; the filesystem acts as external persistent memory, treating files as ground truth rather than conversation history

---

**Q10.** What is the book's specific guidance on CLAUDE.md file size?

🅐 Target under 500 lines — if beyond this, create separate CLAUDE-extended.md files loaded sequentially

🅑 No recommended size limit — CLAUDE.md should be comprehensive since Claude Code uses semantic search to load only relevant sections

🅒 Target under 100 lines — split into domain-specific files (CLAUDE-backend.md, CLAUDE-frontend.md) in relevant subdirectories

🅓 Target under 200 lines — if it grows beyond 200 lines, split using @path/to/file imports (e.g., @docs/conventions.md) to keep each file focused; concise instructions get better adherence

---

**Q11.** What is the MOST precise distinction between CLAUDE.md (Auto Memory) and CLAUDE.md (the file you write)?

🅐 CLAUDE.md loads every session automatically; Auto Memory requires the /memory command to load

🅑 CLAUDE.md is stored in the project repository and shared with the team; Auto Memory is private per machine

🅒 CLAUDE.md covers project-level context; Auto Memory covers conversation-level context stored for future sessions

🅓 CLAUDE.md is written by YOU (your instructions, standards, context for Claude); Auto Memory is written BY CLAUDE (its own notes about what it discovered — build commands, debugging insights, patterns — saved to ~/.claude/projects/<project>/memory/)

---

**Q12.** Why does the book recommend using BOTH CLAUDE.md AND AGENTS.md in the same project?

🅐 AGENTS.md is required by AAIF certification for any project using MCP integrations; CLAUDE.md is Anthropic's proprietary format — both are mandatory for compliance

🅑 CLAUDE.md takes precedence when conflicts arise; AGENTS.md is a fallback for other AI tools — together they provide primary and secondary instruction layers

🅒 AGENTS.md covers build-time configuration; CLAUDE.md covers runtime behavior — together they provide complete project coverage

🅓 AGENTS.md provides universal portability (60,000+ projects, all major AI coding agents); CLAUDE.md provides Claude-specific depth (Skills, MCP configs, hooks); CLAUDE.md references @AGENTS.md for shared content and adds Claude-specific features on top

---

**Q13.** What SPECIFIC lesson does the 'tax professional vs 300-IQ genius' analogy teach about Agent Skills?

🅐 Domain experts are always more valuable than AI because human intuition can never be captured digitally

🅑 AI agents should be fine-tuned on domain data rather than prompted, since fine-tuning creates deep procedural knowledge

🅒 AI should focus on tasks where intelligence is the limiting factor since it inherently outperforms humans on pure reasoning

🅓 AI agents today have intelligence and execution but lack domain expertise — Skills fill this gap by giving agents the encoded procedures, edge cases, and patterns that make generic capability specifically useful, just as the professional's expertise beats the genius's raw intelligence

---

**Q14.** Skills use three-level progressive disclosure. What problem does this SPECIFICALLY solve?

🅐 It prevents unauthorized access — Level 1 is public, Level 2 requires authentication, Level 3 is encrypted for licensed users

🅑 It enforces a three-stage quality review — Level 1 is draft, Level 2 is community-reviewed, Level 3 is Anthropic-certified

🅒 It optimizes for hardware — Level 1 for low-power devices, Level 2 for standard compute, Level 3 requires GPU acceleration

🅓 It prevents context window overload — only name+description loads at startup (~100 tokens), full SKILL.md loads when activated (<5K tokens), supporting files load only when executing — like a smartphone with 100 apps that only activates the ones you tap

---

**Q15.** Which four properties make Skills STRATEGIC ASSETS rather than just convenient shortcuts?

🅐 Portability (across cloud providers), Security (encrypted), Scalability (millions of concurrent requests), Discoverability (marketplace indexed)

🅑 Versioning (automatic Git tracking), Testing (built-in unit tests), Documentation (auto-generated API docs), Deployment (one-click CI/CD)

🅒 Speed (faster than prompting), Accuracy (higher precision), Cost (cheaper per call), Coverage (broader knowledge domain)

🅓 Reliability (deterministic/script-backed vs ad-hoc), Token Cost (load when triggered vs pay every conversation), Asset Type (reusable scalable IP vs disposable conversation), Integration (API-ready via Agent SDKs vs human copy-paste)

---

**Q16.** The Stack Analogy maps AI components to computing. Which mapping is MOST accurate and what is the KEY implication?

🅐 Foundation Models = Operating Systems; Agent Runtimes = Applications; Agent Skills = Libraries

🅑 Foundation Models = Databases; Agent Runtimes = APIs; Agent Skills = User Interfaces

🅒 Foundation Models = Compilers; Agent Runtimes = IDEs; Agent Skills = Source Code

🅓 Foundation Models = Processors; Agent Runtimes (Claude Code) = Operating Systems; Agent Skills = Applications — few companies build processors/OS, but millions build applications encoding domain expertise; this is the layer that opens for everyone

---

**Q17.** Which bundled slash command SPECIFICALLY generates a CLAUDE.md by analyzing your existing codebase?

🅐 /setup — runs a guided interview where Claude asks questions and generates CLAUDE.md from your answers

🅑 /scaffold — creates complete project structure including CLAUDE.md, AGENTS.md, and .claude/skills/ as a one-time initialization

🅒 /context — regenerates context files based on current repository state, typically run after major refactors

🅓 /init — causes Claude to analyze your codebase and automatically generate a CLAUDE.md with build commands, test instructions, and project conventions based on what it reads in your actual files

---

**Q18.** Non-technical users (accountants, recruiters, lawyers) creating Skills in the first weeks after launch SPECIFICALLY validates which design principle?

🅐 Claude Code's terminal interface is more accessible than expected — most knowledge workers can learn CLI within weeks

🅑 AI can infer domain expertise from general business documents without explicit procedural documentation

🅒 The agentskills.io marketplace has sufficient reach to attract diverse user communities beyond developers

🅓 Domain expertise — not programming ability — is the real requirement for skill creation; markdown + YAML is accessible to anyone who can write structured text; the barrier is willingness to articulate procedures clearly, not technical skill

---

**Q19.** The book describes a 'Convergence Path' between Claude Code and Cowork. What does this mean for learning investment?

🅐 Invest primarily in Claude Code terminal skills first since they form the foundation for understanding Cowork's simplified interface

🅑 Invest equally in both immediately since they will merge into a single product within 6 months, making the distinction irrelevant

🅒 Invest primarily in Cowork since it represents the future direction — the terminal interface is being deprecated in favor of the GUI

🅓 Don't invest heavily in interface-specific patterns that won't transfer — focus on agentic reasoning patterns, skill design, and workflow thinking that are interface-independent, since Claude Code now runs in VS Code, JetBrains, desktop app, web browser, and iOS

---

**Q20.** A data scientist needs to write Python scripts, run Jupyter notebooks, create a PDF stakeholder report, and email it to the team. What does the decision framework prescribe?

🅐 Use only Claude Code — terminal's Python integration and git support make it superior for the entire workflow including document generation and email

🅑 Use only Cowork — its document Skills and browser integration handle Python execution via plugins, report generation, and email distribution in a single visual interface

🅒 Use Claude Code for analysis and Cowork for the report, but use a human team member to handle email since neither interface provides reliable professional email sending

🅓 A hybrid approach: Claude Code for writing and debugging Python scripts and running Jupyter notebooks (code-primary), then Cowork for creating the formatted PDF stakeholder report and using browser integration to email it (document-primary)

