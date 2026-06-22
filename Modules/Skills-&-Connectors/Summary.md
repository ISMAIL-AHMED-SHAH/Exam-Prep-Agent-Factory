
# Skills & Connectors

> [!IMPORTANT]
> **Core Sentence (Yaad Rakhein):**
>
> *"Chat message AI ko batata hai kya karna hai ek dafa. Skill AI ko sikhata hai kaise karna hai har dafa. Connector AI ko hands deta hai aap ke real apps tak pahunchne ke liye."*

**Foundations Course | 5 of 6**
**14 Sections | AI ko ek dafa sikhao, apps se connect karo, zero code**

---

## Table of Contents

* [Part 1 — Do Upgrades](#part-1--do-upgrades)

  * [1. Chat Box se Operating Layer Tak](#1-chat-box-se-operating-layer-tak)
  * [2. Skill Kya Hai](#2-skill-kya-hai)
  * [3. Connector Kya Hai](#3-connector-kya-hai)
  * [4. Skills vs Connectors vs Projects vs Custom Instructions](#4-skills-vs-connectors-vs-projects-vs-custom-instructions)
  * [5. Automatic Ya Manual Trigger?](#5-slash-command-ya-ai-khud-jaan-leta-hai)
* [Part 2 — Jo Pehle Se Mojood Hai](#part-2--jo-pehle-se-mojood-hai)

  * [6. Built-in Skills](#6-built-in-skills)
  * [7. Apps Connect Karna](#7-apps-connect-karna)
  * [8. Skills + Connectors Together](#8-real-magic--skills--connectors-together)
  * [9. Kaunsa Problem Kya Maangta Hai](#9-kaunsa-problem-kya-maangta-hai)
* [Part 3 — Apna Skill Banana](#part-3--apna-skill-banana)

  * [10. AI Se Skill Likhwana](#10-fastest-path--ai-se-likhwana)
  * [11. SKILL.md Ki Anatomy](#11-skillmd-ki-anatomy)
  * [12. Description Field](#12-description-field--sab-se-important-cheez)
  * [13. Test Aur Iterate](#13-test-then-iterate)
  * [14. Save Aur Share](#14-save-karna-aur-share-karna)
* [Part 4 — Same Skill, Paanch Jagah](#part-4--same-skill-paanch-jagah)
* [Part 5 — Safety](#part-5--safely-use-karna)

---

# Part 1 — Do Upgrades

## 1. Chat Box se Operating Layer Tak

Daily frustration:

* Accountant har mahine same formatting instructions paste karta hai
* Doctor har dafa SOAP format explain karta hai
* Marketer har dafa brand voice rules repeat karta hai

AI normally yeh sab chat khatam hone par bhool jata hai.

### Kitchen Analogy

| Component    | Meaning    |
| ------------ | ---------- |
| Kitchen      | Connectors |
| Recipe Cards | Skills     |
| Cook         | AI         |

> [!TIP]
> Sirf kitchen do → AI improvise karega.
>
> Sirf recipes do → AI instructions samjhega lekin real world mein kuch access nahin kar sakega.
>
> Dono do → Consistent, repeatable results.

---

## 2. Skill Kya Hai

Mystery hatane ke baad:

> [!NOTE]
> Skill sirf ek folder hota hai jismein ek text file hoti hai:
>
> ```text
> SKILL.md
> ```

### Minimum Structure

```yaml
name:
description:
```

Aur uske baad plain-English instructions.
---
<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/caf2963b-d1cc-41db-ae2c-5967efce7718" />

---

### Progressive Disclosure

> [!IMPORTANT]
> AI har skill ka sirf description hamesha yaad rakhta hai.
>
> Full instructions tabhi load hoti hain jab request relevant ho.

### Result

* Dozens of skills install ho sakti hain
* Performance slow nahin hoti
* Sirf relevant skill activate hoti hai

---

## 3. Connector Kya Hai

Connector AI ko aap ke apps aur data tak controlled access deta hai.

Yeh generally MCP (**Model Context Protocol**) standard par based hota hai.

### Teen Important Facts

| Rule                          | Meaning                                                 |
| ----------------------------- | ------------------------------------------------------- |
| Permissions inherit hoti hain | AI sirf wahi access kar sakta hai jo aap kar sakte hain |
| Read-only ya Read-Write       | Aap decide karte hain                                   |
| Per-conversation activation   | Aap enable karte hain                                   |

> [!WARNING]
> Google Drive connect karna poori company ko expose nahin karta.
>
> Sirf woh files available hoti hain jin tak aap ke account ki access hai.

---

## 4. Skills vs Connectors vs Projects vs Custom Instructions

| Feature             | One-Line Test                                            |
| ------------------- | -------------------------------------------------------- |
| Skill               | "Main har dafa explain karta rehta hoon kaise karna hai" |
| Connector           | "Main doosri app se data copy-paste karta rehta hoon"    |
| Project             | "Same files aur rules har task mein lagte hain"          |
| Custom Instructions | "Main chahta hoon yeh har jagah hamesha sach ho"         |

### Important Difference

| Feature | Loading Behavior |
| ------- | ---------------- |
| Project | Always loaded    |
| Skill   | On-demand        |

> [!TIP]
> Background knowledge → Project
>
> Repeatable procedure → Skill

---

## 5. Slash Command Ya AI Khud Jaan Leta Hai?

Modern systems mein skills aksar automatically activate hoti hain.

### Default Behavior

| Situation              | Behavior                                |
| ---------------------- | --------------------------------------- |
| Normal request         | AI matching skill khud choose karta hai |
| Specific skill chahiye | Skill ka naam mention karein            |

### Example

```text
Use my monthly-close skill.
```

### Takeaway

> [!IMPORTANT]
> 90% cases mein AI ko skill choose karne dein.
>
> Isi liye description field sab se important hoti hai.

---

# Part 2 — Jo Pehle Se Mojood Hai

## 6. Built-in Skills

Kuch skills already platform mein built hoti hain.

### Common Capabilities

* Word (.docx) generation
* PowerPoint creation
* Excel spreadsheets
* PDF generation

> [!TIP]
> Sirf feature enable karne se yeh tools available ho jate hain.

### Important

> [!NOTE]
> Har built-in skill skill-library mein nazar nahin aati.
>
> Bohat si engine level capabilities hoti hain.

---

## 7. Apps Connect Karna

Usually ek minute se kam lagta hai.

### General Flow

```text
Connectors
    ↓
Choose Service
    ↓
Sign In
    ↓
Authorize
    ↓
Enable
```

### Practical Notes

* Connect karna aur enable karna alag cheezein hain
* Bohat zyada connectors active hon to on-demand mode useful hota hai

### Example

Doctor workflow:

1. AI form generate kare
2. Drive mein save kare
3. Later search kare
4. SOAP note banaye

Same connector:

* Read bhi karta hai
* Write bhi karta hai

---

## 8. Real Magic — Skills + Connectors Together

### Formula

```text
Connector
     +
Skill
     =
Automation
```

### Example: Accountant

| Step                         | Component |
| ---------------------------- | --------- |
| Ledger fetch karna           | Connector |
| Formatting rules apply karna | Skill     |
| Final report generate karna  | Both      |

### Result

> [!SUCCESS]
> 2-hour monthly routine
>
> → 2-minute review process

### Same Pattern

| Role     | Connector | Skill           |
| -------- | --------- | --------------- |
| Marketer | Notion    | Brand Voice     |
| Engineer | Linear    | Design Review   |
| Teacher  | Drive     | Lesson Planning |

---

## 9. Kaunsa Problem Kya Maangta Hai

Do sawal poochiye:

### Friction Test

| Problem                            | Solution  |
| ---------------------------------- | --------- |
| Same formatting repeat hoti hai    | Skill     |
| Apps se data copy-paste karte hain | Connector |
| Dono problems hain                 | Both      |
| One-off answer chahiye             | Neither   |

### Important Cautions

> [!WARNING]
> Har task skill ke layak nahin hota.
>
> Sirf repeatable workflows ko automate karein.

> [!WARNING]
> Har connector ek access point hai.
>
> Sirf woh connect karein jo zaroori ho.

---

# Part 3 — Apna Skill Banana

## 10. Fastest Path — AI Se Likhwana

AI khud skills create karne mein madad kar sakta hai.

### Workflow

```text
Describe Outcome
        ↓
Answer Questions
        ↓
AI Generates SKILL.md
        ↓
Review
        ↓
Save
```

> [!TIP]
> Yeh "Code You Never Write" philosophy ka perfect example hai.
>
> Aap architect hain, coder nahin.

---

## 11. SKILL.md Ki Anatomy

### Level 1 — Frontmatter

```yaml
---
name:
description:
---
```

Yeh hamesha loaded rehta hai.

### Level 2 — Instructions

Actual workflow aur process.

### Level 3 — Optional Assets

```text
references/
assets/
scripts/
```

### Rules

> [!WARNING]
>
> * File ka naam exactly `SKILL.md`
> * Folder name kebab-case mein
> * Name aur description clean text hon
> * Reserved brand names avoid karein

---

## 12. Description Field — Sab Se Important Cheez

AI relevance decide karne ke liye instructions nahin parhta.

Sirf description parhta hai.

### Formula

```text
What it does
+
When to use it
+
Exact trigger phrases
```

### Example

| Bad                | Better                                                                                                  |
| ------------------ | ------------------------------------------------------------------------------------------------------- |
| Helps with reports | Prepares monthly client summaries. Use when user asks for client summary, monthly close, account review |

### Debugging Trick

AI se poochiye:

```text
When would you use my client-summary skill?
```

Agar answer wrong lagta hai:

* Description improve karein
* Trigger phrases add karein
* Negative triggers add karein

### Example

```text
Do NOT use for one-off calculations.
```

---

## 13. Test, Then Iterate

### Build Loop

```text
Generate
    ↓
Review
    ↓
Test Triggering
    ↓
Test Output
    ↓
Test Edge Cases
    ↓
Improve
```

### Common Failures

| Failure                        | Fix                         |
| ------------------------------ | --------------------------- |
| Skill trigger nahin hoti       | Description vague hai       |
| Har cheez par trigger hoti hai | Description broad hai       |
| Wrong output                   | Instructions improve karein |

> [!TIP]
> Description aur trigger phrases aksar sab se pehla fix hote hain.

---

## 14. Save Karna Aur Share Karna

Skill complete hone ke baad:

```text
Save Skill
```

### Result

* Personal Skills mein store ho jati hai
* Automatically enabled ho sakti hai
* Private rehti hai

### Team Plans

> [!NOTE]
> Organizations:
>
> * Skills share kar sakti hain
> * Directory publish kar sakti hain
> * Updates automatically propagate ho sakti hain

---

# Part 4 — Same Skill, Paanch Jagah

## Portability — Open Standard

Ek hi `SKILL.md` multiple environments mein use ho sakti hai.

### Surfaces

| Surface                  | Use Case          |
| ------------------------ | ----------------- |
| Claude.ai                | General users     |
| Cowork / OpenWork        | Knowledge workers |
| Claude Code / OpenCode   | Developers        |
| Other compatible systems | Shared standards  |

### Important Difference

| Open Skills  | Vendor Features   |
| ------------ | ----------------- |
| Portable     | Locked            |
| Reusable     | Platform-specific |
| Standardized | Proprietary       |

> [!WARNING]
> Custom GPTs aur Gems jaisi systems platform-specific ho sakti hain.
>
> Standard skill formats zyada portable hoti hain.

---

# Part 5 — Safely Use Karna

## Do Real Risks

### 1. Malicious Skills

> [!WARNING]
> Skill sirf text file hoti hai.
>
> Hidden instructions harmful behavior trigger kar sakti hain.

Possible dangers:

* Prompt injection
* Data exfiltration
* Unexpected actions

---

### 2. Over-Broad Connector Access

> [!WARNING]
> Write access galat jagah dene se:
>
> * Files modify ho sakti hain
> * Emails send ho sakti hain
> * Data delete ho sakta hai

---

## Safe-Use Checklist

### Skills

* [x] Trusted sources se install karein
* [x] SKILL.md khud parhein
* [x] AI se summary mang kar verify karein

### Connectors

* [x] Read-only se start karein
* [x] Write access gradually dein
* [x] Minimum required scope use karein
* [x] Backup aur recovery process samjhein

### General Rule

> [!IMPORTANT]
> **Least Privilege Principle**
>
> AI ko sirf utni access dein jitni workflow ko waqai zaroorat ho.

---

# Skills & Connectors Recap

| Concept             | One-Line Summary                                   |
| ------------------- | -------------------------------------------------- |
| Skill               | AI ko repeatable process sikhata hai               |
| Connector           | AI ko real apps aur data tak access deta hai       |
| Project             | Shared context aur files hamesha loaded rakhta hai |
| Custom Instructions | Global preferences store karta hai                 |
| Skills + Connectors | Real automation enable karte hain                  |
| Description         | Skill ka most important hissa                      |
| Safety              | Minimum access, maximum control                    |

---

> [!SUCCESS]
> **One-Line Summary**
>
> Skills AI ko **kaise kaam karna hai** sikhati hain, Connectors AI ko **kahan kaam karna hai** batate hain, aur dono mil kar simple chat ko repeatable real-world automation mein badal dete hain.
