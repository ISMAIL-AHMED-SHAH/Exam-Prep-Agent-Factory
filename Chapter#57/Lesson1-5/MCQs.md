
📡 *CHAPTER 57 — EXTEND YOUR CLAW WITH MCP*
*GAF1 Exam Prep | 20 MCQs | Lessons 1–5*
━━━━━━━━━━━━━━━━━━━━━━

*Q1.* What is the core distinction between an agent's 'knowledge' and its 'ability' in MCP?

🅐 Knowledge is in MEMORY.md; ability is in SKILL.md

🅑 Knowledge = training data (rules/theory); ability = live tool (real-time facts)

🅒 Knowledge = model size; ability = token limit

🅓 Knowledge = passive recall; ability = active memory search

*Q2.* James's agent is compared to 'a consultant who never leaves the conference room.' What does this mean?

🅐 The agent only answers questions asked in chat

🅑 The agent knows the domain but cannot act on live systems

🅒 The agent is restricted to read-only by the Privacy Router

🅓 The agent can only run scheduled tasks

*Q3.* What is the difference between an MCP 'consumer' and an MCP 'producer'?

🅐 Consumer = SSE; producer = streamable-http

🅑 Consumer = gateway config; producer = workspace config

🅒 Consumer configures existing server; producer creates new server with new tools

🅓 Consumer = stdio; producer = HTTP

*Q4.* The Skill-Driven Build Pattern has 5 steps. What is Step 3?

🅐 Configure CLAUDE.md with project rules

🅑 Install a skill that gives Claude Code domain expertise

🅒 Describe what you need in plain language

🅓 Verify the result


*Q5.* What command installs the mcp-builder skill?

🅐 openclaw skill install mcp-builder

🅑 npx skills add https://github.com/anthropics/skills --skill mcp-builder

🅒 claude code --install-skill mcp-builder

🅓 uv add mcp-builder --skill


*Q6.* After installing mcp-builder, what directories are inside .claude/skills/mcp-builder/?

🅐 tools/, prompts/, config/

🅑 SKILL.md only

🅒 SKILL.md, reference/, scripts/

🅓 SKILL.md, hooks/, manifests/

*Q7.* The rule 'Use spec-first development' in CLAUDE.md prevents what?

🅐 Claude Code using pip instead of uv

🅑 Claude Code jumping to code without agreeing on requirements → rework

🅒 Claude Code loading the wrong MCP transport

🅓 Claude Code writing tests before running the server


*Q8.* When does Claude Code read skill files?

🅐 Every time it executes a tool call

🅑 Only when asked with /load-skill

🅒 On session start — not mid-conversation

🅓 Continuously during every message


*Q9.* James's analogy: 'Skill = manual. CLAUDE.md = checklist. Keys = ____.'

🅐 The mcp-builder package

🅑 Starting Claude Code

🅒 The SOUL.md file

🅓 Running uv


*Q10.* Which transport is recommended for most production MCP servers in Chapter 57?

🅐 stdio — simplest, no running server needed

🅑 SSE — real-time streaming support

🅒 streamable-http stateless — network accessible, no session tracking, agent handles context

🅓 streamable-http stateful — sessions give server memory


*Q11.* Emma's 'shipping label' analogy describes which transport concept?

🅐 stdio — direct pipe between processes

🅑 SSE — server pushes updates

🅒 Stateless — every request carries everything the server needs

🅓 Stateful — server remembers past interactions


*Q12.* Which transport option locks you to the same machine only?

🅐 streamable-http

🅑 SSE

🅒 stdio

🅓 websocket


*Q13.* After choosing transport in Lesson 3, what should you add to CLAUDE.md?

🅐 The full server code template

🅑 'Use streamable-http stateless transport on port 8000'

🅒 The learner ID generation algorithm

🅓 A list of all tools you plan to build


*Q14.* In the Describe-Steer-Verify cycle, what happens in the 'Steer' phase?


🅐 Claude Code runs tests and starts the server

🅑 You review the spec and push back if it doesn't match requirements

🅒 You write the tool description yourself

🅓 Claude Code connects the server to OpenClaw


*Q15.* Why is the tool description the most important element of an MCP tool spec?

🅐 It determines the URL path of the tool

🅑 It sets the timeout duration for tool calls

🅒 The agent reads it to decide which tool to call when multiple tools are available

🅓 It configures return type validation


*Q16.* What does MCP Inspector do, and how do you launch it?

🅐 Validates CLAUDE.md — launched with: claude validate

🅑 Shows gateway logs — launched from OpenClaw dashboard

🅒 Lets you call tools one at a time and see inputs/outputs — launched with: npx @modelcontextprotocol/inspector

🅓 Checks security — launched with: openclaw mcp inspect


*Q17.* What does Claude Code do automatically during 'Build and Verify'?

🅐 Writes code only — you run tests and server yourself

🅑 Runs tests, starts server, makes real tool call, shuts down, reports results

🅒 Runs tests and starts server — you make the tool call manually

🅓 Connects to OpenClaw and sends a WhatsApp test message


*Q18.* What are the two commands to connect your server to OpenClaw and activate it?

🅐 openclaw mcp add tutorclaw ... then openclaw server reload

🅑 openclaw mcp set tutorclaw '{...}' then openclaw gateway restart

🅒 openclaw tools register ... then openclaw agent refresh

🅓 openclaw connect mcp ... then openclaw mcp activate


*Q19.* Why is a text response alone NOT proof that an MCP tool actually ran?

🅐 Text responses are delayed 30 seconds when tools are involved

🅑 The agent can fabricate a plausible answer from training data — tool badge is the proof

🅒 Text responses are encrypted and can't be verified

🅓 Gateway strips tool results before sending to WhatsApp


*Q20.* What causes silent connection failure when connecting to OpenClaw, and what is the only diagnostic?

🅐 Missing CLAUDE.md — check with: claude config verify

🅑 Single character off in URL (missing /mcp, wrong port) — gateway log is the only diagnostic

🅒 Wrong transport in SOUL.md — check with: openclaw mcp status

🅓 Server timeout over 5 seconds — check with: openclaw mcp ping


━━━━━━━━━━━━━━━━━━━━━━


*ANSWER KEY:*
Q1-B | Q2-B | Q3-C | Q4-C | Q5-B | Q6-C | Q7-B | Q8-C | Q9-B | Q10-C | Q11-C | Q12-C | Q13-B | Q14-B | Q15-C | Q16-C | Q17-B | Q18-B | Q19-B | Q20-B

