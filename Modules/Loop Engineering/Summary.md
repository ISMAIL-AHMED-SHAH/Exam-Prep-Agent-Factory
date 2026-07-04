# 🔁 Loop Engineering — A Crash Course 

*15 Concepts · 6 Parts · GIAIC Agent Factory*

---

## Part 1: The Shift

### Concept 1 — Prompting se Looping tak
Ab tak hum agent ko turn-by-turn prompt karte thay — aap type karte, agent reply karta, aap check karte, phir agla instruction dete. Loop mein ye role reverse ho jata hai: aap ek system banate hain jo khud hi agent ko prompt karta rehta hai.

**Key Points:**
- Value khatam nahi hoti, sirf do jagah shift hoti hai: **Intent** (kya chahiye, precisely) aur **Accountability** (result ki zimmedari)
- Loop beech ke steps automate karta hai — shuruaat aur zimmedari hamesha aapki rehti hai

> ⚠️ Loop "set it and forget it" nahi hai — khud chalne wala loop khud mistakes bhi kar sakta hai.

---

<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/8dc52205-12b7-4364-ac59-d5ec73a47bd4" />

---
### Concept 2 — Loop ke 6 Parts
Har real loop mein 5 working parts + 1 spine hota hai.

- **Heartbeat** — schedule ya event jo loop start karta hai
- **Worktree** — isolation, taake parallel agents ek dusre ka kaam overwrite na karein
- **Skill** — project ki knowledge ek dafa likhi hui
- **Sub-agents** — maker-checker split
- **Connector (MCP)** — loop ko real tools mein "act" karne dena
- **State / Memory (Spine)** — disk pe file jo yaad rakhti hai kal kya hua

> ⚠️ No spine, no loop: state save nahi ho rahi to loop wahi pehla step repeat karega.
<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/7e9c903b-82b4-460b-975b-992b859ddf8f" />

### Concept 3 — Do Raaste: Claude Code vs OpenCode
- **Claude Code** — sab parts built-in: `/loop`, `/goal`, cloud Routines, `--worktree`, Channels
- **OpenCode** — sirf "layer below": `opencode run` ek beat hai, aap khud heartbeat banate ho (cron, GitHub Actions)
- Same idea, alag wiring — skill transfer hoti hai, keybind nahi
---
<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/1425ba77-9b58-48ec-80c4-8a08783fd055" />

---

## Part 2: The Heartbeat

### Concept 4 — In-Session Loops (`/loop`)
Simplest heartbeat: session khuli rehte hue prompt ko baar baar repeat karna.

- Claude Code: bundled `/loop` skill
- OpenCode: khud `while true; do ... sleep; done` shell se banana parta hai
- Session band = loop band — ye safety feature hai, bug nahi
<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/d97a402a-9cfa-4f96-b17a-2f1d306d0a7b" />
---
### Concept 5 — Run-Until-Done (`/goal`)
Pehli dafa **maker-checker** idea: loop khud faisla nahi karta ke kaam done hai — ek alag, chota model transcript parh kar decide karta hai.

- Stopping condition command se prove ho sakni chahiye ("tests pass")
- OpenCode: capped shell loop + exit codes checker ka kaam karte hain

> ⚠️ Hamesha 2 stops rakho: Success condition + Ceiling (max tries/spend).

### Concept 6 — Unattended Schedules
Task chalta hai chahe laptop on ho ya off.

- **Cloud Routines** (Claude Code) — Anthropic servers pe chalti hain, laptop off ho tab bhi
- `claude -p` ya `opencode run` — crontab mein daal ke headless one-shot
- OpenCode ka heartbeat hamesha OS ya CI hota hai

### Concept 7 — Event-Driven
Schedule "har ghanta check karo" poochta hai; event "jab X ho, react karo" poochta hai.

- Claude Code: Routines GitHub webhook pe trigger, Channels (Telegram/Discord/iMessage) events push karte hain
- OpenCode: `opencode github install` se GitHub events pe react karta hai

---

## Part 3: The Body

### Concept 8 — Isolation: Worktrees
Ek se zyada agents ek sath chalein to ek dusre ki files overwrite kar sakte hain. Git worktree = alag working folder, alag branch, same repo history.

- Claude Code: `--worktree` flag ya `isolation: worktree`
- OpenCode: `git worktree add`

### Concept 9 — Knowledge: Skills
Loop har baar "cold" start hota hai. Skill (SKILL.md) wo knowledge hai jo ek dafa likh do, har run parhta hai.

