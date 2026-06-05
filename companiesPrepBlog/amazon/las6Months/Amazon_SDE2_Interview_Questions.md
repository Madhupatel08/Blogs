# Amazon SDE2 (L5) Interview Questions — Last 6 Months

> Compiled from real interview experiences shared on **LeetCode Discuss**, **GeeksforGeeks**, **InterviewBit / interviewexperiences.in**, **HelloInterview**, **CrackingWalnuts**, **Medium**, and **LinkedIn** (roughly Dec 2025 – Jun 2026).
>
> **Disclaimer:** Amazon rotates its question bank frequently. The *exact* question number rarely repeats, but the underlying **pattern** does. Prepare by pattern, not by memorization.

---

## Table of Contents

1. [Interview Process Overview](#1-interview-process-overview)
2. [Coding / DSA Questions](#2-coding--dsa-questions)
3. [Low-Level Design (LLD / OOD)](#3-low-level-design-lld--ood)
4. [High-Level / System Design (HLD)](#4-high-level--system-design-hld)
5. [Behavioral / Leadership Principles](#5-behavioral--leadership-principles)
6. [Most-Asked Topic Frequency](#6-most-asked-topic-frequency)
7. [Preparation Resources](#7-preparation-resources)

---

## 1. Interview Process Overview

A typical SDE2 (L5) loop in 2026:

| Round | Duration | What it Tests | Weight |
|-------|----------|---------------|--------|
| Online Assessment (OA) | ~2.5 hrs | 2 coding problems + system design MCQs + Work Style Survey | Gate |
| Phone Screen (Coding + LP) | 60 min | 1 medium problem + 2 LP questions | ~15% |
| Coding Round | 60 min | 1–2 medium problems, LP woven in | ~15% |
| System Design (HLD) | 60 min | End-to-end service design with customer framing | ~20% |
| Object-Oriented Design (LLD) | 60 min | Class design for a real product feature | ~15% |
| Bar Raiser | 60 min | Deep LP probing + 1 technical question (veto power) | ~20% |
| Hiring Manager | 60 min | LPs, culture & team fit | ~15% |

**Key observations from recent candidates:**
- Coding bar is **medium difficulty** (LeetCode mediums, occasionally a hard). It's considered the *lowest* coding bar of big tech at SDE2 — but the LP bar is **not** low.
- **Every single round** weaves in Leadership Principles (typically 2 LP questions/round, ~20–30 min).
- Most coding rejections come from **unhandled edge cases, weak complexity analysis, or non-modular code** — not wrong solutions.
- The **Bar Raiser** is an experienced cross-team interviewer with veto power; expect deep follow-ups on trade-offs and LP consistency.

---

## 2. Coding / DSA Questions

### Arrays / Two Pointers / Sliding Window
- **Two Sum** (LC 1)
- **3Sum** / 3-Sum with two-pointer optimization (LC 15)
- **Container With Most Water** (LC 11)
- **Trapping Rain Water** (LC 42)
- **Subarray Sum Equals K** (LC 560)
- **Sliding Window Maximum** — max in a window of size 3 (LC 239)
- **Product of Array Except Self** (LC 238)
- **Merge Intervals** (LC 56)
- **Maximum Passengers in Car Pooling** (LC 1094)
- Sum of numbers in a window of size 3 (sliding window basic)
- Longest substring with at most K replacements
- Maximum sum subarray (including circular arrays)
- Find duplicates / missing elements efficiently

### Strings / Hashing
- **Longest Substring Without Repeating Characters** (LC 3)
- **Group Anagrams** (LC 49)
- **Valid Parentheses** (LC 20)
- **Minimum Window Substring** (LC 76)
- **Longest Palindromic Substring** (LC 5)
- **Remove Duplicate Letters** — *Amazon twist:* return the **largest** lexicographical result (variant of LC 316, greedy + monotonic stack)
- **Reorganize String** (LC 767)

### Stack / Monotonic Stack
- **Next Greater Element** using a monotonic stack (LC 496 / 503)
- Greedy + stack variants

### Linked Lists
- **Reverse Nodes in K-Group** (LC 25)
- **Copy List with Random Pointer** (LC 138)

### Trees / BST
- **Binary Tree Cameras** (LC 968) — *asked as a "Hard" in a May 2026 R1*
- **Maximum Sum BST in Binary Tree** (LC 1373) — *Bar Raiser round*
- **Serialize and Deserialize Binary Tree** (LC 297)
- Trim binary tree to a complete binary tree while maintaining a "trash" queue (BFS variant)
- Find a special number in an array (one element with a different frequency) — solved via binary search
- Lowest Common Ancestor & root-to-node path problems

### Graphs / BFS / DFS
- **Number of Islands** (LC 200)
- **Number of Distinct Islands** (LC 694)
- **Minimum Number of Days to Disconnect Island** (LC 1568)
- **Word Ladder** (LC 127)
- **Course Schedule** (LC 207)
- **Currency Conversion** — given a file of rates (USD→EUR, EUR→GBP…), find the rate between two arbitrary currencies (graph + DFS/BFS, with optimization follow-ups)
- Word-search style problem solved via BFS, with optimization discussion

### Dynamic Programming
- **Coin Change** (LC 322)
- **Longest Increasing Subsequence** (LC 300)
- **Word Break** (LC 139)
- DP-on-trees variants
- Subsequence / combination counting problems

### Heaps / Priority Queue
- Top-K elements problems
- Priority-queue scheduling-style problems

### Design-Within-Coding
- **LRU Cache** (LC 146)
- **Insert Delete GetRandom O(1)** (LC 380)
- **First Unique Number** (LC 1429)

---

## 3. Low-Level Design (LLD / OOD)

Recent prompts reported (60-min round; focus on clean class hierarchy, SOLID, extensibility, edge cases, and design patterns — Strategy, Factory, Observer):

- **Board game** similar to Ludo/Chess — class responsibilities, where "move a piece" behavior lives
- **Uber / Ride-Hailing System** — Rider, Driver, Trip, Payment, Location entities; trip state machine (`requested → accepted → in_progress → completed/cancelled`); driver matching via geospatial index (quadtree/geohash); surge pricing; idempotent payments
- **Rider-Finding Service** for a quick-commerce app
- **Offline Download Manager** for a social media app
- **Food Ordering System** — classes/services for search, sort, ordering, rating
- **Vending Machine** (get class boundaries right — ~4 classes, not 12)
- **Parking Lot** — `ParkingSpot`, `Vehicle` (Car/Bike subclasses), `Ticket`, `ParkingLot`; thread-safe spot allocation
- **Rate Limiter** — pluggable algorithms (Token Bucket, Leaky Bucket, Fixed/Sliding Window); `isAllowed(request)`; thread safety
- **Basic Calculator** — emphasis on extensibility for new operations
- **Elevator System**
- **Internal AWS feature** (Bar Raiser) — both HLD and LLD discussion

**What kills candidates:** 12 classes when 4 are needed; methods that do too much/too little; missing the obvious edge case (e.g., "what if the parking lot is full?").

---

## 4. High-Level / System Design (HLD)

Reported designs (lead with **customer requirements**, then APIs, data model, scale, and trade-offs):

- **Coursera-like platform** — user management, course catalog, payments, notifications, video streaming
- **Google Docs** — collaborative real-time document editing
- **YouTube** — video uploads, likes/dislikes, comments; storage scaling, high-concurrency read/write
- **Uber** — high-level cab demand surge handling + API & DB schema
- **Event Logging System** — scalability, reliability, data processing
- **WhatsApp Read Receipts** (ticks / delivery status)
- **FastTag / electronic toll collection** — requirements, Redis, scalability
- **Amazon Ads Server** — thousands of ad requests/sec, storage, caching, real-time analytics, traffic-spike handling
- Common Amazon prompts: **Order Service**, **Notification System**, **API Rate Limiting**, **Recommendation Cache**, **URL Shortener with analytics**, **S3-lite file storage**

---

## 5. Behavioral / Leadership Principles

LP questions appear in **every** round. Prepare **2–3 STAR stories per principle**, ideally from the **last 12–18 months**, with specific metrics and *your personal* contribution.

### Frequently reported LP questions
**Dive Deep**
- "Tell me about a time you had to investigate a technical issue deeply and identify the root cause."
- "What is your role when a job fails in production?"

**Bias for Action**
- "Tell me about a time you had to make a decision quickly without complete information."

**Ownership**
- "Tell me about a time you owned a module/project end-to-end, from conception to completion."
- "Tell me about a time you missed a tight deadline. How did you handle it?"

**Deliver Results**
- "Describe a time you compromised on quality to meet a tight deadline."

**Customer Obsession**
- "Tell me about a time you went above and beyond for a customer."
- "Tell me about a time you simplified a complex process/feature for a customer."

**Earn Trust / Conflict**
- "Describe a conflict or disagreement with your manager and how you resolved it."

**Invent and Simplify / Insist on Highest Standards**
- "Tell me about a time you identified an inefficiency and improved an existing process."

**Are Right, A Lot**
- Follow-ups on calculated risk-taking and decisions defended with data.

**Other reported themes:** delivering impact with vague/ambiguous requirements, prioritizing operational excellence vs. feature work, pushing back on unrealistic timelines.

### STAR tips from successful candidates
- Use **S**ituation, **T**ask, **A**ction, **R**esult — interviewers are trained to score in this structure.
- Lead with **data points** and **ownership**; avoid "we", emphasize "I".
- In LLD/HLD rounds, always **justify design decisions** (why a method belongs in a class, why a pattern fits).
- Strong communication & structured explanation matter as much as the correct solution.

---

## 6. Most-Asked Topic Frequency

Approximate frequency of topics appearing in Amazon coding rounds (aggregated from reported experiences):

| Topic | Approx. Frequency | Difficulty Skew |
|-------|------------------|-----------------|
| Arrays & Sliding Window | ~75% | Medium |
| Trees (BST / Binary Tree) | ~70% | Medium–Hard |
| Strings & Hashing | ~62% | Easy–Medium |
| Two Pointers | ~55% | Easy–Medium |
| Dynamic Programming | ~55% | Medium–Hard |
| Graphs (BFS/DFS) | ~48% | Medium |
| Stack / Monotonic Stack | ~39% | Medium |
| Heaps / Priority Queue | ~38% | Medium–Hard |
| Linked Lists | ~35% | Easy–Medium |
| Recursion / Backtracking | ~30% | Hard |

**Takeaway:** Master traversal patterns (inorder/preorder/postorder/level-order), BST ops, LCA & path problems for trees. For DP, **Coin Change + LIS + Word Break** cover ~70% of Amazon DP variants.

---

## 7. Preparation Resources

- **DSA:** LeetCode (Amazon-tagged), NeetCode 150, Striver's A2Z DSA / SDE Sheet — aim for **80–100 high-quality solves** by pattern.
- **HLD:** HelloInterview, "Designing Data-Intensive Applications".
- **LLD:** Shrayansh Jain (Udemy/YouTube), practice SOLID + design patterns (Strategy, Factory, Observer, Singleton).
- **Behavioral:** Memorize all **16 Leadership Principles**; prepare STAR stories; practice telling each in ~90 seconds.

### Source experiences referenced
- LeetCode Discuss — "Amazon SDE 2 Interview Experience (India) — R1, May 2026"
- LeetCode Discuss — "Amazon SDE 2 (L5) | Bangalore | Interview Experience, May 2026"
- interviewexperiences.in — "Amazon SDE2 (full loop)", "Amazon SDE II — Need Honest Feedback", "Amazon SDE 2 | Selected"
- GeeksforGeeks — "Amazon Interview Experience For A SDE-2"
- Medium — Himanshu Dhawan, "Amazon Interview Experience | SDE-2 | 2026"
- HelloInterview — "Amazon L5 Interview Guides & Questions (2026)"
- CrackingWalnuts — "Amazon SDE II Interview Guide 2026"
- LinkedIn — Piyush Nirala, "My Amazon SDE2 Interview Experience"
- interviewhelp.io — "Amazon SDE2 interview experience [USA]"

---

*Last updated: June 2026. Patterns are more durable than specific questions — prepare accordingly.*
