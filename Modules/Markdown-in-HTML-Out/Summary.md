
# 📝 Markdown In, HTML Out

> **14 Concepts · 4 Parts**  
> *GIAIC Agent Factory | Foundations Course*

---

## 📖 Overview

This chapter explains the two most important document languages used in AI workflows:

- **Markdown** → Best for communicating with AI.
- **HTML** → Best for communicating with humans.

Learning when and where to use each format makes your prompts clearer, your outputs more readable, and your workflow far more efficient.

> [!IMPORTANT]
> **Golden Rule**
>
> - **You → AI = Markdown**
> - **AI → Human = HTML**
> - **AI → AI = Markdown**

---

## 📽️ Presentation

Click the image below to open the slides.

[![Google Slides](images/slides-preview.png)](https://docs.google.com/presentation/d/1P2nO1M7s5TMpOA8cTOMVy1mPiIgv6KKalm0nJlKoG90)

## 🎯 Learning Outcomes

By the end of this chapter, you'll understand:

- Why structure matters more than long prompts
- When to use Markdown vs HTML
- How to write clean AI specifications
- How to publish AI-generated content
- Which document format fits each use case

---

# 📑 Table of Contents

- [Introduction](#introduction--two-document-languages)
- [Part 1 — The Two Languages](#part-1--the-two-languages)
- [Part 2 — Markdown: The Writing Language](#part-2--markdown-the-writing-language)
- [Part 3 — HTML: The Reading Language](#part-3--html-the-reading-language)
- [Part 4 — Three Working Modes](#part-4--one-exercise-three-motions)
- [Quick Recap](#quick-recap)

---

# Introduction — Two Document Languages

**Markdown** is plain text with lightweight formatting symbols.

Examples:

```md
# Heading

- Bullet

1. Numbered List

**Bold**
```

**HTML** is the language used to build web pages.

The real skill isn't learning both languages—

it's knowing **when to use each one.**

---

## Power User Workflow

| Direction | Best Format |
|------------|-------------|
| You → AI | Markdown |
| AI → Human | HTML |
| AI → AI | Markdown |

> [!TIP]
> Before writing anything, ask:
>
> **"Who is the final reader?"**
>
> - Browser → HTML
> - AI / Future Chat → Markdown
> - Social Media → Plain Text

---

# Part 1 — The Two Languages

---

# Concept 1 — Why Agents Need Structure

Agents understand structured information much better than long paragraphs.

## Example

❌ Hidden inside prose

```
Budget should not exceed PKR 50,000.
```

✅ Separate heading

```md
## Budget

Maximum: PKR 50,000
```

Nothing changed except the visibility.

> [!IMPORTANT]
> Critical constraints deserve their own heading—not a sentence hidden inside a paragraph.

---

# Concept 2 — Markdown In, HTML Out

Markdown is ideal for AI.

HTML is ideal for humans.

| Direction | Format | Why |
|------------|---------|-----|
| You → Agent | Markdown | Removes ambiguity |
| Agent → Human | HTML | Beautiful, readable, shareable |
| Agent → Agent | Markdown | Compact context |

> [!NOTE]
> If humans will read the final result in a browser, choose **HTML**.
>
> If another AI (or future chat) will read it, choose **Markdown**.

---

# Part 2 — Markdown: The Writing Language

---

# Concept 3 — Headings

Use headings to organize information.

## Rules

- One `#` title per document
- Don't skip heading levels
- Write headings as claims

### Example

❌ Budget

✅ Budget: PKR 50,000 Maximum

---

# Concept 4 — Lists

Use the right list for the right purpose.

| Type | Best For |
|--------|----------|
| Bullets | Unordered items |
| Numbers | Sequential steps |

### Better Bullet

❌ Website should load quickly.

✅ Website should load in under **3 seconds on a 3G connection.**

> [!TIP]
> Every requirement should be measurable.

---

# Concept 5 — Code Blocks

Triple backticks create fenced code blocks.

````text
```python
print("Hello")
```
`````

Benefits:

* Separates instructions from data
* Prevents confusion
* Shows examples clearly

> [!IMPORTANT]
> Examples are better than descriptions.

---

# Concept 6 — Links and Images

Links give AI access to real content.

Images should always include meaningful captions.

### Bad

```
Image.png
```

### Better

```
Homepage wireframe showing navigation redesign
```

> [!TIP]
> AI reads the caption before understanding the image.

---

# Concept 7 — Your First Complete Specification

A good specification contains six sections.

```text
Goal
↓
Context
↓
Requirements
↓
Hard Constraints
↓
Out of Scope
↓
Expected Output
```

### Why Each Section Matters

| Section          | Purpose                   |
| ---------------- | ------------------------- |
| Goal             | Defines success           |
| Context          | Gives background          |
| Requirements     | Lists features            |
| Hard Constraints | Prevents mistakes         |
| Out of Scope     | Prevents over-engineering |
| Expected Output  | Prevents format drift     |

> [!WARNING]
> Validate the specification before execution.

---

# Part 3 — HTML: The Reading Language

---

# Concept 8 — Why Ask for HTML?

HTML makes information easier to consume.

Benefits:

* Better information density
* Easy navigation
* Shareable
* Interactive
* Easy to reuse

> [!NOTE]
> For short answers, HTML is unnecessary.
>
> Plain text is faster.

---

# Concept 9 — Prompting for HTML

Don't write HTML yourself.

Instead, describe:

1. Who will read it
2. What it should accomplish
3. Whether it should be interactive
4. How it will be consumed

---

# Concept 10 — Five HTML Patterns

| Pattern              | Best Use                 |
| -------------------- | ------------------------ |
| Plans & Explorations | Compare multiple options |
| Explainers & Reports | Long reports             |
| Code Reviews         | Annotated code           |
| Design Prototypes    | UI mockups               |
| Throwaway Editors    | One-time tools           |

---

# Concept 11 — Browser vs Social Media

Social platforms ignore HTML.

## WhatsApp

Supports:

* *Bold*
* *Italic*

## LinkedIn

* Strong opening line
* Plain formatting

HTML matters only for:

* Preview cards
* Generated images

> [!WARNING]
> Never paste raw HTML into social media.

---

# Concept 12 — Publishing Options

| Need               | Recommended Tool  |
| ------------------ | ----------------- |
| Quick sharing      | Claude.ai Publish |
| Store file         | GitHub Gist       |
| Permanent website  | GitHub Pages      |
| Easiest deployment | Netlify           |

---

# Concept 13 — Choosing the Right Document Format

Choose based on the destination.

| Destination      | Format |
| ---------------- | ------ |
| Read only        | HTML   |
| Print / Sign     | PDF    |
| Edit             | Word   |
| Present          | Slides |
| Spreadsheet      | Excel  |
| Machine-readable | CSV    |

> [!TIP]
> CSV is to structured data what Markdown is to structured text.

---

# Part 4 — One Exercise, Three Motions

---

# Concept 14 — Three Working Modes

## 💬 Chat

Works only with pasted content.

---

## 💻 Terminal

Can access an entire project folder.

---

## 🖥️ Desktop

Visual interface.

Shows a plan.

Waits for approval.

> [!IMPORTANT]
> Always ask:
>
> **"Show me the plan first. Don't execute anything until I approve."**

---

# 📝 Quick Recap

| Concept | Summary                                          |
| ------- | ------------------------------------------------ |
| 1       | Structure improves AI accuracy                   |
| 2       | Markdown In → HTML Out                           |
| 3       | Use meaningful headings                          |
| 4       | Bullets for sets, numbers for sequences          |
| 5       | Triple backticks separate data from instructions |
| 6       | Links and captions improve understanding         |
| 7       | Every spec should have six sections              |
| 8       | HTML improves readability                        |
| 9       | Describe the desired HTML instead of writing it  |
| 10      | Five reusable HTML patterns                      |
| 11      | Social media prefers plain text                  |
| 12      | Publish using Claude, Gist, Pages, or Netlify    |
| 13      | Choose format based on destination               |
| 14      | Three modes: Chat, Terminal, Desktop             |

---

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/1c984740-39ad-478a-a49a-4db03c639dcb" />


# 🎓 Graduation Signal

You're ready for the next level when:

* You naturally write prompts in Markdown.
* You request HTML for reports and documentation.
* You organize requirements using headings and lists.
* You think about the final reader before choosing a format.

---

> [!SUCCESS]
> **One-Line Summary**
>
> Great AI users write **Markdown for machines** and generate **HTML for people**.

```
```
