# PhonePe SDE-2 (Software Engineer 2) — Interview Process

> Compiled from real candidate interview experiences on LeetCode Discuss, GeeksforGeeks,
> Glassdoor, Desi QnA, Medium, LinkedIn, and interview-experience blogs (2022–2026).
> Treat this as a directional guide — the exact order/number of rounds varies by team and recruiter.

---

## 1. Overview

- **Role:** Software Development Engineer 2 (SDE-2 / Software Engineer 2)
- **Total rounds:** Usually **4 technical rounds** (occasionally 5 if a round is repeated, or an extra OA for some pipelines).
- **Typical experience band:** 2–5 years.
- **Locations:** Bangalore, Pune (primarily).
- **Sourcing:** Referral, Instahyre, recruiter outreach (LinkedIn), campus/lateral hiring consultants.
- **Timeline:** Usually **1 round per week**; full cycle takes **1–3 months**. One round per week is common.

### Weightage (approximate)
| Area | Weight |
|------|--------|
| Machine Coding / LLD | ~30% |
| DSA / Problem Solving | ~20–30% |
| System Design (HLD) | ~25% |
| Hiring Manager / Behavioral | ~15–20% |

> Key theme reported by almost every candidate: PhonePe is **code-heavy** and places huge emphasis on
> **clean, modular, extensible, thread-safe code** and **defending your design trade-offs**.

---

## 2. The Rounds (typical flow)

```
Recruiter screen  →  Round 1: Machine Coding (LLD)  →  Round 2: DSA / PSDS
                  →  Round 3: System Design (HLD)   →  Round 4: Hiring Manager (HM)
```

Some pipelines (especially via OA platforms) start with an **Online Assessment** before Round 1.

---

### Round 0 (optional): Online Assessment (OA)
- Platform: HackerRank / CodeSignal / company portal.
- Format: 3–4 coding problems (sometimes + MCQs on CS fundamentals or Android for mobile roles).
- Topics seen: matrix paths, array frequency optimization, game theory, tree-based DP, count islands (graph), top-K API endpoints (HashMap + Min-Heap), string rotation.

---

### Round 1: Machine Coding / Low-Level Design (LLD)
- **Duration:** 90–120 min implementation + 30 min evaluation/discussion.
- **Formats seen:**
  - Take-home on CodeSignal/CodePair (90 min timed), OR
  - Problem mailed with a **24-hour** deadline to submit working code (ZIP), OR
  - Live machine coding.
- **What you build:** A complete, runnable mini-system (console or web/in-memory DB is fine) for an LLD problem.
- **Then:** A follow-up evaluation call where you give the interviewer a **code walkthrough** — they ask:
  - Why these classes / this structure? Which **design patterns** and **SOLID principles**?
  - How do you **scale** / add a new feature with minimal changes?
  - **Concurrency / race conditions / thread-safety**, exception handling.
- **What is graded:** Modularity, extensibility, OOP design, design patterns, separation of concerns, exception handling, test cases passing, code readability.

> ⚠️ Reality check from candidates: some interviewers have a "fixed solution" in mind and nitpick
> (e.g., "should have a Repository class", "use ConcurrentHashMap"). Aim for clean, idiomatic,
> pattern-driven code even under time pressure. Passing all test cases does **not** guarantee a pass —
> the design discussion matters as much.

➡️ See **`PhonePe_SDE2_LowLevelDesign.md`** for the full list of LLD problems.

---

### Round 2: DSA / Problem Solving & Data Structures (PSDS)
- **Duration:** ~60 min.
- **Format:** 2–3 problems (sometimes 1 puzzle). Conducted by a Senior SDE (sometimes via Interview Vector / Interview Vector-style partners).
- **Difficulty:** LeetCode **Medium to Hard**.
- **Style quirk:** Questions are often given as **descriptive paragraphs / real-world scenarios**, not one-line LeetCode prompts. You must extract the core problem yourself.
- **Expectations:**
  - Sometimes **approach only**, sometimes **full working code + run against multiple test cases**.
  - Always discuss **time & space complexity** and go brute-force → optimized step by step.
  - Pseudo-code in Notepad/editor is sometimes required — practice writing without IDE autocomplete.
