# 🎓 Building TutorClaw — 

> [!NOTE]
> **Deep Dive Chapter 58** • **21 Lessons** • **6 Phases** • **The AI Agent Factory**
>
> Yeh chapter Chapter 57 ka continuation hai. Chapter 57 mein hum ne ek MCP Tool banaya tha, jabke is chapter mein usi knowledge ko use karke **TutorClaw** naam ka ek complete production-ready AI Tutor build kiya jata hai.

---

## 📑 Table of Contents

- [Overview](#-overview)
- [Phase 1 — Blueprint](#phase-1--blueprint-l1-l2)
- [Phase 2 — Local Build](#phase-2--local-build-l3-l8)
- [Phase 3 — The Harness](#phase-3--the-harness-l9-l12)
- [Phase 4 — Monetize](#phase-4--monetize-l13-l15)
- [Phase 5 — Identity and Polish](#phase-5--identity-and-polish-l16-l19)
- [Phase 6 — Reflect and Ship](#phase-6--reflect-and-ship-l20-l21)
- [21 Lessons Quick Recap](#-21-lessons-quick-recap)
- [Major Takeaways](#-major-takeaways)

---

# 📖 Overview

TutorClaw ek **9-tool AI Tutor** hai jo completely local architecture par chal sakta hai.

### Architecture

```text
            User
              │
              ▼
      OpenClaw Infrastructure
              │
              ▼
         Shim Skill (~50 lines)
              │
              ▼
         MCP Server (Your IP)
              │
   ┌──────────┼──────────┐
   ▼          ▼          ▼
State      Content    Pedagogy
```

### Tool Categories

| Category | Tools |
|----------|-------|
| 🗂 State | register_learner, get_learner_state, update_progress |
| 📚 Content | get_chapter_content, get_exercises |
| 🎯 Pedagogy | generate_guidance, assess_response |
| 💻 Code | submit_code |
| 💳 Monetization | get_upgrade_url |

---

# Phase 1 — Blueprint (L1-L2)

## Lesson 1 — The Application Blueprint

Architecture consists of only **two components**:

- MCP Server
- Shim Skill

> [!IMPORTANT]
> **Platform Inversion**
>
> Learner OpenClaw ka infrastructure use karta hai (Compute, WhatsApp, Agent Loop).
>
> Aap sirf:
>
> - Content
> - Pedagogy
> - Branding
>
> provide karte ho.

> [!TIP]
> MCP Boundary hi aap ki **Intellectual Property (IP)** ki boundary hoti hai.

---

## Lesson 2 — Designing the Tool Surface

Har MCP Tool ka contract:

| Part | Description |
|------|-------------|
| Name | Tool name |
| Description | Tool ka purpose |
| Inputs | Required parameters |
| Outputs | Expected response |
| Tier | Free / Gated |

### Resource Types

| Resource | Notes |
|----------|-------|
| JSON State | Single Point of Failure |
| Content Directory | Markdown Chapters |
| Mock Sandbox | Code Execution |
| Stripe API | Payments |

---

# Phase 2 — Local Build (L3-L8)

## Lesson 3 — Build the State Tools

State database ki jagah **JSON Files** use hoti hain.

✅ Restart Test

```text
Register
    ↓
Stop Server
    ↓
Restart
    ↓
Data should still exist
```

---

## Lesson 4 — Build the Content Tools

Content stored as

- Markdown Chapters
- JSON Exercises

Free Tier:

```
Chapter 1 → Chapter 5
```

Paid Tier:

```
Everything
```

---

## Lesson 5 — Build the Pedagogy Tools

### PRIMM-Lite

```text
Predict
   ↓
Run
   ↓
Investigate
```

generate_guidance uses two different contexts:

| Parameter | Purpose |
|-----------|----------|
| content | Learner context |
| system_prompt_addition | Agent behavior |

> [!TIP]
> Yeh separation AI behavior ko kaafi flexible bana deta hai.

---

## Lesson 6 — Build Code & Upgrade Tools

### submit_code

Mock Sandbox

- subprocess
- timeout
- blocked imports

### get_upgrade_url

Mock Stripe placeholder.

> [!WARNING]
> `"MOCK: Replace in Lesson 14"` comment zaroor likhein.
>
> Warna production mein mock hi reh jata hai.

---

## Lesson 7 — Full Cycle Test

Complete integration test using all **9 tools**.

Common failures

- Wrong state key
- Empty content directory
- Capitalization mismatch

---

## Lesson 8 — Expected vs Actual

Workflow

```text
Acceptance Criteria
        ↓
Run Tests
        ↓
Compare Results
        ↓
Grade Gaps
```

Tool badges

| Badge | Meaning |
|-------|----------|
| Single | One Tool |
| Multiple | Tool Chain |
| None | Possible Hallucination |

---

# Phase 3 — The Harness (L9-L12)

## Lesson 9 — Agent Instruction Manual

AGENTS.md works like an employee handbook.

Contains

- Session Start Protocol
- Tutoring Flow
- Tool Selection Rules
- Error Handling

---

## Lesson 10 — Context Engineer Your Tools

Tool descriptions have **two layers**.

### Layer 1

One precise sentence.

### Layer 2

- WHEN to call
- NEVER call

> [!IMPORTANT]
> Elimination-based tool selection AI ko significantly fast banati hai.

> [!WARNING]
> Emma ka product sirf **one-line descriptions** ki wajah se 2 mahine mein fail ho gaya.

---

## Lesson 11 — Test Suite

Design test matrix first.

Test Categories

- Valid Input
- Invalid Input
- Tier Gating
- State Persistence

Total

- 24+ Tests
- 5 Test Files

---

## Lesson 12 — All Tests Green

Debug Loop

```text
Assertion
    ↓
Describe
    ↓
Run
    ↓
Repeat
```

> [!IMPORTANT]
> Tests implementation ko nahi,
>
> **behavior verify karti hain.**

---

# Phase 4 — Monetize (L13-L15)

## Lesson 13 — Tier Gating

Single Source of Truth

```python
check_tier()
```

Controls

- Tier
- Daily Exchanges

Free users

```
50 Exchanges / Day
```

---

## Lesson 14 — Stripe Checkout

Cash Register Analogy

| Secret | Direction |
|---------|-----------|
| API Key | Outbound |
| Webhook Secret | Inbound |

> [!IMPORTANT]
> Sirf Checkout URL enough nahi hota.
>
> **Webhook hi actual payment confirmation hota hai.**

Stripe Test Card

```
4242 4242 4242 4242
```

---

## Lesson 15 — Test Payment Flow

```text
Paywall
    ↓
Checkout
    ↓
Payment
    ↓
Webhook
    ↓
Upgrade Tier
    ↓
Unlock Content
```

> [!TIP]
> Stripe API ko tests mein mock kiya jata hai.

---

# Phase 5 — Identity and Polish (L16-L19)

## Lesson 16 — Shim Skill

Server down hone par tutor generic chatbot ban sakta hai.

Shim sirf support karta hai

- PRIMM-Lite
- Chapters 1–5

Shim support **nahi** karta

- Progress
- Personalization
- Code Execution
- Chapter 6+

> [!WARNING]
> **Degraded-but-functional** hamesha **generic assistant** se better hota hai.

---

## Lesson 17 — Dedicated Agent

Three files define the personality.

| File | Responsibility |
|------|----------------|
| AGENTS.md | WHAT |
| SOUL.md | WHO |
| IDENTITY.md | HOW |

> [!TIP]
> Frustration handler sab se important behavior hota hai.

---

## Lesson 18 — Route and Bind

Keyword matching unreliable hoti hai.

Priority Order

```text
Peer Match
      ↓
Account Match
      ↓
Channel Match
      ↓
Default
```

Dedicated WhatsApp Group best solution hai.

---

## Lesson 19 — Harden & Polish

Three common failures

- Crash
- Confusing Error
- Silent Success

Structured Logs

- Timestamp
- Tool Name
- Learner ID
- Parameters
- Status
- Duration

> [!WARNING]
> Har user ek edge-case generator hota hai.

---

# Phase 6 — Reflect and Ship (L20-L21)

## Lesson 20 — Publish to ClawHub

### Publish

- MCP Config
- Shim Skill
- SOUL.md
- IDENTITY.md
- AGENTS.md

### Keep Private

- Server Code
- JSON Database
- Content Files
- Stripe Keys

> [!IMPORTANT]
> Publish **map**, not the **treasure**.

---

## Lesson 21 — Full Engine

### 7-Level Verification Ladder

```text
Tool Isolation
      ↓
Tools Together
      ↓
Correct Selection
      ↓
Edge Cases
      ↓
Makes Money
      ↓
Has Identity
      ↓
Graceful Degradation
```

> [!IMPORTANT]
> Tests contract verify karti hain.
>
> Implementation badal sakti hai (JSON → PostgreSQL), lekin agar interface same hai to tests bhi same rahenge.

---

# 📝 21 Lessons Quick Recap

| # | Summary |
|---|---------|
| 1 | Blueprint & Platform Inversion |
| 2 | Tool Surface Design |
| 3 | JSON State Tools |
| 4 | Content Tools |
| 5 | PRIMM-Lite Pedagogy |
| 6 | Mock Sandbox & Stripe |
| 7 | Full Integration Test |
| 8 | Expected vs Actual |
| 9 | AGENTS.md |
| 10 | Context Engineering |
| 11 | Test Matrix |
| 12 | Behavior-Based Testing |
| 13 | Tier Gating |
| 14 | Stripe Checkout |
| 15 | Payment Flow |
| 16 | Shim Skill |
| 17 | Dedicated Agent |
| 18 | Route & Bind |
| 19 | Hardening |
| 20 | ClawHub Publishing |
| 21 | Verification Ladder |

---

# 🎯 Major Takeaways

> [!TIP]
> Build **contracts**, not implementations.

> [!IMPORTANT]
> MCP Boundary = IP Boundary.

> [!TIP]
> Tests should verify **behavior**, not storage.

> [!WARNING]
> Never ship mock code without clearly marking it.

> [!NOTE]
> Graceful degradation is a feature, not a failure.

---

<div align="center">

# 📚 Agent Factory Notes

### Deep Dive Chapter 58 • Extend Your Claw with MCP

Made with ❤️ for **GIAIC Students**

</div>
