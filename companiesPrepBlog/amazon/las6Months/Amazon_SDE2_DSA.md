# Amazon SDE2 — DSA / Coding Questions (Last 6 Months)

> Compiled from real interview experiences on **LeetCode Discuss**, **GeeksforGeeks**, **InterviewBit / interviewexperiences.in**, **HelloInterview**, **CrackingWalnuts**, **Medium**, and **LinkedIn** (~Dec 2025 – Jun 2026).
>
> **Note:** Amazon rotates questions frequently — the exact problem rarely repeats, but the **pattern** does. Prepare by pattern.

---

## How the Coding Rounds Work
- **Difficulty:** mostly LeetCode **medium**, occasionally a hard. Usually **1–2 problems** per 60-min round.
- LP questions woven into every coding round (~20–30 min).
- **Most rejections come from:** unhandled edge cases (null nodes, empty input, overflow), weak time/space analysis, and non-modular code — *not* wrong answers.
- Always: ask clarifying questions → explain approach in plain English → write clean code with edge cases → state complexity at the end.

---

## Arrays / Two Pointers / Sliding Window
| Question | LeetCode |
|----------|----------|
| Two Sum | LC 1 |
| 3Sum (two-pointer optimization) | LC 15 |
| Container With Most Water | LC 11 |
| Trapping Rain Water | LC 42 |
| Subarray Sum Equals K | LC 560 |
| Sliding Window Maximum (max in window of size 3) | LC 239 |
| Product of Array Except Self | LC 238 |
| Merge Intervals | LC 56 |
| Maximum Passengers in Car Pooling | LC 1094 |
| Sum of numbers in a window of size 3 (basic sliding window) | — |
| Longest substring with at most K replacements | LC 424 |
| Maximum sum subarray (incl. circular arrays) | LC 53 / 918 |
| Find duplicates / missing elements efficiently | LC 287 / 448 |

## Strings / Hashing
| Question | LeetCode |
|----------|----------|
| Longest Substring Without Repeating Characters | LC 3 |
| Group Anagrams | LC 49 |
| Valid Parentheses | LC 20 |
| Minimum Window Substring | LC 76 |
| Longest Palindromic Substring | LC 5 |
| Remove Duplicate Letters — **Amazon twist: return the *largest* lexicographical result** | variant of LC 316 |
| Reorganize String | LC 767 |

## Stack / Monotonic Stack
| Question | LeetCode |
|----------|----------|
| Next Greater Element (monotonic stack) | LC 496 / 503 |
| Greedy + stack variants | — |

## Linked Lists
| Question | LeetCode |
|----------|----------|
| Reverse Nodes in K-Group | LC 25 |
| Copy List with Random Pointer | LC 138 |

## Trees / BST
| Question | LeetCode |
|----------|----------|
| Binary Tree Cameras (asked as "Hard" in May 2026 R1) | LC 968 |
| Maximum Sum BST in Binary Tree (Bar Raiser) | LC 1373 |
| Serialize and Deserialize Binary Tree | LC 297 |
| Trim binary tree to a complete binary tree + maintain "trash" queue (BFS) | — |
| Find a special number in array (one element with different frequency) — binary search | — |
| Lowest Common Ancestor & root-to-node path problems | LC 236 |

## Graphs / BFS / DFS
| Question | LeetCode |
|----------|----------|
| Number of Islands | LC 200 |
| Number of Distinct Islands | LC 694 |
| Minimum Number of Days to Disconnect Island | LC 1568 |
| Word Ladder | LC 127 |
| Course Schedule | LC 207 |
| Currency Conversion (rates file → rate between two currencies; optimization follow-ups) | LC 399 |
| Word-search style problem via BFS + optimization | LC 79 / 212 |

## Dynamic Programming
| Question | LeetCode |
|----------|----------|
| Coin Change | LC 322 |
| Longest Increasing Subsequence | LC 300 |
| Word Break | LC 139 |
| DP-on-trees variants | — |
| Subsequence / combination counting | — |

> **Coin Change + LIS + Word Break cover ~70% of Amazon DP variants.**

## Heaps / Priority Queue
- Top-K elements problems (LC 215, LC 347)
- Priority-queue scheduling-style problems

## Design-Within-Coding
| Question | LeetCode |
|----------|----------|
| LRU Cache | LC 146 |
| Insert Delete GetRandom O(1) | LC 380 |
| First Unique Number | LC 1429 |

---

## Topic Frequency (aggregated)
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

## Resources
- LeetCode (Amazon-tagged), **NeetCode 150**, **Striver's A2Z / SDE Sheet**.
- Aim for **80–100 high-quality solves by pattern**, not raw volume.

*Last updated: June 2026.*
