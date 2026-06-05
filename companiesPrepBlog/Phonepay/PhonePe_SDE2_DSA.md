# PhonePe SDE-2 — DSA / Problem Solving Questions

> Compiled from real candidate experiences (LeetCode Discuss, GeeksforGeeks, Glassdoor, Desi QnA,
> LinkedIn, blogs) and the CodeJeet PhonePe question bank (102 LeetCode-tagged problems).

## How the DSA round works (quick recap)
- ~60 min, **2–3 problems** (+ occasional puzzle).
- Difficulty: **LeetCode Medium → Hard**.
- Questions are usually **descriptive paragraphs / real-world scenarios**, not direct prompts.
- Expectations: brute-force → optimal, **always discuss time & space complexity**, sometimes full working code tested on multiple inputs, sometimes approach-only / pseudo-code on Notepad.

### Topic frequency (from CodeJeet's PhonePe tag breakdown — 102 problems)
| Topic | Approx. count | Priority |
|-------|--------------|----------|
| Array | 70 | 🔴 Highest |
| Dynamic Programming | 31 | 🔴 High |
| Sorting | 24 | 🟠 |
| Hash Table | 24 | 🟠 |
| String | 20 | 🟠 |
| BFS | 18 | 🟠 |
| Greedy | 15 | 🟠 |
| Binary Search | 14 | 🟡 |
| DFS | 14 | 🟡 |
| Graph Theory | 14 | 🟡 |
| Trees | recurring | 🟡 |

Difficulty mix of the tagged set: **3 Easy, 63 Medium, 36 Hard** → focus on **Medium** first.

---

## 1. Arrays / Hashing / Prefix Sum / Sliding Window
- **Build lowest number by removing N digits** from a given number (a.k.a. *Remove K Digits*, LC 402) — *asked, GFG link confirmed*.
- **Maximize sum by picking prefix/suffix elements** of an array.
- **Range queries on digits** in numbers.
- **Missing number** in a sorted array.
- **Array frequency optimization** problem (OA).
- **User with max log time in last 1 hour** — variation of **prefix sum** over timestamps. *(asked)*
- **Top / most-frequent API endpoints** — HashMap + Min-Heap (top-K). *(OA)*
- **Longest substring with K unique characters.**
- **Smallest range covering elements from K lists** (LC 632).
- **Trapping Rain Water** (LC 42). *(asked)*
- **Minimum number of platforms required** (GFG). *(asked)*
- Sliding-window based array problem (descriptive). *(asked)*
- **String rotation check** / valid string rotation. *(OA)*
- **Valid subsets / combination finding** (with DP). *(asked)*
- **Koko Eating Bananas** (LC 875) — binary search on answer. *(asked)*

## 2. Strings
- **Regular Expression Matching** (LC 10). *(reported)*
- **Evaluate expressions with brackets** / expression evaluation.
- **String rotation** check.
- Longest substring with K unique characters (also above).

## 3. Stacks / Queues
- **Next Greater Element** (and close variations) — *write full code + test*. *(asked)*
- Expression evaluation with brackets (stack-based).

## 4. Trees
- **Binary Tree Maximum Path Sum** (LC 124) — and **variations**. *(asked)*
- **Binary Tree Cameras** (LC 968). *(asked)*
- **Spread of infection in a binary tree** / Amount of Time for Binary Tree to be Infected (LC 2385). *(asked)*
- **Tree traversal** based question with a minor addition/twist. *(asked, multiple candidates)*
- **Sum of Distances in Tree** (LC 834) — Hard, tree DP. *(CodeJeet PhonePe tag)*
- General traversals, path sums, lowest common ancestor.

## 5. Graphs
- **Minimum Spanning Tree (MST)** — approach/algorithm only. *(asked)*
- **Course Schedule** (LC 207) — topological sort; interviewer pushed for *better than BFS*. *(asked)*
- **Number of Provinces** (LC 547) — connected components. *(asked)*
- **Number of Islands** / count islands via graph traversal. *(OA)*
- **Disconnected graphs** — model + BFS. *(asked)*
- **Graph modeling problem followed by DFS** (+ complexity). *(asked)*
- **Number of ways to start at vertex A and return to A of a triangle using N hops.** *(asked — combinatorics/DP on graph)*
- **Reachable Nodes in Subdivided Graph** (LC 882) — Hard, Dijkstra/heap. *(CodeJeet tag)*
- **Shortest Cycle in a Graph** (LC 2608) — Hard, BFS. *(CodeJeet tag)*
- **Longest Cycle in a Graph** (LC 2360) — Hard, DFS. *(CodeJeet tag)*
- **Collect Coins in a Tree** (LC 2603) — Hard, tree + graph. *(CodeJeet tag)*

## 6. Dynamic Programming
- **Minimum coins problem** (coin change, LC 322).
- **Tree-based DP** (e.g., Sum of Distances in Tree, OA tree-DP).
- **Game theory** problem (OA).
- Subsequence / optimization (min/max) DP patterns.
- Valid subsets / combinations using DP (above).
- Regular Expression Matching (DP, above).

## 7. Greedy
- **Chocolate / Candy Distribution** (LC 135, "Candy") — children ratings, min candies. *(asked, GFG)*.
- **Remove K Digits** (greedy + stack, above).
- Smallest range covering K lists (greedy + heap, above).

## 8. Binary Search
- **Koko Eating Bananas** (LC 875). *(asked)*
- Binary search on answer / sorted-array searches.
- Missing number in sorted array (above).

## 9. Math / Puzzles
- **rand12() from rand6()** — implement uniform 1–12 using a given uniform 1–6 (with *exact* equal probability). *(asked as a puzzle, GFG)*.
- Famous competitive-math question (one candidate solved via BFS instead). *(asked)*

---

## Suggested practice set (high ROI)
1. Remove K Digits (LC 402)
2. Next Greater Element II (LC 503)
3. Course Schedule I/II (LC 207/210)
4. Number of Provinces (LC 547)
5. Trapping Rain Water (LC 42)
6. Minimum Platforms (GFG)
7. Binary Tree Maximum Path Sum (LC 124)
8. Binary Tree Cameras (LC 968)
9. Amount of Time for Binary Tree to Be Infected (LC 2385)
10. Candy (LC 135)
11. Koko Eating Bananas (LC 875)
12. Smallest Range Covering Elements from K Lists (LC 632)
13. Coin Change (LC 322)
14. Longest Substring with At Most K Distinct Characters (LC 340)
15. Sum of Distances in Tree (LC 834)

> Tip: Practice converting **paragraph/scenario descriptions** into these known patterns, and rehearse
> the **brute-force → optimal** narration out loud with complexities.
