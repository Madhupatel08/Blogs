# Salesforce SDE2 / MTS — DSA / Coding Questions (Last 6 Months)

> Compiled from real interview experiences on **LeetCode Discuss**, **GeeksforGeeks**, **interviewexperiences.in**, **CodingKaro**, **Medium**, and **Substack (roundz)** (~Dec 2025 – Jun 2026).
>
> **Note:** Salesforce hires for **scalable, multi-tenant thinking + clean code**, not LeetCode-Hard speed. Coding bar is **medium**.

---

## How the Coding Rounds Work
- **OA:** 2–4 LeetCode **medium-to-hard** problems on HackerRank (often proctored — mic & camera on). Some candidates report TLE on the last problem.
- **Technical rounds:** 60 min each, usually start with project discussion, then 1–2 coding problems.
- **Java fluency expected** (core platform is Java), but interviews are language-agnostic — show mastery of one language, especially **memory management & concurrency**.
- Evaluated on: correctness, **code structure/cleanliness**, edge cases, time/space optimization, and how you handle **larger inputs**.

---

## Arrays / Strings
| Question | LeetCode |
|----------|----------|
| Zigzag Conversion (string across N rows) | LC 6 |
| Letter Combinations of a Phone Number (keypad) | LC 17 |
| Max possible **even sum** from an array | — |
| Array problem with large-input / edge-case follow-ups | — |
| Simple string warm-up → then a DP follow-up | — |

## Hashing / Heaps (Priority Queue)
| Question | LeetCode |
|----------|----------|
| Top K Frequent Words | LC 692 |
| Top K Frequent Elements (heap / PQ) | LC 347 |

## Graphs / BFS / DFS
| Question | LeetCode |
|----------|----------|
| Number of Islands (variant) | LC 200 |

## Sliding Window / Prefix
| Question | LeetCode |
|----------|----------|
| Longest Well-Performing Interval | LC 1124 |
| **M microservices report Y/N daily → longest streak of consecutive all-pass days** (Well-Performing Interval variant) | — |

## Greedy / Two-Pointer
| Question | Source |
|----------|--------|
| Policemen Catching Thieves | GeeksforGeeks |
| "Pairs"-style problem | — |

## Dynamic Programming
| Question | Notes |
|----------|-------|
| A challenging DP question after an easy string warm-up | Reported in Round 2 |

---

## Topics to Prioritize (highest yield first)
1. **Arrays & Strings** — two pointers, sliding window, frequency maps.
2. **Graphs** — BFS/DFS, islands, connected components.
3. **Heaps / Priority Queue** — Top-K problems recur.
4. **HashMaps** — frequency counting, fast lookups.
5. **Dynamic Programming** — present but manageable; don't over-index on niche DP.
6. **Concurrency** — reason about thread-safety in code.

## Strategy & Resources
- Solve **100–150 LeetCode Mediums**, prioritizing **Arrays, Strings, Graphs** over niche DP.
- Practice in **Java**; emphasize clean, modular, production-ready code.
- Always state **time/space complexity** and discuss scaling to larger inputs.

*Last updated: June 2026.*
