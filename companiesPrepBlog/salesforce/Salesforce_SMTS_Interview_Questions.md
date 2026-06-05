# Salesforce SDE2 / MTS / SMTS Interview Questions — Last 6 Months

> Compiled from real interview experiences on **LeetCode Discuss**, **GeeksforGeeks**, **InterviewBit / interviewexperiences.in**, **gitGood.dev**, **CodingKaro**, **Medium**, **Substack (roundz)**, and **System Design Handbook** (~Dec 2025 – Jun 2026).
>
> **Disclaimer:** Salesforce rotates questions and many candidates sign NDAs, so exact problems vary. The **patterns** and **themes** below are consistent across recent reports. Salesforce hires for the ability to build **scalable, multi-tenant** software — not raw algorithmic speed.

---

## Table of Contents
1. [Interview Process Overview](#1-interview-process-overview)
2. [Coding / DSA Questions](#2-coding--dsa-questions)
3. [Low-Level Design (LLD / OOD)](#3-low-level-design-lld--ood)
4. [High-Level / System Design (HLD)](#4-high-level--system-design-hld)
5. [Behavioral / Ohana Values](#5-behavioral--ohana-values)
6. [What Makes Salesforce Different](#6-what-makes-salesforce-different)
7. [Preparation Resources](#7-preparation-resources)

---

## 1. Interview Process Overview

The Salesforce engineering ladder: **AMTS** (entry) → **MTS** (SDE2) → **SMTS** (Senior, ~3–5 YOE) → **LMTS** → **PMTS** → **Architect** → **Distinguished Engineer**.

A typical MTS / SMTS loop (process spans ~2–5 weeks):

| Round | Duration | What it Tests |
|-------|----------|---------------|
| Recruiter Screen | 15–45 min | Background, motivation, comp, role expectations |
| Online Assessment (OA) | 60–75 min | 2–4 LeetCode medium-to-hard problems (HackerRank, proctored) |
| Technical Round 1 (DSA) | 60 min | 1–2 problem-solving questions + project discussion |
| Technical Round 2 (DSA / LLD) | 60 min | DSA + Low-Level Design, or pure problem solving |
| System Design (HLD) | 60–75 min | Multi-tenant SaaS, distributed systems |
| Core Backend (sometimes) | 60 min | Java, JVM, concurrency, Kafka, distributed systems |
| Hiring Manager + Culture | 45–60 min | Project deep-dive, behavioral, Ohana values |

**Key observations from recent candidates:**
- Coding bar is **medium difficulty** — Salesforce explicitly does *not* test for "LeetCode Hard in 20 min." It tests judgment, concurrency, and clean code.
- **Java fluency is expected** (the core platform is heavily Java), though interviews are language-agnostic.
- System design is an exercise in **multi-tenancy**, not just scale — the recurring theme is the **"noisy neighbor"** problem (one tenant must not degrade others).
- Behavioral rounds filter for **Ohana** cultural alignment and **stewardship** ("we enabled this", not "I built this"). A technically perfect but arrogant candidate gets rejected in debrief.
- No elimination between back-to-back technical rounds is common; onsite rounds are often scheduled on the same day.

---

## 2. Coding / DSA Questions

### Reported in recent OAs / technical rounds
| Question | Source / LeetCode |
|----------|-------------------|
| **Zigzag Conversion** — print a string in zigzag across N rows | LC 6 |
| **Letter Combinations of a Phone Number** (keypad strings) | LC 17 |
| **Top K Frequent Words** | LC 692 |
| **Number of Islands** (variant) | LC 200 |
| **Top K Frequent Elements** (solved via heap / PQ) | LC 347 |
| **Longest Well-Performing Interval** | LC 1124 |
| **M microservices report Y/N daily → longest streak of consecutive all-pass days** (variant of Well-Performing Interval) | — |
| **Policemen Catching Thieves** | GeeksforGeeks |
| **Pairs**-style problem | — |
| Max possible **even sum** from an array | — |
| A challenging **Dynamic Programming** question (after an easy string warm-up) | — |
| Array-based problem with **large-input / edge-case** follow-ups | — |

### Topics to prioritize
- **Arrays & Strings** — two pointers, sliding window, frequency maps (highest yield).
- **Graphs** — BFS/DFS, islands, connected components.
- **Heaps / Priority Queue** — Top-K problems appear repeatedly.
- **HashMaps** — frequency counting, lookups.
- **Dynamic Programming** — present but usually manageable; don't over-index on niche DP.
- **Concurrency** — be ready to reason about thread-safety in code.

> **Strategy:** Solve **100–150 LeetCode Mediums**, prioritizing **Arrays, Strings, and Graphs** over niche DP. Focus on clean, production-ready code and complexity analysis, not speed.

---

## 3. Low-Level Design (LLD / OOD)

Recent reported prompts (interviewer often leaves requirements **vague on purpose** — ask clarifying questions):

| Prompt | Key Pattern / Focus |
|--------|---------------------|
| **Parking Lot** (THE most common) | Strategy pattern for parking strategies; `Vehicle`, `Spot`, `Ticket` classes; "lot full" edge case |
| **Meeting Room Scheduler** | Book/cancel/view rooms; handle conflicting meetings; search by room or employee |
| **Elevator System** | **State pattern** (Moving Up / Moving Down / Idle); request scheduling |
| **Notification Library** | Pluggable channels (email, SMS, push); Strategy/Factory patterns |
| **Connection Pool with internal request queue** | Fixed reusable connections; `requestId`; queue waiters; thread-safety |
| **LRU / LFU Cache** | HashMap + doubly linked list; eviction policy |
| **In-Memory Cache with custom eviction policy** | Pluggable eviction strategy |
| **Rate Limiter** | Per-`resourceId` limits; Token Bucket / Sliding Window |
| **RPC Framework** | Serialization, stubs, transport abstraction |
| **Stack with Increment operation** | Amortized O(1) increment |
| **Movie ticket booking (BookMyShow)** | Seat locking, concurrency, search |
| **Chess Game** | Piece hierarchy, move validation |

**What they evaluate:** SOLID principles, clean API signatures, abstraction/interfaces, correct design patterns (Strategy, State, Factory, Observer), concurrency handling, and edge cases.

---

## 4. High-Level / System Design (HLD)

60–75 min; the dominant theme is **multi-tenant SaaS**.

### Reported / common prompts
- Design a **multi-tenant platform feature that customers can extend** (think Apex triggers) without one customer's bad code breaking another's experience.
- **Shard a service across hundreds of thousands of tenants.**
- Handle a **"noisy neighbor"** — a customer with 1000× the average data/traffic.
- Build a **metadata-driven configuration system**.
- Design a **large-scale distributed backend service** (consistency vs. availability, geo-distribution, caching, event-driven patterns, data modeling, storage selection, API design).
- CRM-flavored designs: accounts/contacts/opportunities data model, workflow automation (triggers, queues, event-driven pipelines), real-time notifications.

### What interviewers probe
- **Tenant isolation** & data security across shared infrastructure.
- **Data partitioning / sharding** — typically by **org ID / tenant ID** or region.
- **Noisy-neighbor mitigation** — rate limiting, quotas, resource fairness.
- **Consistency vs. availability** (CAP) — strong consistency for workflow/opportunity updates; availability for analytics.
- **Caching** hot data (Redis/Memcached), low latency, queues/event buses.
- **Extensibility** — customer customization without cross-tenant breakage.

> A real debrief example: a candidate designed a *standard* distributed cache and was rejected because it **lacked tenant-level isolation**. Always design with multi-tenancy first.

---

## 5. Behavioral / Ohana Values

Behavioral rounds are a **primary filter**, not a formality. Salesforce evaluates alignment with the **Ohana** philosophy and **V2MOM** goal-setting.

### Salesforce core values
1. **Trust** — security, reliability, transparency.
2. **Customer Success** — customer outcomes over individual heroics.
3. **Innovation** — continuous improvement.
4. **Equality** — inclusion and fairness.
5. **Sustainability** — long-term, responsible stewardship.

### Reported behavioral themes / questions
- "Why do you want to switch?" / "Why Salesforce?"
- Project deep-dives — your **role + impact** (not just the team's).
- Tell me about a time you made a **technical compromise** (map 3 projects via STAR, highlighting trade-offs).
- Navigating **cross-team / cross-functional** complexity and legacy debt with empathy.
- Mentoring others; improving overall **team health** (stewardship).
- Handling **compliance / regulatory** constraints (SOC 2, HIPAA, FedRAMP) for some segments.
- Usage of **AI in day-to-day** work.
- Relocation concerns.

> **Mindset shift:** answers should move from "**I** built this" to "**We** enabled this." They look for stewardship and collaboration, not room-dominating "leadership."

---

## 6. What Makes Salesforce Different
- **Multi-tenancy obsession** — every design question implicitly asks "how does this stay isolated and fair across hundreds of thousands of tenants?"
- **API stability & versioning** — enterprise customers depend on stable contracts; review Salesforce's public API/versioning approach.
- **Medium coding bar, high judgment bar** — concurrency, memory management, and clean code matter more than exotic algorithms.
- **Culture is a hard filter** — Ohana alignment can override raw technical strength.

---

## 7. Preparation Resources
- **DSA:** LeetCode (Salesforce-tagged), focus 100–150 Mediums on Arrays/Strings/Graphs/Heaps. Practice in **Java**.
- **LLD:** Practice Strategy, State, Factory, Observer patterns; SOLID; thread-safety (locks, CAS, executors, deadlocks).
- **HLD:** System Design Handbook (Salesforce guide), study **multi-tenant architecture**, sharding by tenant, noisy-neighbor mitigation; *Designing Data-Intensive Applications*.
- **Core Backend:** JVM internals, Kafka/queues/backpressure, distributed transactions, REST lifecycle, observability.
- **Behavioral:** Prepare STAR stories framed around **Ohana values** and stewardship.

### Source experiences referenced
- LeetCode Discuss — "Salesforce | MTS | Selected | Interview Experience"
- interviewexperiences.in — "Salesforce MTS", "Salesforce SDE2 March 2026", "Salesforce AMTS Bangalore Jan 2026"
- Medium — Tanu, "My Salesforce Interview Experience (MTS – Selected)"; Padma, "My Salesforce SMTS Interview Experience"; Prashant Priyadarshi, "Salesforce Low Level Design Questions from recent Interviews"
- Substack (roundz) — "Interview Experience: Salesforce SMTS"
- gitGood.dev — "Salesforce Software Engineer (SMTS to Distinguished) Prep"
- CodingKaro — "Salesforce Interview Questions & Experiences 2026"
- System Design Handbook — "Salesforce System Design Interview Guide"
- sirjohnnymai.com — "Salesforce SDE interview questions 2026"

---

*Last updated: June 2026. Patterns and multi-tenancy thinking are more durable than specific questions.*
