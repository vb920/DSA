---

### 1. 1D DP & Basic State Transitions

These problems require looking back at 1 or 2 previous states to determine the current state.

* Climbing Stairs
* Min Cost Climbing Stairs
* House Robber
* 2 Keys Keyboard

### 2. Subarrays & Subsequences

Problems focused on contiguous (subarray) or non-contiguous (subsequence) elements, often requiring you to track ongoing sums, products, or differences.

* Maximum Subarray (The Base)
* Maximum Product Subarray (The "Min/Max" Trick)
* Wiggle Subsequence (The State Machine)
* Longest Arithmetic Subsequence of Given Difference (The Hash Map DP)
* Minimum Swaps To Make Sequences Increasing (The Two-State DP)
* Constrained Subsequence Sum (The Deque Optimization)
* Find the Count of Monotonic Pairs I
* Find the Count of Monotonic Pairs II

### 3. Longest Increasing Subsequence (LIS) Variants

A specific subset of subsequence problems relying on the classic LIS pattern (often optimized from $O(n^2)$ to $O(n \log n)$ via binary search/patience sorting).

* Longest Increasing Subsequence (patience sorting)
* Number of Longest Increasing Subsequence
* Largest Divisible Subset
* Russian Doll Envelopes


### 4. Knapsack Patterns (0/1, Unbounded, & Multi-dimensional)

Problems where you must choose subsets of items under specific constraints (weight, cost, count).

* 0/1 Knapsack (template) — NEW
* Rod Cutting (unbounded knapsack template) — NEW
* Partition Equal Subset Sum
* Target Sum (reduce to subset sum)
* Coin Change (min # of coins)
* Coin Change II (count ways; combos vs permutations)
* Ones and Zeroes (2D knapsack)
* Last Stone Weight II (balance split)
* Shopping Offers (state compression by quantities)
* 
### 5. State Machine / Stock Problems

Problems best solved by defining discrete states (e.g., holding, empty, cooldown) and mapping the transitions between them.

* Best Time to Buy and Sell Stock
* Best Time to Buy and Sell Stock II
* Best Time to Buy and Sell Stock with Cooldown
* Best Time to Buy and Sell Stock with Transaction Fee
* Best Time to Buy and Sell Stock III
* Best Time to Buy and Sell Stock IV

### 6. Grid, Pathfinding & Matrix DP

2D DP problems where state transitions involve moving through a matrix, or calculating properties of sub-grids.

* Unique Paths
* Unique Paths II
* Minimum Path Sum
* Minimum Falling Path Sum
* Minimum Falling Path Sum II
* Dungeon Game
* Maximal Square
* Count Square Submatrices with All Ones
* Matrix Block Sum
* Maximal Rectangle (histogram technique)

### 7. String DP (LCS, Matching, Word Break)

Dynamic programming applied to strings, often involving two pointers iterating through two separate strings, or checking dictionary words.

* Longest Common Subsequence
* Edit Distance
* Regular Expression Matching
* Wildcard Matching
* Shortest Common Supersequence
* Minimum ASCII Delete Sum for Two Strings
* Word Break
* Word Break II
* Longest String Chain
* Distinct Subsequences
* Distinct Subsequences II
* String Compression II

### 8. Palindromic DP

String problems specifically focused on the properties of palindromes (expanding from centers or bounding via two pointers).

* Longest Palindromic Substring
* Count Palindromic Substrings — NEW
* Longest Palindromic Subsequence
* Minimum Insertion Steps to Make a String Palindrome
* Palindrome Partitioning I — NEW
* Palindrome Partitioning II
* Palindrome Partitioning III


### 9. Interval DP & Array Partitioning

Problems where you define a DP state based on a subarray range `[i, j]` and solve by testing all split points `k` between `i` and `j`.

* Matrix Chain Multiplication — NEW (classic interval template)
* Burst Balloons
* Minimum Score Triangulation of Polygon
* Minimum Cost Tree From Leaf Values
* Minimum Cost to Cut a Stick
* Partition Array for Maximum Sum (kept once)
* Allocate Mailboxes
* Filling Bookcase Shelves
* Remove Boxes

### 10. Counting, Combinatorics & Probability

Problems asking for "number of ways", probabilities, or expected values, often utilizing overlapping subproblems in permutations/combinations.

* Combination Sum IV
* Number of Dice Rolls With Target Sum
* Student Attendance Record I (LC551)
* Student Attendance Record II (LC552)
* Count Vowels Permutation
* Count Numbers with Unique Digits
* Soup Servings
* New 21 Game
* Knight Dialer
* K Inverse Pairs Array

### 11. Digit DP

Counting specific types of numbers in a range `[L, R]`. The state usually tracks the current digit index, whether the current prefix is tightly bound to the limit, and problem-specific constraints (e.g., parity, specific digits).

* Non‑negative Integers without Consecutive Ones
* Numbers At Most N Given Digit Set
* Numbers With Repeated Digits
* Number of Digit One

### 12. Bitmask DP & State Compression

Using integers as bitmasks to represent small sets of elements (usually $N \le 20$), allowing you to track which items have been used/visited.

* Smallest Sufficient Team
* Stickers to Spell Word
* Maximum Students Taking Exam
* Minimum Cost to Connect Two Groups of Points
* Shortest Path Visiting All Nodes
* Distribute Repeating Integers

### 13. Tree DP & Re-rooting

Applying DP on tree structures, usually traversing post-order (bottom-up) where a parent's state depends on its children's states.

* House Robber III
* Longest ZigZag Path in a Binary Tree
* Maximum Sum BST in Binary Tree
* Sum of Distances in Tree (re‑rooting DP)
* Minimize the Total Price of the Trips
* Maximum Points After Collecting Coins From All Nodes (kept once)
* Maximum Score After Applying Operations on a Tree

### 14. Game Theory & Minimax DP

Turn-based games where you must assume both players play optimally. You usually maximize your score while minimizing the opponent's.

* Predict the Winner
* Stone Game
* Stone Game VII
* Stone Game V

### 15. Advanced, Math & Miscellaneous DP

Problems that combine DP with advanced math, greedy optimizations, graphs, or tricky state definitions that don't neatly fit standard buckets.

* Super Egg Drop
* Get the Maximum Score
* Maximum Sum of 3 Non‑Overlapping Subarrays
* Super Washing Machines
* Reduce Dishes
* Freedom Trail
* Paint House III

### 16. DP on DAGs

* Longest Increasing Path in a Matrix (The Implicit Matrix DAG)
* Longest String Chain (The Implicit Array DAG)
* All Paths From Source to Target (The Traversal Baseline)
* Number of Restricted Paths From First to Last Node (Dijkstra + DP Combo)
* Parallel Courses III (Scheduling and Max Time DP)
---
