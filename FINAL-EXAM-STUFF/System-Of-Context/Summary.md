# 🔗 The System of Context: Connecting the Records to Real Work

> **Course:** GIAIC Final Exam Marathon · Part 2 — Get Ready for the Market
> **Prerequisite:** [Designing the Vertical SoR](./designing-vertical-sor-notes.md)
> **Note:** Yeh **bohot bara** chapter hai. Templates section (aakhir mein) source page pe truncate ho gaya — baaqi **poora** mil gaya (11 major sections + Ayesha ka poora example + 8 invariants + 11 failure modes).

---

## 📑 Table of Contents

- [Core Idea](#-core-idea)
- [Fourteen Key Words](#-fourteen-key-words)
- [1. Why the Vertical SoR Is Necessary and Not Enough](#1-why-the-vertical-sor-is-necessary-and-not-enough)
- [2. Two Kinds of Record, and the Layer Above Them](#2-two-kinds-of-record-and-the-layer-above-them)
- [3. Three Layers, Three Jobs](#3-three-layers-three-jobs)
- [4. The One Law: Authority Never Moves](#4-the-one-law-authority-never-moves)
- [5. The Model Is Not a Source Either](#5-the-model-is-not-a-source-either)
- [6. Authority Is Scoped Across Many Records](#6-authority-is-scoped-across-many-records)
- [7. The Three Questions, Three Paths](#7-the-three-questions-and-the-three-paths)
- [8. The Context Packet](#8-what-the-layer-assembles-the-context-packet)
- [9. What May Be Indexed, What Must Be Asked](#9-what-may-be-indexed-and-what-must-be-asked)
- [10. Permission Comes Before the Model](#10-permission-comes-before-the-model)
- [11. Provenance Travels With Every Item](#11-provenance-travels-with-every-item)
- [12. Conflict Is a Result, Not a Failure](#12-conflict-is-a-result-not-a-retrieval-failure)
- [13. Read, Reason, Act, and Record](#13-read-reason-act-and-record)
- [The Eight Invariants](#the-eight-invariants-of-the-connecting-layer)
- [Where It Sits in the FDE AF Model](#where-it-sits-in-the-fde-af-model)
- [Consolidate by Default, Specialize Deliberately](#consolidate-by-default-specialize-deliberately)
- [The Open Reference Implementation](#the-open-reference-implementation)
- [When You Do Not Need One](#when-you-do-not-need-one)
- [Two Temperaments, One Layer](#two-temperaments-one-layer)
- [Ayesha Connects Her First Customer](#ayesha-connects-her-first-customer)
- [The Eleven Failure Modes](#the-eleven-failure-modes)
- [❌ Common Mistakes](#-common-mistakes)
- [💡 Pro Tips](#-pro-tips)
- [🧠 Memory Tricks](#-memory-tricks-yaad-rakhne-ke-tareeqe)
- [📌 One-Line Chapter Summary](#-one-line-chapter-summary-table)

---

## 🎯 Core Idea

> **One sentence:** *System of Record decide karta hai kya sach hai. System of Context decide karta hai kya pohanchta hai.*

> 💡 **In Plain Words:** Aapke records batate hain profession ko kya chahiye. Customer ke apps batate hain abhi kya ho raha hai. System of Context dono connect karta hai, current task ke liye jo relevant hai woh dhoondta hai, permission check karta hai, har source label rakhta hai, aur ek cited bundle handover karta hai. **Yeh apni koi truth add nahi karta. Yeh kabhi new source of truth nahi banta.**

<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/143ad4d9-89f8-4d9b-84bf-71ca55ffd753" />


> ❗ **Naming Honesty:** "System of Context" is book ki apni coinage nahi — Glean (market ka best-known naam) yeh term already use karta hai. Book jaan-boojh kar market ke words use karti hai. Lekin book isse **narrower** use karti hai — vendor ke liye yeh product hai, is book ke liye yeh **architectural position** hai (2 SoRs ke upar, Worker ke neeche, authority kabhi hold nahi karta).

---

## 📖 Fourteen Key Words

| Word | Plain Meaning |
|---|---|
| **System of Context** | Layer jo sources connect karti hai, current task ke liye assemble karti hai |
| **Authority** | Source ka right ek specific question settle karne ka |
| **Authority routing** | Decide karna kaunsa source govern karta hai, retrieval se **pehle** |
| **Context packet** | Temporary, cited bundle — ek actor, ek case, ek moment ke liye |
| **Provenance** | Item kahan se aaya, kiska hai, kaunsi version, kab parha gaya |
| **Connector** | Controlled path ek source mein — content + access rules dono carry karta hai |
| **Indexed context** | Content ek searchable index mein copy hui, sync hoti rehti hai |
| **Live context** | Current information, source se fetch hoti hai task chalte waqt |
| **Permission inheritance** | Har item ke access rules uske home system se har result mein carry hote hain |
| **Governed truth** | SoR se content — citable, class/version/scope ke saath |
| **Supporting context** | Ungoverned source se content — evidence ki tarah citable, rule ki tarah kabhi nahi |
| **Federated** | Kai alag records, har ek apni authority rakhta hai, ek layer joins bina merge kiye |
| **Canonical** | Original, official version — copy ke opposite |
| **Chunking** | Document ko chhote pieces mein katna, search index ke liye |

---

## 1. Why the Vertical SoR Is Necessary and Not Enough

> 💡 **In Plain Words:** Aapka record profession jaanta hai. Yeh customer ka current contract, aaj ki delivery, latest approval, ya woh message jo ek exception explain karta hai — nahi jaanta. Worker ko dono chahiye.

Ab aapke paas **2 Systems of Record** hain: **Agent Factory SoR** (shared method — architecture, FDE AF Model, standards — har customer pe identical) aur **Vertical SoR** (profession — corpus, map, reflexes, invariants, hierarchy, permissions — sirf aapki).

> ⚠️ **Warning:** Dono mein se koi bhi customer ki operating situation nahi jaanta. Worker ko 2 sawaal ek saath jaanne hote hain: **"Profession kya require karti hai?"** aur **"Is case mein abhi kya sach hai?"**

> 📌 **Key Takeaway:** Yeh layer skip karo, to lesson hard way seekhte ho — Worker standard perfectly cite karega, contract dhoond nahi payega. **Ek brilliant graduate, pehle din, textbook pakde, ek building mein jahan kisi ne filing cabinet nahi dikhaya.**

---

## 2. Two Kinds of Record, and the Layer Above Them

> 💡 **In Plain Words:** "Record" ab do cheezein cover karta hai. Customer ka ERP "kya hua" ka record hai. Aapki Vertical SoR "profession kya require karti hai" ka record hai. Dono authoritative hain, koi doosre ka sawaal jawab nahi de sakta. System of Context koi record hi nahi hai.

|  | **Traditional SoR** | **Governed Knowledge Record** | **System of Context** |
|---|---|---|---|
| Kya hai | ERP, CRM, HRIS, ledger | Agent Factory SoR + Vertical SoR | Connecting layer |
| Kya owns karta hai | **State** — kya hua, balance kya hai | **Rules & method** — profession kya require karti hai | **Koi truth nahi** — connectors, indexes, routing, permissions |
| Kis pe authoritative | Apne scope ke facts | Profession ki requirements | **Kisi bhi sawaal pe nahi** |
| Sawaal jo answer karta hai | Number kya hai? | Rule kya hai? | Abhi is task ke liye relevant kya hai? |
| Kaun banata hai | Customer, decades mein | Aap, apne expert ke saath | Aap, har customer pe |

> ❗ **Important:** **Dono pehle 2 columns Systems of Record hain, dono authoritative hain.** Ek state ka malik, dusra rules ka. Ledger nahi bata sakta treatment sahi hai ya nahi. Standard nahi bata sakta balance kya hai. Ek se doosre ka sawaal poochho, confident **useless** jawab milega.

<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/3b57c93c-8b3b-4ff6-a8e1-07ad3e741e18" />


### QuickBooks Holds the Data. Not the Profession.

> 📝 **Example:** QuickBooks poochho account 1200 mein kya hai — exact jawab milega. Poochho Henderson lease finance lease ki tarah classify honi chahiye thi ya nahi — **kuch nahi milega.** **QuickBooks authoritative hai kya record hua. Aapka record authoritative hai kya record hona chahiye tha.**

> ⚠️ **One Word of Caution:** Vendor material yeh distinction "storage vs interpretation" keh kar bayan karta hai — jo seller ke favor mein bent hai. **Sahi baat:** traditional record apne domain mein authoritative + complete hai, uske bahar silent hai. **"Gap scope ka hai, seriousness ka nahi."** Isse "storage" kehna finance director ko bata dega aap uski duniya kitni kam samajhte ho.

---

## 3. Three Layers, Three Jobs

> 💡 **In Plain Words:** Ek layer se teeno kaam mat karwao. Records truth ke malik hain. Context layer relevant cheez assemble karti hai. Worker reason/act karta hai.

| Layer | Sawaal | Kaam | Kabhi Yeh Na Bane |
|---|---|---|---|
| **Systems of Record** | Officially kya sach hai? | Facts/rules/versions/permissions govern karna | Loose search index |
| **System of Context** | Abhi is task ke liye kya relevant hai? | Connect/route/retrieve/filter/rank/label/cite/assemble | Shadow source of truth |
| **Human/AI Worker** | Kya conclude/karna chahiye? | Reason, decide (authority ke andar), act, evidence produce | Apna ungoverned policy maker |

> 📌 **The One Distinction:** *System of Context **access** mein upar baithta hai, **authority** mein nahi.* Woh sab dekh sakta hai. Woh outrank nahi karta. **Access upar point karta hai. Authority wapas source ki taraf point karti hai.**

<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/c9d6d467-df53-493a-80ce-e6acb5ac8c93" />

---

## 4. The One Law: Authority Never Moves

> 💡 **In Plain Words:** Ek delivery driver socho. Driver parcel deta hai. Parcel sender ka hai, driver ka nahi. System of Context driver hai. Record sender hai. Jab Worker bataye jawab kahan se aaya, usse **record** naam lena chahiye, **driver** kabhi nahi.

> **📌 The Law:** *System of Context authority carry karta hai. Yeh kabhi hold nahi karta.*

Jab Worker ek standard cite karta hai, citation **register row** ki taraf point karti hai (publisher, class, jurisdiction, version, stable ID) — context layer ki taraf nahi, na uski rakhi hui copy ki taraf. **Copy ek finding aid hai. Record source hai.**

> ⚠️ **Warning — Jab Yeh Matter Karta Hai:** Standard supersede hota hai, aapka **impact record** trace karta hai kaunse maps/reflexes/evals move hone chahiye — yeh chain record se hoti hai. Context layer ko dusri authority banne do, chain ek branch grow karti hai jo koi govern nahi karta. Corpus current hai, Worker purana rule quote karta hai index se jise kabhi message nahi mila.

<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/a1e9ef81-2d9c-490b-9f62-53286ccd8cc1" />

---

## 5. The Model Is Not a Source Either

> 💡 **In Plain Words:** Upar wala law kehta hai authority records mein rehti hai, connecting layer mein kabhi nahi. Yeh model mein bhi nahi rehti. Model information pe achha reason kar sakta hai. Yeh **woh jagah nahi ban sakta jahan se information aati hai.**

> ⚠️ **Model Ke Paas Koi Source Nahi Hota.** Weights ek training corpus ka compression hain, record nahi. Koi register row nahi — publisher, authority class, jurisdiction, version, effective period, owner, rights basis, koi bhi nahi, aur baad mein add nahi ho sakti.

> ❗ **"Plausibility is not provenance."** Model **most likely continuation** produce karta hai. Ek rule jo rule jaisa lage aur ek rule jo asal mein rule ho — same shape hai. Isliye fluency **koi information nahi deti** correctness ke baare mein.

> 📌 **The Settling Test:** *"Kya reviewer is conclusion ko record se rebuild kar sakta hai, model se poochhe bina?"* Haan → model ne reason kiya. Nahi → model source tha, conclusion defensible nahi hai.

### Three Places the Model Quietly Becomes the Source

| # | Trap | Cure |
|---|---|---|
| 1 | **The gap fill** — retrieval kuch nahi deti, model guess kar deta hai, koi error nahi dikhta | Missing evidence packet ka field ho; reflex jo source na milne pe escalate kare |
| 2 | **The drifting paraphrase** — sahi passage retrieve hota hai, apne alfaz mein restate hota hai, threshold ghum jaati hai | Governing text quote/cite karo, re-express mat karo |
| 3 | **Unmanaged persistent model memory** | Facts kisi ke bina owner/version ke sessions mein carry hote hain — shadow record product feature se aata hai |

> 💡 **What the Model Is Actually For:** 10-80-10 ka **middle 80%** — execution layer. Records governed intent (10%) dete hain, model apply karta hai (80%), named human close karta hai (10%). **System of Context isliye exist karta hai kyunke middle 80% ko supply chahiye, model khud ko supply nahi kar sakta.**

<img width="1448" height="1086" alt="image" src="https://github.com/user-attachments/assets/1932fe34-0b24-4923-987c-b630e726531a" />

---

## 6. Authority Is Scoped Across Many Records

> 💡 **In Plain Words:** Koi single document har sawaal nahi jeetta. Aapka record professional work govern karta hai. Signed contract apni terms govern karta hai. ERP govern karta hai invoice post hua ya nahi. **Federated** = kai records, har ek apni authority rakhte hue, ek layer joins karta hai bina kisi ko merge kiye.

> ❗ Aapka record pehle hi refinement de chuka hai: hierarchy **hamesha ek ladder nahi hoti** — higher source **sirf tab** jeetta hai jab dono same question address karein. System of Context isse unavoidable banata hai.

### 8 Questions Jo Request Ki Shape Resolve Karte Hain

1. Kaunsi profession is sawaal ki malik hai?
2. Kaun pooch raha hai?
3. Kis customer, kis case ke liye?
4. Kaunsa task perform ho raha hai?
5. Kaunsi jurisdiction, kaunsi effective date?
6. Kaunsa source har fact/rule ka malik hai?
7. Yeh insaan/Worker kya parh sakta hai?
8. Koi action follow ho sakta hai to kya?

> 📌 **Sawaal 1 Sab Se Pehle Hai:** **"Relevance authority nahi hai. Retrieval candidates dhoondti hai. Governance decide karti hai kya count hota hai."**

### The Portfolio, Not the Pair

> ❗ [Choosing Your Vertical] kehta hai ek banao — ek profession, ek country, ek expert. Yeh advice change nahi hoti. Lekin customer jahan deploy karte ho ek **company** hai, profession nahi — company kai verticals ek saath chalati hai.

**3 Rules:**
1. **Ek vertical ki methodology apni seam kabhi cross nahi karti** — sales record ka qualification method revenue-recognition question pe **koi authority nahi** rakhta, chahe words overlap ho ke achha retrieve ho
2. **2 records ko kabhi ek corpus mein merge mat karo** — blended page kisi bhi profession mein cite nahi ho sakta
3. **Aapka asset compose hota hai** — poori company ki knowledge own karne ki zaroorat nahi, ek profession deeply own karo

> 📌 **Kya Multiply Nahi Hoti:** Kai Vertical SoRs hoti hain, lekin **exactly ek** Agent Factory SoR — kyunke banane/governing ka method har profession mein same hai.

<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/c75ac7a9-287a-4480-a2c2-bfa70f2ff483" />
---
### One Business Event, Several Governing Records

> 📝 **Example:** "20% discount, is quarter revenue" — ek sentence, **ek sawaal nahi**. Qualification→Sales. Discount authority→Sales. Enforceability→Legal. Checks→Compliance. Revenue timing→Accounting. Tax→Tax. Kya discuss hua→**koi record nahi, supporting context**. Delivery→live query. Invoice→live query.

> ⚠️ **Seams Hi Interesting Disagreements Hain:** Sales sahi keh sakta hai "deal June mein close hua." Accounting sahi keh sakta hai "revenue abhi recognize nahi ho sakti." **Dono sahi hain** — do professions do alag sawaal answer kar rahi hain. Worker jo inhe blend kare, ek claim banata hai jo **kisi profession ne nahi kiya**. Yeh "resolved by scope" hai.

<img width="1448" height="1086" alt="image" src="https://github.com/user-attachments/assets/f5921d87-724c-4b57-873b-29a2ba5cd518" />


---

## 7. The Three Questions, and the Three Paths

> 💡 **In Plain Words:** Worker sirf 3 tarah ke sawaal poochta hai. Rule kya hai? Number kya hai? Is case ke baare mein log kya keh rahe the? Har sawaal ka apna path, apna source type.

| Sawaal | Source | Path | Kya Milta Hai |
|---|---|---|---|
| Rule kya hai? | Vertical/Agent Factory SoR | Retrieval, governed authored pages | Governed truth, citable |
| Number kya hai? | Jo system usse own karta hai | Typed query, MCP | Exact current value, ya honest failure |
| Case ke baare mein kya kaha gaya? | Customer ke apps | Retrieval, ungoverned corpus | Supporting context — evidence, kabhi governing rule nahi |

> ⚠️ **Warning:** Worker jo pehchan na sake kaunsa sawaal poochh raha hai, teenon ko same tareeqe se answer karega — teesra path chupke se pehle do ko **swallow** kar lega.

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/f414a7de-c35a-49b6-8ba3-0347a481dd16" />


---

## 8. What the Layer Assembles: The Context Packet

> 💡 **In Plain Words:** System of Context har matching paragraph ek prompt mein nahi daalta. Yeh ek controlled package banata hai: governing rules, current facts, supporting context, conflicts, missing evidence, permissions, citations.

**7 Operations:** Connect → Identify (actor/Worker/customer/case/jurisdiction/date/action) → Retrieve → Filter (permission/scope) → Rank (sirf similarity nahi — authority, applicability, freshness, case identity, confidence, completeness) → Assemble → Deliver (record karo kya hua).

> ⚠️ **Assembly Warning:** Packet ek budget ke against banta hai (finite context window). Compression legitimate hai — **lekin "compress the prose, never compress the provenance."** Version stamp drop karna, 2 sources ko ek sentence mein merge karna — evidence ko text mein convert karna hai.

### Packet Contents

| Part | Kya |
|---|---|
| Request | Task, actor, customer, case, jurisdiction, date, action |
| Governing authority | Exact rules/standards/policies/reflex steps |
| Current facts | Live/synced facts |
| Supporting context | Messages, notes, drafts, background |
| Conflicts | Disagreeing sources, authority/scope/dates preserved |
| Missing evidence | Reflex ko chahiye, layer nahi mila |
| Permission envelope | Kya read/recommend/prepare/execute ho sakta hai |
| Citations | Har material claim ke liye stable references |

### The Packet Is Temporary — 3 Constitution Rules

1. **Packet authority inherit karta hai.** Kabhi banata nahi.
2. **Packet permissions inherit karta hai.** Kabhi widen nahi karta.
3. **Packet expire hota hai.** Current facts refresh hote hain jab freshness answer badal sakti ho.

> 📌 **Key Takeaway:** Durable cheez source + evidence hai jo task ke baad wapas likhi jaati hai. Packet sirf **working view** hai.

<img width="1166" height="1349" alt="image" src="https://github.com/user-attachments/assets/6cc61fae-39e0-44ff-aecd-eaf5da48f2d3" />

---

## 9. What May Be Indexed, and What Must Be Asked

> 💡 **In Plain Words:** 3 tarah ki information Worker tak pohanchti hai, har ek alag route se. Customer ke emails/chat/files index ho sakte hain. Aapke governed pages bhi index ho sakte hain, lekin record ko **confirm** karna chahiye Worker rely karne se pehle. Live numbers **har baar poochne padte hain**.

> **📌 The Whole Rule:** *Index working context. Discover governed knowledge. Query current truth live.*

### Governed Knowledge: Discover, Phir Confirm

**Discovery poochta hai:** relevant info kahan exist kar sakti hai? (recall, similarity, speed ke liye optimize) — output ek **pointer** hai: "yahan dekho."
**Confirmation poochta hai:** kaunsa source officially applicable hai is decision pe? (domain, class, jurisdiction, version, effective date, applicability, approval, permission, canonical identity check karti hai) — output ek **answer** hai: "yeh govern karta hai."

> 📌 **Fixed Sequence:** Search discovers → Layer routes → Applicable record confirms → Worker cites/reasons → Checkers validate → Governed tools act/record.

<img width="1638" height="960" alt="image" src="https://github.com/user-attachments/assets/bb222c51-de30-4441-a016-569c0b2e76fd" />

### Current State: Har Baar Poochho

> ⚠️ **Warning — The Deciding Sentence:** *"Agar stale value conclusion, permission, payment, filing, ya customer action badal sakti hai, live fetch karo."* Same source ko 2 modes chahiye ho sakte hain — contract indexed (clauses dhoondhne ke liye) + contract system live query (confirm karne ke liye version still active hai).

### The Ungoverned Stays Ungoverned

> ❗ Customer ki working material **kabhi aapki corpus nahi banti** — **supporting context** rehti hai. Sirf tab move hoti hai jab pattern 3+ customers pe repeat ho, de-identified ho, promotion review pass kare, aapke expert se apni awaaz mein rewrite ho.

### Why Chunking Is Where Governance Disappears

> ⚠️ **Important:** Ek SoR entry **12 cheezein** carry karti hai (stable ID, domain, class, jurisdiction, version, effective date, approval, applicability, owner, superseded-by, checker, permission boundary). Generic indexing pipeline sirf **sentence** preserve karti hai — 12 controls gaayab, kuch bhi announce nahi karta unki absence.

> 📌 **The Refusal:** Ek single vector database jismein chat + contract + sales rule + accounting policy sab mil jayein, System of Context **nahi hai** — yeh ek **accidental shadow System of Record** hai.

<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/5031edd9-710c-4173-a8fd-61d2807bf2fa" />

---

## 10. Permission Comes Before the Model

> 💡 **In Plain Words:** Sab kuch retrieve mat karo aur baad mein forbidden parts chhupao. Jo cheez reader nahi dekh sakta, woh model context mein **kabhi entry hi na kare**.

> ⚠️ **The Skipped Invariant:** Yeh skip karna sab kuch aasan bana deta hai — **6 hafton tak.** Document ke access rules uske home system mein rehte hain. Layer copy kare, to access rules bhi saath copy hone chahiye, aur **har query pe dobara check** hone chahiye.

**3 Alag Permission Sawaal:**
1. Kya yeh insaan yeh source dekh sakta hai?
2. Kya yeh Worker (is task ke liye) yeh source dekh sakta hai?
3. Kya Worker woh action perform kar sakta hai jo follow ho sakti hai?

> ❗ **"A hidden passage inside the model context is not hidden."** Retrieve everything → model ko bhejo → model ko bolo mat batana — yeh unsafe order hai. Safe order: identity resolve → source permissions resolve → filter → retrieve/rank → assemble → **action permission** alag se, tool boundary pe.

<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/ee8285dc-a52d-43c6-a322-0322e43d6b0e" />

### Why This Is a Control Question, Not Only Privacy

> ⚠️ **Segregation of Duties** combinations ke baare mein hai, visibility ke baare mein nahi. **Real exposure zyada broad hai:** access control poori control environment ki foundation hai. Firm ka periodic access review ek user ke specific entitlements certify karta hai. Layer usse content de deta hai jo woh entitlements kabhi grant nahi karte — **koi cheez churayi nahi gayi, koi documented rule nahi tootha, lekin access review ab ek jhooti tasveer certify kar raha hai.**

> 📌 **The Argument to Make:** *"Context layer jo entitlement model se bahar effective access grant karta hai, ek control nahi todta — yeh chupke se woh review invalidate kar deta hai jo sab controls ko certify karti hai."*

---

## 11. Provenance Travels With Every Item

> 💡 **In Plain Words:** Ek useful jawab sirf sentence nahi dikhata. Yeh dikhata hai sentence kahan se aaya, kaunsi version, kya govern karta hai, kya current tha.

| Field | Kyun Zaroori |
|---|---|
| Source system | Owner identify karta hai |
| Stable ID | Reviewer dobara exact item retrieve kar sake |
| Authority class | Law/standard/contract/policy/transaction/guidance/message/example |
| Scope | Kaunsa sawaal, customer, jurisdiction, case |
| Version + effective period | Retired rules silently return na ho |
| Owner | Kaun responsible hai |
| Retrieved/synced at | Kitna fresh tha |
| Permission basis | Yeh reader kyun allowed tha |
| Citation | Human check kar sake |

> 📌 **Bina Provenance Ke, Packet Text Ka Dher Hai. Iske Saath, Reviewable Evidence Hai.**

### Governed Truth vs Supporting Context (Second Axis)

> ⚠️ **The Failure to Watch:** Worker se poocha jaye "cost capitalize karni chahiye?" Best-matching passage: 3-saal purana email — "hum yeh hamesha capitalize karte hain." Fluent, relevant, **precisely wrong as a basis.** Sahi jawab: requirement standard se route karo, email ko sirf past-practice evidence ki tarah use karo, agar disagree karein to flag karo. **12 mahine repeat hui accounting error phir bhi error hai.**

---

## 12. Conflict Is a Result, Not a Retrieval Failure

> 💡 **In Plain Words:** Jab 2 sources disagree karein, unhe ek sentence mein blend mat karo jo koi source ne kaha hi nahi. Disagreement visible rakho, decide karo kaunsa source govern karta hai, escalate karo jab authority settle na kar sake.

**3 Outcomes:**
- **Resolved by scope** — sources alag sawaal answer karti hain, dono apne sawaal pe sahi hain (2 verticals ka seam — everyday case)
- **Resolved by authority** — ek applicable source govern karta hai, hierarchy batati hai kaunsa
- **Unresolved** — Worker escalate karta hai, evidence already organized ke saath

> 📌 **"A trustworthy System of Context does not make disagreement disappear. It makes disagreement reviewable."**

<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/acd1ec71-c260-4401-84af-b41f9620f545" />

---

## 13. Read, Reason, Act, and Record

> 💡 **In Plain Words:** Dhoondhna karna jaisa nahi hota. Layer dhoondti hai. Worker sochta hai. Governing record rules check karti hai. Tool action karta hai. Jo system result ka malik hai, woh likh leta hai.

**5 Alag Jobs, Hamesha Yehi Order:** Layer find+understand → Worker permitted reasoning/decision → **Vertical SoR rules/permissions/invariants validate karti hai** → Governed tools action perform karte hain → Result-owning system record karta hai.

> ❗ **Yeh Middle Step Drop Karna Aasan, Mehnga Hai.** Discount approval sales record se validate hoti hai CRM likhne se pehle. Journal entry accounting record se validate hoti hai ERP hold karne se pehle. **"System of Context kabhi second transaction system nahi banna chahiye, aur kabhi governed record ke around likhne ka tareeqa nahi banna chahiye."**

| Surface | Operation | Risk Agar Galat |
|---|---|---|
| Retrieval | Search/read/cite/compare | Information exposure |
| Calculation/Checking | Validate/classify/calculate/test | Incorrect conclusion |
| Preparation | Draft/prepare/stage | Incorrect proposed record |
| Execution | Send/post/release/approve/pay | Real-world consequence |

> ⚠️ **"The System of Context must never turn access into permission."**

<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/a364f72d-45e0-4ceb-9c25-6d68b0234f2e" />

---

## The Eight Invariants of the Connecting Layer

| # | Invariant | Kyun Hold Karta Hai |
|---|---|---|
| 1 | Authority kabhi move nahi hoti | Warna impact chain ek ungoverned branch grow karti hai |
| 2 | Relevance authority nahi hai — routing retrieval se pehle | Warna top-ranked passage chupke se rule ban jaati hai |
| 3 | Permission inherited hai, invented nahi, model se pehle enforce hoti hai | Warna layer sab se helpful data breach ban jaata hai |
| 4 | Freshness per-field decide hoti hai | Warna Worker exact sawaal ka jawab confidently stale deta hai |
| 5 | Provenance har item ke saath travel karti hai, summarizing strip nahi karti | Warna contract, policy, rumour ek jaisi lagti hain |
| 6 | Conflict preserve + escalate hoti hai, blend nahi | Warna system ek claim banata hai jo koi source ne nahi kiya |
| 7 | Ungoverned silently governed nahi banta | Warna customer ki galtiyan aapki profession ke record mein aapki stamp le kar aati hain |
| 8 | Discovery confirmation nahi hai | Warna indexed copy chupke se authority ban jaati hai |

---

## Where It Sits in the FDE AF Model

> **Layer 3 pattern prepare karta hai** (koi customer data nahi — source classes, routing rules, packet shape, connector templates, retrieval evals). **Layer 4 customer ko bind karta hai** (unke apps, identity provider, contracts, credentials, case identifiers).

> 📌 **Commercial Consequence:** Layer 3 pattern = **asset**, aap client-to-client carry karte ho. Layer 4 fitting = **service**, har client pe perform karte ho. Confuse karna hi ek founder ko "busy consulting practice" aur "sellable business" mein confuse karta hai.

<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/732ff23a-749f-4e06-b800-90977a40ae66" />
---

## Consolidate by Default, Specialize Deliberately

> ❗ Thesis kehta hai: consolidate by default (ek Postgres). Yeh page opposite advice jaisi lagti hai — **hai nahi**. **Consolidation sahi hai jab ek set of invariants sab data govern kare. Specialization sahi hai jab 2 sets of invariants opposite directions mein khinchen.**

> 📌 Record ko exactness/versioning/audit-trail chahiye. Customer ki duniya ko breadth/freshness/permission-fidelity chahiye (dozen systems se mirrored). Dono ko ek store mein force karo, dono worse ho jaate hain.



---

## The Open Reference Implementation

> **Onyx** = open reference implementation (students practice karte hain). **Glean** = best-known commercial example. Doctrine product-independent hai.

**4 Interfaces Jo Open Rehne Chahiye:** MCP (agent-facing) · OpenAPI (governed capabilities) · Connectors/ingestion APIs · Source-owned identifiers/citations.

> ⚠️ **What the Community Edition Cannot Prove:** Onyx Community Edition permission-sync connectors, RBAC, group-based permissions **Enterprise Edition** ke features hain. **"A feature list is not proof"** — production deployment ko demonstrate karna hai ke identity/permission/sync/audit controls actually enforce hote hain.

---

## When You Do Not Need One

> ⚠️ Har vertical ko yeh layer nahi chahiye. **Ek gate non-negotiable hai: "Jab tak thin slice complete na ho aur pehla Worker usse cite na kare, System of Context mat banao."** Bina governed cheez ke ek connecting layer, ambitions wala search box hai.

Zaroorat hai jab "yeh kyun aisa kiya gaya" ka jawab **kisi bhi governed system ke bahar** rehta ho — long professional relationships (audit firms, legal practices, consultancies) mein yeh nature se hota hai.

---

## Two Temperaments, One Layer

> 📌 **8 invariants identical, 3 questions identical, indexing rules identical.** Sirf 2 cheezein change hoti hain:

|  | Sales | General Ledger |
|---|---|---|
| Ungoverned material kahan | **Center mein** — transcripts/emails deal file ki evidence base hain | **Edge pe** — systems numbers rakhte hain |
| Heaviest connection | Conversation records, indexed | Accounting system, live query |
| Characteristic mistake | Offhand remark confirmed field ban jaata hai | Stale indexed balance current ki tarah answer hota hai |
| Permission failure ki cost | Confidentiality breach | Access review jo ab false picture certify karti hai |

> ⚠️ **Sales Uncomfortable Case Hai** — ungoverned material hi evidence hai. Transcript claim kabhi prove nahi karta, sirf batata hai claim kahan se aayi.

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/4b993bed-77dd-454e-833c-eb8a396bd0cd" />

---

## Ayesha Connects Her First Customer

> Uske paas slice hai. Chicago partner ne sign kiya. Ab woh firm ke andar hai, aur uska record room mein **sab se chhoti cheez** hai. Firm ke paas 22 saal ke working papers SharePoint mein hain, engagement letters email mein, unusual treatments ki reasoning chat mein (aur ek senior manager ke dimaag mein jo aksar travel karta hai).

**3 Steps:**
1. **Authority route karti hai connect karne se pehle.** Going-concern evidence → Vertical SoR. Account 1200 balance → typed query, **kabhi index nahi** ("embedded balance ek photograph hai ek number ka jo already move ho chuka hai"). Henderson lease 2023 decision → SharePoint (isi liye firm ko context layer chahiye).
2. **Permissions ko answers se pehle test karti hai.** First-year junior ki tarah login kar ke compensation policy poochti hai — **correct result: kuch nahi** (junior SharePoint mein woh documents nahi khol sakta). Engagement manager, phir partner ki tarah dobara test.
3. **Ek line likhti hai engagement design record mein:** *"Firm ka apna material is client ke baare mein evidence hai. Profession ki requirements record se aati hain. Worker kabhi dono confuse nahi karega."*

> 📝 **6 Hafte Baad:** Worker lease classification prepare karta hai, standard cite karta hai, 2023 memo attach karta hai (firm's prior treatment ki tarah labeled), **phir woh karta hai jo search tool kabhi nahi karta**: report karta hai ke dono disagree karte hain, kaunsa authority test apply hua batata hai, partner ko escalate karta hai. Partner agree karta hai, ek treatment correct karta hai jo firm ne 3 saal repeat kiya tha.

---


<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/cc70c80b-82bf-4cf4-bf38-c74b62281a00" />

---
## The Eleven Failure Modes

| # | Failure | Cure |
|---|---|---|
| 1 | The flat index — sab kuch equally authoritative | Authority routing |
| 2 | The flattened portfolio — sales rule accounting question answer karta hai | Federation |
| 3 | Reliance on the copy — synced page hi authority ban jaati hai | Discovery ≠ confirmation |
| 4 | The stale answer — synced copy jahan live chahiye tha | Indexed-or-live decision, per field |
| 5 | Retrieve first, hide later — forbidden content model context mein pohanchti hai | Permission before model |
| 6 | The model as quiet source — retrieval kuch nahi deti, model guess karta hai | Missing evidence = packet field, escalate |
| 7 | The prompt as integration layer — lamba prompt, real connections nahi | Connectors, tools, deterministic policy |
| 8 | Citations without provenance | Full provenance envelope |
| 9 | The blended conflict — 2 disagreeing sources ek sentence mein | Conflict preservation + escalation |
| 10 | The shadow record — context platform apni copy trust hone lagti hai | Source-owned live retrieval |
| 11 | The product-shaped doctrine — architecture vendor define karta hai | Open interfaces, replaceable components |

---

## ❌ Common Mistakes

| Mistake | Kyun Galat Hai |
|---|---|
| Context layer ko naya source of truth samajhna | Yeh koi truth nahi hold karta — sirf carry karta hai |
| Model ko source ki tarah trust karna | Model ke paas koi register row nahi, plausibility provenance nahi hai |
| Live numbers ko index karna | Stale value confident galat jawab deta hai |
| Retrieve karna phir hide karna | Model context mein daali hui cheez "hidden" nahi rehti |
| 2 verticals ko ek corpus mein merge karna | Blended page kisi bhi profession mein cite nahi hoti |
| Conflict ko ek smooth sentence mein blend karna | Koi source ne wo claim kiya hi nahi |
| Thin slice complete hone se pehle context layer banana | "Ambitions wala search box" — kuch governed hi nahi hai connect karne ko |

## 💡 Pro Tips

- 💡 Har material item ko full provenance do — source, stable ID, class, scope, version, owner, freshness, permission basis, citation
- 💡 "Discovery finds a pointer, confirmation gives an answer" — dono ko kabhi confuse mat karo
- 💡 Compress the prose, never compress the provenance
- 💡 Permission test karo answers test karne se pehle — junior/manager/partner teeno se login karke
- 💡 Segregation-of-duties argument se bachein, "invalidates the access review" argument use karein — zyada accurate aur zyada strong hai

## 🧠 Memory Tricks (Yaad Rakhne Ke Tareeqe)

- **"SoR decides what's true. SoC decides what arrives."**
- **"It carries authority. It never holds it."** — delivery driver analogy
- **"Can a reviewer rebuild this without asking the model?"** — settling test
- **Index working context. Discover governed knowledge. Query current truth live.**
- **"Access points up. Authority points back."**
- **8 Invariants** — har ek "warna kya hota hai" ke saath yaad rakho

---

## 📌 One-Line Chapter Summary Table

| Section | One-Line Takeaway |
|---|---|
| 1-2. Two Records | Vertical SoR profession jaanti hai, customer ki state nahi — ERP ≠ profession |
| 3-4. Layers + One Law | Access upar, authority wapas source ki taraf — layer kabhi authority hold nahi karta |
| 5. Model Not a Source | Weights ke paas register row nahi — fluency correctness nahi hai |
| 6-7. Scoped Authority | Federated portfolio, ek business event kai records govern karte hain |
| 8. Context Packet | Temporary, authority/permissions inherit karta hai, expire hota hai |
| 9. Index vs Ask | Working context index, governed knowledge discover+confirm, live truth query |
| 10. Permission First | Model se pehle filter — warna helpful data breach |
| 11-12. Provenance + Conflict | Har item labeled; disagreement reviewable banao, disappear mat karo |
| 13. Read-Reason-Act-Record | 5 alag jobs, hamesha same order |
| 8 Invariants | Poore chapter ka core — kabhi change nahi hote |
| Ayesha | Authority route, permissions test, phir connect |
| 11 Failure Modes | Har ek ka naam + cure |

---

<div align="center">

# 🔗 The System of Context
### Connecting the Records to Real Work • 13 Sections • 8 Invariants • GIAIC Agent Factory

**Built By Ismail Ahmed Shah | GIAIC 2026**

Made with ❤️ for the AI Builders Community

</div>
