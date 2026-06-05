# Amazon DSA Interview Preparation Guide (2025)

> Compiled from interview experiences posted in 2025 on LeetCode Discuss, Medium, and GeeksforGeeks. ~100+ questions grouped by data structure/algorithm pattern, each with the recommended approach. Practice each problem 2–3 times rather than skimming many — Amazon recycles the same patterns.

**Interview format reminder**: SDE-1 typically gets a 45–60 min round with 1 medium + 1 follow-up, or 2 mediums. SDE-2 sees 1 hard or 1 medium + design follow-up. Most rounds also include 15–20 min on Leadership Principles. Expect deep follow-ups on time/space complexity and edge cases.

---

## 1. Arrays & Greedy

### Easy
| # | Problem | Approach |
|---|---------|----------|
| 9 | Palindrome Number | Reverse half the digits and compare; avoid string conversion for O(1) space. |
| 88 | Merge Sorted Array | Two pointers starting from the end of both arrays, write into nums1 from the back. |
| 169 | Majority Element | Boyer–Moore voting — single pass, O(1) space. |
| 760 | Find Anagram Mappings | Hashmap of value → index in B, then map each A[i] to that index. |

### Medium
| # | Problem | Approach |
|---|---------|----------|
| 48 | Rotate Image | Transpose the matrix in place, then reverse each row. |
| 54 | Spiral Matrix | Maintain four boundaries (top, bottom, left, right) and shrink them after each traversal. |
| 56 | Merge Intervals | Sort by start; iterate and merge when current.start ≤ last.end. |
| 78 | Subsets | Backtracking or iterative — for each element, double the existing subsets. |
| 253 | Meeting Rooms II | Min-heap of end times, or sort starts/ends separately and sweep. |
| 348 | Design Tic-Tac-Toe | Track row/col/diagonal counters per player; +1 for player 1, –1 for player 2. |
| 361 | Bomb Enemy | Precompute kills in each direction with DP to avoid recomputation. |
| 556 | Next Greater Element III | Find first decreasing digit from right, swap with smallest larger digit on its right, then sort the suffix. |
| 569 | Max Chunks To Make Sorted | Compare running max with index — if max == i, you can chunk here. |
| 635 | Design Log Storage System | Store as strings; for retrieval, truncate timestamps to the granularity and compare lexically. |
| 2139 | Min Moves to Reach Target Score | Work backward from target: halve if even, else subtract 1. |

### Hard
| # | Problem | Approach |
|---|---------|----------|
| 273 | Integer to English Words | Split number into groups of three digits, convert each group, append scale ("Thousand", "Million"…). |
| 768 | Max Chunks To Make Sorted II | Monotonic stack: keep max of each chunk; pop and merge when current value < top. |
| 1842 | Next Palindrome Using Same Digits | Take left half, compute next permutation, mirror to right half. |

---

## 2. Two-Pointers & Sliding Window

### Easy
| # | Problem | Approach |
|---|---------|----------|
| 125 | Valid Palindrome | Two pointers from both ends, skip non-alphanumeric. |
| 283 | Move Zeroes | Two pointers — write index advances only on non-zero. |

### Medium
| # | Problem | Approach |
|---|---------|----------|
| 3 | Longest Substring Without Repeating Characters | Sliding window + hashmap of last seen index; shrink left when duplicate. |
| 11 | Container With Most Water | Two pointers; move the shorter line inward. |
| 15 | 3Sum | Sort, fix one number, two pointers for the other two; skip duplicates. |
| 31 | Next Permutation | Find first decreasing element from right, swap with next larger on the right, reverse the suffix. |
| 76 | Minimum Window Substring | Sliding window with character-need counter; track when all chars satisfied. |
| 159 | Longest Substring with At Most 2 Distinct Characters | Sliding window with hashmap; shrink when map size > 2. |
| 189 | Rotate Array | Reverse whole array, then reverse first k, then reverse rest. |
| 277 | Find the Celebrity | Two-pointer elimination — if A knows B, A isn't celebrity; verify candidate at the end. |
| 340 | Longest Substring with At Most K Distinct Characters | Same as #159 generalized to k. |
| 424 | Longest Repeating Character Replacement | Window of size (maxFreq + k); expand if window length – maxFreq ≤ k. |
| 560 | Subarray Sum Equals K | Prefix sum + hashmap of count of each sum seen. |

