# JioStar / Disney+ Hotstar — SDE2 Interview Questions (Categorized)

> Compiled from publicly shared interview experiences on LeetCode Discuss, GeeksforGeeks,
> InterviewBit/Desi QnA, Medium, DevBrainiac, Substack and similar resources.
> Treat these as *patterns and themes* to prepare, not a fixed question bank — the
> exact problems rotate, but the topics and difficulty are highly consistent.
>
> **Role:** SDE2 / Senior Software Engineer (Backend, ~3–6 YOE)
> **Note:** "Disney+ Hotstar" and "JioStar / JioHotstar" share largely the same loop after the merger.

---

## Difficulty & Theme Summary

| Category | Difficulty | Frequency | Core focus |
|---|---|---|---|
| DSA / Coding | LeetCode Medium → Hard | 2 rounds (almost always) | Optimized solutions, edge cases, clear thinking |
| Low Level Design (LLD) | Medium–Hard | 1 round (very common) | OOD, SOLID, concurrency, working code |
| System Design (HLD) | Hard | 1 round (often combined with LLD or in HM round) | Scale, distributed systems, trade-offs |
| Techno-Managerial / Bar Raiser / HM | — | 1 round | Project depth, concurrency, ownership, behavior |

The recurring signal across all reports: **interviewers care more about your reasoning,
trade-offs, and communication than about whether you instantly recall the optimal answer.**

---

## 1. DSA / Coding Round Questions

Two coding rounds are standard. Questions are usually LeetCode **Medium to Hard**, often with
a twist on constraints. Interviewers ask for brute force first, then push toward the optimal
solution while probing time/space complexity and edge cases.

### Arrays & Strings
- **Minimum Cost to Sort Array** — sort an array where cost of sorting a subarray = (length)². Find minimum total cost. (asked SDE2 Round 1)
- **Longest Increasing Subsequence (LIS)** — brute force → DP → binary search optimization.
- **Permutations of a String** — recursion/backtracking; follow-ups: avoid duplicates, optimize memory, iterative version.
- Create the **biggest number by concatenating array integers**.
- **Intersection & Union of two arrays** (optimized).
- Longest substring without repeating characters.

### Dynamic Programming
- LIS (above) and its variants.
- **Minimum cost to merge all elements of a list** (classic interval/merge DP).
- Online Assessment: 2 problems, both LeetCode-medium **DP** (90 min).
- Variation of the "Broken Calculator" problem.
- "Minimum value to get positive step-by-step sum" (LeetCode).

### Trees
- **Binary Tree Maximum Path Sum** — heavy discussion on reasoning, not just code.
- **Maximum path sum in a tree** (with helper-class / struct design expected).
- Check if a **binary tree is balanced**.

### Graphs (very common — appears in almost every loop)
- Shortest path using **Dijkstra's algorithm**.
- **Detect a cycle in a directed graph** (asked indirectly).
- **Word Ladder** — shortest transformation sequence (BFS on graph).
- **Largest connected component** in a graph (DFS) — sometimes wrapped in a story.
- **Minimum number of jumps in a matrix** to reach an end point, up to k jumps at a time, 4 directions (BFS; follow-up: why does BFS guarantee shortest path?).

### Linked Lists
- **Merge two sorted linked lists.**
- **Reverse a linked list** — both recursive and iterative.
- **Reverse a linked list in groups/parts.**

### Stacks / Monotonic Structures
- **Stock Span Problem** — discuss O(n²) → O(n) with O(n) space → O(n) with constant space.

### Math / Streaming
- Given a **stream of integers**, determine if the number formed so far is divisible by `x` (e.g., stream 1,2,3,4 → is 1234 divisible by x?). Solve using modular arithmetic.

### What they evaluate in coding rounds
- Optimized solution + correct complexity analysis.
- Writing `main` + helper functions, not just the core function.
- Explicitly defining and handling **edge cases**.
- Continuous "think out loud" communication.
- Behavior under tightened constraints / large inputs.

---

## 2. Low Level Design (LLD) Questions

Usually one dedicated round (sometimes labeled "System Design" but driven mostly toward LLD).
Expect to define entities, class diagram, APIs, DB schema, and frequently **write working code**
(especially in JioHotstar Java-based machine-coding style rounds).

- **Design an Instagram-like photo-sharing app** — user/post models, feed generation, comment & like systems, API structure, DB schema, scaling likes, image uploads, notification triggers, extensibility. (SDE2)
- **Design an API Rate Limiter (in Java, working code)** — compare Fixed Window, Sliding Window Log, Sliding Window Counter, Token Bucket, Leaky Bucket; pick one and implement. Follow-ups on thread safety, lock contention, expired-entry cleanup, background maintenance tasks, concurrent collections vs `synchronized`. (Staff/SDE2)
- **Design Google Calendar** — mostly LLD, last ~15 min on HLD.
- **Design Splitwise** + entity diagram, FRs and NFRs (often paired with "how does UPI / a payments system work").
- **Notification Service** design (recurring LLD theme).
- **Ticket / Movie-seat Booking System** — concurrency-heavy LLD (see techno-managerial below).

