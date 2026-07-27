# 🔁 Loop Engineering — Crash Course

> Final Exam Marathon • Part 1 of Advanced Agentic Coding
> ✅ **Complete Pass:** Yeh notes ab sare 15 Concepts (Part 1–6) cover karte hain.

## 📖 Core Metaphor
Loop = **Heartbeat** (kab chalta hai) + **Body** (kya kaam karta hai) + **Spine** (kya yaad rakhta hai). Yeh teeno mil kar ek "agent loop" banate hain jo bina insaan ke baar baar prompt kiye khud chalta rehta hai.

---

## Part 1 — The Shift: Prompting se Looping tak

### Concept 1 — Prompting vs Looping
Purana tareeqa: prompt likho, jawab lo, dobara prompt karo — **prompting**, har step pe insaan chahiye.
**Looping** mein ek dafa system set karo jo khud-b-khud repeat hota hai — trigger fires, agent kaam karta hai, result milta hai, phir agla trigger wait karta hai.

> **Key Point:** Loop Engineering = AI ko "one-shot assistant" se "standing system" mein badalna.
> 
> <img width="3200" height="1840" alt="image" src="https://github.com/user-attachments/assets/99254873-18b3-4a98-84eb-e6572d81c48e" />

---
### Concept 2 — Loop kis se banta hai (6 parts)
Har loop mein: **Trigger**, **Context**, **Model**, **Tools**, **Output/Action**, **Memory/State**.

> **Key Point:** Naya automation banate waqt in 6 parts ko explicitly identify karo.
>
> <img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/2a58a410-e6fc-4ff1-8e6b-6094c6baf0cb" />

---
### Concept 3 — Small Loop vs Big Loop, do tools
**Small loop** = ek chhota single-purpose automation. **Big loop** = multiple small loops mil kar pura workflow.
Course do tools dikhata hai: **Claude Code** (Anthropic CLI agent) aur **OpenCode** (open-source alternative).

> **Key Point:** Tool badal sakta hai, 6-part structure universal rehta hai.

**Part 1 Recap:** Prompting ek-baari, looping repeat. Har loop 6 parts se milta hai. Small loops mil kar Big loop banate hain — tool sirf implementation detail hai.

---

## Part 2 — The Heartbeat: Loop kab chalta hai

### Concept 4 — In-session Loop (/loop)
Simplest heartbeat: current session ke andar `/loop` command repeat karta hai jab tak roka na jaye — insaan ki live monitoring ke saath.

> **Key Point:** In-session loop sirf session open hone tak zinda rehta hai.

### Concept 5 — Conditional Loop (/goal — run-until-done)
`/goal` completion-based hai — fixed number of times nahi, balke goal complete hone tak chalta hai.

> **⚠️ Warning:** Agar "done" clearly define nahi, loop infinite chal sakta hai ya galat waqt ruk sakta hai.

### Concept 6 — Scheduled Heartbeat (Routines / cron)
**Interval-based** (har 30 min) aur **cron/clock-based** (roz 7am) alag mechanism hain.

> **⚠️ Warning:** Interval heartbeat exact clock time guarantee nahi karta — precise time ke liye cron chahiye.

| Type | Kab chalta hai | Best use-case |
|---|---|---|
| Interval Heartbeat | Har X minutes/hours | Regular checks, exact time critical nahi |
| Cron / Scheduled | Exact clock time (7:00am) | Precise daily/weekly reports |

<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/4645eec0-8c5f-47ae-a5b1-c9b46e74a3e6" />
---

### Concept 7 — Event-driven Heartbeat
Time pe nahi, **event** pe chalta hai — webhook, GitHub Action, channel message.

> **Key Point:** Event-driven = "kya hua" based. Scheduled = "kab hua" based. Galat type choose karna missed triggers deta hai.

**Part 2 Recap:** Heartbeat 4 flavors — in-session, conditional/goal-based, scheduled (interval/cron), event-driven.

---

## Part 3 — The Body: Loop kya kaam karta hai

### Concept 8 — Worktrees (Isolation)
Parallel agents ko alag worktree (isolated workspace/branch) chahiye — warna kaam overwrite hota hai.

> **⚠️ Warning:** Bina isolation ke race conditions aur conflicting changes bante hain.

### Concept 9 — Skills (Knowledge)
Reusable "how-to" instructions jo agent ko specific kaam sikhati hain — ek dafa likho, agent har relevant task pe khud load karta hai.

### Concept 10 — Connectors / MCP (Action)
Real duniya se connection — Gmail, Slack, GitHub, database. Skills = "kaise", Connectors = "power".

### Concept 11 — Maker–Checker Subagents
Maker kaam karta hai, checker verify karta hai — dono alag context mein taake checker biased na ho.

> **Key Point:** Separate context zaroori hai warna checker sirf "rubber stamp" karega.

### Interlude A — Codify the Body: Dynamic Workflows
Fixed workflow ki jagah agent khud decide kare kaunse steps chahiye based on current situation.

### Interlude B — Codify the Checker: Verification Skills
Checker ko bhi "verification skills" milti hain — kaise verify karna hai, yeh bhi consistent/repeatable banta hai.

