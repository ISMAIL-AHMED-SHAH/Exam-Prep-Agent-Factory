

**📚 Ch.12 Lesson 3 — AIFF Standards, Nine Pillars of AIDD & Digital FTE Business Strategy**
*Exam L1: P2-GAF1 Prep | 20 Questions | All answers are D*

---

**Q1.** What made the AAIF announcement on December 9, 2025 historically unprecedented in the AI industry?

🅐 It was the first time any AI company open-sourced a production-grade agent framework
🅑 It established the first government-backed regulatory framework for AI agent deployment
🅒 It created the first shared cloud infrastructure for AI agents eliminating per-company compute costs
🅓 OpenAI, Anthropic, and Block — fierce competitors — came together to donate core technologies to neutral Linux Foundation governance, joined by AWS, Google, Microsoft, Bloomberg, and Cloudflare

---

**Q2.** The book uses the USB analogy to explain AAIF. Which aspect of USB MOST precisely maps to what MCP achieves?

🅐 USB's plug shape — MCP standardizes the visual format of agent responses
🅑 USB's power delivery — MCP standardizes how much compute each agent can consume
🅒 USB's data transfer speed — MCP ensures all agents communicate at the same token processing speed
🅓 USB's universal interface standard — before USB every device-port pair needed proprietary cables; before MCP every agent-tool pair needed custom integration code; both eliminated the M×N combinatorial explosion

---

**Q3.** A developer exposes 'send_email' as a Resource instead of a Tool in MCP. What is the SPECIFIC consequence?

🅐 The agent will send emails automatically without user confirmation, creating a security vulnerability
🅑 The email sends with corrupted formatting due to different data serialization formats
🅒 The MCP server throws a runtime error and refuses to process any requests
🅓 The agent can SEE the send_email option but cannot execute it — Resources are read-only (eyes, not hands); only Tools change state and perform actions

---

**Q4.** What is the HIERARCHY RULE that makes AGENTS.md powerful for large enterprise codebases?

🅐 Root AGENTS.md takes absolute precedence, enforcing company-wide rules uniformly
🅑 AGENTS.md files are processed alphabetically when conflicts arise
🅒 Rules from all AGENTS.md files are merged additively and apply simultaneously
🅓 The nearest AGENTS.md file takes precedence — enabling monorepo support where frontend/backend subprojects each override root-level rules with their own specific conventions

---

**Q5.** Progressive Disclosure in Agent Skills achieves 80-98% token reduction. How does it work?

🅐 The agent compresses skill descriptions using a specialized tokenization algorithm
🅑 The agent loads all skills at startup but removes them from context after use
🅒 Skills are stored in a vector database retrieved via semantic similarity search above 0.85 threshold
🅓 At startup only name + description (~100 tokens) loads per skill; full SKILL.md loads when activated (<5K tokens); supporting resources load only when actually needed during execution

---

**Q6.** The book recommends: 'Use Claude Code for productivity today. Study goose for building Custom Agents tomorrow.' What is the PRECISE reason for this distinction?

🅐 goose is more powerful than Claude Code for production enterprise workloads
🅑 goose supports more programming languages than Claude Code for polyglot codebases
🅒 goose integrates with more MCP servers than Claude Code
🅓 goose is Apache 2.0 open source — its source code is a battle-tested blueprint showing how production agents implement MCP, handle streaming, and manage context; Claude Code (proprietary) is optimized for productivity but its internals cannot be studied

---

**Q7.** AIDD is defined as a 'specification-first methodology.' Which of the 9 AIDD characteristics MOST directly captures what 'specification-first' means in practice?

🅐 AI-Augmented — agents handle all implementation details
🅑 Production-Ready — specifications written first ensure production standards from day one
🅒 Version-Controlled — specifications must be tracked before implementation begins
🅓 Specification-Driven — you define WHAT to build and how it should behave before any code is written; AI agents then generate, test, and refine the implementation from that specification

---

**Q8.** Pillar 6 (TDD) plays a unique role in AIDD that differs from traditional development. What is this unique function?

🅐 TDD in AIDD eliminates the need for human code review — passing tests are the sole quality gate
🅑 TDD in AIDD allows developers to skip the specification phase since tests implicitly define requirements
🅒 TDD in AIDD is used exclusively for regression testing when specifications update
🅓 TDD serves as the primary quality gate for AI-generated code that cannot be manually verified line by line — you define expected behavior through tests; any AI-generated code must pass those tests before acceptance

---

**Q9.** Why is Pillar 5 (Linux Universal Dev Environment) specifically critical for AI Coding Agents (Pillar 1)?

🅐 Linux environments provide superior AI model performance — most LLMs were trained on Linux-generated code
🅑 Linux environments have better security features protecting sensitive API keys during development
🅒 Linux environments provide faster disk I/O reducing AI agent tool call latency
🅓 AI CLI agents write shell scripts and execute commands that must run consistently across developer machines and cloud environments — without Bash standardization (WSL2/macOS/Linux), agents cannot write portable automation that works everywhere

---

**Q10.** Maya built a full financial analytics platform in one week — attributed to 'system completeness.' What does this mean?

🅐 Maya used all available AI tools simultaneously — parallel compute compressed the timeline
🅑 Maya's exceptional talent was amplified by AI tools creating a multiplicative effect
🅒 Maya purchased enterprise AI subscriptions providing unlimited context windows
🅓 Maya worked within a complete integrated system where all nine pillars amplified each other — no single pillar enabled the week-long build; eliminating every specialist silo simultaneously made it possible

---

**Q11.** Why was M-Shaped development (deep expertise in 2-4 domains) 'nearly impossible' before AIDD?

