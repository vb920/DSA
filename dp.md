# Dynamic Programming: FAANG SDE-2 Mastery List (Top 2-3%)

This list is heavily curated for top-tier FAANG interviews (L4/L5 / SDE-2 levels). It strips away strictly Competitive Programming (CP) concepts (like Knuth Optimization, Convex Hull Trick, and obscure Digit DPs), focusing purely on deep architectural intuition, space optimization, and recognizing state transitions under pressure.

## 1. 1D DP & Base State Transitions
* **SDE-2 Expectation:** 100% bug-free implementation, intuitively optimizing from $O(N)$ space down to $O(1)$ space using rolling variables without being prompted.
* Climbing Stairs / Min Cost Climbing Stairs
* House Robber I, II
* Decode Ways
* Integer Break
* Perfect Squares

## 2. Strings & 2D Sequences (The Core)
* **SDE-2 Expectation:** Flawless transition logic and edge-case handling (e.g., empty string padding).
* Longest Common Subsequence (LCS)
* Edit Distance (Levenshtein)
* Regular Expression Matching (Classic FAANG Hard)
* Wildcard Matching
* Interleaving String
* Word Break I
* Distinct Subsequences I, II

## 3. Subarrays (Contiguous DP)
* **SDE-2 Expectation:** Knowing when to track multiple running states (Min/Max) vs standard local optimums.
* Maximum Subarray (Kadane’s) / Maximum Sum Circular Subarray
* Maximum Product Subarray (Min/Max tracking technique)
* Largest Divisible Subset

## 4. DP + Binary Search (Explicit Pattern)
* **SDE-2 Expectation:** Interviewers often test whether you can recognize a *hidden* LIS after sorting elements by a specific dimension.
* Longest Increasing Subsequence ($O(N \log N)$ patience sorting is fully expected)
* Longest Bitonic Subsequence
* Russian Doll Envelopes (Sorting + LIS trick — 2D optimization)
* Minimum Operations to Make a Subsequence

## 5. DP + Greedy Boundary Overlap
* **SDE-2 Expectation:** "Do you overuse DP when greedy works?" Interviewers check if you know when a DP state can be fully bypassed by a greedy contiguous boundary trick.
* Jump Game I / II
* Partition Labels
* Minimum Number of Taps to Open to Water a Garden

## 6. Reconstruction Problems (Very Important)
* **SDE-2 Expectation:** The classic FAANG follow-up: "Now return the actual sequence/path." You must know how to confidently trace backwards through your DP table via parent pointers.
* Print LCS (Longest Common Subsequence path)
* Print LIS (Tracing parent pointers)
* Word Break II (Reconstructing sentences using backtracking + memoization)

## 7. Knapsack Patterns (0/1 & Unbounded)
* **SDE-2 Expectation:** Recognizing bounded vs unbounded choices intuitively, and knowing the core trick: rolling the 1D array backwards (0/1) vs forwards (unbounded).
* Partition Equal Subset Sum (0/1 Base pattern)
* Target Sum
* Last Stone Weight II
* Coin Change I (Min coins — Unbounded)
* Coin Change II (Total combinations — Unbounded)
* Ones and Zeroes (2-Dimensional Knapsack constraint)

## 8. Explicit State Machines
* **SDE-2 Expectation:** Defining explicit states (e.g., `hold`, `sold`, `rest`) mathematically rather than writing complex nested loops.
* Best Time to Buy and Sell Stock with Cooldown
* Best Time to Buy and Sell Stock with Transaction Fee
* Best Time to Buy and Sell Stock III (At most 2 transactions — 3D State)
* Best Time to Buy and Sell Stock IV (Generic K transactions)
* Wiggle Subsequence

## 9. Grid, Pathfinding & Multi-Agent DP
* **SDE-2 Expectation:** Condensing a 2D matrix into a 1D rolling row, and handling multi-agent coordination.
* Unique Paths I, II
* Minimum Path Sum
* Dungeon Game (Reverse bottom-up health tracking)
* Maximal Square / Maximal Rectangle (DP or Histogram logic)
* Longest Increasing Path in a Matrix (DFS + Memoization core logic)
* Cherry Pickup I & II (Multi-agent synchronization — *Highly tested in senior loops*)