**Part 3 Recap:** Body = Worktrees + Skills + Connectors/MCP + Maker-Checker subagents. Interludes inhe dynamic aur codified/reusable banate hain.

---

## Part 4 — The Spine: Loop kya yaad rakhta hai

### Concept 12 — State / Memory (The Spine)
Model har run ke darmiyan sab bhool jaata hai — state disk pe file (jaise `progress.md`) mein zinda rehni chahiye, session ke andar nahi. Spine baaqi 5 parts ko jorta hai:
`Heartbeat → Spine(read progress.md) → Worktree → Skill → Subagents(maker/checker) → Connector(MCP/PR) → Spine again(update progress.md)`.

Cloud Routine ka run stateless hota hai — har Monday subah fresh session banta hai, kaam karta hai, band ho jaata hai. Isi liye spine repo mein hona zaroori hai, machine pe nahi.

> **Exam-style Scenario:** "Loop har subah chalta hai, par har run fresh start hota hai, kal ka kaam yaad nahi." → Missing part = **Spine (state/memory)**. Bina state file ke loop apna pehla step hi repeat karta rahega.

### Concept 13 — Cost by Cadence (Routine daily caps)
Routines ek daily run-limit ke saath aati hain — launch ke waqt: **5/day Pro**, **15/day Max**, **25/day Team/Enterprise** (numbers change ho sakte hain, `claude.ai/settings/usage` pe check karo).

> **Arithmetic example:** Issue triage (1) + evening summary (1) + PR-review Routine with 4 PRs (4) = **6 runs** — Pro cap (5) se 1 zyada. Fix: reports merge karo, extra usage buy karo, ya plan upgrade karo.

> **⚠️ Warning:** Cadence directly cost multiply karta hai.

**Part 4 Recap:** Spine = disk-based state, cross-run memory deta hai. Cost by Cadence = daily run-limits jo pehle se plan karni chahiye.

---

## Part 5 — Complete Worked Example

### Morning Triage Loop — 6 Parts ek diagram mein
Har weekday 9am: **Heartbeat** → **Spine** (progress.md read) → CI failures/issues dhoondo → **Worktree** mein isolated fix, project ki triage **Skill** se → **Subagent (checker)** se grade → PASS: **Connector (MCP)** se GitHub PR khol do; risky: progress.md mein likh do human ke liye → **Spine** update.

> **Key Point:** Parts 2–4 ka har concept is diagram ki ek line hai.

### Checker Design — Rubric ko stopping condition banana
Jahan mechanical checks nahi milti, reviewer agent written rubric use karta hai. Trick: score + bar do ("do not stop below 95") — soft judgment ko actionable condition banata hai.

> **⚠️ Warning:** Model ka score bhi claim hai, proof nahi — passing test se kamzor. Weaker checker = zyada reliance human gate pe.

**Part 5 Recap:** Sab concepts ek real loop mein assemble hote hain. Checker jitna weak, human gate pe utni zyada reliance.
<img width="1448" height="1086" alt="image" src="https://github.com/user-attachments/assets/c2bcfd3e-b700-406a-8d4a-1da6dd11c0a0" />

---

## Part 6 — Staying the Engineer

### Concept 14 — The Human Gate
Risky actions (deploys, destructive ops, financial moves, privacy-sensitive data, external messages) hamesha human approval ke peeche gate honi chahiye.

> **Key Point:** Blocked/exhausted/stagnant runs "successful" nahi hote — agent inhe "done" dress-up na kare.

### Concept 15 — Traps that Grow
- **Comprehension debt:** loop jitni tez ship karta hai jo aapne nahi likha, utna gap badhta hai samajh aur repo content mein.
- **Cognitive surrender:** apni opinion chhod dena, jo mile accept kar lena — comfortable trap. Loop leverage hai, judgment ka substitute nahi.
- **Cost per accepted change:** asal metric — kitna output actually accept hota hai. 10 mein se 6 reject = loop review-work wapis aap pe daal raha hai.

> **⚠️ Warning (Ralph Wiggum failure mode):** Agent kabhi completion signal jaldi de deta hai jab kaam adhoora ho. Isi liye objective, deterministic gate chahiye — sirf self-report pe trust na karo.

**Part 6 Recap:** "Build the loop. But build it like someone who intends to stay the engineer, not just the person who presses go." Human gate + traps ki awareness hi loop ko safe rakhti hai.

<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/8cf0e97c-0d3b-4ecc-b93a-2dd8b1d6017c" />

---
<img width="1597" height="985" alt="image" src="https://github.com/user-attachments/assets/8d40fe4d-2cdb-4339-afc9-7302b1c05b83" />
---

## Practice / Appendix (summary)
Course ke saath practice projects aur Routines appendix bhi hai (tool setup, scheduling syntax, dogfooding exercises) — hands-on hai, MCQ-testable concept content nahi.

---

*Ismail Ahmed Shah — GIAIC Final Exam Marathon 2026 · Full — Concepts 1–15 (Parts 1–6) + interludes complete*