### LLD topics to master
- SOLID principles, common design patterns (Strategy, Factory, Observer, Singleton).
- Clean class boundaries, interfaces, extensibility (Open/Closed).
- **Concurrency & thread safety** within a single service (locks, atomics, concurrent collections).
- API design, DB schema design, indexing.
- Handling edge cases and production readiness.

---

## 3. High Level / System Design (HLD) Questions

Appears as its own round or inside the Bar Raiser / Hiring Manager round. Strong emphasis on
**scale** (Hotstar famously handles 25M+ concurrent live viewers), distributed systems, and trade-offs.

- **Design a scalable video / live streaming service** (the signature Hotstar question).
- **Design a recommendation / recommender system for Hotstar.**
- **Design a real-time view counter** — count live views on a streaming app like Hotstar.
- **Design a Real-time Monitoring and Alerting System.**
- **Design a URL shortening service.**
- **Design the architecture of a CDN (Content Delivery Network).**
- **Design a Notification System** (at scale).
- Discuss **Kafka / message-queue internals** and where you'd use them in your architecture.
- Design a data model for a **social media platform**.
- Other practice targets reported: WhatsApp, Food Delivery, Ticket Booking.

### HLD topics to master
- Requirement gathering: nail FRs and NFRs, ask for **scale** up front.
- Sharding, replication, caching strategies, consistency models.
- Load handling, autoscaling, traffic spikes (live-event scaling).
- Event-driven architecture, message queues (Kafka), pub/sub.
- Latency, availability, fault tolerance trade-offs.
- SQL vs NoSQL choice and justification, indexing, query optimization for large datasets.

---

## 4. Techno-Managerial / Bar Raiser / Hiring Manager Round

Less coding, more engineering maturity, depth, and behavior. Often blends a design/architecture
discussion with leadership-style behavioral questions.

### Technical-depth discussion topics
- **Locking mechanisms in a ticket booking system**: what happens when multiple users book the same seat simultaneously?
  - Concurrency control, distributed locking.
  - **Optimistic vs pessimistic locking.**
  - Race conditions, database transactions, deadlock scenarios, scalability trade-offs.
- Deep dive into **past projects**: architecture decisions, production incidents, scaling challenges, why you chose a specific technology.
- Hypothetical "what would you do if…" situations layered onto your own projects.
- Sometimes an additional HLD problem (e.g., recommender system).

### Behavioral / managerial
- Ownership and end-to-end feature delivery.
- Communication and collaboration within teams.
- Prioritization under pressure.
- Amazon-Leadership-Principle-style behavioral questions (use the **STAR** framework).
- Motivation / culture fit: why Hotstar, other offers, location/relocation preference.

---

## 5. CS Fundamentals (commonly probed throughout)

Frequently sprinkled into coding/HM rounds (especially relevant from SDE-1 reports, still useful for SDE2):

- **OS:** paging, memory management, processes vs threads, synchronization.
- **Computer Networks:** DNS, how a DNS server works, TCP/HTTP basics.
- **DBMS:** SQL vs NoSQL, indexing, transactions, query optimization.
- **OOP:** core principles, applied in LLD.
- Language internals (e.g., "how does a C++ vector grow / manage capacity?").

---

## Recommended Practice List (by priority)

1. **Graphs** — BFS/DFS, Dijkstra, cycle detection, connected components (highest hit rate).
2. **Dynamic Programming** — LIS, interval/merge DP, grid DP.
3. **Trees** — path sum, balanced tree, traversals with helper classes.
4. **Arrays/Strings + Two Pointers/Sliding Window.**
5. **LLD:** Rate Limiter, Splitwise, Notification Service, Booking System, Instagram.
6. **HLD:** Video streaming, Recommendation system, Real-time counter, Notification system, URL shortener.
7. **Concurrency:** optimistic/pessimistic locking, race conditions, thread safety.

---

## Sources

- LeetCode Discuss — "Disney+HotStar / JioStar SDE2"
- DevBrainiac — Disney+ Hotstar SDE-2 Interview Experience; JioHotstar Staff SWE Experience
- GeeksforGeeks — Disney+Hotstar Recruitment Process; SDE-1 2022 Interview Experience
- Desi QnA — Disney+ Hotstar SDE 2 / SDE 1 Interview Experience sets
- Medium — JioHotstar SDE2 / Senior SWE Interview Experiences (Siddharth Raja, Frontend Army)
- Substack (roundz) — Disney+ Hotstar SDE-1 Interview Experience
- Hello, World! (glich.co) — Hotstar Senior Software Engineer interview process