## 10. Palindromic DP
* **SDE-2 Expectation:** Differentiating substring vs subsequence transitions based on strictly expanding the boundary `(i+1, j-1)`.
* Longest Palindromic Substring (DP & Expand from center)
* Longest Palindromic Subsequence
* Palindrome Partitioning II (Min cuts)
* Count Different Palindromic Subsequences

## 11. Interval DP (Merging / Partitioning)
* **SDE-2 Expectation:** Easily identifying the standard $O(N^3)$ pattern: doing DP on a subarray `[i, j]` and testing all split points `k`.
* Matrix Chain Multiplication (The mathematical template)
* Burst Balloons (The quintessential FAANG interval hard)
* Minimum Cost Tree From Leaf Values
* Minimum Cost to Cut a Stick
* Strange Printer

## 12. Tree DP (Bottom-Up State Passing)
* **SDE-2 Expectation:** Writing a DFS that returns a tuple of states (e.g., `[include_node, exclude_node]`), eliminating external memoization tables.
* Binary Tree Maximum Path Sum (Implicit DP)
* Diameter of Binary Tree
* House Robber III
* Longest ZigZag Path in a Binary Tree
* Binary Tree Cameras

## 13. DP + Heap / Dijkstra Hybrids
* **SDE-2 Expectation:** Knowing when to abandon a pure DP matrix because the state space is too sparse, wrapping your DP transitions inside a Priority Queue instead.
* Minimum Cost to Reach Destination in Time (Min cost with constraints using PQ)
* Cheapest Flights Within K Stops (DP + shortest path hybrid)
* Trapping Rain Water II (Heap boundary reduction)

## 14. Bitmask DP & State Compression
* **SDE-2 Expectation:** Recognizing that small constraints ($N \le 20$) are a massive hint to treat visited nodes/states as an integer bitmask.
* Travelling Salesman Problem (Classic state template)
* Shortest Path Visiting All Nodes
* Smallest Sufficient Team
* Minimum Cost to Connect Two Groups of Points

## 15. Game Theory / Minimax DP
* **SDE-2 Expectation:** Understanding how to cache the opponent’s optimal choice: maximizing your score minus their score.
* Predict the Winner / Stone Game
* Nim Game
* Flip Game II

## 16. DP on DAGs / Topological DP
* **SDE-2 Expectation:** Combining graph traversal (Topological Sort / Dijkstra) with DP state accumulation. Essential for prerequisite and routing problems.
* Longest Increasing Path in a Matrix (DAG interpretation and topological extraction)
* Longest String Chain (The Implicit Array DAG)
* All Paths From Source to Target (The Traversal Baseline)
* Number of Restricted Paths From First to Last Node (Dijkstra + DP Combo)
* Parallel Courses III (Scheduling and Max Time DP)
* Shortest Path in DAG (DP formulation)
* Counting paths in DAG

### **How to Make It a 10/10 (Constructive Additions)**

To make this the ultimate, exhaustive mastery list, consider adding the following three missing nuances:

**1. Probability and Combinatorial DP**
This is a highly tested sub-genre, particularly at Google and Meta. It tests a candidate's ability to handle fractional states and expected values.

* **SDE-2 Expectation:** Handling floating-point states and recognizing when paths diverge with specific probabilities.
* *Knight Probability in Chessboard*
* *Soup Servings*
* *Dice Roll Simulation*

**2. DP + Trie / Advanced String Matching**
While you have the core string patterns in Section 2, FAANG often combines String DP with a Trie to optimize dictionary lookups from $O(L)$ to $O(1)$ per character.

* **SDE-2 Expectation:** Recognizing when a standard `HashSet` lookup inside a Word Break DP is too slow and upgrading the architecture with a Trie.
* *Concatenated Words*
* *Word Break II* (revisited with Trie optimization)

**3. The "Why" Between Top-Down vs. Bottom-Up**
Add a meta-expectation regarding communication. At the SDE-2 level, a candidate shouldn't just default to Bottom-Up Tabulation. They need to articulate *why* they are choosing one over the other.

