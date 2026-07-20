# 🔧 Extend Your Claw with MCP

> **Deep Dive Chapter 57 · 5 Lessons · Agent Factory (Roman Urdu Notes)**

---

## 📖 Overview

In **Chapter 56**, aap ne kisi **aur developer ka MCP Server** connect kiya tha (Time Server).

Is chapter mein aap **apna khud ka MCP Server** build karte hain using the **`mcp-builder` Skill**, following the:

> **Describe → Steer → Verify**

development workflow.

---

## 🎯 Learning Objectives

After completing this chapter, you should be able to:

- ✅ Understand the difference between **Knowledge** and **Ability**
- ✅ Build your own MCP Server
- ✅ Use the official **mcp-builder** Skill
- ✅ Choose the correct MCP Transport
- ✅ Write better MCP Specifications
- ✅ Connect your server with OpenClaw
- ✅ Debug MCP connection problems

---

# 📑 Table of Contents

- [Lesson 1 — Your Agent Needs Hands](#lesson-1--your-agent-needs-hands)
- [Lesson 2 — Set Up the Workshop](#lesson-2--set-up-the-workshop)
- [Lesson 3 — Choose Your Wire](#lesson-3--choose-your-wire)
- [Lesson 4 — Spec and Build Your First Tool](#lesson-4--spec-and-build-your-first-tool)
- [Lesson 5 — Connect and Test from WhatsApp](#lesson-5--connect-and-test-from-whatsapp)
- [Quick Revision](#-quick-revision)

---
> [!NOTE]
> 📄 **Reference PDF**
>
> This lesson is based on the official MCP Blueprint.
>
> **Download / View PDF:** [📥 The MCP Blueprint](PDFs/the-mcp-blueprint.pdf)
---

# Lesson 1 — Your Agent Needs Hands

## 📖 Summary

Training data AI ko **knowledge** deti hai.

MCP tools AI ko **real-world abilities** dete hain.

Without tools, AI sirf explain karta hai.

With MCP, AI **actual action** perform karta hai.

---

## 💡 Core Idea

> **Knowledge tells.**
>
> **Tools do.**

---

## 📊 Knowledge vs Ability

| Knowledge | Ability |
|-----------|----------|
| Training Data | External Tool |
| Knows timezones | Knows current time |
| Static | Live |
| Can explain | Can perform |

---

> [!IMPORTANT]
> Chahe training data kitni bhi achi ho,
> **live external tools ki jagah kabhi nahi le sakti.**

---

## 👨‍💻 Producer vs Consumer

| Consumer | Producer |
|-----------|-----------|
| Existing MCP Server use karta hai | Apna MCP Server banata hai |
| Configuration | Design |
| JSON + Restart | Tool Architecture |

---

## 🛠️ Skill-Driven Build Pattern

```text
Install Skill
      ↓
Configure CLAUDE.md
      ↓
Describe Tool
      ↓
Claude Code Builds
      ↓
You Verify
```

---

> [!TIP]
>
> Skill ko ek licensed specialist samjho.
>
> General AI har cheez thori si jaanta hai.
>
> Skill kisi ek domain ka expert hota hai.

---

## ⭐ Key Takeaways

- Knowledge ≠ Ability
- Tools real work karte hain
- Producer aur Consumer alag roles hain
- Skill development workflow follow karo

---

# Lesson 2 — Set Up the Workshop

## 📖 Summary

Apna MCP Server banane ke liye sirf teen basic cheezein chahiye.

---

## 📂 Workshop Structure

| Component | Purpose |
|-----------|----------|
| Empty Folder | MCP Project |
| mcp-builder Skill | Domain Expertise |
| CLAUDE.md | Project Rules |

---

## 🛠️ Installation

```bash
mkdir tutorclaw-mcp
```

```bash
npx skills add ... --skill mcp-builder
```

---

## 📄 CLAUDE.md Rules

- Use mcp-builder Skill
- Use uv
- Spec-first Development

---

> [!WARNING]
> Skills session start hone par load hoti hain.

Agar Skill ignore ho rahi ho:

- Start a new session

---

## 🌍 Language Choice

| Language | Framework |
|----------|-----------|
| Python | FastMCP |
| TypeScript | MCP SDK |

✅ Dono officially supported hain.

---

## ⭐ Key Takeaways

- Empty directory se shuru karo
- Official Skill install karo
- CLAUDE.md rules likho
- Ek hi language stick karo

---

# Lesson 3 — Choose Your Wire

## 📖 Summary

Transport select karna architecture decision hai.

---

## ❓ Three Questions

1. Laptop only ya Anywhere?

2. Session tracking chahiye?

3. Agent yaad rakhe ya Server?

---

## 📊 Decision

| Requirement | Choice |
|-------------|--------|
| Anywhere | ✅ Streamable HTTP |
| No Session | ✅ Stateless |
| Agent Memory | ✅ Stateless |

---

## 📦 Stateless Analogy

Stateless request:

📦 Shipping Label

Har package apni information khud carry karta hai.

---

## 📌 Stateful vs Stateless

| Stateful | Stateless |
|-----------|------------|
| Server remembers | Request remembers |
| Complex | Simple |
| Session Cleanup | No Cleanup |

---

> [!TIP]
> Most MCP Tool Servers ke liye
>
> **Stateless** best choice hota hai.

---

> [!WARNING]
> Stateless har jagah best nahi.

Multi-step workflows ke liye Stateful bhi useful hai.

---

## 📝 CLAUDE.md Rule

```text
Use streamable-http stateless transport on port 8000
```

---

## ⭐ Key Takeaways

- Pehle requirements samjho
- Stateless default choice hai
- Transport decision CLAUDE.md mein document karo

---

# Lesson 4 — Spec and Build Your First Tool

## 📖 Summary

Claude Code implementation karta hai.

Aap specifications likhte ho.

---

## 🎯 Describe

Sirf batana hai:

- Kya banana hai

Nahi batana:

- Kaise banana hai

---

## 📋 Specification

Good Spec includes:

| Field | Importance |
|-------|-------------|
| Tool Name | High |
| Description | ⭐ Highest |
| Inputs | High |
| Outputs | High |

---

> [!IMPORTANT]
> Tool Description sab se important field hai.

Ye decide karti hai ke model tool kab use karega.

---

## 🔄 Describe → Steer → Verify

```text
Describe
     ↓
Steer
     ↓
Verify
```

---

## 🧪 Build Process

Claude Code automatically:

- Writes Code
- Runs Tests
- Starts Server
- Calls Tool
- Verifies Result
- Stops Server

---

> [!TIP]
> Specification contract nahi.

Review karo.

Improve karo.

Questions poochho.

---

## ⭐ Key Takeaways

- Focus on WHAT
- Claude handles HOW
- Tool Description is everything
- Specification evolves through steering

---

# Lesson 5 — Connect and Test from WhatsApp

## 📖 Summary

Ab MCP Server ko OpenClaw ke saath connect karna hai.

---

## 🔌 Connection Commands

```bash
openclaw mcp set tutorclaw '{"url":"http://localhost:8000/mcp","transport":"streamable-http"}'
```

```bash
openclaw gateway restart
```

---

> [!WARNING]
> Ek character bhi galat URL

ya

Gateway Restart miss

=

Silent Failure

---

## ✅ Verification

Wrong verification:

❌ WhatsApp reply dekhna

Correct verification:

✅ Dashboard Tool Badge

---

## 🔍 Diagnostic Checklist

1. Server running?
2. URL correct?
3. Gateway restarted?
4. Gateway Logs checked?

---

> [!IMPORTANT]
> Dashboard Tool Badge hi actual proof hai.

Chat response kabhi kabhi hallucinate bhi ho sakti hai.

---

## ⭐ Key Takeaways

- Same commands, different URL
- Restart zaroori hai
- Dashboard > Chat Response
- Logs are the source of truth

---

# 📌 Quick Revision

| Lesson | Main Idea |
|---------|-----------|
| Lesson 1 | Knowledge vs Ability |
| Lesson 2 | Workshop Setup |
| Lesson 3 | Transport Selection |
| Lesson 4 | Specification First |
| Lesson 5 | Connect & Verify |

---

# 📝 One-Line Recap

1. Knowledge explains, tools perform.
2. Producers build MCP Servers; consumers use them.
3. Build workflow = Install → Configure → Describe → Build → Verify.
4. Workshop = Empty Folder + mcp-builder Skill + CLAUDE.md.
5. Python and TypeScript are both supported.
6. Streamable HTTP + Stateless is the recommended default.
7. Choose Stateful only when workflows require memory.
8. Record transport decisions inside CLAUDE.md.
9. Describe **what**, not **how**.
10. Tool Description is the most important part of the specification.
11. Steering improves the specification before implementation.
12. Claude Code automatically builds, tests, and verifies tools.
13. Describe → Steer → Verify is the complete development cycle.
14. Connecting an MCP Server uses the same commands with a different URL.
15. Dashboard Tool Badge is the real proof—not the chat response.

---

# 💡 Exam Tips

> [!TIP]
> Remember these high-frequency concepts:
>
> - Knowledge vs Ability
> - Producer vs Consumer
> - Skill-Driven Build Pattern
> - Streamable HTTP
> - Stateless vs Stateful
> - Describe → Steer → Verify
> - Tool Description
> - Dashboard Tool Badge
> - Silent Failure
> - Gateway Logs

---

<div align="center">

## 📚 Agent Factory Notes

**Deep Dive Chapter 57 • Extend Your Claw with MCP**

Made with ❤️ for GIAIC Students

</div>