---

## 3. Hash Table & String Manipulation

### Easy
| # | Problem | Approach |
|---|---------|----------|
| 1 | Two Sum | Single-pass hashmap of value → index. |
| 14 | Longest Common Prefix | Vertical scan: compare ith char across all strings until mismatch. |
| 136 | Single Number | XOR of all elements (duplicates cancel). |
| 242 | Valid Anagram | Count characters with a length-26 array. |

### Medium
| # | Problem | Approach |
|---|---------|----------|
| 49 | Group Anagrams | Hashmap keyed by sorted string (or 26-char count signature). |
| 244 | Shortest Word Distance II | Preprocess hashmap of word → sorted indices; merge two index lists with two pointers. |
| 267 | Palindrome Permutation II | Build half from char counts, then permute that half uniquely; mirror for full palindrome. |

---

## 4. Stack & Monotonic Stack

### Easy
| # | Problem | Approach |
|---|---------|----------|
| 20 | Valid Parentheses | Push opens, pop and match closes. |
| 496 | Next Greater Element I | Monotonic decreasing stack while iterating nums2; map each value to its next greater. |

### Medium
| # | Problem | Approach |
|---|---------|----------|
| 150 | Evaluate Reverse Polish Notation | Stack of operands; on operator, pop two, apply, push back. |
| 227 | Basic Calculator II | Stack: push numbers, apply *,/ immediately on previous, sum at end. |
| 394 | Decode String | Two stacks (count, prefix string) — push on '[', pop and build on ']'. |
| 503 | Next Greater Element II | Iterate twice (2n) with a monotonic stack to handle circularity. |
| 735 | Asteroid Collision | Stack; on each new asteroid, compare with top while signs differ (right vs left). |

### Hard
| # | Problem | Approach |
|---|---------|----------|
| 84 | Largest Rectangle in Histogram | Monotonic increasing stack; on pop, compute area with current index as right boundary. |
| 224 | Basic Calculator | Stack stores sign and result before each '('; reset on '(' and apply on ')'. |

---

## 5. Linked List

### Easy
| # | Problem | Approach |
|---|---------|----------|
| 21 | Merge Two Sorted Lists | Dummy head, walk both lists, attach smaller. |

### Medium
| # | Problem | Approach |
|---|---------|----------|
| 2 | Add Two Numbers | Iterate both lists with a carry; create nodes as you go. |
| 138 | Copy List with Random Pointer | Hashmap old → new, or interleave-copy-then-split. |
| 353 | Design Snake Game | Deque of body positions + hashset for O(1) collision check. |
| 707 | Design Linked List | Implement with sentinel head; mind index bounds. |

### Hard
| # | Problem | Approach |
|---|---------|----------|
| 25 | Reverse Nodes in k-Group | Count k nodes ahead, reverse if available, recurse/iterate to next group. |

---

## 6. Binary Search

### Easy
| # | Problem | Approach |
|---|---------|----------|
| 69 | Sqrt(x) | Binary search for largest n where n*n ≤ x. |
| 268 | Missing Number | XOR all indices and values, or sum formula minus actual sum. |

### Medium
| # | Problem | Approach |
|---|---------|----------|
| 33 | Search in Rotated Sorted Array | Binary search — determine which half is sorted, then check if target lies in it. |
| 528 | Random Pick with Weight | Prefix sums + binary search a random number in [1, total]. |
| 852 | Peak Index in a Mountain Array | Binary search — if mid < mid+1, peak is right; else left. |
| 875 | Koko Eating Bananas | Binary search on the speed; feasibility check sums ceil(pile/speed). |
| 1060 | Missing Element in Sorted Array | Binary search on "missing count up to index i" = arr[i] – arr[0] – i. |
| 2055 | Plates Between Candles | Prefix array of plate counts + nearest-candle arrays; answer each query in O(1). |

### Hard
| # | Problem | Approach |
|---|---------|----------|
| 4 | Median of Two Sorted Arrays | Binary search the partition on the shorter array so that left halves have right combined size. |

