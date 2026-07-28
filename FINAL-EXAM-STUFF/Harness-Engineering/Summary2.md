# 🛡️ Harness Engineering — Crash Course

> Final Exam Marathon • Part 1 of Advanced Agentic Coding

## 📖 Core Equation
`Agent = Model + Harness`. Model sirf intelligence deta hai. **Harness** woh layer hai jo us intelligence ko reliable banati hai. Loop Engineering ka 4-layer stack: `prompt → context → harness → loop`. Harness **ek beat ke andar** rehta hai.
<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/883910a3-416c-47d3-9b9b-debc927411be" />

---

## Part 1 — The Box You Were Standing In

### Concept 1 — Harness kya hai (4 zaroori parts)
**Agent loop** (engine), **Tool interface**, **Context management**, **Control mechanisms**. Claude Code aur OpenCode dono mein yeh chaaron parts hain.

> **Analogy:** Model = engine. Harness = poori gaadi (brakes, mirrors, seatbelt, dashboard).

> **⚠️ Going Deeper:** 95% per-step reliability pe, 20-step chain sirf ~36% waqt clean complete hoti hai. Harness poori chain pe attack karta hai.

### Concept 2 — Inner Harness vs Outer Harness
**Inner** = model maker banata hai (choose karo, edit nahi). **Outer** = aap configure/build karte ho (tools, permissions, hooks, logs).

> **Key Point:** "Prompt fix karoon ya rule?" — agar masla kya-kar-sakta-hai/kya-jaanta-hai/kaise-check-hota-hai se related hai, fix **outer harness** mein hai.

### Concept 3 — The Five Verbs
**Constrain, Inform, Verify, Correct, Escalate.**

> **⚠️ Sab se important line:** "Ek guardrail harness mein rehta hai, kabhi prompt mein nahi."

| Surface | Guide karta hai? | Mechanically enforce? |
|---|---|---|
| Prompt / rules file | Haan | Nahi |
| Permission deny rule | Haan | Haan (tool layer) |
| Sandbox / network fence | Haan | Haan (OS layer) |
| Hook (after action) | Haan | Sirf aage — undo nahi |
| Required CI + branch protection | Haan | Haan (merge pe) |

**Part 1 Recap:** Harness = loop + tools + context + controls. 5 verbs, aur guardrail hamesha harness mein.
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/84f046c4-ddbc-436a-9ee0-541e50f3cc8c" />

---
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/ba21437b-4a48-496d-b8cb-e6760b03dfad" />
---

## Part 2 — Constrain

### Concept 4 — Permission Rules: Allow, Ask, Deny
**Allow** = green light. **Ask** = doorbell. **Deny** = wall. Sort by **blast radius**, frequency se nahi.

> **Precedence:** Deny > Ask > Allow.

> **⚠️ Warning:** Deny patterns text match karte hain, meaning nahi — command deny rules tripwire hain, sandbox asal wall hai.

### Concept 5 — Sandboxes: Nuksaan Impossible Banana
4 fences: **Worktree, Filesystem fence, Network fence, Branch fence**. Prompt injection perfect rules ko bhi bypass kar sakti hai — sandbox model pe trust hi nahi karta.

> **⚠️ Tool Poisoning:** Attack tool ki description/metadata mein chupti hai. Defense: enforced MCP allowlist, version-pinned, deny-by-default egress.

**Part 2 Recap:** Constrain = Permission rules (blast-radius se sort) + Sandboxes (4 fences).

---

## Part 3 — Inform

### Concept 6 — Context Surfaces as Harness Parts
**Rules file** = hamesha kya sach hai. **Skills** = specific kaam kaise karna hai. **Connectors** = kya reach kar sakta hai.

> **Triage Rule:** always-true → rules file, task-specific → skill, reach → connector.

### Concept 7 — AX (Agent Experience)
3 findings: **Kam, focused tools**; **Tool descriptions asal kaam karti hain**; **Errors agla step batayein**.

> **Test:** "Kya ek competent ajnabi sirf yeh text dekh kar sahi agla step le sakta hai?"

**Part 3 Recap:** Rules file, Skills, Connectors — 3 alag sawal. AX = surfaces ko agent ke liye design karna.

---

## Part 4 — Verify & Correct

### Concept 8 — Hooks
Continuous verification. **Gate hooks** (PreToolUse/Stop) block kar sakti hain. **Post hooks** undo nahi kar sakti, error next turn mein feedback banta hai.

> **Key Point:** "Done" ab model ka claim nahi, harness ka proven state hai.

### Concept 9 — Typed Output
Fixed JSON shape maango, field-by-field validate karo (values, sirf presence nahi).

> **⚠️ Warning:** Malformed/unexpected verdict → escalate, guess/retry mat karo.
<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/f9c53847-31d3-4b08-b71c-7dee38032b69" />

### Concept 10 — Correct: Recovery + The Ratchet
**Recovery (fast):** Transient → retry+cap; Hard failure → skip/escalate; Poisoned state → checkpoint pe wapis.

**The Ratchet (slow):** har galti ko harness mein permanent fix banao.
<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/7ba9b98d-6e5b-4b27-b111-b0a0d2b4fbef" />


| Class | Sign | Verb | Fix kahan |
|---|---|---|---|
| Context | Usko pata nahi tha | Inform | Rules file/Skill/Tool desc |
| Constraint | Aisa kaam jo nahi karna chahiye tha | Constrain | Permission/Sandbox/Fence |
| Verification | Bura kaam "done" keh diya | Verify | Hook/CI/Typed output |
| Planning | Sahi pieces, galat order | Structure | Chhota task/Subagent/Caps |

**Part 4 Recap:** Hooks continuous verification. Typed output machine-checkable. Correct = recovery + ratchet.
<img width="1448" height="1086" alt="image" src="https://github.com/user-attachments/assets/5fffbf94-a402-453b-9276-cc6ca74119ed" />

---

## Part 5 — Complete Harness, Twice

### Minimum Safe Harness Checklist (8 Boxes)
Deny list • Fence • Lean tools • Blocking hook • Typed verdict • Escalation path • Log • Way back.

### The Bad Night — With and Without
Bina harness: .env leak, test delete, false PASS, PR merge. Harness ke saath: deny+fence block karte hain, typed reviewer catch karta hai, escalation "needs a human" mein le jaata hai.

> **⚠️ Key Insight:** Green suite proof nahi, evidence hai.

**Part 5 Recap:** 8 boxes, dono tools mein same property, alag owners.
<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/62344ad8-935e-4729-8296-6b8a748e5690" />

---

## Part 6 — Staying the Engineer

### Concept 11 — Observability
Dekh nahi sakte to hai hi nahi. 3 Habits: **log every beat**, **failure loud**, **cost as signal**.

### Concept 12 — Harness ki Limits
**Capability-Control trade-off, Harness Coupling, Rule Debt** — 3 forces jo endless tightening rokti hain.

> **⚠️ Closing:** "Humans steer. Agents execute." Harness = judgment made durable.

**Part 6 Recap:** Observability zaroori hai. 3 forces batati hain kab rukna hai.

---

*Ismail Ahmed Shah — GIAIC Final Exam Marathon 2026 · Full — Concepts 1–12 (Parts 1–6) complete*
