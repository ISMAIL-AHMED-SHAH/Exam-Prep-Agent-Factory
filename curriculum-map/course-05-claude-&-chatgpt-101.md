# Course 05 — Claude & ChatGPT 101
## ChatGPT & Claude Quick Reference

> [!NOTE]
> **Course Type:** Reference & Companion  
> **Source:** [Claude & ChatGPT 101 — Panaversity Agent Factory](https://agentfactory.panaversity.org/docs/claude-chatgpt-101-crash-course)  
> **Estimated Study Time:** 30–35 minutes reading + 25 minutes practice  
> **Status:** Topic tree supplied as fully read on 14 October 2026; embedded teaching slides and interactive study aids are not independently verified.

## Table of Contents

- [Overview](#overview)
- [Learning Objectives](#learning-objectives)
- [Course Roadmap](#course-roadmap)
- [The 9 Core Concepts](#the-9-core-concepts)
- [Claude vs ChatGPT: Quick Reference](#claude-vs-chatgpt-quick-reference)
- [Essential Mental Models](#essential-mental-models)
- [Security and Responsible Use](#security-and-responsible-use)
- [Practice Activities](#practice-activities)
- [Revision Checklist](#revision-checklist)
- [Quick Self-Test](#quick-self-test)
- [Key Takeaways](#key-takeaways)
- [Source and Verification Notes](#source-and-verification-notes)

---

## Overview

This reference explains where important controls live in Claude and ChatGPT, what those controls do, and how to choose the right feature for a particular task.

The goal is **not to memorize every button**. Learn the underlying patterns, then find the corresponding control in either interface.

### Learning Objectives

By the end, you should be able to:

- Navigate the Claude and ChatGPT chat workspaces.
- Choose an appropriate model and reasoning level.
- Supply files and context that improve answers.
- Distinguish instructions, memory, projects, and skills.
- Understand artifacts, writing blocks, code blocks, plugins, connectors, and apps.
- Choose between web search, thinking mode, and research mode.
- Evaluate AI using work whose correct result is already known.
- Protect sensitive information and retain responsibility for final decisions.

## Course Roadmap

| Part | Focus | Core Concepts |
|---|---|---|
| 1 | The Cockpit | 1–3: Interfaces, models, context |
| 2 | Making the Workspace Yours | 4–7: Projects, memory, outputs, skills |
| 3 | Extending Reach | 8–9: Integrations, evaluation |
| 4 | Practice & Review | Six exercises, self-check, glossary |

## The 9 Core Concepts

### Part 1 — The Cockpit

#### 1. Two Cockpits, One Discipline

Claude and ChatGPT have different interfaces, but many underlying capabilities overlap.

Both offer ways to work with conversations, models, files, instructions, memory, projects, and research features.

**Transferable skills:**
- Describe tasks clearly.
- Provide relevant context.
- Decide what to delegate.
- Verify outputs.
- Choose the required level of capability.
- Protect sensitive information.

> [!TIP]
> Learn the workflow, not just the location of a button.

#### 2. Models and Thinking Modes

Choose the capability level according to the task.

| Capability Level | Suitable Tasks |
|---|---|
| Fast default | Everyday questions, routine drafting, summaries |
| Thinking / reasoning | Multi-step logic, mathematics, analysis, difficult debugging |
| Flagship / high capability | Complex, demanding work requiring stronger overall capability |

**Two rules:**
1. Start with the fast option for routine tasks.
2. Escalate when the task genuinely requires deeper reasoning or stronger capability.

Model names and available features change over time. Check the current product interface and vendor documentation.

#### 3. Context You Attach

Models produce better-grounded answers when they receive the information needed for the task.

Common context includes:
- PDFs and Word documents
- Spreadsheets and CSV files
- Images and screenshots
- Code files
- Relevant conversation history and instructions

If a long conversation starts forgetting rules, contradicting earlier figures, or becoming generic, ask for a state summary. Correct it, start a fresh conversation, and reattach essential files.

> [!IMPORTANT]
> Better context can improve results more than a clever prompt alone.

### Part 2 — Making the Workspace Yours

#### 4. Projects: A Room for One Stream of Work

A project organizes ongoing work in one place.

Typical components include:
- Related chats
- Knowledge files
- Standing project instructions

Create a project when the same background, files, or instructions repeatedly appear across conversations. One-off questions usually do not need one.

#### 5. Memory and Standing Instructions

These features preserve different kinds of context.

| Feature | Main Purpose | Example |
|---|---|---|
| Instructions | Stable rules | “Use simple language.” |
| Memory | Evolving information and preferences | Recurring goals or working preferences |
| Projects | Context for a particular workstream | A course, client, or product |

Review stored information periodically. Correct outdated details, remove unnecessary information, and follow your organization's policies for sensitive data.

Temporary or incognito chats may reduce what is saved to conversation history or memory, but they should **not** be assumed to eliminate every form of data retention.

#### 6. Artifacts and Writing Blocks: Work You Can Take Away

Conversation is for discussing work; dedicated output areas help produce and revise finished deliverables.

- **Claude artifacts:** Separate outputs such as documents, code, diagrams, dashboards, and interactive applications.
- **ChatGPT writing blocks and code blocks:** Editable areas for writing and code within the conversation.
- **Structured data:** Tables or spreadsheet files for organized information.
- **Code execution:** Useful for calculations that should be computed rather than estimated.

For better deliverables, specify the goal, audience, format, and expected behavior. Revise one change at a time and verify important calculations.

#### 7. Skills and Plugins: Packaged Ways of Working

A skill packages a repeatable method so it does not need to be explained from scratch every time.

| Component | What It Does |
|---|---|
| Project | Keeps relevant context together |
| Skill | Packages a method for a task |
| Custom GPT | Provides a separately configured assistant |
| Connector / App | Connects the assistant to an external system |
| Plugin | May bundle several capabilities together |

A skill can contain instructions, examples, resources, and sometimes code. Reusable methods are more portable than prompts tied to a single conversation.

### Part 3 — Extending Reach

#### 8. Connectors, Apps, and Routing the Question

Connectors and apps can let an assistant access information in external systems, depending on available capabilities and permissions.

Examples include email, calendars, cloud storage, project-management tools, and organizational knowledge bases.

**MCP — Model Context Protocol** is a shared standard for connecting AI applications with external tools and data sources.

Choose the right mode for the work:

| Need | Appropriate Route |
|---|---|
| One current fact | Web search |
| Difficult reasoning without new information | Thinking mode |
| Thorough investigation with cited findings | Research mode |
| Information inside an organization's systems | Authorized workplace search or connected apps |

Before connecting a service, check what it can read, whether it can take actions, whether you trust it, and whether you are authorized to connect it.

#### 9. Prove It on Work You Already Know

Do not judge an assistant solely by benchmarks, impressive demonstrations, or confident-looking answers. Test it against your own tasks and standards.

**The five-step proving loop:**

1. Pick one recurring task.
2. Find a completed example with a known result.
3. Ask the assistant to reproduce the result.
4. Compare the output with the known answer.
5. Refine the instructions, test again, or keep the task human-led.

Passing a test earns confidence for similar work. It does not prove that every future answer will be correct or transfer responsibility away from you.

## Claude vs ChatGPT: Quick Reference

| Capability | Claude | ChatGPT |
|---|---|---|
| Separate finished outputs | Artifacts | Writing blocks and code blocks |
| External integrations | Connectors | Apps |
| Persistent workspaces | Projects | Projects |
| Standing preferences | Settings and styles | Custom Instructions |
| External tool standard | MCP support | MCP support |
| Model selection | Current model picker | Current model picker |
| Web investigation | Available features vary | Available features vary |

**Important:** This is a conceptual comparison, not a guarantee that every feature is available on every plan or account. Product interfaces, naming, limits, and permissions can change.

## Essential Mental Models

Remember these six rules:

1. **Model selection:** Choose capability according to task difficulty.
2. **Context:** Attach the information required for a good answer.
3. **Persistence:** Instructions = stable rules; memory = evolving context; projects = scoped work.
4. **Reusable methods:** Package recurring workflows into skills.
5. **Routing:** Search for facts, use thinking for reasoning, and research for investigation.
6. **Evaluation:** Test against known results before relying on AI for recurring work.

## Security and Responsible Use

- Connect only services you trust and are authorized to use.
- Review permissions before enabling external integrations.
- Avoid placing unnecessary sensitive information in chats, memory, or project files.
- Periodically review stored context for stale or incorrect details.
- Verify important claims, calculations, and citations.
- Keep high-risk decisions under appropriate human control.
- Disclose AI assistance where required by policy or context.

## Practice Activities

Complete the six exercises from the source course:

- [ ] **Guided tour:** Predict two features, then compare the assistant's description with the actual interface.
- [ ] **Same task, both assistants:** Compare their results and identify missing context.
- [ ] **Create a project:** Generate project instructions and prioritize useful documents.
- [ ] **Audit memory:** Review what is remembered; keep, correct, or delete as appropriate.
- [ ] **Route three questions:** Select search, thinking, or research before asking.
- [ ] **Test on known work:** Reproduce a completed task and record matches, missing instructions, and work that should remain human-led.

## Revision Checklist

- [ ] Explain why learning both interfaces can be useful.
- [ ] Distinguish fast, reasoning, and flagship model choices.
- [ ] Explain how attachments improve task context.
- [ ] Describe when to create a project.
- [ ] Distinguish instructions, memory, and projects.
- [ ] Explain artifacts versus writing blocks and code blocks.
- [ ] Distinguish skills, plugins, custom GPTs, and connectors/apps.
- [ ] Explain MCP and why integrations require permission checks.
- [ ] Choose between search, thinking, research, and workplace search.
- [ ] Describe the five-step proving loop.
- [ ] Explain what a successful test establishes—and what it does not.
- [ ] Review privacy, data retention, and human accountability considerations.

## Quick Self-Test

Try answering without looking at the notes:

1. Why should you learn capability tiers before memorizing model names?
2. When should you use thinking mode?
3. What is the difference between instructions, memory, and projects?
4. Where should finished writing, code, structured data, and calculations live?
5. Complete the sentence: Projects store ______; skills package ______.
6. What is MCP, and why does it matter across AI platforms?
7. Why test an assistant on a previous task with a known result?
8. What does passing a test establish, and what responsibility remains yours?

## Key Takeaways

- The interfaces differ, but the underlying work patterns often overlap.
- Strong context and clear task descriptions are essential.
- Choose tools according to the work rather than habit.
- Permissions, privacy, and verification are part of competent AI use.
- Trust should be earned through testing—not assumed from confident output.

## Source and Verification Notes

- **Primary source:** [Claude & ChatGPT 101 — Panaversity Agent Factory](https://agentfactory.panaversity.org/docs/claude-chatgpt-101-crash-course)
- The supplied topic tree reports that the page was fetched and read in full on **14 October 2026**.
- The source describes product-specific behavior and reports vendor-documentation verification dated **25 August 2026**. Check current official documentation for changes to features, plans, and limits.
- The embedded teaching-aid slideshow, interactive flashcards, and gated understanding test were marked **not verified** in the supplied tree.
- This file is a **revision overview**, not a verbatim reproduction of the full topic tree. Keep the complete tree in a separate file such as `course-05-topic-tree.md`.

---

*Built for structured learning and revision — Agent Factory Exam Prep.*