* **SDE-2 Expectation:** The ability to explain that Top-Down (Memoization) is superior when the state space is massive but sparse (e.g., *Burst Balloons* or *Regular Expression Matching*), whereas Bottom-Up is superior for strict cache-locality and $O(1)$ space optimization.

---

## 📘 DP Sheet — Additions

### **17. Digit DP (Simplified — Tight-Bound Template)**
* **SDE-2 Expectation:** Recognizing "count numbers ≤ N with property X" as a digit-position recursion with a `tight` boolean flag. Only 2–3 problems needed — know the template, not the theory.
* *Number of Digit One (LC 233)*
* *Numbers At Most N Given Digit Set (LC 902)*
* *Count Numbers with Unique Digits (LC 357)* — warm-up, closed-form acceptable

### **18. Bitmask Feasibility & Partitioning (Complement to #14)**
* **SDE-2 Expectation:** Distinguishing TSP-style *optimization* over masks from *feasibility* checks (`can[mask] = true/false`) and subset-enumeration tricks (`sub = (sub-1) & mask`).
* *Partition to K Equal Sum Subsets (LC 698)*
* *Distribute Repeating Integers (LC 1655)*
* *Matchsticks to Square (LC 473)* — same pattern, different skin

### **19. Counting DP with Modular Arithmetic**
* **SDE-2 Expectation:** Handling large counts via `% 1e9+7` cleanly, defining transitions that sum over previous states rather than max/min.
* *Domino and Tromino Tiling (LC 790)*
* *Count Vowels Permutation (LC 1220)*
* *Number of Ways to Stay in the Same Place After Some Steps (LC 1269)*

### **20. Tree DP with Rerooting**
* **SDE-2 Expectation:** Two-pass DFS: compute subtree answers bottom-up, then re-root by pushing parent contributions top-down. Recognize "answer for every node as root" phrasing instantly.
* *Sum of Distances in Tree (LC 834)*
* *Reorder Routes variant practice: Maximum Score of a Node Sequence? No — use Re-rooting on LC 834 + LC 310 Minimum Height Trees (topological peel, adjacent technique)*

### **21. Binary Search on Answer + Greedy Feasibility Check**
* **SDE-2 Expectation:** Spotting "minimize the maximum" / "maximize the minimum" phrasing → binary search the answer, validate with an O(N) greedy sweep. Know when this beats direct DP.
* *Split Array Largest Sum (LC 410)*
* *Find Minimum Time to Finish All Jobs (LC 1723)* — binary search vs bitmask comparison
* *Koko Eating Bananas (LC 875)* — baseline warm-up

### **22. Probability & Combinatorial DP** *(your proposed addition — formalized)*
* **SDE-2 Expectation:** Floating-point states, expected-value accumulation, and probability of reaching a state rather than cost.
* *Knight Probability in Chessboard (LC 688)*
* *Soup Servings (LC 808)*
* *Dice Roll Simulation (LC 1223)*

### **23. DP + Trie Hybrid** *(your proposed addition — formalized)*
* **SDE-2 Expectation:** Upgrading HashSet dictionary lookups inside string DP to Trie traversal when word lengths are bounded or prefixes overlap heavily.
* *Concatenated Words (LC 472)*
* *Word Break II (LC 140)* — Trie-optimized revisit
* *Extra: Longest Word in Dictionary (LC 720)* — light warm-up

### **24. Meta-Pattern: Top-Down vs Bottom-Up Articulation** *(your proposed addition — formalized)*
* **SDE-2 Expectation:** Verbally justifying your choice before coding:
  - **Top-down (memo):** sparse/massive state space, early termination natural (*Burst Balloons*, *Regex Matching*)
  - **Bottom-up (tabulation):** full table needed anyway, enables O(1) rolling space (*House Robber*, *Coin Change*)
  - **Hybrid:** memoize first during interview, offer tabulation as follow-up optimization
* Practice articulation on: *Edit Distance*, *Burst Balloons*, *Regular Expression Matching*

---
