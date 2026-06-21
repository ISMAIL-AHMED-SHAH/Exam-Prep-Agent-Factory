# 📙 Step 3 — AI Prompting in 2026: 13 Key Concepts

## Table of Contents

1. [Novice vs Power User](#1-novice-vs-power-user)
2. [Pretrained Knowledge](#2-pretrained-knowledge)
3. [Teen Retrieval Modes](#3-teen-retrieval-modes)
4. [Context Poora Game Hai](#4-context-poora-game-hai)
5. [Reasoning — "Think Hard"](#5-reasoning--think-hard)
6. [Sycophancy aur Isay Kaise Rokein](#6-sycophancy-aur-isay-kaise-rokein)
7. [Brainstorm-Iterate Loop](#7-brainstorm-iterate-loop--sab-se-important-habit)
8. [Multimodal: Images, Audio, aur Aage Kya](#8-multimodal-images-audio-aur-aage-kya)
9. [Ek Prompt Se Chhoti Apps Banana](#9-ek-prompt-se-chhoti-apps-banana)
10. [Data Analysis — Model Code Likhta aur Run Karta Hai](#10-data-analysis--model-code-likhta-aur-run-karta-hai)
11. [AI Desktop Apps aur Permissions](#11-ai-desktop-apps-aur-permissions)
12. [Cost, Speed, aur Kaunsa Model Kab](#12-cost-speed-aur-kaunsa-model-kab)
13. [Testing aur Staying Current](#13-concept-13--testing-aur-staying-current)
14. [Key Takeaways](#key-takeaways)

---

# 📙 Step 3 — AI Prompting in 2026: 13 Key Concepts

## 1. Novice vs Power User

Farq intelligence ka nahin hota.

Farq **briefing quality** ka hota hai.

### 🔴 Novice Prompt

```text
Which car should I buy?
```

Result:

* Generic suggestions
* Generic pros & cons
* Little personalization

### ✅ Power User Prompt

Provide:

* Spec sheets
* Dealer quotes
* Insurance plans
* Budget
* Constraints
* Priorities

Result:

* Personalized analysis
* Better recommendations
* Context-aware tradeoffs

> [!TIP]
> AI ko ek highly capable fresh graduate samjhein.
>
> Smart hai.
>
> Motivated hai.
>
> Lekin aap ke business, preferences aur context ke baare mein nahin jaanta.

### Better Mental Model

```text
New Colleague
      ↓
Needs Context
      ↓
Gets Briefed
      ↓
Produces Better Work
```

---

## 2. Pretrained Knowledge

AI ne duniya ke baare mein internet aur documents se seekha hota hai.

Examples:

* Reddit
* Wikipedia
* Books
* Research Papers
* Public Websites

### Reliability by Category

| Category                     | Reliability |
| ---------------------------- | ----------- |
| Cooking                      | High        |
| Popular Movies               | High        |
| Celebrity News               | High        |
| Quasars                      | Variable    |
| Regional History             | Sparse      |
| Niche Professional Knowledge | Sparse      |
| Your Company Data            | Absent      |
| Recent News Beyond Training  | Absent      |

> [!WARNING]
> Confidence ≠ Correctness
>
> AI kabhi kabhi poore confidence ke saath ghalat jawab bhi de sakta hai.

---

## 3. Teen Retrieval Modes

### Comparison Table

| Mode          | Speed           | Best For                    | Weakness                      |
| ------------- | --------------- | --------------------------- | ----------------------------- |
| Pretrained    | Seconds         | Definitions, Stable Facts   | Stale Information             |
| Web Search    | Tens of Seconds | Current Events, Recent News | Source Quality Varies         |
| Deep Research | Minutes         | Multi-Source Analysis       | Overkill for Simple Questions |

### AI vs Google

| Google                | AI                |
| --------------------- | ----------------- |
| Specific Link Chahiye | Synthesis Chahiye |
| Exact Website         | Comparison        |
| Product Page          | Tradeoffs         |
| Navigation            | Analysis          |

### Web Search Improvement Habits

#### Habit 1

Trusted sources specify karein.

Example:

```text
Use sources from WHO, NIST and OpenAI.
```

#### Habit 2

Inline citations maangein.

Example:

```text
Cite every major claim.
```

#### Habit 3

Unverified claims flag karne ko kahen.

Example:

```text
Clearly label uncertain information.
```

> [!TIP]
> Better inputs = Better search results.

---

## 4. Context Poora Game Hai

Model sirf wohi dekh sakta hai jo context window mein maujood ho.

### Context Stack

```text
Uploaded Files
      ↓
Chat History
      ↓
User Prompt
      ↓
Tool Descriptions
      ↓
System Instructions
```

### Context Window Evolution

| Year            | Approximate Capacity    |
| --------------- | ----------------------- |
| 2022            | Few Thousand Words      |
| 2026            | Hundreds of Thousands   |
| High-End Models | Up to ~1 Million Tokens |

> [!TIP]
> Prompt send karne se pehle poochein:
>
> "Ek smart new colleague ko jawab dene ke liye kya information chahiye hogi?"

Phir woh attach kar dein.

### ⚠️ Context Rot

Problem:

```text
Project Planning
      ↓
Vacation Advice
      ↓
Medical Question
      ↓
Coding Debugging
```

Result:

* Lower quality responses
* Confused context
* Lost assumptions

> [!WARNING]
> Jab topic significantly change ho jaye to nayi chat start karein.

### Projects Feature

Ek dafa context define karein:

* Instructions
* Files
* Reference Docs

Phir future chats automatically inherit kar sakti hain.

Examples:

* Claude Projects
* ChatGPT Projects
* Gemini Notebooks / NotebookLM

---

## 5. Reasoning — "Think Hard"

Purana Prompt:

```text
Think step by step.
```

Modern Alternative:

```text
Think hard before answering.
```

ya

```text
Think carefully before responding.
```

### Kab Use Karein?

✅ Complex analysis

✅ Planning

✅ Coding

✅ Strategy

✅ Multi-step reasoning

### Kab Avoid Karein?

❌ Quick lookups

❌ Small summaries

❌ Casual brainstorming

❌ Simple factual questions

> [!NOTE]
> Deep reasoning zyada time aur zyada compute consume karta hai.

### AI Capability Trend

```text
Mid-2024
~7 Minute Human Tasks
      ↓
Early-2025
~1 Hour Human Tasks
      ↓
Future
Longer and Longer Tasks
```

---

## 6. Sycophancy aur Isay Kaise Rokein

AI aksar user se agree karne ki taraf bias rakhta hai.

Is behavior ko **Sycophancy** kehte hain.

### Bad vs Better Prompts

| Sycophancy Bait              | Neutral Rewrite                   |
| ---------------------------- | --------------------------------- |
| Find evidence this will work | Evaluate strengths AND weaknesses |
| Why is A better than B?      | Compare A and B using criteria    |
| Tell me my draft is ready    | Score and critique this draft     |

### Objective Rubric Pattern

Example:

```text
Score this business idea from 1-10:

1. Real Problem
2. Paying Market
3. Competitive Advantage
```

### Why Numbers Matter

Instead of:

```text
Strong
Good
Promising
```

Use:

```text
6/10
7/10
9/10
```

> [!TIP]
> Numbers force commitment.
>
> Prose often hides uncertainty.

---

## 7. Brainstorm-Iterate Loop — Sab Se Important Habit

Yeh poore chapter ki highest leverage technique hai.

### Recommended Process

#### 1️⃣ Context Do

Include:

* Goals
* Constraints
* Audience
* Files

#### 2️⃣ Multiple Options Maango

```text
Give me 5 options.
```

#### 3️⃣ Feedback Do

Specify:

* Kya pasand aaya
* Kya reject hua
* Kyun

#### 4️⃣ New Options Maango

Feedback-informed alternatives generate karwao.

#### 5️⃣ Iterate

Continue until:

```text
3 Options
      ↓
2 Strong Options
      ↓
1 Winner
```

#### 6️⃣ Expand

Sirf final choice ko detail mein expand karwao.

> [!WARNING]
> First draft aksar "slop" hota hai.
>
> Polished lagta hai.
>
> Lekin content weak ho sakta hai.

### Writing Workflow

```text
Outline
   ↓
Critique
   ↓
Expand
   ↓
Critique
   ↓
Full Draft
   ↓
Grade
   ↓
Improve
```

Target:

```text
9.5/10+
```

---

## 8. Multimodal: Images, Audio, aur Aage Kya

### Image Input

#### Strong At

* Whiteboards
* Diagrams
* Screenshots
* Handwritten Notes
* Overall Scenes

#### Weak At

* Tiny Details
* Cluttered Images
* Fine Visual Inspection

### Image Generation Tips

#### Tip 1

Prompt AI se likhwao.

AI generally richer prompts likhta hai.

#### Tip 2

Visual vocabulary build karo.

Examples:

* Cinematic
* Watercolor
* Isometric
* Claymation
* Photorealistic

### Designer-Quality Diagram Workflow

```text
Claude
  ↓
SVG
  ↓
PNG
  ↓
ChatGPT / Gemini
  ↓
Redraw & Polish
```

### Audio

#### Long Dictation

Bol kar explain karna aksar typing se zyada context capture karta hai.

#### Meeting Summaries

Upload:

```text
1 Hour Recording
```

Output:

* Decisions
* Action Items
* Open Questions

---

## 9. Ek Prompt Se Chhoti Apps Banana

### Prompt Template

```text
🎯 Goal:
What should it do?

📥 Input:
What does the user provide?

📤 Output:
What should the user see?
```

### Good Examples

* Pomodoro Timer
* Bill Splitter
* Outfit Picker
* Fireworks Simulator
* Simple Games

### Tools

| Tool             | Purpose               |
| ---------------- | --------------------- |
| Claude Artifacts | Interactive Apps      |
| ChatGPT Canvas   | Interactive Workspace |
| Gemini Canvas    | Interactive Apps      |

### Current Limitations

❌ Multiplayer Games

❌ Real-Time Audio AI

❌ Complex Production Apps

---

## 10. Data Analysis — Model Code Likhta aur Run Karta Hai

Modern AI systems analysis ke liye code likh aur execute kar sakte hain.

### Critical Prompt

```text
Write and run code to answer this.

Show me the code you ran.
```

> [!IMPORTANT]
> Yeh prompt analysis aur guessing ke darmiyan farq paida karta hai.

### Verification Prompt

```text
Tell me:

- Row Count
- Column Names
- Date Range

Before Analysis
```

### Best Use Cases

* CSV Files
* Bank Transactions
* Business Data
* Tracking Logs
* Spreadsheet Analysis

---

## 11. AI Desktop Apps aur Permissions

AI desktop tools aap ki files:

* Read
* Search
* Edit
* Organize

kar sakte hain.

### Safe Workflow

```text
Task
  ↓
Request Plan
  ↓
Review Plan
  ↓
Approve
  ↓
Execute
```

### Risks

> [!WARNING]
> AI ke delete ki hui files recycle bin mein na bhi ja sakti hain.

> [!WARNING]
> AI edits aksar undo history maintain nahin karti.

### Permission Ladder

```text
Read Only
      ↓
Limited Write
      ↓
Task-Specific Access
      ↓
Trusted Workflow
```

> [!TIP]
> Trust se pehle track record build karein.

---

## 12. Cost, Speed, aur Kaunsa Model Kab

### Modality Comparison

| Modality | Speed           | Cost                 |
| -------- | --------------- | -------------------- |
| Text     | Seconds         | Fractions of a Cent  |
| Speech   | Seconds         | Few Cents per Minute |
| Images   | Tens of Seconds | Several Cents        |
| Video    | Minutes         | Cents to Dollars     |

### Current Strength Snapshot

| Platform | Strengths                       |
| -------- | ------------------------------- |
| Claude   | Reasoning, Code, Long Documents |
| ChatGPT  | Image Generation, Voice         |
| Gemini   | Search, Google Workspace        |

> [!TIP]
> Ek hi prompt ko multiple models mein test karna worthwhile hota hai.

### Benchmark Habit

Check periodically:

```text
Arena Leaderboard
```

Leaders frequently change.

---

## 13. Concept 13 — Testing aur Staying Current

### Habit 1 — Backup Model

Hamesha:

```text
Primary Tool
      +
Backup Tool
```

rakhein.

Agar jawab weak lage:

* Same prompt copy karein
* Backup model mein paste karein
* Compare karein

---

### Habit 2 — Prompt Library

Save:

* Best prompts
* Best workflows
* Best templates

Over time:

```text
Prompt Collection
      ↓
Personal Operating System
```

---

### Habit 3 — Learn from Failures

Jab model ghalat ho:

❌ Emotional reaction nahin

✅ Observation

Questions:

* Kahan fail hua?
* Kis information ki kami thi?
* Kis mode ka use karna chahiye tha?

---

### Monthly Ritual

```text
Arena Leaderboard Check
         ↓
Run Same Task on 3 Models
         ↓
Compare Results
         ↓
Use Current Winner
         ↓
Repeat Next Month
```

> [!IMPORTANT]
> AI landscape rapidly change hota hai.
>
> Best model aaj wala ho sakta hai.
>
> Zaroori nahin ke kal bhi wahi ho.

---

# Key Takeaways

* Better prompting = Better briefing.
* Context quality response quality ko drive karti hai.
* Retrieval mode task ke mutabiq choose karein.
* Sycophancy ko objective scoring se reduce karein.
* Brainstorm → Feedback → Iterate workflow use karein.
* Multimodal AI text se bohat aage ja chuka hai.
* Small apps prompts se generate ki ja sakti hain.
* Data analysis ke liye code execution verify karein.
* Permissions gradually grant karein.
* Multiple models regularly compare karein.
* Continuous testing AI literacy ka core part hai.

---