- **Hot topics:** Arrays (sliding window, prefix sum), Graphs (BFS/DFS/MST/topo sort), Trees, Stacks (NGE), DP, Greedy, Binary Search.

➡️ See **`PhonePe_SDE2_DSA.md`** for the full categorized question list.

---

### Round 3: System Design / High-Level Design (HLD)
- **Duration:** ~60 min.
- **Format:** One open-ended design problem; **you drive** the discussion.
- **Expected flow:** Requirements (FR + NFR) → capacity estimation / back-of-envelope → high-level architecture → API design → DB schema & choice → deep dives → trade-offs.
- **What they probe:**
  - **SQL vs NoSQL** justification, Cassandra/Mongo vs RDBMS trade-offs, foreign keys in NoSQL.
  - **Scalability**: how to handle high-traffic APIs (e.g., search), read replicas/slaves, sharding.
  - **Microservice segregation**, API gateway, **auth/authz** across services & token propagation.
  - **Capacity estimation** (be ready — several candidates got caught off guard here).
  - Search indexing, feed generation, caching, fault tolerance, API-failure handling.
- **Twist seen:** Sometimes they ask you to design the **HLD of your current project** instead of a standard problem.

➡️ See **`PhonePe_SDE2_SystemDesign.md`** for the full list of HLD problems.

---

### Round 4: Hiring Manager (HM) / Managerial Round
- **Duration:** ~45–60 min.
- Taken by a Senior Engineering Manager / the hiring manager.
- **Content:**
  - Deep dive into your **current/past projects**, your **contribution & impact**, architecture decisions.
  - **Behavioral**: why PhonePe, why switch, conflict handling (e.g., code-review disagreements), dealing with deadlines, ownership of production issues, team ethics.
  - Some **technical cross-questions** on past work (e.g., SQL vs NoSQL choice in your team).
  - SDLC questions, "first 90 days" plans, how you'd build a new feature end-to-end.
  - Ends with Q&A.

➡️ See **`PhonePe_SDE2_OtherRounds.md`** for HM/behavioral question bank.

---

## 3. Preparation Checklist

**LLD / Machine Coding**
- [ ] Practice 8–10 classic LLD problems end-to-end in your language (Java is most common).
- [ ] Internalize SOLID, GoF design patterns (Strategy, Factory, Observer, Repository, Singleton, State).
- [ ] Default to thread-safe structures (ConcurrentHashMap), proper exception handling, layered architecture (entity / repository / service).
- [ ] Time yourself at 90 min; keep code runnable with a quick demo/main + test cases.

**DSA**
- [ ] Arrays (sliding window, prefix sum, range queries), Graphs (BFS/DFS/MST/topo), Trees, Stacks, DP, Greedy, Binary Search.
- [ ] Practice reading **scenario/paragraph** style problems and converting to known patterns.
- [ ] Always state complexity; practice brute → optimal narration; practice on Notepad.

**System Design**
- [ ] Capacity estimation / back-of-envelope math.
- [ ] SQL vs NoSQL trade-offs, sharding, replication, caching, message queues (Kafka), idempotency.
- [ ] API gateway, auth/authz, microservices, fault tolerance.
- [ ] Be able to design your own project at a whiteboard level.

**HM / Behavioral**
- [ ] STAR-format stories on impact, conflict, failure, ownership, deadlines.
- [ ] Crisp "why PhonePe" and "why leaving" narratives.

---

## 4. Sources
- LeetCode Discuss — PhonePe interview experiences
- GeeksforGeeks — PhonePe Interview Experience (SDE-2, SDE 2–5 yrs)
- Glassdoor — PhonePe Software Engineer interview questions
- Desi QnA — PhonePe SDE 2 sets (Set-2, Set-12, Set-17)
- Medium — Arpit Chauhan, Suresh (CodeWithTech)
- LinkedIn — Hari Krishna Doradla interview experience
- roundz.substack.com — Interview Experience #101 & #174
