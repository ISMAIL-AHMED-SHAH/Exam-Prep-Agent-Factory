# 🛡️ Harness Engineering — Crash Course

> [!NOTE]
> **Final Exam Marathon** • **Advanced Agentic Coding**
>
> Yeh notes **Harness Engineering** ke **12 Concepts (Parts 1–6)** ko complete cover karte hain. Focus is baat par hai ke AI sirf intelligent hi nahi, **reliable, predictable aur safe** bhi ho.

---

# 📑 Table of Contents

- [Core Equation](#-core-equation)
- [Part 1 — The Box You Were Standing In](#part-1--the-box-you-were-standing-in)
- [Part 2 — Constrain](#part-2--constrain)
- [Part 3 — Inform](#part-3--inform)
- [Part 4 — Verify & Correct](#part-4--verify--correct)
- [Part 5 — Complete Harness, Twice](#part-5--complete-harness-twice)
- [Part 6 — Staying the Engineer](#part-6--staying-the-engineer)
- [One-Line Recap](#-one-line-recap)
- [Major Takeaways](#-major-takeaways)

---

# 🧠 Core Equation

```text
Agent = Model + Harness
```

| Component | Responsibility |
|-----------|----------------|
| 🤖 Model | Intelligence, reasoning |
| 🛡 Harness | Reliability, safety, control |

The complete engineering stack is:

```text
Prompt
   ↓
Context
   ↓
Harness
   ↓
Loop
```

> [!IMPORTANT]
> Loop Engineering ne poora loop explain kiya tha.
>
> **Harness Engineering ek single beat ke andar hone wali engineering ko explain karti hai.**

<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/f504f621-c90e-487a-b4a5-e4b7d22fd889" />

---

# Part 1 — The Box You Were Standing In

## Concept 1 — What is a Harness?

Har Harness ke **4 core components** hote hain.

| Component | Purpose |
|-----------|----------|
| 🔄 Agent Loop | Execution engine |
| 🔧 Tool Interface | Tools ko safely use karna |
| 📚 Context Management | Correct information dena |
| 🛡 Control Mechanisms | Rules, verification, safety |

Claude Code aur OpenCode dono isi architecture ko follow karte hain.

---

### 🚗 Car Analogy

```text
Model
   │
 Engine

Harness
   │
 Brakes
 Mirrors
 Dashboard
 Seatbelt
 Steering
```

Engine powerful ho sakta hai...

Lekin brakes ke bina dangerous hai.

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/105cd49e-ed72-4296-98fc-d12f1ae3fb1c" />

---

> [!WARNING]
> ## Compounding Failure
>
> Agar har step **95% reliable** hai...
>
> Aur workflow mein **20 steps** hain...
>
> Final success approximately **36%** reh jati hai.
>
> Harness poori chain ki reliability improve karta hai, sirf ek step ki nahi.

---

## Concept 2 — Inner vs Outer Harness

Harness ke do layers hote hain.

| Inner Harness | Outer Harness |
|--------------|---------------|
| Model maker build karta hai | Developer build karta hai |
| Tool calling | Permissions |
| Context window | Hooks |
| Safety training | Logs |
| Fixed | Customizable |

---

> [!TIP]
> Agar problem yeh ho:
>
> - Agent kya kar sakta hai
> - Agent kya jaanta hai
> - Agent kaise verify hota hai
>
> To solution **Outer Harness** mein hota hai, prompt mein nahi.

---

## Concept 3 — The Five Verbs

Har Harness in **5 verbs** ke around design hota hai.

| Verb | Responsibility |
|------|----------------|
| 🛑 Constrain | Limit actions |
| 📖 Inform | Correct knowledge provide karo |
| ✅ Verify | Proof generate karo |
| 🔄 Correct | Recover aur improve karo |
| 👨 Escalate | Human tak le jao |

---

> [!IMPORTANT]
> **Guardrails Harness mein rehte hain.**
>
> Prompt kabhi security boundary nahi hota.

---

## Enforcement Surfaces

| Surface | Guides Agent? | Mechanically Enforced? |
|---------|:-------------:|:----------------------:|
| Prompt / Rules File | ✅ | ❌ |
| Permission Rules | ✅ | ✅ Tool Layer |
| Sandbox / Network Fence | ✅ | ✅ Operating System |
| Post Hooks | ✅ | ⚠ Forward Only |
| CI + Branch Protection | ✅ | ✅ Merge Gate |

---

# 📌 Part 1 Recap

- Harness = Loop + Tools + Context + Controls
- Inner vs Outer Harness
- Five Verbs
- Guardrails belong in the Harness

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/b990be67-8f49-470f-bea8-32960366a61f" />

---

# Part 2 — Constrain

## Concept 4 — Permission Rules

Permissions teen categories ki hoti hain.

| Type | Meaning |
|------|----------|
| ✅ Allow | Green Light |
| ❓ Ask | Doorbell |
| ⛔ Deny | Wall |

Priority

```text
Deny
 ▲
Ask
 ▲
Allow
```

Always

```
Deny > Ask > Allow
```

---

> [!TIP]
> Rules ko **blast radius** ke hisaab se design karo...
>
> Frequency ke hisaab se nahi.

---

> [!WARNING]
> Deny Rules sirf **text** match karti hain.
>
> Actual protection **Sandbox** provide karta hai.

---

## Concept 5 — Sandboxes

Permissions decide karti hain

> Agent **kya** kar sakta hai.

Sandbox decide karta hai

> Agent **kahan** kar sakta hai.

---

### Four Security Fences

| Fence | Purpose |
|-------|----------|
| 📂 Worktree | Workspace isolation |
| 📁 Filesystem | File protection |
| 🌐 Network | Internet restriction |
| 🌿 Branch | Git safety |

---

### Tool Poisoning

Attack sirf prompt mein nahi hota...

Tool ki metadata ya description mein bhi ho sakta hai.

---

### Defence

- MCP Allowlist
- Version Pinning
- Deny-by-default Network Egress

---

> [!WARNING]
> Prompt Injection aur Tool Poisoning dono different attacks hain.

---

# 📌 Part 2 Recap

Constrain =

- Permission Rules
- Sandboxes
- Four Fences

---

# Part 3 — Inform

## Concept 6 — Context Surfaces

Agent ko information **3 different surfaces** se milti hai.

| Surface | Question |
|----------|----------|
| 📖 Rules File | Hamesha kya sach hai? |
| 🧰 Skills | Yeh kaam kaise karna hai? |
| 🔌 Connectors | Main kis system tak reach kar sakta hoon? |

---

### Triage Rule

| Situation | Correct Place |
|-----------|---------------|
| Always True | Rules File |
| Task Specific | Skill |
| External Access | Connector |

---

## Concept 7 — AX (Agent Experience)

Agent ke experience ko design karna bhi engineering hai.

### Three Findings

✅ Kam aur focused tools

✅ Good descriptions matter

✅ Errors next step batayen

(Self-Healing)

---

> [!TIP]
> Test:
>
> **"Kya ek competent ajnabi sirf yeh text dekh kar sahi agla step le sakta hai?"**

---

# 📌 Part 3 Recap

- Rules File
- Skills
- Connectors
- AX = Agent Experience

---

# Part 4 — Verify & Correct

## Concept 8 — Hooks

Hooks continuously verify karte hain.

| Hook | Purpose |
|------|----------|
| 🚦 Pre Hook | Block kar sakta hai |
| 🔄 Post Hook | Sirf feedback deta hai |

---

> [!IMPORTANT]
> "Done" ab model ka claim nahi...
>
> Harness ki **verified state** hai.
<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/324a7876-7283-4140-aa52-a1e03bb9121e" />

---

## Concept 9 — Typed Output

Harness structured JSON expect karta hai.

Example

```json
{
  "passed": true,
  "score": 98,
  "reason": "..."
}
```

Validation

- Fields exist
- Values valid

---

> [!WARNING]
> Malformed verdict ko retry mat karo.
>
> Seedha **Escalate** karo.

---

## Concept 10 — Correct

Correction ke do parts hote hain.

---

### Recovery

| Failure | Solution |
|----------|----------|
| Transient | Retry + Cap |
| Hard Failure | Skip / Escalate |
| Poisoned State | Restore Checkpoint |

---

### The Ratchet

```text
Mistake
   │
   ▼
Harness Improvement
   │
   ▼
Never Repeat
```

---

### Four Failure Classes

| Failure | Sign | Verb | Fix |
|----------|------|------|-----|
| Context | Pata nahi tha | Inform | Rules / Skills |
| Constraint | Wrong action | Constrain | Permission / Sandbox |
| Verification | False Done | Verify | Hooks / Typed Output |
| Planning | Wrong sequence | Structure | Smaller Tasks |

<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/41efadcd-5414-4f95-adb9-8720073bc843" />

---
<img width="1448" height="1086" alt="image" src="https://github.com/user-attachments/assets/9e18c892-ed45-401f-92b8-345dfd9bbdaa" />
---

# 📌 Part 4 Recap

- Hooks verify continuously
- Typed Output is machine-checkable
- Recovery fixes today
- Ratchet fixes forever

---

# Part 5 — Complete Harness, Twice

## Minimum Safe Harness (8 Boxes)

| Box | Purpose |
|------|----------|
| 🚫 Deny List | Forbidden Actions |
| 🧱 Fence | Isolation |
| 🧰 Lean Tools | Smaller Surface |
| 🪝 Blocking Hook | Verification |
| 📄 Typed Verdict | Machine Proof |
| 👨 Escalation Path | Human Review |
| 📊 Logging | Audit Trail |
| ↩ Recovery Path | Rollback |

---

## Without vs With Harness

### ❌ Without Harness

- .env leaked
- Tests deleted
- False PASS
- PR merged

---

### ✅ With Harness

- Deny Rule blocks
- Sandbox blocks
- Typed Reviewer catches issue
- Human escalation

---

> [!IMPORTANT]
> Green Test Suite is **evidence**...
>
> It is **not proof**.

---

# 📌 Part 5 Recap

- Same 8 boxes
- Different platforms
- Same engineering principles
- 
---
<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/b0db5529-b129-476c-80f2-12fe0d9ebb0b" />

---

# Part 6 — Staying the Engineer

## Concept 11 — Observability

> [!IMPORTANT]
> Agar dekh nahi sakte...
>
> To effectively woh exist hi nahi karta.

---

### Three Habits

- 📜 Log every beat
- 🚨 Fail loudly
- 💰 Cost is a signal

---

## Concept 12 — Limits of the Harness

Teen natural limits hamesha rahengi.

| Force | Meaning |
|--------|----------|
| Capability vs Control | Har rule kuch capability remove karta hai |
| Harness Coupling | Contracts se couple karo |
| Rule Debt | Purane rules regularly clean karo |

---

> [!WARNING]
> Over-engineering bhi problem ban sakti hai.

---

> [!NOTE]
> **Humans steer.**
>
> **Agents execute.**
>
> Harness insani judgment ko durable banata hai.

---

# 📝 One-Line Recap

| # | Summary |
|---|---------|
| 1 | Agent = Model + Harness |
| 2 | Harness has 4 components |
| 3 | Inner vs Outer Harness |
| 4 | Five Verbs |
| 5 | Enforcement Surfaces |
| 6 | Permission Rules |
| 7 | Four Sandboxes/Fences |
| 8 | Rules, Skills & Connectors |
| 9 | Agent Experience (AX) |
| 10 | Hooks & Verification |
| 11 | Typed Output |
| 12 | Recovery & Ratchet |
| 13 | 8-Box Harness |
| 14 | Observability |
| 15 | Harness Limits |

---

# 🎯 Major Takeaways

> [!IMPORTANT]
> Intelligence without Harness is unreliable.

> [!TIP]
> Guardrails belong in the Harness—not in prompts.

> [!IMPORTANT]
> Verification should produce **proof**, not confidence.

> [!WARNING]
> Prompt Injection and Tool Poisoning require different defences.

> [!TIP]
> Every failure should improve the Harness (The Ratchet).

> [!NOTE]
> Reliability is engineered **around** the model, not **inside** it.

---

<div align="center">

# 🛡 Harness Engineering Notes

### 12 Concepts • 6 Parts • GIAIC Agent Factory

**Built By Ismail Ahmed Shah | GIAIC 2026**

Made with ❤️ for the AI Builders Community

</div>