---

## 7. Tree / Binary Tree

### Easy
| # | Problem | Approach |
|---|---------|----------|
| 101 | Symmetric Tree | Recurse with mirrored pairs (left.left vs right.right, left.right vs right.left). |
| 103 | Binary Tree Zigzag Level Order Traversal | BFS with a flag; reverse alternate levels (or use a deque). |
| 236 | Lowest Common Ancestor of a Binary Tree | Recurse; if both children return non-null, current node is the LCA. |
| 250 | Count Univalue Subtrees | Post-order: subtree is unival if both children are unival and equal to current value. |
| 543 | Diameter of Binary Tree | Recurse computing height; update global diameter as leftH + rightH at each node. |

---

## 8. Graph (BFS / DFS / Union-Find / Topological Sort)

### Medium
| # | Problem | Approach |
|---|---------|----------|
| 79 | Word Search | DFS with backtracking; mark visited in place. |
| 128 | Longest Consecutive Sequence | HashSet; for each number that has no n-1 predecessor, count up. |
| 200 | Number of Islands | DFS/BFS flood-fill on '1' cells; count starts. |
| 207 | Course Schedule | Topological sort via Kahn's BFS or DFS cycle detection. |
| 210 | Course Schedule II | Same as 207, append nodes to result in topological order. |
| 261 | Graph Valid Tree | n-1 edges and fully connected (Union-Find or BFS). |
| 323 | Number of Connected Components | Union-Find; count distinct parents. |
| 490 | The Maze | BFS/DFS rolling ball until it hits a wall; mark stop positions. |
| 505 | The Maze II | Dijkstra-style BFS with distance updates on stop positions. |
| 547 | Number of Provinces | Union-Find or DFS on the adjacency matrix. |
| 994 | Rotting Oranges | Multi-source BFS from all rotten cells simultaneously. |

### Hard
| # | Problem | Approach |
|---|---------|----------|
| 127 | Word Ladder | BFS over words; preprocess pattern buckets (`h*t`, `ho*`) for O(1) neighbor lookup. |
| 212 | Word Search II | Trie of all words + DFS in grid; prune by trie traversal. |
| 631 | Design Excel Sum Formula | Cell value + dependency graph; on set, recompute dependents via DFS. |
| 827 | Making a Large Island | Label each island and store its size; for each 0, sum unique neighboring island sizes + 1. |

---

## 9. Heap / Priority Queue

### Medium
| # | Problem | Approach |
|---|---------|----------|
| 215 | Kth Largest Element in an Array | Min-heap of size k, or Quickselect average O(n). |
| 347 | Top K Frequent Elements | Bucket sort by frequency, or min-heap of size k. |
| 767 | Reorganize String | Max-heap by frequency; pop two most frequent, append, decrement, push back. |
| 1057 | Campus Bikes | Sort all (worker, bike) distance triples; assign greedily. |
| 1167 | Minimum Cost to Connect Sticks | Min-heap; repeatedly pop two smallest, sum, push back. |
| 2336 | Smallest Number in Infinite Set | Min-heap for added-back numbers + integer pointer for the rest. |

### Hard
| # | Problem | Approach |
|---|---------|----------|
| 23 | Merge k Sorted Lists | Min-heap of list heads, or divide-and-conquer pairwise merge. |
| 239 | Sliding Window Maximum | Monotonic decreasing deque storing indices. |
| 295 | Find Median from Data Stream | Two heaps — max-heap for lower half, min-heap for upper half, rebalance. |
| 642 | Design Search Autocomplete System | Trie with top-3 sentences cached at each node, or trie + heap on retrieval. |

---

## 10. Design

### Medium
| # | Problem | Approach |
|---|---------|----------|
| 146 | LRU Cache | HashMap + doubly linked list; move on access, evict from tail. **The single most-asked Amazon question — drill it.** |
| 362 | Design Hit Counter | Circular buffer of 300 timestamps + counts, or queue of timestamps. |
| 380 | Insert Delete GetRandom O(1) | HashMap of value → index + dynamic array; on delete swap with last. |

