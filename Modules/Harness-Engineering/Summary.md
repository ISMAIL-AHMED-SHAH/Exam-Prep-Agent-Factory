# 🛡️ Harness Engineering: A Crash Course (Roman Urdu Notes)

> [!NOTE]
> **12 Concepts** • **6 Parts** • **GIAIC Agent Factory**
>
> Loop Engineering ne humein **bara loop (heartbeat, beats, maker-checker, spine)** samjhaya tha. Yeh chapter us loop ke **ek beat ke andar hone wali engineering** ko explain karta hai.
>
> Focus model par nahi, **model ke around bani reliability layer** par hai — jise **Harness** kehte hain.

---

# 📑 Table of Contents

- [Core Equation](#-core-equation)
- [Part 1 — The Box You Were Standing In](#part-1--the-box-you-were-standing-in)
- [Part 2 — Constrain](#part-2--constrain)
- [Part 3 — Inform](#part-3--inform)
- [Part 4 — Verify & Correct](#part-4--verify--correct)
- [Part 5 — A Complete Harness, Twice](#part-5--a-complete-harness-twice)
- [Part 6 — Staying the Engineer](#part-6--staying-the-engineer)
- [Dogfooding — This Book's Own Harness](#-dogfooding--this-books-own-harness)
- [One-Line Recap](#-one-line-recap)
- [Major Takeaways](#-major-takeaways)

---

# 🧠 Core Equation

> [!IMPORTANT]
>
> ## Agent = Model + Harness
>
> - **Model** provides intelligence.
> - **Harness** provides reliability, control, and safety.
>
> A powerful model without a good harness can still confidently make disastrous mistakes.

---

# Why Harness Exists

Imagine this situation:

```text
Delete test folder
        │
        ▼
Agent:
"Done ✅"
```

Reality:

```text
Tests deleted ❌
Nothing verified ❌
Agent still confident ❌
```

Problem model mein nahi tha.

Problem **Harness** ki missing verification layer thi.

---
<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/e25cdd2d-8e88-44e6-b4f0-386fa3b63b9e" />
---

# Part 1 — The Box You Were Standing In

## Concept 1 — What a Harness Is

Harness ke **4 essential components** hote hain.

| Component | Purpose |
|-----------|---------|
| 🔄 Agent Loop | Execution cycle |
| 🔧 Tool Interface | Agent kis tool ko kaise use kare |
| 📚 Context Management | Kya information available hai |
| 🛡 Control Mechanisms | Safety, permissions, verification |

---

### Car Analogy

```text
Model = Engine

Harness =
    Brakes
    Mirrors
    Dashboard
    Seatbelt
    Steering
```

Engine powerful ho sakta hai...

...lekin brakes ke bina dangerous hai.

---

> [!WARNING]
> **Compounding Failure**
>
> Agar har step **95% reliable** hai...
>
> Aur task mein **20 steps** hain...
>
> Final success sirf approximately **36%** reh jati hai.
>
> Isi liye Harness improvements coding benchmarks mein **10× tak gains** de sakti hain.

---

## Concept 2 — Inner Harness vs Outer Harness

Harness ke do layers hote hain.

| Inner Harness | Outer Harness |
|--------------|---------------|
| Model maker banata hai | Aap configure karte hain |
| Tool Calling | Permissions |
| Context Window | Hooks |
| Safety Training | Logs |
| Fixed | Customizable |

---


<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/629b720b-4a51-4b93-813a-26c02645ced8" />
---

> [!TIP]
> Agar problem yeh hai:
>
> - Agent kya jaanta hai
> - Agent kya kar sakta hai
> - Agent kaise verify hota hai
>
> To solution **Outer Harness** mein milega, prompt mein nahi.

---

## Concept 3 — The Five Verbs

Har Harness in **5 verbs** ke around design hota hai.

| Verb | Purpose |
|------|---------|
| 🛑 Constrain | Kya kar sakta hai limit karo |
| 📖 Inform | Zaroori knowledge do |
| ✅ Verify | Kaam prove karo |
| 🔄 Correct | Recover aur improve karo |
| 👨 Human | Escalate karo |

---

> [!IMPORTANT]
> **Guardrails hamesha Harness mein hone chahiye.**
>
> Prompt kabhi permanent security boundary nahi hota.

---
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/35aff50e-67f5-4135-8eaf-7b897c2af6a0" />
---

# Part 2 — Constrain

## Concept 4 — Permission Rules

Permissions teen types ki hoti hain.

| Permission | Meaning |
|------------|---------|
| ✅ Allow | Green Light |
| ❓ Ask | Doorbell |
| ⛔ Deny | Wall |

---

### Priority

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
> Permissions ko **frequency** se nahi...
>
> **Blast Radius** ke basis par design karo.

---

Money bhi ek constraint hai.

Examples

- Spend Caps
- Model Routing
- Daily Budget

---

> [!WARNING]
> Deny Rules sirf **text match** karti hain.
>
> Real protection **Sandbox** provide karta hai.

---

## Concept 5 — Sandboxes

Permission batata hai

> Agent **kya** kar sakta hai.

Sandbox batata hai

> Agent **kahan** kar sakta hai.

---

### Prompt Injection

Prompt ke andar hidden malicious instructions.

---

### Four Security Fences

| Fence | Purpose |
|-------|----------|
| 📂 Worktree | Working directory limit |
| 📁 Filesystem | File access |
| 🌐 Network | Internet control |
| 🌿 Branch | Git protection |

---

Main branch hamesha protected honi chahiye.

Unattended pushes sirf

```
claude/*
```

branches par.

---

> [!WARNING]
> ## Tool Poisoning
>
> Attack prompt mein nahi...
>
> Tool ki **description** ya **metadata** mein bhi chhupa ho sakta hai.
>
> ### Defense
>
> - MCP Allowlist
> - Version Pinning
> - Deny-by-default Network Egress

---

# Part 3 — Inform

## Concept 6 — Context Surfaces

Agent ko information 3 jagah se milti hai.

| Surface | Question |
|----------|----------|
| Rules File | Hamesha kya sach hai? |
| Skills | Yeh kaam kaise karna hai? |
| Connectors | Main kis system tak reach kar sakta hoon? |

---

### Triage

Agar agent ko kuch pata nahi tha...

To dekho missing knowledge kis surface mein honi chahiye.

```text
Rules File

or

Skill

or

Connector
```

---

## Concept 7 — AX (Agent Experience)

Reader insaan nahi...

Reader **Agent** hai.

Assume

- Mid-task hai
- Question nahi pooch sakta
- Bas available information use karega

---

### Three Findings

✅ Fewer tools are better

✅ Good descriptions matter

✅ Errors should explain the next action

(Self-Healing)

---

> [!WARNING]
> AX ka matlab context ke hisaab se different hota hai.
>
> - **Designing Agent Experiences** course → Human Experience
> - Industry AX → Agent Experience

---
<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/2c0fe42c-8b05-433e-a095-ba6e4114fba6" />
---

# Part 4 — Verify & Correct

## Concept 8 — Hooks

Difference

### Maker-Checker

Verification har beat ke end par.

### Hook

Verification continuously.

---

### Hook Types

| Hook | Purpose |
|------|----------|
| Before Action | Block kar sakta hai |
| After Action | Feedback de sakta hai |

---

Exit Codes

| Code | Meaning |
|------|----------|
| 0 | Pass |
| 2 | Block |

---

> [!IMPORTANT]
> "Done" ab model ka claim nahi...
>
> Harness ki **proven state** hai.

---

## Concept 9 — Typed Output

Harness sirf text nahi dekhta.

Structured JSON verdict expect karta hai.

Example

```json
{
  "passed": true,
  "reason": "...",
  "score": 98
}
```

---

Validation means

❌ Field exist karta hai

✔ Value bhi correct honi chahiye

---

> [!WARNING]
> Malformed JSON ko retry nahi karna.
>
> Seedha **Escalate** karo.

---

## Concept 10 — Correct

Correction ke do parts hain.

---

### Recovery

| Failure | Action |
|----------|---------|
| Transient | Retry + Limit |
| Hard Failure | Escalate / Reroute |
| Poisoned State | Restore Checkpoint / Git Commit |

---
<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/ac0571c2-0df8-418d-b880-5b6d6ce08511" />

---
### The Ratchet

Har mistake ko permanent Harness improvement mein convert karo.

```text
Mistake
    │
    ▼
Harness Change
    │
    ▼
Never Repeat
```

---
<img width="1448" height="1086" alt="image" src="https://github.com/user-attachments/assets/e2d96eb1-4768-48cc-bfb2-d7294879f49f" />
---

### Four Failure Classes

| Failure | Sign | Verb | Fix |
|----------|------|------|-----|
| Context | Pata nahi tha | Inform | Rules / Skill |
| Constraint | Nahi karna chahiye tha | Constrain | Permissions / Sandbox |
| Verification | Wrong work accepted | Verify | Hooks / Typed Output |
| Planning | Sahi pieces, wrong order | Structure | Smaller Tasks |

---

> [!WARNING]
> Harness ko bhi test karo.
>
> Har Harness change ke baad same benchmark tasks dobara run hone chahiye.

---

# Part 5 — A Complete Harness, Twice

## 8-Box Checklist

| Box | Purpose |
|------|----------|
| 🚫 Deny List | Forbidden actions |
| 🧱 Fence | Isolation |
| 🧰 Lean Tools | Minimal surface |
| 🪝 Blocking Hook | Verification |
| 📄 Typed Verdict | Structured proof |
| 👨 Escalation Path | Human review |
| 📊 Logging | Audit trail |
| ↩ Way Back | Recovery |

---

> [!IMPORTANT]
> Model same ho sakta hai...
>
> Lekin Harness decide karta hai
>
> - Leak hoga?
> - Block hoga?
> - Log hoga?
> - Human review tak jayega?

---

### Claude Code vs OpenCode

Same Harness.

Different owners.

| Claude Code | OpenCode |
|-------------|----------|
| Tool controls | Platform controls |
| Internal hooks | CI |
| Internal sandbox | Container |
| Internal Git | Platform Git |

Property same.

Address different.
---
<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/073ebbb1-0f06-4140-927f-eb0c63139c03" />

---

# Part 6 — Staying the Engineer

## Concept 11 — Observability

> [!IMPORTANT]
> Agar dekh nahi sakte...
>
> To effectively woh exist hi nahi karta.

---

### Three Habits

- Log everything
- Fail loudly
- Cost is a signal

---

## Concept 12 — Limits of the Harness

Harness bhi perfect nahi hota.

### Capability vs Control

Har naya rule...

Ek capability bhi remove karta hai.

---

### Harness Coupling

Contracts ke saath couple karo.

Behavior ke saath nahi.

---

### Rule Debt

Har 90 din baad review karo.

Unused rules remove kar do.

---

> [!WARNING]
> Apna custom Harness tab banao...
>
> Jab existing product ki boundaries aapki real requirements ko block kar rahi hon.

---

> [!NOTE]
> **Humans steer.**
>
> **Agents execute.**

---

# 🍽 Dogfooding — This Book's Own Harness

Book khud bhi Harness principles follow karti hai.

| Verb | Implementation |
|------|----------------|
| Constrain | claude/* branches |
| Inform | Style Rules File |
| Verify | Linters + Typed Verdict |
| Correct | Review → New Linter Rules |
| Escalate | Claims author ke paas |

---

> [!WARNING]
> Model ka **95 score** sirf ek claim hai.
>
> Human gate tak pohanchne ka decision Harness karta hai.

---

# 📝 One-Line Recap

| # | Summary |
|---|---------|
| 1 | Agent = Model + Harness |
| 2 | Harness ke 4 parts |
| 3 | Inner vs Outer Harness |
| 4 | Five Verbs |
| 5 | Allow / Ask / Deny |
| 6 | Four Security Fences |
| 7 | Rules Files, Skills, Connectors |
| 8 | AX (Agent Experience) |
| 9 | Hooks = Proven "Done" |
| 10 | Typed JSON Output |
| 11 | Recovery + Ratchet |
| 12 | 8-Box Harness Checklist |
| 13 | Observability + Harness Limits |

---

# 🎯 Major Takeaways

> [!IMPORTANT]
> A great model without a great Harness is still unreliable.

> [!TIP]
> Guardrails belong in the Harness, **not** in prompts.

> [!IMPORTANT]
> Verification should produce **proof**, not confidence.

> [!WARNING]
> Prompt Injection is only one attack. Tool Poisoning is another.

> [!TIP]
> Every failure should permanently improve the Harness (The Ratchet).

> [!NOTE]
> Reliability is engineered outside the model.

---

<div align="center">

# 🛡 Harness Engineering Notes

### 12 Concepts • 6 Parts • GIAIC Agent Factory

Made with ❤️ for the AI Builders Community

**From: Ismail Ahmed Shah | GIAIC 2026**

</div>
