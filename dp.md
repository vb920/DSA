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