🅐 Domain information was not publicly available, requiring specialized university programs for each
🅑 Companies required formal certifications for each domain, making multi-domain practice legally impossible
🅒 Development tools were domain-specific and incompatible, preventing cross-domain workflows
🅓 Mastering multiple domains required thousands of solo hours per skill — the cognitive load of learning, practicing, and maintaining mastery across 2-4 domains simultaneously was humanly overwhelming without AI assistance to fill knowledge gaps on demand

---

**Q12.** Sarah's story (Productivity Trap) vs Marcus's story (Ownership Model) — which framing MOST precisely captures the difference?

🅐 Sarah failed because she used AI casually while Marcus succeeded through rigorous prompt engineering
🅑 Sarah failed because she chose a commoditizing field; Marcus succeeded by choosing a niche field
🅒 Sarah failed because she didn't build a product; Marcus succeeded by building a subscription service
🅓 Sarah used AI to facilitate her own labor (making herself a faster human worker); Marcus used AI to productize his expertise (encoding his knowledge into an asset he owns, that works without him, that compounds in value)

---

**Q13.** The 90/10 Moat framework says 'Prompt Engineering is NOT a Moat.' What IS the actual moat?

🅐 The moat is proprietary training data — prompts can be reverse-engineered within weeks
🅑 The moat is deployment speed — faster AI models will eliminate prompt-based advantage within months
🅒 The moat is API access to exclusive models — but same models are available to all competitors
🅓 The moat is knowing what the correct answer is supposed to look like — the 10% of domain insight that detects when AI's generic output misses something critical; prompt engineering is insufficient because it is easy to learn and AI is improving to understand natural language without it

---

**Q14.** The Snakes and Ladders framework says Layer 1 is a 'Snake.' What historical lesson from Microsoft Windows Mobile validates this?

🅐 Windows Mobile failed because Microsoft chose inferior technical architecture vs iOS and Android
🅑 Windows Mobile failed because Microsoft launched too late into the consumer market
🅒 Windows Mobile failed because Microsoft underfunded marketing vs Apple's billion-dollar campaigns
🅓 Windows Mobile tried to win on consumer appeal (Layer 1) against Apple and Google — a two-player game — collapsing to 5% market share by 2010; Microsoft should have focused on enterprise first (Layer 2/3) then built upward

---

**Q15.** Which ordering from FASTEST to SLOWEST 'Time to Revenue' across the four monetization models is MOST accurate?

🅐 Subscription → Marketplace → Success Fee → License
🅑 Marketplace → License → Subscription → Success Fee
🅒 Success Fee → Subscription → License → Marketplace
🅓 Subscription & Marketplace (both: Weeks) → Success Fee (Months) → License (3–6 months enterprise sales cycle)

---

**Q16.** The PPP strategy reduces CAC by 60-80% vs direct competition. What is the SPECIFIC mechanism in Phase 2?

🅐 PPP uses AI agents to automate outbound sales prospecting, replacing human SDRs
🅑 PPP offers freemium tiers attracting large user volumes at zero cost before converting to paid
🅒 PPP undercuts incumbent pricing by 50-70%, making value immediately obvious to cost-sensitive buyers
🅓 PPP piggybacks on incumbent vendor marketplaces (Salesforce AppExchange, Shopify Store) — existing customers discover your agent within their trusted ecosystem, eliminating cold outreach and brand-building costs

---

**Q17.** Phase 3 of PPP achieves 'zero user friction' during the strategic pivot. Why does skill portability make this possible?

🅐 Users are automatically migrated by the incumbent platform's data export tools
🅑 Phase 3 involves rebranding the existing platform so users experience no infrastructure change
🅒 The agent's UI is redesigned to be more intuitive, making the transition feel like an upgrade
🅓 Agent Skills were built on standardized SKILL.md definitions not hard-coded API calls — 're-pointing' a skill from Canvas API to your native database requires no change to user-facing behavior; users interact identically before and after

---

**Q18.** The Three Requirements for Vertical Success: what specific failure mode occurs when an agent has Domain Expertise + Deep Integrations but NO Complete Agentic Solution?

🅐 The agent becomes a security liability due to uncontrolled data access patterns
🅑 The agent fails accuracy requirements because expertise cannot be properly applied without orchestration
🅒 The agent creates regulatory violations because incomplete solutions cannot log decisions properly
🅓 The agent becomes just a data pipeline — useful for reading and writing data but not solving end-to-end business problems; it is a curiosity, not a product enterprises will pay for

---

**Q19.** Shadow Mode deployment has three phases. What SPECIFIC threshold determines graduation from Phase 1 to Phase 2?

🅐 The agent must achieve 95%+ accuracy on the Golden Dataset of 50+ real-world scenarios
🅑 The agent must complete a minimum of 30 days of shadow operation regardless of accuracy
🅒 The agent must receive explicit approval from a compliance officer certifying the decision logic
🅓 The agent must demonstrate agreement with human decisions 80%+ of the time during shadow operation — indicating sufficient alignment to begin informing (not replacing) human decisions in Phase 2

---

**Q20.** A proposed hiring agent screens resumes and forwards only 'qualified' candidates to hiring managers. Which combination of Red Flag signals triggers the 3+ threshold requiring you to stop?

🅐 Insufficient Audit Trail + Regulatory Uncertainty + Adversarial Time Pressure (hiring deadline approaching)
🅑 High-Consequence Errors + Untrained Data + No Audit Trail — resume errors cause reputational harm
🅒 Irreplaceable Human Judgment + Regulatory Uncertainty — only 2 signals, needs review not abandonment
🅓 Biased/Untrained Data (historical hiring bias) + No Audit Trail for Decisions (EEO laws require documented rationale) + Irreplaceable Human Judgment (candidate evaluation requires contextual judgment no dataset captures) = 3 signals → stop and redesign