> Rule: jo cheez har run pe dobara explain karni parti, wo skill mein daal do.

### Concept 10 — Action: Connectors (MCP)
Sirf files parhne wala loop sirf "baat" kar sakta hai. Connectors (MCP) loop ko karne dete hain — PR khol na, Slack pe post karna.

### Concept 11 — Maker-Checker: Sub-agents
Sab se important rule: jo agent kaam likhta hai, wohi usay approve nahi kar sakta. Ek doosra agent wo miss karta hai jo pehla sure tha ke sahi hai.

- Claude Code: `.claude/agents/` mein defined
- OpenCode: checker ko apna sasta, read-only model do

> ⚠️ Har sub-agent apna model + tools chalata hai — checker jahan matter kare wahin use karo.

### Concept 11b — Dynamic Workflows
Claude Code poori orchestration ko ek rerunnable script mein codify karta hai.

> ⚠️ Workflow ek beat ki "body" hai, poora loop nahi — iska koi heartbeat ya spine nahi.

---

## Part 4: The Spine

### Concept 12 — State jo Runs ke Darmiyan Bachta Hai
Model har run ke baad sab bhool jata hai. Fix: state ko disk pe rakho.

- **Rules file** (CLAUDE.md/AGENTS.md) — steady habits
- **Progress file** (progress.md) — asal spine
- Har run shuru mein progress file parhta hai, end mein update karta hai

---

## Part 5: A Complete Loop, Twice

### Morning Triage Loop (Practical Example)
Har weekday 9am overnight CI failures dekhta hai, safe fixes draft karta hai, checker se grade karwata hai, PASS pe PR khol ta hai.

**Minimum Safe Loop Checklist:**
- Success condition + Ceiling
- Isolated branch/worktree
- Read-only checker
- State file (spine)
- Human gate — risky kaam kabhi seedha `main` pe nahi
- Log/notification
<img width="1448" height="1086" alt="image" src="https://github.com/user-attachments/assets/ea2560e3-bcdc-4c5c-91b7-833e907e6f6a" />

---

## Part 6: Staying the Engineer

### Bonus — Teen Loops: Coding, Feedback, Outside
- **Coding loop** (minutes) — jo aap ne banaya
- **Feedback loop** (hours) — aap try karte ho, instructions update karte ho
- **Outside loop** (days) — real users use karte hain

> Andrew Ng ka Context Advantage: agent teeno loops khud nahi chala sakta kyunke aap kuch jaante ho jo wo nahi jaanta.

### Concept 13 — Token Cost, Asal Limit
Cadence keybind se zyada matter karta hai.

- Har loop cap karo
- Model job se match karo
- Prompt/rules file short rakho
- Kam frequency pe chalao

> ⚠️ Same loop 5 beats/day = ~$20/month, har 5-min chale to $1000+/month.

### Concept 14 — Kaam Check Karna Ab Bhi Apka Kaam Hai
"Done" ek claim hai, proof nahi. Aap hi confirm karte ho ke shipped code actually kaam karta hai.

### Concept 15 — Apne Project Ko Samajhna Mat Chhodo
Loop tez code ship karta hai, gap barhta hai jo aap ne likha nahi.

> ⚠️ AI Gravity (Eric So): AI ko zyada sochne dene ka constant pull. Loop isi pull ko heartbeat deta hai.

---

## 📝 One-Line Recap

1. Prompting → Looping: value intent + accountability mein shift hoti hai
2. Loop ke 6 parts: Heartbeat, Worktree, Skill, Sub-agents, Connector, Spine
3. Claude Code parts ship karta hai; OpenCode layer below deta hai
4. `/loop` session ke sath band ho jata hai
5. `/goal` — command decide karta hai "done", agent nahi
6. Unattended schedule — laptop off hone pe bhi chalta hai
7. Event-driven — event pe react karta hai
8. Worktree — parallel agents overwrite nahi karte
9. Skill — project knowledge ek dafa likhi
10. Connector (MCP) — real tools mein action
11. Maker-checker — likhne wala aur checker alag
12. Dynamic Workflow — ek beat ki body, poora loop nahi
13. Spine — state jo runs ke darmiyan bachta hai
14. Complete loop — 7-point safety checklist
15. Teen loops: coding, feedback, outside
16. Token cost — cadence sab se bara driver
17. Checking ab bhi insaan ka kaam hai
18. Apna project samajhna mat chhodo

---


