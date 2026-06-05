# Microsoft SDE2 — DSA / Coding Questions (Last 6 Months)

> Compiled from real interview experiences on **LeetCode Discuss**, **GeeksforGeeks**, **interviewexperiences.in**, **Medium**, **LinkedIn**, **YouTube**, and Microsoft-tagged question lists (~Dec 2025 – Jun 2026).
>
> **Note:** Microsoft favors **clean, readable, practical code** over LeetCode-Hard gymnastics. Coding bar is **medium**. Interviewers are explicitly instructed to judge **code quality** and **edge-case handling**.

---

## How the Coding Rounds Work
- **OA:** 2–3 medium (occasionally medium-hard) problems on Codility/HackerRank; all custom test cases must pass.
- **Onsite:** 1–2 problems per 60-min round; clarify constraints → brute force → optimize → test. Microsoft often pairs **2 DSA rounds**.
- Expect **resume / project discussion** at the start of each round.
- Language-agnostic, but show mastery; **OOP cleanliness matters** more than at peers.

---

## Reported in Recent Interviews (last 6 months)
| Question | LeetCode / Source |
|----------|-------------------|
| **Shortest path in a weighted grid** with constraints (graph + DP) | — |
| **Meeting Rooms II** (min rooms) — implement PQ **and** two-pointer | LC 253 |
| **Maximum Reward Path** — `n` tiles with +/- rewards, jumps of +1/+2/+3, maximize reward to reach `n-1` (DP) | — |
| **Linked list cycle** — detect & remove, in-place | LC 141 / 142 |
| Simplified **regex-style string matching** | LC 10 (simplified) |
| **Topological Sort** — task scheduling | LC 207 / 210 |
| **Valid Parentheses** variant — multiple bracket rules | LC 20 (variant) |
| **Number of Provinces / friend circles** — disconnected groups | LC 547 |
| **Binary search on answer** — like "Min Days to Make Bouquets" / "Kth smallest" | LC 1482 / 378 |
| **Stream of numbers** — efficiently check for primes | — |
| A **tree** question + a **DP** question (popular Microsoft pair) | — |
| Linked-list design question (build from scratch, customize per test case) + a **math** question | — |
| "Design a file system snapshot tracker" → reduces to tree traversal + hash-backed state | — |

## Microsoft Favorites / Frequently Tagged
**Linked Lists** (very high)
- Add Two Numbers (LC 2), Merge Two Sorted Lists (LC 21), Merge K Sorted Lists (LC 23)
- Copy List with Random Pointer (LC 138), Reverse Linked List II (LC 92), Rotate List (LC 61), Swap Nodes in Pairs (LC 24)

**Arrays & Strings** (very high)
- Two Sum & variations (LC 1), Search in Rotated Sorted Array (LC 33)
- Group Anagrams (LC 49), Valid Parentheses (LC 20), Longest Palindromic Substring (LC 5)
- Longest Substring Without Repeating Characters (LC 3), Minimum Window Substring (LC 76)
- String to Integer / atoi (LC 8), Edit Distance (LC 72), Decode Ways (LC 91)

**Trees** (high)
- Validate BST (LC 98), Serialize/Deserialize Binary Tree (LC 297)
- Lowest Common Ancestor (LC 235/236), Construct Tree from Preorder+Inorder (LC 105)
- Diameter of Binary Tree (LC 543), Kth Smallest in BST (LC 230), Path Sum (LC 112)

**Graphs** (high)
- Clone Graph (LC 133), Course Schedule (LC 207), Number of Islands (LC 200)
- Word Ladder (LC 127), Rotting Oranges (LC 994), Shortest Path in Binary Matrix (LC 1091), Alien Dictionary (LC 269)

**Heaps / Sliding Window**
- Kth Largest, median of data stream, sliding-window maximum

**DP (recursion + memoization preferred over tables)**
- Coin Change, Decode Ways, Edit Distance, jump/reward path variants

---

## Topic Frequency (Microsoft)
| Topic | Frequency |
|-------|-----------|
| Arrays & Strings | Very High |
| Trees & Graphs | High |
| Linked Lists | High |
| Hash Maps (state tracking) | High |
| Recursion / Backtracking | Medium |
| Dynamic Programming | Medium |

## Priority Topics (from recent guides)
- Trees & graphs (DFS/BFS, topological sort, LCA)
- Heaps & sliding window (median streams, kth largest)
- **Recursion with memoization** (not DP tables)
- Array manipulation with two pointers
- Hash maps for **state tracking** (not just counting)

## Resources
- LeetCode **Microsoft-tagged** mediums; practice with a 45-min timer, no hints.
- Emphasize clean decomposition, edge cases (null, empty, concurrent modification), and complexity analysis.

*Last updated: June 2026.*