### Hard
| # | Problem | Approach |
|---|---------|----------|
| 460 | LFU Cache | HashMap + frequency-buckets (each a doubly linked list); track min frequency. |
| 588 | Design In-Memory File System | Tree of directory nodes; each node has children map + optional file content. |

---

## 11. Dynamic Programming

### Easy
| # | Problem | Approach |
|---|---------|----------|
| 70 | Climbing Stairs | Fibonacci: dp[i] = dp[i-1] + dp[i-2]. |
| 118 | Pascal's Triangle | Each row built from previous row. |
| 121 | Best Time to Buy and Sell Stock | Track min so far; max profit = price – minSoFar. |

### Medium
| # | Problem | Approach |
|---|---------|----------|
| 5 | Longest Palindromic Substring | Expand around each center (2n–1 centers), or DP table. |
| 22 | Generate Parentheses | Backtracking with open/close counts. |
| 45 | Jump Game II | Greedy: track current end and farthest reachable; bump jumps when i == currentEnd. |
| 53 | Maximum Subarray | Kadane's: currentMax = max(num, currentMax + num). |
| 55 | Jump Game | Greedy: track farthest reachable; if i > farthest, fail. |
| 62 | Unique Paths | dp[i][j] = dp[i-1][j] + dp[i][j-1]; reducible to 1D. |
| 122 | Best Time to Buy and Sell Stock II | Sum of all positive deltas. |
| 152 | Maximum Product Subarray | Track current max AND min (negatives can flip). |
| 198 | House Robber | dp[i] = max(dp[i-1], dp[i-2] + nums[i]). |
| 238 | Product of Array Except Self | Prefix product pass + suffix product pass. |
| 322 | Coin Change | dp[amount] = min(dp[amount – coin] + 1) over all coins. |
| 518 | Coin Change II | Outer loop over coins, inner over amounts (each coin used after the other to avoid double-counting). |
| 634 | Find the Derangement of an Array | D(n) = (n-1) * (D(n-1) + D(n-2)). |
| 1062 | Longest Repeating Substring | Binary search on length + rolling hash (or DP). |
| 1066 | Campus Bikes II | Bitmask DP over assigned bikes; minimize total Manhattan. |

### Hard
| # | Problem | Approach |
|---|---------|----------|
| 42 | Trapping Rain Water | Two pointers tracking leftMax/rightMax; water at i = max – height[i]. |
| 140 | Word Break II | DFS + memoization keyed on remaining string. |
| 472 | Concatenated Words | Sort by length; for each word, run Word Break using only shorter words in the dict. |
| 1289 | Minimum Falling Path Sum II | Track the two smallest values from previous row to update current in O(n²). |

---

## Mini interview-experience deltas (Jan–Feb 2025, paraphrased)

A few questions that showed up in recent live rounds, not necessarily on the canonical list above — worth a glance:

- **Grid maximum-sum path with roadblocks**: DP on grid; skip cells with negative values; classic min-path-sum variant.
- **Keys and Rooms** (LC 841): BFS/DFS from room 0, mark visited.
- **Sort Colors** (LC 75): Dutch national flag, three pointers.
- **Number of Islands II** (LC 305): Union-Find with rank, add land one at a time.
- **Regions Cut by Slashes** (LC 959): Model each cell as 4 triangles, union them based on the slash; count connected components.
- **Task Scheduler** (LC 621): Heap of counts + cooldown queue, or formula `(max-1)*(n+1) + tiesAtMax`.
- **N-ary tree node count at level L with dynamic add/remove**: HashMap of level → count, update on insert/delete.

---

## Suggested 4-week plan

- **Week 1** — Arrays, Two Pointers/Sliding Window, Hashing, Strings (~30 problems).
- **Week 2** — Stack, Linked List, Binary Search, Trees (~25 problems).
- **Week 3** — Graphs, Heaps, Design (LRU/LFU are non-negotiable) (~25 problems).
- **Week 4** — DP, mock interviews, redo the questions you stumbled on (~20 problems + 5 mocks).

Aim for the medium and hard tier — Amazon rarely asks pure easies in interviews; easies show up as warm-ups before the real question. Always discuss complexity and edge cases out loud; that's half the signal interviewers grade on.

Good luck.