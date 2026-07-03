# Code You Never Write 

> 📘 **Foundations Course | 4th of 6**
> 13 Concepts | AI code likhta hai, run karta hai, fix karta hai — aap sirf describe karte hain

---

> 💡 **Core Sentence (yaad rakhein):**
> "Aap code likhna nahin seekh rahe — aap code ke liye achha client banana seekh rahe hain. Achha client clear brief likhta hai, kaam ko un cheezoon ke khilaf check karta hai jo woh khud jaanta hai, aur jo pay kiya woh keep karta hai."

---

## 📑 Contents

- [Part 1 — The Deal (Concepts 1-3)](#part-1--the-deal-concepts-1-3)
- [Part 2 — Commissioning Code (Concepts 4-8)](#part-2--commissioning-code-concepts-4-8)
- [Part 3 — Paanch Surfaces (Concepts 9-11)](#part-3--paanch-surfaces-concepts-9-11)
- [Part 4 — Safety aur Edge of Map (Concepts 12-13)](#part-4--safety-aur-edge-of-map-concepts-12-13)

---

## 📘 Part 1 — The Deal (Concepts 1-3)

### Concept 1 — Code Ab Coding Se Gated Nahin

70 saal tak code ka gatekeeper tha: ya seekho likhna, ya haath se karo. **Naya deal:** AI developer hai, aap client hain — aur yeh developer seconds mein kaam karta hai, free mein, aur revisions se kabhi nahin thakta.

**Teen cheezein ek saath mature huin:**
- AI **working code likhta** hai well-described small problems ke liye
- AI **khud run karta** hai — aap ko kuch install nahin karna, code paste nahin karna
- AI **khud fix karta** hai — error message loop mein wapas aata hai aur AI correct karta hai

> 🎯 **Reframe:** "Kya main yeh kar sakta hoon?" poochna band karo. **"Kya main yeh describe kar sakta hoon?"** poochna shuru karo.

**Chhe professions, zero lines of code:**

| Profession | Kya describe kiya | Result |
|---|---|---|
| Bookkeeper | Do files match karni hain, mismatches dhundho | 1,400 rows mein 23 mismatches seconds mein |
| Doctor | Worst no-show days/slots kaunse hain | Monday 9am 3x worse nikla |
| Marketer | Chaar platform exports ek table mein | Merge, normalize, table aur chart |
| Teacher | 200 students ke weighted grades + comments | Sab ek run mein |
| Student | 300 photos date se rename karo | 1 minute mein 300 renamed |
| Network Engineer | 40 devices se health report pull karo | Script daily uske desk tak pahunchne se pehle |

---

### Concept 2 — Code Kya Hota Hai — 60-Second Version

Code = computer ke liye **exact instructions** jo perfectly, kisi bhi speed par, kisi bhi kitni baar follow ki jati hain.

**Do main languages:**

| Language | Kab use hoti hai | Aap ka role |
|---|---|---|
| **Python** | Files, spreadsheets, data, reports, automation — is course ka kaam | Kabhi choose nahin karte |
| **JavaScript** | Clickable tools, web games, interactive pages | Kabhi choose nahin karte |

> 💡 **Aap language kabhi choose nahin karte.** Aap outcome describe karte hain — "number/file chahiye" (Python) ya "click karne wali cheez chahiye" (JS) — AI decide karta hai.

> ⚠️ **Warning:** Code exact hai **dono directions mein** — 300 files sahi rename karega same 4 seconds mein jo ghalat karne lagte. Isi liye verification (C6) aur blast radius (C12) exist karte hain.

---

### Concept 3 — Dividing Line — Konse Problems Code Problems Hain

**VPRF Test** — koi bhi **ek signal kafi hai:**

| Signal | Test | Example |
|---|---|---|
| **V — Volume** | Haath se comfortably karne se zyada items | 300 files rename, 5,000 rows total |
| **P — Precision** | Ghalat digit ke consequences hain | Invoices, payroll, grades, money |
| **R — Repetition** | Agli hafte/mahine phir uthega yeh kaam | Month-end reports, daily health checks |
| **F — Files** | Problem files mein rehti hai, sentences mein nahin | Spreadsheets, exports, image folders |

**Quick examples:**

| Task | Code Problem? | Kyun |
|---|---|---|
| Meeting decline email draft karo | ❌ No | Koi VPRF signal nahin |
| 80 contracts mein non-standard clause dhundho | ✅ Yes | Volume + Files |
| Is saal fuel spend kya tha? | ✅ Yes | Precision + Files |
| 300 vacation photos date se rename karo | ✅ Yes | Volume + Files |
| Har Monday teen exports ek report mein combine karo | ✅ Yes | Repetition — sab se strong |

> ⚠️ **Trap:** "Roughly how did sales trend?" conversational lagta hai — lekin agar us number par koi decision depend karta hai, yeh **code problem hai** chahe aap casually puchein. Phrasing decide nahin karta — decision ka weight karta hai.

---

## 📗 Part 2 — Commissioning Code (Concepts 4-8)

### Concept 4 — AI Ke Haath Hilwao — Automatic vs Explicit

AI kabhi estimate kar leta hai jab compute karna chahiye. Same confident tone, same tidy numbers — lekin computed nahin. **Silent failure mode — enemy number one.**

> 🎯 **Teen-Line Incantation (desk par pin karein):**
> ```
> Write and run code to answer this.
> Show me the code you ran.
> Before analyzing anything, tell me the exact row count,
> the column names, and the date range of the file.
> ```

- **Line 1** = computation force karo
- **Line 2** = proof (agar code block nahin aaya, code run nahin hua)
- **Line 3** = lie detector (agar AI file parh raha hai, row count exact hoga)

| Phrasing | Kya hota hai |
|---|---|
| "What does this data show?" | Glance-based summary — estimates as facts |
| "Roughly how did costs trend?" | Almost always a glance |
| "Write and run code to compute cost by month." | Code, har baar ✅ |

> ⚠️ "Code" kaho, language specify mat karo. "Write and run code" — AI sahi tool choose karta hai.

---

### Concept 5 — Problem Brief Karo, Program Nahin

**Sab se liberating fact:** Best code briefs mein koi technical language nahin hoti. Outcome describe karte hain, AI implement karta hai.

**Paanch-Section Brief:**

```markdown
# Brief: [task ka naam]

## Goal
Problem kab solve hogi?

## Input
Kya de raha hoon? (files, format, roughly kitne rows)

## Output
Exactly kya chahiye? (number, table, chart, HTML report)

## Rules  ← BEGINNERS SKIP KARTE HAIN ★
Woh constraints jo koi stranger nahin jaanta
(School year August mein, "Pending" = not submitted)

## Edge cases  ← BEGINNERS SKIP KARTE HAIN ★
Imperfect data ke saath kya ho?
("Blank row ho to skip karo, list mein daalo")
```

> ⚠️ **Do sections jo sab se zyada matter karte hain — aur sab se zyada skip hote hain:**
> - **Rules** = aap ki professional knowledge jو AI kabhi nahin jaanata
> - **Edge cases** = imperfect data ka behavior — "If you hit a row you can't interpret, skip it and list it at the end"

> 💡 **Discovery First:** Edge cases nahin pata? Pehle poochein: *"Before doing anything, examine the files and tell me what could be ambiguous, inconsistent, or surprising."* AI inspect karta hai — phir aap Edge cases likho.

---

### Concept 6 — Verification — Kaam Jo Aap Parh Nahin Sakte

**Paanch Verification Rungs (badti mehnat ke order mein):**

| Rung | Method | Best for |
|---|---|---|
| **1 ★ Most Powerful** | **Known-Answer Test** — ek slice jis ka answer already pata hai | Har baar — kabhi skip nahin hota |
| **2** | **Reality Questions** — row counts, plausible range, biggest item | Everyday work |
| **3** | **Plain-English Replay** — code ka procedure plain English mein | Logic errors pakadne ke liye |
| **4** | **Adversarial Pass** — AI se apna kaam attack karwao | Higher stakes |
| **5** | **Cross-Model Check** — doosre AI se same brief chalao | Money, grades, signed work |

> 💡 **Pharmacist example:** Usne fake 10-unit discrepancy plant ki — script ne plant pakad li + 4 real discrepancies. Plant ne 4 real catches par trust earn kiya. **Data mein known error salt karo — agar script dhoondh le, baaki results earned hain.**

> ⚠️ **Golden Rule:** Kabhi precision-critical number par act mat karo jise aap ne independent knowledge ke khilaf test nahin kiya.

---

### Concept 7 — Jab Toote — Errors Dialogue Hain, Failure Nahin

**Mindset shift:** Error project fail nahin hua — computer exactly bata raha hai precisely kya chahiye.

**Red text ke liye puri skill:**
> *"It stopped and showed this error. Diagnose it, fix the code, and run it again: [red text paste karein]"*

Bas itna. Error interpret nahin karna — forward karna hai.

**Wrong-but-running (zyada mushkil case):**
> *"Output shows total sales of 4.2M but I know this year was around 12M. Show me the row count you processed, the date range, and the first 5 rows as the code sees them."*

| Symptom | Prompt |
|---|---|
| Red text, script ruk gaya | Pura error paste: "diagnose, fix, rerun" |
| Chalta hai lekin number ghalat | Symptom + expected value + row counts maango |
| Same fix teen baar fail | "Step back, restate fresh, propose two different approaches" |

---

### Concept 8 — Script Rakhein — Solved Problem Button Ban Jati Hai

Repetition signal ka payoff: **ek baar likhi script hamesha ke liye asset hai.**

**Teen-Part Habit:**

1. **Script file ke taur par maango** — *"Save this as a script file, named clearly, with a plain-English description at the top."*
2. **Brief saath rakhein** — Script = how (machines). Brief = what & why (humans aur future AI). Future mein: "late-cutoff rule change ho gaya, update karo."
3. **Folder structure dein:**

```
my-scripts/
  essay-submissions/
    brief.md          ← what & why
    submissions.py    ← code (aap ne kabhi nahin parha)
    sample-class/     ← known-answer test pre-packaged
  monthly-campaign-rollup/
    brief.md
    rollup.py
    sample-april/
```

| Bina habit | Habit ke saath |
|---|---|
| Har mahine fresh se explain karo | "Run the script on the new files." |
| Subtle rule drift har run mein | Rules frozen hain script mein |
| Sirf aap ko faida | Colleague ko folder do — minutes mein productive |

---

## 📙 Part 3 — Paanch Surfaces (Concepts 9-11)

### Concept 9 — Claude.ai — Home Surface

Code **sandbox** mein execute hota hai — Anthropic ki taraf ka temporary computer. Aap ke computer par kuch touch nahin — **zero-risk surface** seekhne ke liye.

| Strength | Limitation |
|---|---|
| Zero installation, zero machine risk | Sandbox sirf upload dekhta hai — 40 files = 40 uploads |
| One-off aur exploratory jobs ke liye perfect | Sandbox temporary — scripts download nahin ki to khatam |
| Full loop visible: brief → code → verify → iterate | Recurring jobs = har baar re-upload |

> 💡 **Graduation signal:** Claude.ai tab chhodein jab uploading annoy karne lage.

---

### Concept 10 — Claude Code & OpenCode — Agent in Your Folder

Terminal mein rehte hain. **Reframe:** *"Terminal sirf ek chat box hai jo folder ke andar baithta hai."*

**Kya milta hai:**
- Files already wahan hain — **koi upload nahin**
- Code directly files par run hota hai
- Scripts **forever persist** karte hain
- Errors **self-heal** hote hain
- **Scheduled runs** possible hain

| Tool | Kya hai |
|---|---|
| **Claude Code** | Anthropic ka, polished, Claude chalata hai |
| **OpenCode** | Open-source, koi bhi model (free/self-hosted) |

> 💡 **Non-programmers bhi yahan belong karte hain** — marketing "developers ke liye" hai, lekin boundary galat hai. Accountants aur researchers in tools ke heaviest users hain jo file upload se thak gaye the.

---

### Concept 11 — Cowork & OpenWork — Delegation with Safety Ritual

Desktop apps — same file-touching power, knowledge workers ke liye. **Built-in safety rhythm: plan first, act after approval.**

**Surface selection table:**

| Situation | Surface |
|---|---|
| Ek file ke bare mein one-off question | **Claude.ai** |
| Seekhna, explore karna | **Claude.ai** |
| Problem folders mein hai, repeat hogi, scripts persist chahiye | **Claude Code / OpenCode** |
| Same, lekin plan approve karna chahiye terminal nahin | **Cowork / OpenWork** |
| Schedule par run ya doosre systems touch karne | **Claude Code / OpenCode** |

> 💡 **Honest advice:** Claude.ai par tiko jab tak uploading week ka annoying hissa na ban jaye. Yeh hi graduation signal hai.

---

## 📕 Part 4 — Safety aur Edge of Map (Concepts 12-13)

### Concept 12 — Blast Radius — Real Files Ko Touch Karne Ke Rules

Claude.ai par mistakes free hain. Jab code aap ke machine par chale: **woh exactly karta hai jo bola gaya — including the wrong thing — at scale.**

> ⚠️ **Critical Warnings:**
> - Agent se delete kiye files aksar **Recycle Bin skip kar jati hain**
> - Script se edit ki files **koi undo history nahin rakhti**

**Chaar Rules — Teen sentences per brief, 90 seconds per run:**

| Rule | Command |
|---|---|
| **1. Copies par kaam karo** | *"First copy the folder to [name]-backup, then work on the original."* |
| **2. Dry run maango** | *"Don't change anything. Show me every operation (old → new name) and wait for approval."* |
| **3. Territory scope karo** | Sab se chhota folder — kabhi home directory ya poori disk nahin |
| **4. New files mein output** | *"Write results to a new file; leave originals untouched."* |

**Brief mein standing ritual:**
```
Copy the folder to a backup first. Show me your plan before
changing anything, and wait for approval. Write all output
to new files; never modify the originals.
```

---

### Concept 13 — Edge of the Map

**Is course ki territory:** VPRF se trip hone wali har reconciliation, rollup, rename, merge, clean, cross-check, flag, chart, report — zyada tar professionals ke liye saal mein saikdoon ghante.

**Map ke bahar (More engineering needed):**

| Category | Kyun map ke bahar |
|---|---|
| Software jo log login karte hain | Accounts, payments, simultaneous users = products, not scripts |
| Always-on automation with consequences | "Email clients automatically" — verification checks nahin pahunch sakti |
| High-stakes no-undo acts | Code prepare kare, human fire kare |
| Judgment wearing computation costume | "Kaunse employees promote karein" — criteria hi poora problem hai |

> 💡 **Golden distinction:** Code computes — **aap decide karte hain.**

---

## 📌 Quick Recap — 13 Concepts, Ek Line Har Ek

| # | Concept |
|---|---|
| C1 | Code gated nahin ab — describe karo, AI karta hai |
| C2 | Python = data; JS = clickable — AI choose karta hai, aap nahin |
| C3 | VPRF test — V(olume) P(recision) R(epetition) F(iles) |
| C4 | "Write and run code. Show the code. Row count first." |
| C5 | Paanch-section brief: Goal, Input, Output, **Rules**, **Edge cases** |
| C6 | Known-answer test → Reality Qs → Plain-English Replay → Adversarial → Cross-model |
| C7 | Red text paste karo — "diagnose, fix, rerun" |
| C8 | Brief + Script + Sample folder = reusable asset forever |
| C9 | Claude.ai = zero-risk sandbox, one-off jobs ke liye home |
| C10 | Claude Code/OpenCode = agent in your folder, no uploading |
| C11 | Cowork/OpenWork = desktop app, plan-then-approve built-in |
| C12 | Copies → Dry run → Small scope → New files |
| C13 | Always-on automation aur judgment calls map ke bahar |

---

*GIAIC | P1-AFAP Exam Prep | Agent Foundations & Prompting | 2026*
