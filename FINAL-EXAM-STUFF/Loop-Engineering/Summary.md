# 🔁 Loop Engineering — Crash Course

> [!NOTE]
> **Final Exam Marathon** • **Advanced Agentic Coding** • **Complete Pass**
>
> **Concepts 1–15 (Part 1–6)** + **Interludes**

---

# 📑 Table of Contents

- [Core Metaphor](#-core-metaphor)
- [Part 1 — The Shift](#part-1--the-shift-prompting-se-looping-tak)
- [Part 2 — The Heartbeat](#part-2--the-heartbeat-loop-kab-chalta-hai)
- [Part 3 — The Body](#part-3--the-body-loop-kya-kaam-karta-hai)
- [Part 4 — The Spine](#part-4--the-spine-loop-kya-yaad-rakhta-hai)
- [Part 5 — Worked Example](#part-5--complete-worked-example)
- [Part 6 — Staying the Engineer](#part-6--staying-the-engineer)
- [Practice / Appendix](#practice--appendix-summary)
- [One-Line Recap](#-one-line-recap)
- [Major Takeaways](#-major-takeaways)

---

# 🧠 Core Metaphor

```text
Heartbeat → Body → Spine
```

| Component | Meaning |
|-----------|----------|
| ❤️ Heartbeat | Loop kab chalta hai |
| 💪 Body | Loop kya karta hai |
| 🧠 Spine | Loop kya yaad rakhta hai |

> [!IMPORTANT]
> Agent Loop = **Heartbeat + Body + Spine**

Yeh system bina manual prompting ke **autonomously repeat hota hai**.

---

# Part 1 — The Shift: Prompting se Looping tak

## Concept 1 — Prompting vs Looping

### Prompting

```text
Prompt → Answer → Prompt → Answer
```

- Har step pe human chahiye
- One-time execution

---

<img width="3200" height="1840" alt="image" src="https://github.com/user-attachments/assets/67ea074c-7017-4635-95de-668b71164021" />
---

### Looping

```text
Trigger → Run → Action → Wait → Repeat
```

- Ek dafa setup
- Automatically repeat hota hai

---

> [!IMPORTANT]
> Loop Engineering AI ko **One-shot Assistant** se **Standing System** banati hai.

---

## Concept 2 — Loop ke 6 Components

| Component | Role |
|-----------|------|
| 🚀 Trigger | Start condition |
| 📚 Context | Knowledge |
| 🤖 Model | Reasoning |
| 🔧 Tools | Capabilities |
| 📤 Output | Result |
| 💾 Memory | State |

---

> [!TIP]
> Har automation design karte waqt pehle in 6 parts ko identify karo.

---
<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/c83b0088-bf47-423d-a1dd-5731377001ce" />
---

## Concept 3 — Small vs Big Loop

| Type | Meaning |
|------|----------|
| Small Loop | Single-purpose automation |
| Big Loop | Multiple loops combined |

---

### Tools

- Claude Code
- OpenCode

---
<img width="1614" height="975" alt="image" src="https://github.com/user-attachments/assets/bfd9e0f2-cfbb-4084-9641-f7fd5e082a59" />

---

> [!NOTE]
> Tools change ho sakte hain, structure nahi.

---

# 📌 Part 1 Recap

- Prompting = manual
- Looping = automated
- 6-part structure universal

---

# Part 2 — The Heartbeat: Loop kab chalta hai

## Concept 4 — In-session Loop

```text
/loop
```

- Session ke andar run karta hai
- Session band → loop band

---

## Concept 5 — Conditional Loop (/goal)

```text
Run until DONE
```

---

> [!WARNING]
> "Done" clear define nahi hoga to:
>
> - Infinite loop
> - Premature stop

---

## Concept 6 — Scheduled Heartbeat

| Type | Timing | Use |
|------|--------|-----|
| Interval | Every X time | Monitoring |
| Cron | Exact time | Reports |

---

> [!WARNING]
> Interval ≠ exact timing  
> Exact ke liye Cron use karo

---

## Concept 7 — Event-driven Heartbeat

```text
Event → Trigger → Run
```

Examples

- GitHub Action
- Webhook
- Message

---

> [!IMPORTANT]
> Event-driven = **kya hua**  
> Scheduled = **kab hua**
---
<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/0b27dab4-8b51-4009-a840-08fc9866da46" />

---

# 📌 Part 2 Recap

4 types of heartbeat

- In-session
- Goal-based
- Scheduled
- Event-driven

---

# Part 3 — The Body: Loop kya kaam karta hai

## Concept 8 — Worktrees (Isolation)

Parallel execution ke liye alag workspace zaroori.

---

> [!WARNING]
> Without isolation:
>
> - Race conditions
> - Conflicts
> - Overwrites

---

## Concept 9 — Skills (Knowledge)

Reusable instructions

> "Kaise karna hai"

---

## Concept 10 — Connectors / MCP

External systems access

> "Kaam karne ki power"

---

| Skills | Connectors |
|--------|-----------|
| Knowledge | Action |

---

## Concept 11 — Maker–Checker

```text
Maker → Work
Checker → Verify
```

---

> [!WARNING]
> Same context = fake verification

---

# 🔄 Interlude A — Dynamic Workflows

Agent khud decide karta hai steps.

---

# 🔄 Interlude B — Verification Skills

Verification bhi reusable honi chahiye.

---

# 📌 Part 3 Recap

- Worktrees = isolation
- Skills = knowledge
- Connectors = action
- Maker–Checker = reliability

---

# Part 4 — The Spine: Loop kya yaad rakhta hai

## Concept 12 — State / Memory

Model har run ke baad sab bhool jata hai.

Solution:

```text
progress.md (disk state)
```

---

### Flow

```text
Heartbeat
   ↓
Read Spine
   ↓
Execute
   ↓
Update Spine
```

---

> [!IMPORTANT]
> Cloud runs stateless hote hain  
> Spine repo mein hona chahiye

---

### Exam Scenario

Problem:

> Loop roz chalta hai lekin progress yaad nahi

Answer:

> Missing **Spine (state/memory)**

---

## Concept 13 — Cost by Cadence

Daily run limits exist karte hain.

Example

```text
Task1 (1)
Task2 (1)
PR Reviews (4)
---------
Total = 6 runs
```

---

> [!WARNING]
> Agar plan limit 5 hai → 1 extra run fail hoga

---

### Solutions

- Merge tasks
- Upgrade plan
- Buy extra usage

---

> [!IMPORTANT]
> Frequency × Cost = Total Usage

---

# 📌 Part 4 Recap

- Spine = persistent memory
- Cadence = cost multiplier

---

# Part 5 — Complete Worked Example

## Morning Triage Loop

```text
9 AM Trigger
   ↓
Read progress.md
   ↓
Find Issues
   ↓
Worktree Fix
   ↓
Skill Apply
   ↓
Checker Review
   ↓
PR via Connector
   ↓
Update Spine
```

---

> [!IMPORTANT]
> Yeh ek complete loop ka real-world blueprint hai

---

## Checker Design

Rubric + Score + Threshold

Example

```text
Score ≥ 95 → PASS
Score < 95 → Continue
```

---

> [!WARNING]
> Model score claim hota hai  
> Proof nahi

---

# 📌 Part 5 Recap

- All concepts integrate
- Checker defines stopping condition
---
<img width="1448" height="1086" alt="image" src="https://github.com/user-attachments/assets/a754bf75-6399-4f9e-98e6-2372dab932ea" />

---

# Part 6 — Staying the Engineer

## Concept 14 — Human Gate

Sensitive actions always gated

- Deployments
- Financial actions
- Destructive ops
- External messages

---

> [!IMPORTANT]
> Unsafe automation ≠ automation  
> Human gate zaroori hai

---

## Concept 15 — Traps

### 1. Comprehension Debt

System chal raha hai  
Aap samajh nahi rahe

---

### 2. Cognitive Surrender

Agent ki baat blindly accept karna

---

### 3. Cost per Accepted Change

```text
10 outputs
↓
6 reject
↓
Inefficient loop
```

---

> [!WARNING]
> **Ralph Wiggum Failure Mode**
>
> Agent jaldi "Done" bol deta hai
>
> Solution:
>
> Deterministic validation (not self-report)

---

# 📌 Part 6 Recap

- Human gate critical
- Traps avoid karna zaroori
---
<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/ce68f024-6b5b-4b75-8bf4-1feb2077e664" />

---

# 🧪 Practice / Appendix (Summary)

- Tool setup
- Scheduling syntax
- Dogfooding exercises

> [!NOTE]
> Yeh MCQ-testable nahi, practical section hai

---
<img width="1597" height="985" alt="image" src="https://github.com/user-attachments/assets/1acfe101-2c68-4e8e-8116-2f89b2813b58" />

---

# 📝 One-Line Recap

| # | Summary |
|---|---------|
| 1 | Loop = Heartbeat + Body + Spine |
| 2 | Prompting vs Looping |
| 3 | 6 Core Components |
| 4 | Small vs Big Loop |
| 5 | 4 Heartbeat Types |
| 6 | Worktrees for Isolation |
| 7 | Skills vs Connectors |
| 8 | Maker–Checker Model |
| 9 | Dynamic Workflows |
| 10 | Verification Skills |
| 11 | Spine = Memory |
| 12 | Cost by Cadence |
| 13 | Real Loop Example |
| 14 | Human Gate |
| 15 | Common Traps |

---

# 🎯 Major Takeaways

> [!IMPORTANT]
> Looping builds **systems**, not just answers.

> [!TIP]
> Always define:
>
> - Trigger
> - State
> - Verification

> [!WARNING]
> Undefined "Done" = broken loop

> [!IMPORTANT]
> Memory must live outside the model

> [!WARNING]
> Self-verification is unreliable

> [!TIP]
> Every loop needs:
>
> - Isolation
> - Verification
> - Persistence

---



<div align="center">

# 🔁 Loop Engineering Notes

### 15 Concepts • 6 Parts • GIAIC Agent Factory Loop Engineering

**GIAIC Final Exam Marathon 2026 · Loop Engineering**

**Built By Ismail Ahmed Shah | GIAIC 2026**

Made with ❤️ for the AI Builders Community

</div>
