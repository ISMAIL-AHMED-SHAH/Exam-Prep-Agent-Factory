# 🧩 Problem Solving with General Agents

> **7 Principles + 4-Phase Workflow**  
> *Agent Factory | Foundations Course*

---

## 📖 Overview

This course is about **solving real-world problems with General AI Agents**.

In the **AI Prompting** course, you learned how to **talk** to AI.

In the **Tool Courses**, you learned how to **use AI tools**.

This course teaches you **how to solve problems effectively** using those tools.

> [!IMPORTANT]
> Same AI. Same task.
>
> The difference is the workflow:
>
> - Following the **7 Principles** → Clean result in ~25 minutes
> - Ignoring them → Waste 90+ minutes fixing mistakes

---

## 🎯 Learning Outcome

By the end of this course, you'll understand:

- How professional AI users solve problems
- Why workflows matter more than prompts
- How to avoid the five biggest AI failure modes
- How to work safely with General Agents
- The complete **Explore → Plan → Implement → Commit** workflow

---

# 📑 Table of Contents

- [Mode 1 vs Mode 2](#mode-1-vs-mode-2)
- [Lindy Effect](#lindy-effect--why-old-tools-still-matter)
- [The Seven Principles](#the-seven-principles)
  - Principle 1 — Bash is the Key
  - Principle 2 — Code as Universal Interface
  - Principle 3 — Verification as a Core Step
  - Principle 4 — Small, Reversible Decomposition
  - Principle 5 — Persisting State in Files
  - Principle 6 — Constraints and Safety
  - Principle 7 — Observability
- [The Four-Phase Workflow](#the-four-phase-workflow)
- [Five Failure Patterns](#five-failure-patterns)
- [Worked Example](#worked-example)
- [Quick Recap](#quick-recap)

---

# Mode 1 vs Mode 2

| Mode | Purpose |
|-------|---------|
| **Mode 1 — Problem Solving** | Open a tool, solve a task, ship the result |
| **Mode 2 — Building AI Workers** | Build permanent AI assistants that continue working |

> [!NOTE]
> This course focuses entirely on **Mode 1**.

---
<img width="720" height="310" alt="image" src="https://github.com/user-attachments/assets/2d339893-de5e-40d5-99a5-82a7119bff00" />


# Lindy Effect — Why Old Tools Still Matter

The most valuable computing tools are also some of the oldest:

- Terminal
- Files
- Git
- SQL

This follows the **Lindy Effect**:

> Technologies that remain useful for a long time are likely to stay useful even longer.

### Key Ideas

- AI doesn't replace proven tools.
- AI makes those tools even more valuable.
- Your role changes—it doesn't disappear.

---
<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/76bdd418-23a2-41ca-9ac5-35646edbc465" />


# The Seven Principles

---

# Principle 1 — Bash is the Key

> **Failure Prevented**
>
> *"The agent only talks—it never acts."*

Traditional chatbots only answer questions.

General Agents can:

- Read files
- Write documents
- Execute commands
- Automate workflows

### Beginner Mistake

❌ "How should I organize these files?"

Result:

- Advice only

### Better Prompt

✅ Tell the AI exactly what file to create.

> [!TIP]
> Think of the AI as having **hands**.
>
> Brief the hands—not just the brain.

---

# Principle 2 — Code as Universal Interface

> **Failure Prevented**
>
> *"Natural language keeps getting misunderstood."*

There are two important ideas:

1. AI writes code for complex tasks.
2. Structure is just as important as content.

## Bash vs Code

| Bash | Code |
|------|------|
| Hands | Brain |
| Search | Compute |
| Move | Transform |
| Navigate | Orchestrate |

### Five Powers of Code

- Precise thinking
- Workflow orchestration
- Persistent memory
- Universal compatibility
- Instant tool creation

> [!IMPORTANT]
> Your responsibilities never change:
>
> - Define the problem
> - Verify the results

---

# Principle 3 — Verification as a Core Step

> **Failure Prevented**
>
> *"Looks correct—but breaks in production."*

A polished answer is **not** necessarily a verified answer.

Verification must be part of the workflow.

## Verification Pattern

1. List every factual claim
2. Find supporting evidence
3. Flag unsupported claims
4. Resolve every issue before saving

> [!WARNING]
> The same AI that generated the answer should never be your only verifier.

---

# Principle 4 — Small, Reversible Decomposition

> **Failure Prevented**
>
> *"One huge change destroyed hours of work."*

Break large tasks into:

- Small
- Independent
- Reversible steps

### Workflow

```

Task
↓
Small Step
↓
Check
↓
Save
↓
Next Step

```

### Rule of Thumb

> [!TIP]
> If reversing a change takes more than **2 minutes**, the change was probably too big.

---

# Principle 5 — Persisting State in Files

> **Failure Prevented**
>
> *"The AI forgot everything from yesterday."*

Conversations disappear.

Files persist.

## Rules Files

| Tool | File |
|------|------|
| Claude Code / Cowork | `CLAUDE.md` |
| OpenCode / OpenWork | `AGENTS.md` |

### Typical Structure

- Project overview
- Folder locations
- Critical rules
- References

### Persistence Hierarchy

| Level | Durability |
|--------|------------|
| Conversation | Temporary |
| Project Files | Durable |
| Referenced Files | On-demand |

> [!IMPORTANT]
> Conversations are temporary.
>
> Files are memory.

---

# Principle 6 — Constraints and Safety
<img width="1484" height="1060" alt="image" src="https://github.com/user-attachments/assets/f380b803-a362-414d-b6f6-7b9670536fc8" />


> **Failure Prevented**
>
> *"The AI modified things it wasn't supposed to."*

Constraints increase trust.

They do **not** reduce capability.

## Three Trust Levers

| Lever | Controls |
|--------|-----------|
| Scope | Files & folders |
| Connections | External services |
| Approvals | Human permission |

---

## Autonomy Ladder

1. Watching Closely
2. Ambient Supervision
3. Walk Away
4. Act Without Asking
5. Scheduled Automation

> [!WARNING]
> External files may contain prompt injections.
>
> Stay at **Watching Closely** when working with unknown content.

---
<img width="700" height="450" alt="image" src="https://github.com/user-attachments/assets/98363820-23bb-4d2b-937a-4913aee74ad4" />


# Principle 7 — Observability

> **Failure Prevented**
>
> *"I have no idea what the AI actually did."*

You can only guide what you can see.

Always watch at least one execution for new workflows.

## Five Warning Signs

- References unrelated conversations
- Replies become vague
- Ignores previous constraints
- Repeated apologies without progress
- Wants to touch files you never mentioned

### Recovery

```text
Stop
↓
Clear Session
↓
Paste Important Context
↓
Continue
```

---

# The Four-Phase Workflow

The Seven Principles become one repeatable workflow.

| Phase | Purpose |
|--------|----------|
| 🔍 Explore | Read and understand |
| 📝 Plan | Save a structured plan |
| ⚙️ Implement | Small verified changes |
| ✅ Commit | Final verification |

> [!IMPORTANT]
> Planning is the most important phase.

---
<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/5d47c4ad-6665-4764-ae4a-1ce4d42297f7" />


## Explore

Focus:

- Read only
- Understand the project
- Gather context

Uses:

- Bash
- Observability

---

## Plan

Create:

- Structured plan
- Saved plan file

Uses:

- Code as Interface
- Persistence

---

## Implement

Execute:

- Small steps
- Verify continuously
- Commit frequently

Uses:

- Decomposition
- Verification

---

## Commit

Finish by:

- Final verification
- Update rules file
- Save lessons learned

Uses:

- Observability

---

> [!NOTE]
> **Constraints (Principle 6)** surround the entire workflow.
>
> They are not a phase—they are the safety boundary.

---

# Five Failure Patterns

| # | Pattern | Symptom | Solution |
|---|----------|----------|-----------|
| 1 | The Drift | AI forgets the brief | Principle 5 |
| 2 | The Confident Wrong | Looks right but isn't | Principle 3 |
| 3 | The Big Bang | Massive risky changes | Principle 4 |
| 4 | The Scope Creep | Unauthorized actions | Principle 6 |
| 5 | The Black Box | No visibility | Principle 7 |

---

<img width="700" height="410" alt="image" src="https://github.com/user-attachments/assets/a1810606-3651-49f4-b103-62944a641fa4" />

# Worked Example

The workflow works across domains.

## Engineering

- Review pull requests
- Identify risks
- Produce verified recommendations

## Domain Experts

- Review legal agreements
- Compare vendor contracts
- Flag deviations

### Same Workflow

```text
Explore
    ↓
Plan
    ↓
Implement
    ↓
Commit
```

> [!TIP]
> Domains change.
>
> The workflow does not.

---

# 📝 Quick Recap

| Concept | Summary |
|----------|---------|
| Lindy Effect | Old proven tools become even more valuable with AI |
| Principle 1 | Treat AI as a doer, not just a chatbot |
| Principle 2 | Structure matters as much as content |
| Principle 3 | Always verify independently |
| Principle 4 | Work in small reversible steps |
| Principle 5 | Store knowledge in files |
| Principle 6 | Scope, permissions, and safety first |
| Principle 7 | Observe what the AI actually does |
| Workflow | Explore → Plan → Implement → Commit |
| Failure Patterns | Drift, Wrong Output, Big Bang, Scope Creep, Black Box |

---

# 🎓 Graduation Signal

You're ready for the next stage when:

- You naturally create plans before asking AI to execute.
- You verify results instead of trusting first drafts.
- You work in small, reversible changes.
- You use project files as persistent memory.

---

> [!SUCCESS]
> **One-Line Summary**
>
> Great AI users don't just write better prompts—they follow a repeatable workflow that emphasizes planning, verification, persistence, safety, and observability.
>
> https://agent-factory-quizz.netlify.app/
