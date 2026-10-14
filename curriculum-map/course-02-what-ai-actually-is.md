# 🧠 Course 02 — What AI Actually Is
### The Machine Behind Modern AI

> **Nine ideas. No math. No code.**  
> Understand how AI works, why it behaves unexpectedly, and where human verification remains essential.

**Source:** [What AI Actually Is — Panaversity Agent Factory](https://agentfactory.panaversity.org/docs/what-ai-actually-is-crash-course)

---

## 🗺️ Course at a Glance

| Course component | Details |
|---|---|
| Core ideas | 9 |
| Learning parts | 3 |
| Main topics | 14, including the introduction |
| Subtopics | 88 |
| Nested concepts | 305 |
| Total nodes | **407** |
| Verification | Accessible content verified; 2 nodes not verified |

## 🎯 The Learning Journey

```text
                    WHAT AI ACTUALLY IS
                            │
             ┌──────────────┼──────────────┐
             ▼              ▼              ▼
       PART 01          PART 02         PART 03
     THE MACHINE      ITS BEHAVIOUR     AI THAT ACTS
             │              │              │
       ┌─────┼─────┐  ┌─────┼─────┐    ┌───┴────┐
       ▼     ▼     ▼  ▼     ▼     ▼    ▼        ▼
      Idea  Idea  Idea Idea  Idea  Idea Idea     Idea
       1     2     3   4     5     6    7         8
                                              + Idea 9
```

## 💡 The Nine Core Ideas

### Part 01 — The Machine

**01. It predicts the next piece of text.**  
AI generates likely continuations rather than inherently looking up facts.

**02. It learned by reading, and then the learning stopped.**  
Training adjusts the model's weights; ordinary conversations do not retrain those weights.

**03. There is no separate part that checks whether it is true.**  
A fluent answer can still be false. Human verification remains essential.

### Part 02 — Why It Behaves the Way It Does

**04. It reads in tokens, not letters or words.**  
Tokenization helps explain counting mistakes, text processing, context limits and costs.

**05. The context window is the only thing it can see.**  
The model relies on the information supplied in its current context, including relevant instructions, conversation history and available files.

**06. Its confidence is a learned style, not a truth signal.**  
Confident wording and agreement do not guarantee correctness.

**07. It is brilliant and useless on two tasks in a row.**  
AI capability is uneven: success on one task does not guarantee success on another.

### Part 03 — From Predictor to Agent

**08. Tools let it act, not just describe.**  
Tools, connectors and action-observation loops let AI work toward goals beyond generating text.

**09. “Thinking” is just more prediction before the answer.**  
Reasoning models generate additional working before responding, but this does not create a perfect truth-checker.

---

## 🌳 Complete Course Map

### 00 — Introduction and Orientation
- Course purpose, analogy, problem and expected reading time
- Quick glossary: all **34 entries**
- “Read this one first” callout
- How this course and the prompting course divide the work
- Six connections between AI mechanisms and prompting practices

### 01 — The Questions This Course Answers
- Teacher and self-testing guidance
- Part 1 question table: **Q1–Q8**
- Part 2 question table: **Q9–Q16**
- Part 3 question table: **Q17–Q19**
- Optional Claude.ai appendix pointer

### 02 — Teaching Aid
- Full slideshow embed
- Verification note retained for unreadable slide content

### 03 — Prove It in Two Minutes
- Open an AI chatbot
- Run the strawberry letter-count demonstration
- Understand tokens and the spelling-out workaround
- Explore the typo example
- Understand why surprising behaviour comes from the mechanism
- Warning about memorized test examples
- Nine-ideas roadmap figure

### 04 — The Nine Ideas in One Line Each
- Ideas 1–9, with each original one-line explanation preserved in the detailed tree

### 05 — Part 1: The Machine
- **Idea 1:** Prediction, tokens, autocomplete analogy, weights, stochastic output, lookup misconception, examples, temperature, web search and reliability
- **Idea 2:** Training, data sources, learning process, instruction tuning, human feedback, inference, corrections, cutoff, statelessness, memory, model terminology and consequences
- **Idea 3:** Generation versus verification, hallucination, confidence, tools and the tuition-fee example

### 06 — Part 2: Why It Behaves the Way It Does
- **Idea 4:** Tokens, counting, language differences, cost, context and multimodal inputs
- **Idea 5:** Context window, system prompt, window size, briefing, context rot, replayed chat history, memory, Skills, progressive disclosure and reading-desk analogy
- **Idea 6:** RLHF, confidence, agreeableness, sycophancy and practical fixes
- **Idea 7:** Jagged frontier, examples, causes, verification habits and changing capability

### 07 — Part 3: What Turned a Text Predictor into Something That Acts
- **Idea 8:** Tools, tool calls, observation loops, agents, code execution, connectors, MCP and web search
- **Idea 9:** Reasoning models, working tokens, thinking controls, limitations and intentionally excluded topics

### 08 — Short Recap
- All nine ideas revisited
- One-sentence mental model
- Well-read writer versus librarian analogy

### 09 — Six Hands-On Prompts
1. See prediction rather than lookup
2. Watch learning fail to stick
3. Catch the missing checker
4. Catch transcript replay
5. Feel the jagged frontier
6. Turn thinking on and off

### 10 — Where This Leads
- AI Prompting in 2026
- How to Think in the AI Era
- Markdown In, HTML Out
- Code You Never Write
- Skills & Connectors
- The Agent Factory's predict–act–observe loop
- Appendix pointer

### 11 — Appendix: A Cockpit Tour of Claude.ai
- **A.1:** Getting in
- **A.2:** The window
- **A.3:** The model ladder
- **A.4:** Thinking and effort
- **A.5:** Context-window settings, instructions, projects, memory and chat history
- **A.6:** Uploads
- **A.7:** Artifacts and files
- **A.8:** Search, Research, Skills and Connectors
- **A.9:** Thirty-minute setup
- **A.10:** What changes and what does not

### 12 — Sources and Further Reading
- Anthropic prompt-engineering documentation
- Claude Help Center
- OpenAI token documentation
- Ouyang et al. (2022)
- Dell’Acqua et al. (2023)
- Andrej Karpathy (2023)

### 13 — Flashcards Study Aid
- Flashcard content
- Verification note retained because interactive card text was not delivered

---

## 🔄 The Big Picture

```text
TRAINING
   │
   ▼
PREDICT NEXT TOKENS
   │
   ▼
GENERATE AN ANSWER
   │
   ├── No built-in guarantee of truth
   ├── Limited to available context
   ├── Confidence may be misleading
   │
   ▼
ADD TOOLS + OBSERVATION LOOP
   │
   ▼
AGENTIC BEHAVIOUR
   │
   ▼
HUMAN VERIFICATION
```

## ✅ Revision Checklist

- [ ] Explain all nine ideas without relying on memorized wording.
- [ ] Distinguish prediction from retrieval.
- [ ] Explain training, inference, weights and statelessness.
- [ ] Recognize hallucination and misleading confidence.
- [ ] Explain tokens, context windows and context rot.
- [ ] Understand sycophancy and the jagged frontier.
- [ ] Distinguish tools, connectors, MCP and agents.
- [ ] Explain what reasoning models can and cannot guarantee.
- [ ] Complete the six practical prompts.
- [ ] Review the Claude.ai appendix and sources.
- [ ] Keep all unverified material clearly marked.

---

## 📌 Completeness and Verification

This overview is a **navigation layer**, not a replacement for the complete topic tree.

The detailed file must retain all **407 nodes**, including every glossary entry, numbered question, nested example, table row, callout, figure, appendix control, source, and verification note.

**Verification notes to preserve:**

The source also contains collapsible content and product-specific details that may change over time. Preserve the original wording and flag time-sensitive details for rechecking rather than silently rewriting them.
