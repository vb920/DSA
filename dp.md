---

### 1. 1D DP & Basic State Transitions

These problems require looking back at 1 or 2 previous states to determine the current state.

* Climbing Stairs
* Min Cost Climbing Stairs
* House Robber
* 2 Keys Keyboard

### 2. Subarrays & Subsequences

Problems focused on contiguous (subarray) or non-contiguous (subsequence) elements, often requiring you to track ongoing sums, products, or differences.

* Maximum Subarray
* Maximum Product Subarray
* Maximum Subarray Sum with One Deletion
* Wiggle Subsequence
* Longest Turbulent Subarray
* K‑Concatenation Maximum Sum
* Constrained Subsequence Sum — NEW (DP + deque optimization)
* Arithmetic Slices
* Longest Arithmetic Subsequence
* Longest Arithmetic Subsequence of Given Difference
* Find the Maximum Length of a Good Subsequence II
* Find the Count of Monotonic Pairs I
* Find the Count of Monotonic Pairs II
* Longest Unequal Adjacent Groups Subsequence II
* Find the Maximum Length of Valid Subsequence II
* Minimum Swaps To Make Sequences Increasing
* Maximize Total Cost of Alternating Subarrays

### 3. Longest Increasing Subsequence (LIS) Variants

A specific subset of subsequence problems relying on the classic LIS pattern (often optimized from $O(n^2)$ to $O(n \log n)$ via binary search/patience sorting).

* Longest Increasing Subsequence (patience sorting)
* Number of Longest Increasing Subsequence
* Largest Divisible Subset
* Russian Doll Envelopes
* Maximum Length of Pair Chain
* Make Array Strictly Increasing

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
* Minimum Number of Coins for Fruits
* Count of Sub‑Multisets With Bounded Sum
* Profitable Schemes

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
* Out of Boundary Paths
* Maximum Number of Moves in a Grid (DAG DP)
* Where Will the Ball Fall
* Minimum Falling Path Sum
* Minimum Falling Path Sum II
* Maximum Non Negative Product in a Matrix
* Dungeon Game
* Maximal Square
* Count Square Submatrices with All Ones
* Largest 1‑Bordered Square
* Largest Plus Sign
* Matrix Block Sum
* Maximal Rectangle (histogram technique)
* Max Sum of Rectangle No Larger Than K (row compression + ordered set)
* Number of Submatrices That Sum to Target (row compression + hash)

### 7. String DP (LCS, Matching, Word Break)

Dynamic programming applied to strings, often involving two pointers iterating through two separate strings, or checking dictionary words.

* Longest Common Subsequence
* Delete Operation for Two Strings
* Edit Distance
* Interleaving String
* Regular Expression Matching
* Wildcard Matching
* Shortest Common Supersequence
* Max Dot Product of Two Subsequences
* Apply Operations to Make Two Strings Equal
* Minimum ASCII Delete Sum for Two Strings
* Word Break
* Word Break II
* Unique Substrings in Wraparound String
* Longest String Chain
* Concatenated Words
* Distinct Subsequences
* Distinct Subsequences II
* String Compression II
* Number of Ways to Form a Target String Given a Dictionary

### 8. Palindromic DP

String problems specifically focused on the properties of palindromes (expanding from centers or bounding via two pointers).

* Longest Palindromic Substring
* Count Palindromic Substrings — NEW
* Longest Palindromic Subsequence
* Minimum Insertion Steps to Make a String Palindrome
* Palindrome Partitioning I — NEW
* Palindrome Partitioning II
* Palindrome Partitioning III
* Longest Chunked Palindrome Decomposition
* Minimum Changes to Make K Semi‑palindromes

### 9. Interval DP & Array Partitioning

Problems where you define a DP state based on a subarray range `[i, j]` and solve by testing all split points `k` between `i` and `j`.

* Matrix Chain Multiplication — NEW (classic interval template)
* Burst Balloons
* Minimum Score Triangulation of Polygon
* Minimum Cost Tree From Leaf Values
* Minimum Cost to Merge Stones
* Minimum Cost to Cut a Stick
* Number of Ways of Cutting a Pizza
* Min Cost to Split Array — NEW (D&C optimization exemplar)
* Partition Array for Maximum Sum (kept once)
* Allocate Mailboxes
* Video Stitching
* Filling Bookcase Shelves
* Build Array Where You Can Find The Maximum Exactly K Comparisons
* Remove Boxes
* Strange Printer

### 10. Counting, Combinatorics & Probability

Problems asking for "number of ways", probabilities, or expected values, often utilizing overlapping subproblems in permutations/combinations.

* Combination Sum IV
* Number of Dice Rolls With Target Sum
* Dice Roll Simulation
* Student Attendance Record I (LC551)
* Student Attendance Record II (LC552)
* Number of Music Playlists
* Count Vowels Permutation
* Kth Smallest Instructions
* Count Numbers with Unique Digits
* Count Sorted Vowel Strings
* Soup Servings
* New 21 Game
* Champagne Tower
* Knight Dialer
* Probability of a Two Boxes Having the Same Number of Distinct Balls
* K Inverse Pairs Array

### 11. Digit DP

Counting specific types of numbers in a range `[L, R]`. The state usually tracks the current digit index, whether the current prefix is tightly bound to the limit, and problem-specific constraints (e.g., parity, specific digits).

* Non‑negative Integers without Consecutive Ones
* Numbers At Most N Given Digit Set
* Numbers With Repeated Digits
* Number of Digit One
* Number of Beautiful Integers in the Range
* Count the Number of Powerful Integers
* Find All Good Strings (Digit DP + KMP/Aho-Corasick)

### 12. Bitmask DP & State Compression

Using integers as bitmasks to represent small sets of elements (usually $N \le 20$), allowing you to track which items have been used/visited.

* Smallest Sufficient Team
* Stickers to Spell Word
* Maximum Students Taking Exam
* Number of Ways to Wear Different Hats to Each Other
* Minimum Cost to Connect Two Groups of Points
* Find Minimum Time to Finish All Jobs
* Shortest Path Visiting All Nodes
* Distribute Repeating Integers
* Maximum Number of Achievable Transfer Requests
* Maximize Grid Happiness

### 13. Tree DP & Re-rooting

Applying DP on tree structures, usually traversing post-order (bottom-up) where a parent's state depends on its children's states.

* House Robber III
* Longest ZigZag Path in a Binary Tree
* Maximum Sum BST in Binary Tree
* Number of Ways to Reorder Array to Get Same BST
* Sum of Distances in Tree (re‑rooting DP)
* Count Paths That Can Form a Palindrome in a Tree (bit parity on paths)
* Find Number of Coins to Place in Tree Nodes
* Minimize the Total Price of the Trips
* Time Taken to Mark All Nodes
* Maximum Points After Collecting Coins From All Nodes (kept once)
* Maximum Score After Applying Operations on a Tree

### 14. Game Theory & Minimax DP

Turn-based games where you must assume both players play optimally. You usually maximize your score while minimizing the opponent's.

* Predict the Winner
* Stone Game
* Stone Game VII
* Stone Game V
* Can I Win

### 15. Advanced, Math & Miscellaneous DP

Problems that combine DP with advanced math, greedy optimizations, graphs, or tricky state definitions that don't neatly fit standard buckets.

* Super Egg Drop
* Race Car
* Least Operators to Express Number
* Largest Multiple of Three
* Get the Maximum Score
* Maximum Sum of 3 Non‑Overlapping Subarrays
* Super Washing Machines
* Reduce Dishes
* Pizza With 3n Slices
* Freedom Trail
* Paint House III
* Minimum Sum of Values by Dividing Array

---
