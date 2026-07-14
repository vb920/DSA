Below is the normalized linear solving order. Duplicate appearances are treated as one problem, compound entries are split, and each problem receives one primary pattern.

Because the source contains several hundred distinct entries, I’m presenting the roadmap in continuous numbered parts. Part 1 establishes Arrays/Strings → Matrix Mechanics → Hashing → Prefix Sums → Two Pointers → Sliding Window.

Master DSA Roadmap — Part 1
Array, String, and Matrix Mechanics

1 - Convert 1D Array Into 2D Array - Array / Index Mapping
 2 - Richest Customer Wealth - Matrix / Row Traversal
 3 - Matrix Diagonal Sum - Matrix / Diagonal Traversal
 4 - Check if Matrix is X-Matrix - Matrix / Positional Validation
 5 - Prime in Diagonal - Matrix / Diagonal Traversal
 6 - Difference Between Ones and Zeros in Row and Column - Matrix / Row and Column Counting
 7 - Lucky Numbers in a Matrix - Matrix / Row Minimum and Column Maximum
 8 - Row With Maximum Ones - Matrix / Row Scanning
 9 - Largest Local Values in a Matrix - Matrix / Fixed 2D Window
 10 - Maximum Sum of an Hourglass - Matrix / Fixed Pattern Traversal
 11 - Make a Square with the Same Color - Matrix / Local Enumeration
 12 - Transpose Matrix - Matrix / Coordinate Transformation
 13 - Shift 2D Grid - Matrix / Modular Index Mapping
 14 - Matrix Similarity After Cyclic Shifts - Matrix / Cyclic Indexing
 15 - Spiral Matrix - Matrix / Boundary Traversal
 16 - Spiral Matrix II - Matrix / Boundary Construction
 17 - Diagonal Traverse - Matrix / Direction Simulation
 18 - Sort the Matrix Diagonally - Matrix / Diagonal Grouping
 19 - Rotate Image - Matrix / Transpose and Reverse
 20 - Cyclically Rotating a Grid - Matrix / Ring Traversal
 21 - Rotating the Box - Matrix / Simulation and Rotation
 22 - Set Matrix Zeroes - Matrix / In-Place Markers
 23 - Game of Life - Matrix / In-Place State Encoding
 24 - Where Will the Ball Fall - Matrix / Path Simulation
 25 - Check if Move is Legal - Matrix / Directional Scanning
 26 - Queens That Can Attack the King - Matrix / Ray Traversal
 27 - Max Increase to Keep City Skyline - Matrix / Row and Column Constraints
 28 - Find Valid Matrix Given Row and Column Sums - Matrix / Greedy Construction
 29 - Valid Tic-Tac-Toe State - Matrix / State Validation
 30 - Valid Sudoku - Matrix / Row-Column-Box Constraints
 31 - Find the Minimum Area to Cover All Ones I - Matrix / Bounding Rectangle
 32 - Find the Minimum Area to Cover All Ones II - Matrix / Partitioned Bounding Rectangles
 33 - Subrectangle Queries - Matrix / Mutable Region Simulation
 34 - Image Overlap - Matrix / Translation and Counting
 35 - Matrix Cells in Distance Order - Matrix / Manhattan Distance Ordering
 36 - Minimum Operations to Make a Uni-Value Grid - Matrix / Median and Modular Feasibility
 37 - Number of Laser Beams in a Bank - Matrix / Nonempty Row Counting

Fundamental Hashing and Frequency Counting

38 - Contains Duplicate - Hashing / Set Membership
 39 - Find Common Elements Between Two Arrays - Hashing / Multiset Intersection
 40 - Number of Good Pairs - Hashing / Frequency Counting
 41 - Valid Anagram - Hashing / Character Frequency
 42 - Unique Number of Occurrences - Hashing / Frequency-of-Frequencies
 43 - Find Common Characters - Hashing / Minimum Frequency Intersection
 44 - Find Words That Can Be Formed by Characters - Hashing / Supply and Demand
 45 - Redistribute Characters to Make All Strings Equal - Hashing / Global Frequency Divisibility
 46 - Word Pattern - Hashing / Bijection
 47 - Isomorphic Strings - Hashing / Bidirectional Mapping
 48 - Evaluate the Bracket Pairs of a String - Hashing / Key-Value Substitution
 49 - Bulls and Cows - Hashing / Positional and Multiset Matching
 50 - Alphabet Board Path - Hashing / Character-to-Coordinate Mapping
 51 - Finding the Users Active Minutes - Hashing / Map of Sets
 52 - Group Anagrams - Hashing / Canonical Frequency Signature
 53 - Sort Characters by Frequency - Hashing / Frequency Ordering
 54 - Sort Array by Increasing Frequency - Hashing / Frequency with Tie-Breaking
 55 - Custom Sort String - Hashing / Custom Rank Mapping
 56 - Vowel Spellchecker - Hashing / Layered Canonicalization
 57 - Reconstruct Original Digits from English - Hashing / Distinguishing Frequencies
 58 - Word Subsets - Hashing / Maximum Required Frequency Signature
 59 - Two Sum - Hashing / Complement Lookup
 60 - Pairs of Songs With Total Durations Divisible by 60 - Hashing / Complementary Residues
 61 - Count Pairs That Form a Complete Day II - Hashing / Complementary Residues
 62 - Check if Array Pairs Are Divisible by K - Hashing / Residue Pairing
 63 - Count Number of Bad Pairs - Hashing / Transformed-Key Counting
 64 - Tuple with Same Product - Hashing / Pair Product Counting
 65 - 4Sum II - Hashing / Pair-Sum Decomposition
 66 - Longest Consecutive Sequence - Hashing / Sequence-Start Detection
 67 - Optimal Partition of String - Hashing / Greedy Seen Set
 68 - Insert Delete GetRandom O(1) - Hashing / Array and Index Map
 69 - RandomizedSet with Duplicates - Hashing / Array and Index Sets
 70 - Maximum Equal Frequency - Hashing / Counts of Counts
 71 - Grid Illumination - Hashing / Multi-Dimensional Counters

Prefix Sums, Difference Arrays, and Prefix-State Hashing

72 - Range Sum Query - Immutable - Prefix Sum / Basic Range Query
 73 - Static Range Sum Queries - Prefix Sum / Basic Range Query
 74 - Left and Right Sum Differences - Prefix Sum / Left-Right Aggregation
 75 - Count Vowel Strings in Ranges - Prefix Sum / Boolean Frequency Prefix
 76 - Minimum Penalty for a Shop - Prefix Sum / Split Evaluation
 77 - Product of Array Except Self - Prefix-Suffix Products / Exclusion Aggregation
 78 - Sum of Absolute Differences in a Sorted Array - Prefix Sum / Distance Contribution
 79 - Removing Minimum Number of Magic Beans - Prefix Sum / Sorted Cost Evaluation
 80 - Find Good Days to Rob the Bank - Prefix-Suffix / Monotonic Runs
 81 - Find All Good Indices - Prefix-Suffix / Monotonic Runs
 82 - Movement of Robots - Prefix Sum / Sorted Pairwise Distance
 83 - Power of Heroes - Prefix Sum / Contribution Counting
 84 - Minimum Cost to Make Array Equal - Prefix Sum / Weighted Median Cost
 85 - Minimum Operations to Make All Array Elements Equal - Prefix Sum / Sorted Query Costs
 86 - Range Sum Query 2D - Immutable - 2D Prefix Sum / Rectangle Query
 87 - Matrix Block Sum - 2D Prefix Sum / Fixed-Radius Rectangle
 88 - Forest Queries - 2D Prefix Sum / Rectangle Counting
 89 - Increment Submatrices by One - 2D Difference Array / Rectangle Updates
 90 - Range Add Queries 2D - 2D Difference Array / Rectangle Updates
 91 - Car Pooling - Difference Array / Line Sweep
 92 - Product of the Last K Numbers - Prefix Product / Stream Query
 93 - Subarray Sum Equals K - Prefix Sum and Hashing / Equal-State Counting
 94 - Binary Subarrays with Sum - Prefix Sum and Hashing / Fixed Target
 95 - Count Number of Nice Subarrays - Prefix Sum and Hashing / Odd-Count Transformation
 96 - Subarray Sums Divisible by K - Prefix Modulo / Equal Remainders
 97 - Continuous Subarray Sum - Prefix Modulo / Equal Remainders with Length Constraint
 98 - Make Sum Divisible by P - Prefix Modulo / Minimum Removal
 99 - Count of Interesting Subarrays - Prefix Modulo / Transformed Sequence
 100 - Count the Number of Beautiful Subarrays - Prefix XOR / Equal-State Counting
 101 - XOR Queries of a Subarray - Prefix XOR / Range Query
 102 - Number of Wonderful Substrings - Prefix Bitmask / Parity States
 103 - Find Longest Awesome Substring - Prefix Bitmask / At-Most-One-Odd State
 104 - Path Sum III - Tree Prefix Sum / Ancestor-State Counting
 105 - Number of Submatrices That Sum to Target - 2D Compression / Prefix Hashing
 106 - Submatrix Sum Equals K - 2D Compression / Prefix Hashing
 107 - Max Sum of Rectangle No Larger Than K - 2D Compression / Ordered Prefix Set

Two-Pointer Foundations

108 - Reverse String - Two Pointers / Symmetric Swapping
 109 - Reverse Prefix of Word - Two Pointers / Prefix Reversal
 110 - Reverse Vowels of a String - Two Pointers / Conditional Swapping
 111 - Merge Strings Alternately - Two Pointers / Parallel Traversal
 112 - Reverse Words in a String III - String / Per-Word Reversal
 113 - Reverse Words in a String - Two Pointers / Compaction and Reversal
 114 - Sort Array by Parity - Two Pointers / Partitioning
 115 - Sort Array by Parity II - Two Pointers / Parity Placement
 116 - Rearrange Array Elements by Sign - Two Pointers / Alternating Placement
 117 - Remove Element - Two Pointers / In-Place Filtering
 118 - Remove Duplicates from Sorted Array - Two Pointers / Slow-Fast Compaction
 119 - Apply Operations to an Array - Two Pointers / Transform and Compact
 120 - Partition Array According to Given Pivot - Two Pointers / Three-Way Partition
 121 - Sort Colors - Two Pointers / Dutch National Flag
 122 - Merge Sorted Array - Two Pointers / Reverse Merge
 123 - Merge Two 2D Arrays by Summing Values - Two Pointers / Sorted Merge
 124 - Minimum Common Value - Two Pointers / Sorted Intersection
 125 - Find All K-Distant Indices in an Array - Two Pointers / Interval Expansion
 126 - Shortest Distance to a Character - Two Passes / Nearest Occurrence
 127 - DI String Match - Two Pointers / Extremal Selection
 128 - Separate Black and White Balls - Two Pointers / Movement Counting
 129 - Move Pieces to Obtain a String - Two Pointers / Order-Preserving Matching
 130 - Make String a Subsequence Using Cyclic Increments - Two Pointers / Subsequence Matching
 131 - Sentence Similarity III - Two Pointers / Prefix-Suffix Matching
 132 - Valid Palindrome - Two Pointers / Symmetric Validation
 133 - Valid Palindrome II - Two Pointers / One-Deletion Branch
 134 - Lexicographically Smallest Palindrome - Two Pointers / Greedy Symmetric Replacement
 135 - Minimum Length of String After Deleting Similar Ends - Two Pointers / Boundary Shrinking
 136 - Count Binary Substrings - Two Pointers / Adjacent Run Lengths
 137 - String Compression - Two Pointers / Run-Length Encoding
 138 - Rotate Array - Array / Reversal Technique
 139 - Next Permutation - Two Pointers / Lexicographic Successor
 140 - Next Greater Element III - Two Pointers / Digit Permutation
 141 - Container With Most Water - Two Pointers / Dominated Boundary Elimination
 142 - Watering Plants II - Two Pointers / Bidirectional Simulation

Sorting, Pair Search, and Multi-Pointer Expansion

143 - Assign Cookies - Greedy / Sorted Two Pointers
 144 - Maximum Matching of Players with Trainers - Greedy / Sorted Matching
 145 - Boats to Save People - Greedy / Opposite-End Two Pointers
 146 - Bag of Tokens - Greedy / Opposite-End Trade-Off
 147 - Advantage Shuffle - Greedy / Sorted Matching
 148 - Check If a String Can Break Another String - Greedy / Sorted Dominance
 149 - Largest Merge of Two Strings - Greedy / Lexicographic Suffix Comparison
 150 - Two Sum II - Two Pointers / Sorted Pair Sum
 151 - 3Sum - Two Pointers / Sort and Fix One
 152 - 3Sum Closest - Two Pointers / Closest Pair Around Fixed Element
 153 - 4Sum - Two Pointers / Sort and Fix Two
 154 - K Smallest Pairs - Heap and Two Pointers / Sorted Pair Frontier
 155 - Find K Pairs with Smallest Sums - Heap and Two Pointers / Sorted Pair Frontier
 156 - Find K-th Smallest Pair Distance - Binary Search and Two Pointers / Pair Counting

Fixed-Size Sliding Windows

157 - Substrings of Size Three with Distinct Characters - Sliding Window / Fixed-Size Distinctness
 158 - Maximum Number of Vowels in a Substring of Given Length - Sliding Window / Fixed-Size Counting
 159 - Maximum Average Subarray I - Sliding Window / Fixed-Size Sum
 160 - Number of Sub-arrays of Size K and Average Greater Than or Equal to Threshold - Sliding Window / Fixed-Size Sum
 161 - K Radius Subarray Averages - Sliding Window / Centered Fixed Window
 162 - Check If a String Contains All Binary Codes of Size K - Sliding Window / Fixed-Length Encoding
 163 - Find All Anagrams in a String - Sliding Window / Fixed Frequency Match
 164 - Permutation in String - Sliding Window / Fixed Frequency Match
 165 - Maximum Sum of Distinct Subarrays With Length K - Sliding Window / Fixed-Size Distinct Sum
 166 - Sliding Subarray Beauty - Sliding Window / Ordered Frequency Structure
 167 - Maximum Points You Can Obtain from Cards - Sliding Window / Complement Window
 168 - Grumpy Bookstore Owner - Sliding Window / Maximum Recoverable Contribution
 169 - Maximum Number of Occurrences of a Substring - Sliding Window / Minimum-Length Candidate
 170 - Maximum Sum of 3 Non-Overlapping Subarrays - Sliding Window / Window DP and Reconstruction

Variable-Size Sliding Windows

171 - Minimum Size Subarray Sum - Sliding Window / Positive-Sum Shrinking
 172 - Subarray Product Less Than K - Sliding Window / Multiplicative Shrinking
 173 - Frequency of the Most Frequent Element - Sliding Window / Sorted Equalization Cost
 174 - Fruit Into Baskets - Sliding Window / At Most Two Distinct
 175 - Longest Substring Without Repeating Characters - Sliding Window / Unique Characters
 176 - Optimal Partition of String - Greedy Window / No Repeated Characters
 177 - Longest Repeating Character Replacement - Sliding Window / Replaceable Deficit
 178 - Max Consecutive Ones III - Sliding Window / At Most K Violations
 179 - Longest Subarray of 1's After Deleting One Element - Sliding Window / At Most One Zero
 180 - Maximum Erasure Value - Sliding Window / Unique-Element Sum
 181 - Minimum Consecutive Cards to Pick Up - Sliding Window / Duplicate Endpoints
 182 - Count the Number of Good Subarrays - Sliding Window / At Least K Equal Pairs
 183 - Count the Number of Substrings With Dominant Ones - Sliding Window / Frequency Constraint
 184 - Minimum Operations to Reduce X to Zero - Sliding Window / Longest Complement Subarray
 185 - Number of Subarrays with Bounded Maximum - Sliding Window / Boundary Contribution
 186 - Count Number of Nice Subarrays - Sliding Window / Exactly K via At-Most Difference
 187 - Binary Subarrays with Sum - Sliding Window / Exactly K via At-Most Difference
 188 - Subarrays with K Different Integers - Sliding Window / Exactly K Distinct
 189 - Minimum Window Substring - Sliding Window / Required Frequency Deficit
 190 - Substring with Concatenation of All Words - Sliding Window / Token-Aligned Frequencies
 191 - Longest Nice Subarray - Sliding Window / Disjoint Bitmask
 192 - Maximum White Tiles Covered by a Carpet - Sliding Window / Sorted Interval Coverage

Monotonic Sliding-Window Structures

193 - Sliding Window Maximum - Monotonic Deque / Window Maximum
 194 - Longest Continuous Subarray With Absolute Diff Less Than or Equal to Limit - Dual Monotonic Deques
 195 - Continuous Subarrays - Dual Monotonic Deques / Bounded Range
 196 - Maximum Number of Robots Within Budget - Sliding Window and Deque / Maximum Plus Running Sum
 197 - Max Value of Equation - Monotonic Deque / Transformed Maximum
 198 - Shortest Subarray with Sum at Least K - Prefix Sum and Monotonic Deque
 199 - Jump Game VI - Dynamic Programming and Monotonic Deque
 200 - Constrained Subsequence Sum - Dynamic Programming and Monotonic Deque
 201 - Sliding Window Median - Sliding Window / Dual Heaps
 202 - Moving Stones Until Consecutive II - Sliding Window / Sorted Occupancy
 203 - Find the Median of the Uniqueness Array - Binary Search and Sliding Window / At-Most Distinct Count

Binary Search
Exact Search and Boundary Templates

204 - Binary Search - Binary Search / Exact Match Template
 205 - Guess Number Higher or Lower - Binary Search / Monotonic Comparison
 206 - Search Insert Position - Binary Search / Lower Bound
 207 - First Bad Version - Binary Search / First True Predicate
 208 - Find First and Last Position of Element in Sorted Array - Binary Search / Leftmost and Rightmost Bounds
 209 - Find Smallest Letter Greater Than Target - Binary Search / Upper Bound with Wraparound
 210 - Find Target Indices After Sorting Array - Binary Search / Duplicate Boundaries
 211 - H-Index II - Binary Search / Boundary in Sorted Array
 212 - Arranging Coins - Binary Search / Monotonic Arithmetic Predicate
 213 - Sqrt(x) - Binary Search / Integer Answer Boundary
 214 - Kth Missing Positive Number - Binary Search / Missing-Count Function
 215 - Longest Subsequence With Limited Sum - Prefix Sum and Binary Search / Upper Bound
 216 - Search in a Sorted Array of Unknown Size - Binary Search / Exponential Range Expansion

Binary Search as a Sorted Lookup Tool

217 - Find the Distance Value Between Two Arrays - Binary Search / Nearest Sorted Value
 218 - Minimum Absolute Sum Difference - Binary Search / Nearest Replacement
 219 - Heaters - Binary Search / Nearest Facility
 220 - Successful Pairs of Spells and Potions - Binary Search / Threshold Lookup
 221 - Find K Closest Elements - Binary Search / Optimal Window Boundary
 222 - Find Right Interval - Binary Search / Next Valid Start
 223 - Most Beautiful Item for Each Query - Prefix Maximum and Binary Search / Offline Queries
 224 - Plates Between Candles - Prefix Sum and Binary Search / Nearest Boundaries
 225 - Range Frequency Queries - Binary Search / Position Lists
 226 - Online Election - Prefix Leaders and Binary Search / Historical Query
 227 - Time Based Key-Value Store - Binary Search / Timestamp Floor
 228 - Random Pick with Weight - Prefix Sum and Binary Search / Weighted Selection

Structural Binary Search

229 - Single Element in a Sorted Array - Binary Search / Pair-Index Invariant
 230 - Find Peak Element - Binary Search / Slope Direction
 231 - Peak Index in a Mountain Array - Binary Search / Unimodal Peak
 232 - Find in Mountain Array - Binary Search / Peak and Two Monotonic Halves
 233 - Search a 2D Matrix - Binary Search / Flattened Coordinates
 234 - Count Negative Numbers in a Sorted Matrix - Binary Search / Per-Row Boundary
 235 - Search a 2D Matrix II - Matrix Search / Monotonic Elimination
 236 - Find a Peak Element II - Binary Search / 2D Directional Peak

Rotated Sorted Arrays

237 - Find Minimum in Rotated Sorted Array - Binary Search / Rotation Boundary
 238 - Search in Rotated Sorted Array - Binary Search / Choosing the Sorted Half
 239 - Find Minimum in Rotated Sorted Array II - Binary Search / Rotation with Duplicates
 240 - Search in Rotated Sorted Array II - Binary Search / Duplicate-Aware Rotation

Binary Search on the Answer: Minimum Feasible Value

241 - Koko Eating Bananas - Answer Search / Minimum Feasible Rate
 242 - Capacity to Ship Packages Within D Days - Answer Search / Minimum Feasible Capacity
 243 - Find the Smallest Divisor Given a Threshold - Answer Search / Minimum Feasible Divisor
 244 - Minimum Number of Days to Make M Bouquets - Answer Search / Minimum Feasible Day
 245 - Minimum Speed to Arrive on Time - Answer Search / Minimum Feasible Speed
 246 - Minimum Time to Repair Cars - Answer Search / Minimum Feasible Time
 247 - Minimum Limit of Balls in a Bag - Answer Search / Minimum Feasible Penalty
 248 - Minimized Maximum of Products Distributed to Any Store - Answer Search / Minimum Feasible Allocation
 249 - Minimize the Maximum Difference of Pairs - Answer Search / Minimum Feasible Pair Difference
 250 - Split Array Largest Sum - Answer Search / Minimum Feasible Largest Partition
 251 - Maximum Value at a Given Index in a Bounded Array - Answer Search / Minimum Required Sum
 252 - Maximum Side Length of a Square With Sum at Most Threshold - 2D Prefix Sum and Binary Search / Maximum Feasible Side
 253 - Maximum Number of Removable Characters - Binary Search / Maximum Feasible Removals
 254 - Maximum Number of Tasks You Can Assign - Binary Search and Greedy / Maximum Feasible Assignments
 255 - Earliest Second to Mark Indices I - Answer Search / Prefix Feasibility

Binary Search on the Answer: Maximum Feasible Value

256 - Cutting Ribbons - Answer Search / Maximum Feasible Piece Length
 257 - Maximum Candies Allocated to K Children - Answer Search / Maximum Feasible Share
 258 - Magnetic Force Between Two Balls - Answer Search / Maximum Minimum Distance
 259 - Maximum Tastiness of Candy Basket - Answer Search / Maximum Minimum Difference
 260 - Maximum Running Time of N Computers - Answer Search / Maximum Feasible Runtime
 261 - Maximize the Minimum Powered City - Answer Search / Maximum Feasible Minimum Power
 262 - Minimize the Maximum Distance to Gas Station - Floating-Point Binary Search / Precision

Counting Values at or Below a Candidate

263 - Kth Smallest Number in Multiplication Table - Value Binary Search / Counting Values at Most Mid
 264 - Find K-th Smallest Pair Distance - Value Binary Search / Two-Pointer Pair Counting
 265 - Kth Smallest Element in a Sorted Matrix - Value Binary Search / Matrix Rank Counting
 266 - Kth Smallest Product of Two Sorted Arrays - Value Binary Search / Sign-Aware Product Counting
 267 - Find the Kth Smallest Sum of a Matrix With Sorted Rows - Value Search / Counting Sum Combinations
 268 - Kth Smallest Amount With Single Denomination Combination - Value Search / Inclusion-Exclusion Counting
 269 - Preimage Size of Factorial Zeroes Function - Binary Search / Inverting a Monotonic Count
 270 - Find Duplicate Number - Value Binary Search / Pigeonhole Counting
 271 - Find the Median of the Uniqueness Array - Binary Search and Sliding Window / Subarray Count Predicate
 272 - Maximum Average Subarray II - Floating-Point Binary Search / Prefix-Sum Feasibility

Intervals
Interval Representation and Basic Manipulation

273 - Missing Ranges - Intervals / Detecting Gaps
 274 - Remove Interval - Intervals / Subtracting One Range
 275 - Add Bold Tag in String - Intervals / Mark, Merge, and Render
 276 - Merge Intervals - Intervals / Sort and Consolidate
 277 - Insert Interval - Intervals / Insert into Merged Ranges
 278 - Interval List Intersections - Intervals / Two-Pointer Intersection
 279 - Remove Covered Intervals - Intervals / Dominance after Sorting

Meeting and Occupancy Intervals

280 - Meeting Rooms - Intervals / Overlap Detection
 281 - Meeting Rooms II - Intervals and Heap / Maximum Concurrent Meetings
 282 - Divide Intervals Into Minimum Number of Groups - Intervals and Heap / Resource Allocation
 283 - The Number of the Smallest Unoccupied Chair - Intervals and Heaps / Resource Reuse
 284 - Meeting Rooms III - Intervals and Heaps / Delayed Resource Scheduling
 285 - Count Days Without Meetings - Intervals / Merge and Measure Complement

Interval Scheduling and Coverage

286 - Non-Overlapping Intervals - Greedy Intervals / Earliest Finishing Time
 287 - Minimum Number of Arrows to Burst Balloons - Greedy Intervals / Point Stabbing
 288 - Video Stitching - Greedy Intervals / Farthest-Reach Coverage
 289 - Minimum Interval to Include Each Query - Offline Intervals and Heap / Smallest Active Interval
 290 - Number of Flowers in Full Bloom - Intervals / Sweep-Line Event Counting
 291 - Maximum Number of Non-Overlapping Substrings - Greedy Intervals / Minimal Valid Character Ranges
 292 - Check if Grid Can Be Cut into Sections - Intervals / Projection and Separation

Dynamic Interval Structures

293 - My Calendar I - Ordered Intervals / Rejecting Overlaps
 294 - My Calendar II - Sweep Line / Preventing Triple Booking
 295 - My Calendar III - Sweep Line / Maximum Concurrent Bookings
 296 - Data Stream as Disjoint Intervals - Ordered Intervals / Online Merging
 297 - Range Module - Ordered Intervals / Add, Remove, and Query Coverage

Greedy
Direct Local Choices and Resource Invariants

298 - Lemonade Change - Greedy / Change-Making Invariant
 299 - Minimum Rounds to Complete All Tasks - Greedy Counting / Groups of Two and Three
 300 - Maximum Bags With Full Capacity of Rocks - Greedy / Smallest Deficit First
 301 - Construct K Palindrome Strings - Greedy / Odd-Frequency Feasibility
 302 - Partition Labels - Greedy / Last-Occurrence Boundary
 303 - Largest Multiple of Three - Greedy / Remainder Correction
 304 - Mice and Cheese - Greedy / Largest Reward Deltas
 305 - Most Profit Assigning Work - Greedy / Sorted Capability Sweep
 306 - Previous Permutation With One Swap - Greedy / Largest Smaller Suffix Choice

Reachability and Coverage Invariants

307 - Jump Game - Greedy / Farthest Reachable Position
 308 - Jump Game II - Greedy / Layered Farthest Reach
 309 - Gas Station - Greedy / Prefix-Deficit Restart
 310 - Patching Array - Greedy / Continuous Coverage Invariant
 311 - Minimize Maximum of Array - Greedy and Prefix Sum / Prefix-Average Bound

Ordering and Constructive Greedy

312 - Queue Reconstruction by Height - Greedy / Sort and Indexed Insertion
 313 - Candy - Greedy / Two-Directional Constraints
 314 - Divide Array in Sets of K Consecutive Numbers - Ordered Greedy / Consume from Minimum
 315 - Super Washing Machines - Greedy / Prefix Load Imbalance
 316 - Reduce Dishes - Greedy / Suffix Contribution
 317 - Get the Maximum Score - Greedy and Two Pointers / Switching at Common Values

Scheduling with Heaps

318 - Task Scheduler - Greedy / Frequency-Based Cooldown Scheduling
 319 - Reorganize String - Greedy and Heap / Separate Equal Characters
 320 - Rearrange String K Distance Apart - Greedy and Heap / Cooldown Scheduling
 321 - Longest Happy String - Greedy and Heap / Avoiding Three Consecutive Characters
 322 - Course Schedule III - Greedy and Heap / Deadline Scheduling
 323 - IPO - Greedy and Heap / Capital-Constrained Selection

Advanced Greedy Transformations

324 - Remove Duplicate Letters - Greedy and Monotonic Stack / Lexicographically Minimal Unique Sequence
 325 - Smallest Subsequence of Distinct Characters - Greedy and Monotonic Stack / Canonical Unique Subsequence
 326 - Minimum Operations to Form Subsequence With Target Sum - Greedy Bit Manipulation / Splitting Powers of Two
 327 - Check If a String Can Break Another String - Greedy / Sorted Positional Dominance
 328 - Special Binary String - Recursive Greedy / Canonical Component Ordering

Linked Lists
Basic Traversal and Pointer Mechanics

329 - Convert Binary Number in a Linked List to Integer - Linked List / Forward Traversal
 330 - Design Linked List - Linked List / Node Reads, Writes, and Indexing
 331 - Middle of the Linked List - Linked List / Slow and Fast Pointers
 332 - Linked List Random Node - Linked List / Reservoir Sampling
 333 - Intersection of Two Linked Lists - Linked List / Pointer Switching

Cycle Detection

334 - Linked List Cycle - Linked List / Floyd Cycle Detection
 335 - Linked List Cycle II - Linked List / Cycle Entry Derivation

Reversal and Structural Rewiring

336 - Reverse Linked List - Linked List / Iterative Pointer Reversal
 337 - Palindrome Linked List - Linked List / Find Middle, Reverse, and Compare
 338 - Odd Even Linked List - Linked List / Stable Pointer Partition
 339 - Reverse Nodes in K-Group - Linked List / Segment Reversal

Deletion and Local Mutation

340 - Remove Duplicates from Sorted List - Linked List / Adjacent Deduplication
 341 - Remove Nth Node From End of List - Linked List / Fixed Pointer Gap
 342 - Delete the Middle Node of a Linked List - Linked List / Slow-Fast Deletion

Arithmetic, Merging, and Sorting

343 - Add Two Numbers - Linked List / Digit Simulation with Carry
 344 - Merge Two Sorted Lists - Linked List / Sorted Pointer Merge
 345 - Sort List - Linked List / Merge Sort
 346 - Merge K Sorted Lists - Linked List and Heap / Multiway Merge

Lists with Additional Relationships

347 - Copy List with Random Pointer - Linked List and Hashing / Graph-Like Copy
 348 - Convert Sorted List to Binary Search Tree - Linked List and Tree / Middle-Node Decomposition

Doubly Linked Lists and Stateful Design

349 - Design Browser History - Doubly Linked List / Bidirectional Navigation
 350 - LRU Cache - Hash Map and Doubly Linked List / Recency Eviction
 351 - All O(1) Data Structure - Hash Map and Bucketed Doubly Linked List / Frequency Updates
 352 - LFU Cache - Hash Maps and Frequency Lists / Frequency-Then-Recency Eviction
 353 - Max Stack - Stack, Doubly Linked List, and Ordered Map / Arbitrary Maximum Removal
 354 - Design a Text Editor - Doubly Linked List or Two Stacks / Cursor Editing

Stacks and Queues
Fundamental Stack Mechanics

355 - Valid Parentheses - Stack / Matching Delimiters
 356 - Minimum Add to Make Parentheses Valid - Stack or Counter / Unmatched Delimiters
 357 - Minimum Remove to Make Valid Parentheses - Stack / Removing Unmatched Indices
 358 - Score of Parentheses - Stack / Nested Expression Evaluation
 359 - Simplify Path - Stack / Path Normalization
 360 - Crawler Log Folder - Stack / Directory Navigation
 361 - Baseball Game - Stack / Operation Simulation
 362 - Validate Stack Sequences - Stack / Push-Pop Simulation

Adjacent Cancellation and Reduction

363 - Make The String Great - Stack / Adjacent Pair Cancellation
 364 - Removing Stars From a String - Stack / Destructive Backspace Simulation
 365 - Clear Digits - Stack / Character-Digit Cancellation
 366 - Minimum String Length After Removing Substrings - Stack / Pattern Cancellation
 367 - Remove All Adjacent Duplicates in String II - Run-Length Stack / Counted Cancellation
 368 - Asteroid Collision - Stack / Directional Collision Resolution
 369 - Robot Collisions - Stack / Collision with Mutable Health

Stack-Based Evaluation and Parsing

370 - Evaluate Reverse Polish Notation - Stack / Postfix Evaluation
 371 - Decode String - Stack / Nested Repetition Frames
 372 - Reverse Substrings Between Each Pair of Parentheses - Stack / Nested String Transformation
 373 - Basic Calculator II - Stack / Operator Precedence
 374 - Basic Calculator - Stack and Recursion / Parenthesized Addition and Subtraction
 375 - Basic Calculator III - Parser and Stack / Full Arithmetic Precedence
 376 - Ternary Expression Parser - Stack / Right-to-Left Conditional Parsing
 377 - Parsing a Boolean Expression - Stack / Nested Boolean Evaluation
 378 - Number of Atoms - Stack of Maps / Nested Multipliers
 379 - Different Ways to Add Parentheses - Divide and Conquer / Expression Partitioning
 380 - Integer to English Words - Recursion / Hierarchical Number Formatting

Monotonic Stack Foundations

381 - Final Prices With a Special Discount in a Shop - Monotonic Stack / Next Smaller or Equal
 382 - Next Greater Element I - Monotonic Stack / Next Greater Value
 383 - Next Greater Element II - Monotonic Stack / Circular Next Greater
 384 - Daily Temperatures - Monotonic Stack / Next Greater Index Distance
 385 - Online Stock Span - Monotonic Stack / Previous Greater Boundary
 386 - Maximum Width Ramp - Monotonic Stack / Candidate Left Boundaries
 387 - Number of Visible People in a Queue - Monotonic Stack / Visibility Counting
 388 - 132 Pattern - Monotonic Stack / Ordered Triple Detection
 389 - Find the Number of Subarrays Where Boundary Elements Are Maximum - Monotonic Stack / Boundary-Maximum Counting

Greedy Monotonic Stacks

390 - Remove K Digits - Greedy and Monotonic Stack / Minimum Number Construction
 391 - Find Permutation - Stack and Greedy / Reversing Decreasing Runs
 392 - Car Fleet - Monotonic Stack / Arrival-Time Merging
 393 - Min Cost Tree From Leaf Values - Monotonic Stack / Local Minimum Elimination

Contribution and Histogram Stacks

394 - Sum of Subarray Minimums - Monotonic Stack / Contribution Boundaries
 395 - Largest Rectangle in Histogram - Monotonic Stack / Maximum Span per Height
 396 - Maximal Rectangle - Matrix and Monotonic Stack / Row Histograms
 397 - Number of Submatrices With All Ones - Matrix and Monotonic Stack / Histogram Counting
 398 - Largest Submatrix With Rearrangements - Matrix and Sorting / Rearranged Histogram Widths

Stack and Queue Implementations

399 - Implement Stack Using Queues - Queue Design / LIFO from FIFO
 400 - Implement Queue Using Stacks - Stack Design / Amortized FIFO
 401 - Min Stack - Stack Design / Synchronized Minimum
 402 - Design Circular Queue - Queue Design / Ring Buffer
 403 - Design Circular Deque - Deque Design / Circular Buffer
 404 - Design Front Middle Back Queue - Deque Design / Balanced Halves

Queue and Deque Simulation

405 - Dota2 Senate - Queue / Cyclic Elimination
 406 - Find the Winner of the Circular Game - Queue Simulation / Josephus Process
 407 - Reveal Cards in Increasing Order - Queue / Reverse Process Simulation
 408 - Minimum Number of K Consecutive Bit Flips - Queue or Difference Array / Active Flip Parity
 409 - Stamping the Sequence - Queue / Reverse Dependency Processing

Monotonic Deque Review and Generalization

410 - Sliding Window Maximum - Monotonic Deque / Window Maximum [review from #193]
 411 - Longest Continuous Subarray With Absolute Difference Less Than or Equal to Limit - Dual Deques / Window Range [review from #194]
 412 - Continuous Subarrays - Dual Deques / Bounded Range Counting [review from #195]
 413 - Max Value of Equation - Monotonic Deque / Transformed Window Maximum [review from #197]
 414 - Shortest Subarray With Sum at Least K - Prefix Sum and Monotonic Deque [review from #198]
 415 - Jump Game VI - Dynamic Programming and Monotonic Deque [review from #199]
 416 - Constrained Subsequence Sum - Dynamic Programming and Monotonic Deque [review from #200]

Specialized Stack and Iterator Design

417 - Maximum Frequency Stack - Stack Design / Frequency Buckets
 418 - Flatten Nested List Iterator - Iterator and Stack / Lazy Nested Traversal
 419 - Peeking Iterator - Iterator Design / One-Element Lookahead
 420 - Exclusive Time of Functions - Call Stack / Nested Execution Accounting

Recursion and Backtracking
Recursion Foundations

421 - Fibonacci Number - Recursion / Base Cases and Linear Recurrence
 422 - Pow(x, n) - Divide and Conquer / Exponentiation by Squaring
 423 - Power of Two - Recursion and Bitwise / Repeated Halving
 424 - Find the Winner of the Circular Game - Recursion / Josephus Recurrence
 425 - Different Ways to Add Parentheses - Divide and Conquer / Recursive Expression Splitting

Subsets and Combinations

426 - Subsets - Backtracking / Include-or-Exclude Template
 427 - Subsets II - Backtracking / Duplicate-Safe Subset Generation
 428 - Combinations - Backtracking / Fixed-Length Selection
 429 - Combination Sum - Backtracking / Reusable Candidates
 430 - Combination Sum II - Backtracking / Single-Use Candidates and Deduplication
 431 - Combination Sum III - Backtracking / Fixed Size and Fixed Sum
 432 - Number of Beautiful Subsets - Backtracking / Difference Constraints
 433 - Non-Decreasing Subsequences - Backtracking / Per-Level Deduplication

Permutations and Constructive Search

434 - Permutations - Backtracking / Used-Element State
 435 - Permutations II - Backtracking / Duplicate-Safe Permutations
 436 - Letter Combinations of a Phone Number - Backtracking / Cartesian Product
 437 - Letter Case Permutation - Backtracking / Binary Character Decisions
 438 - Numbers With Same Consecutive Differences - Backtracking / Constructing Digit Sequences
 439 - K-th Lexicographical Happy String - Backtracking / Lexicographic Generation
 440 - Construct Smallest Number From DI String - Backtracking and Greedy / Digit Placement
 441 - Beautiful Arrangement - Backtracking / Position-Based Constraints
 442 - Permutation Sequence - Combinatorics / Factoradic Selection

Valid Sequence Construction

443 - Generate Parentheses - Backtracking / Prefix Validity Invariant
 444 - Restore IP Addresses - Backtracking / Valid Segment Partitioning
 445 - Split Array Into Fibonacci Sequence - Backtracking / Numeric String Partitioning
 446 - Palindrome Partitioning - Backtracking / Palindromic Segment Selection

Grid Backtracking

447 - Word Search - Grid Backtracking / Mark, Explore, and Restore
 448 - Unique Paths III - Grid Backtracking / Visit-Every-Cell Constraint
 449 - N-Queens - Backtracking / Column and Diagonal Constraints
 450 - N-Queens II - Backtracking and Bitmasking / Counting Placements
 451 - Sudoku Solver - Constraint Backtracking / Candidate Placement

Graph and Trie-Assisted Backtracking

452 - All Paths From Source to Target - Graph Backtracking / DAG Path Enumeration
 453 - Word Search II - Trie and Backtracking / Prefix-Pruned Grid Search

Memoized Decision Search

454 - Target Sum - Memoized Recursion / Include Positive or Negative
 455 - Predict the Winner - Minimax / Interval State
 456 - Can I Win - Memoized Search / Bitmask Game State
 457 - Maximum Compatibility Score Sum - Backtracking and Bitmasking / Assignment
 458 - Matchsticks to Square - Backtracking / Symmetric Bucket Assignment
 459 - Partition to K Equal Sum Subsets - Backtracking / Equal-Bucket Construction
 460 - Maximum Number of Achievable Transfer Requests - Backtracking / Net-Balance Constraint
 461 - Distribute Repeating Integers - Backtracking and Bitmasking / Demand Assignment

Advanced Parsing and Expression Search

462 - Expression Add Operators - Backtracking / Expression State and Multiplication
 463 - Remove Invalid Parentheses - Backtracking / Minimum Removal and Deduplication
 464 - Integer to English Words - Recursion / Hierarchical Number Decomposition
 465 - Special Binary String - Recursive Decomposition / Canonical Reordering

Bitwise
Binary Representation Fundamentals

466 - Number of 1 Bits - Bitwise / Kernighan’s Bit-Clearing Trick
 467 - Counting Bits - Bitwise DP / Reusing Smaller States
 468 - Power of Two - Bitwise / Single-Set-Bit Test
 469 - Power of Four - Bitwise / Single Bit at an Even Position
 470 - Number Complement - Bitwise / Width-Limited Inversion
 471 - Hamming Distance - Bitwise / XOR and Population Count
 472 - Reverse Bits - Bitwise / Fixed-Width Reconstruction
 473 - UTF-8 Validation - Bitwise / Prefix-Mask Validation

Carry and Arithmetic

474 - Add Binary - Bitwise Arithmetic / Binary Carry Simulation
 475 - Sum of Two Integers - Bitwise Arithmetic / XOR Sum and AND Carry
 476 - Divide Two Integers - Bitwise Arithmetic / Shifted Subtraction
 477 - Minimum Flips to Make A or B Equal to C - Bitwise / Per-Bit Case Analysis

XOR Cancellation

478 - Single Number - XOR / Pair Cancellation
 479 - Missing Number - XOR / Index-Value Cancellation
 480 - Single Number II - Bitwise / Per-Bit Counts Modulo Three
 481 - Single Number III - XOR / Partition by Distinguishing Bit
 482 - Total Hamming Distance - Bitwise / Per-Bit Contribution Counting

Prefix XOR and Reconstruction

483 - Decode XORed Array - Prefix XOR / Forward Reconstruction
 484 - Find the Original Array of Prefix XOR - Prefix XOR / Inverting Prefix States
 485 - Decode XORed Permutation - XOR / Recovering an Odd-Length Permutation
 486 - Neighboring Bitwise XOR - XOR / Cyclic Reconstruction Constraint
 487 - Minimum Number of Operations to Make Array XOR Equal to K - XOR / Differing-Bit Count
 488 - Find XOR Sum of All Pairs Bitwise AND - Bitwise Algebra / Distributive Identity

Range and Aggregate Bitwise Operations

489 - Bitwise AND of Numbers Range - Bitwise / Common Binary Prefix
 490 - Longest Subarray With Maximum Bitwise AND - Bitwise / Maximum-Value Run
 491 - Maximum OR - Bitwise / Prefix-Suffix Contribution
 492 - Longest Nice Subarray - Sliding Window and Bitmask / Disjoint Set Bits
 493 - Shortest Subarray With OR at Least K - Sliding Window and Bit Counts / Reversible OR
 494 - Find Subarray With Bitwise OR Closest to K - Bitwise / Compressed OR States
 495 - Number of Subarrays With AND Value of K - Bitwise / Compressed AND States

Binary Construction

496 - Gray Code - Bitwise / Reflected Binary Code
 497 - Minimum Array End - Bitwise / Filling Unoccupied Bits
 498 - Minimum Operations to Form Subsequence With Target Sum - Bitwise Greedy / Splitting Powers of Two
 499 - Minimize OR of Remaining Elements Using Operations - Bitwise Greedy / Testing Prefix Bits
 500 - Maximum XOR Product - Bitwise Greedy / Product-Balancing Construction

Binary Tries

501 - Maximum XOR of Two Numbers in an Array - Binary Trie / Greedy Opposite-Bit Search
 502 - Minimum XOR of Two Numbers in an Array - Sorting or Binary Trie / Nearest Bit Pattern
 503 - Maximum XOR With an Element From Array - Offline Queries and Binary Trie / Threshold Insertion

Bitmask Dynamic Programming

504 - Minimum XOR Sum of Two Arrays - Bitmask DP / Assignment
 505 - Smallest Sufficient Team - Bitmask DP / Minimum Cover
 506 - Triples With Bitwise AND Equal to Zero - Bitmask Counting / Pairwise AND States
 507 - Shortest Path Visiting All Nodes - Bitmask BFS / Node-and-Visited State

Trees and Binary Search Trees
Tree Definitions and Basic Traversal

508 - N-ary Tree Basics and Definitions - Tree / Node and Child Representation
 509 - Binary Tree Preorder Traversal - Tree DFS / Root-Left-Right
 510 - Binary Tree Inorder Traversal - Tree DFS / Left-Root-Right
 511 - Binary Tree Postorder Traversal - Tree DFS / Left-Right-Root
 512 - N-ary Tree Preorder Traversal - N-ary Tree / Depth-First Traversal
 513 - N-ary Tree Postorder Traversal - N-ary Tree / Postorder Traversal
 514 - Maximum Depth of Binary Tree - Tree DFS / Height
 515 - Maximum Depth of N-ary Tree - N-ary Tree / Height
 516 - Minimum Depth of Binary Tree - Tree BFS / First Leaf

Structural Comparison and Transformation

517 - Same Tree - Tree Recursion / Structural Equality
 518 - Invert Binary Tree - Tree Recursion / Mirror Transformation
 519 - Symmetric Tree - Tree Recursion / Mirror Comparison
 520 - Merge Two Binary Trees - Tree Recursion / Structural Combination
 521 - Leaf-Similar Trees - Tree DFS / Leaf Sequence
 522 - Subtree of Another Tree - Tree Recursion / Subtree Matching

Height-Based Postorder Patterns

523 - Balanced Binary Tree - Tree Postorder / Height with Validity
 524 - Diameter of Binary Tree - Tree Postorder / Combining Child Heights
 525 - Binary Tree Maximum Path Sum - Tree Postorder / Downward Gain
 526 - Binary Tree Cameras - Tree Postorder / Three-State Coverage
 527 - Distribute Coins in Binary Tree - Tree Postorder / Subtree Balance
 528 - House Robber III - Tree DP / Select-or-Skip State
 529 - Maximum Sum BST in Binary Tree - Tree Postorder / BST Metadata

Breadth-First Traversal

530 - Binary Tree Level Order Traversal - Tree BFS / Level Processing
 531 - Binary Tree Level Order Traversal II - Tree BFS / Bottom-Up Levels
 532 - Binary Tree Zigzag Level Order Traversal - Tree BFS / Alternating Direction
 533 - Binary Tree Right Side View - Tree BFS or DFS / Visible Node by Depth
 534 - Average of Levels in Binary Tree - Tree BFS / Level Aggregation
 535 - Cousins in Binary Tree - Tree BFS / Parent and Depth
 536 - Check Completeness of a Binary Tree - Tree BFS / Null-Gap Invariant
 537 - Count Complete Tree Nodes - Complete Tree / Height Comparison
 538 - Minimum Number of Operations to Sort a Binary Tree by Level - Tree BFS / Cycle Counting
 539 - Vertical Order Traversal of a Binary Tree - Tree Traversal / Row-Column Ordering

Root-to-Leaf Paths

540 - Binary Tree Paths - Tree Backtracking / Root-to-Leaf Enumeration
 541 - Path Sum - Tree DFS / Root-to-Leaf Sum Existence
 542 - Path Sum II - Tree Backtracking / Root-to-Leaf Path Enumeration
 543 - Sum Root to Leaf Numbers - Tree DFS / Path-Value Accumulation
 544 - Path Sum III - Tree Prefix Sum / Ancestor-State Counting
 545 - Boundary of Binary Tree - Tree Traversal / Boundary Decomposition

Ancestors, Distances, and Relationships

546 - Lowest Common Ancestor of a Binary Tree - Tree Recursion / Split Detection
 547 - Smallest Subtree With All the Deepest Nodes - Tree Recursion / Depth and LCA
 548 - All Nodes Distance K in Binary Tree - Tree and Graph / Parent Links with BFS
 549 - Populating Next Right Pointers in Each Node - Tree / Constant-Space Level Linking
 550 - Populating Next Right Pointers in Each Node II - Tree / General Constant-Space Level Linking

Tree Construction

551 - Construct Binary Tree From Preorder and Inorder Traversal - Tree Construction / Root and Inorder Split
 552 - Construct Binary Tree From Inorder and Postorder Traversal - Tree Construction / Reverse Root Selection
 553 - Construct Binary Tree From Preorder and Postorder Traversal - Tree Construction / Full-Tree Decomposition
 554 - Construct String From Binary Tree - Tree DFS / Structural Formatting
 555 - Flatten Binary Tree to Linked List - Tree Rewiring / Reverse Postorder

Serialization and Subtree Identity

556 - Serialize and Deserialize Binary Tree - Tree Serialization / Explicit Null Structure
 557 - Validate Preorder Serialization of a Binary Tree - Tree Serialization / Available-Slot Invariant
 558 - Find Duplicate Subtrees - Tree Hashing / Canonical Subtree Identity

Binary Search Tree Fundamentals

559 - Search in a Binary Search Tree - BST / Ordered Search
 560 - Insert Into a Binary Search Tree - BST / Ordered Insertion
 561 - Validate Binary Search Tree - BST / Global Bounds
 562 - Convert Sorted Array to Binary Search Tree - BST / Balanced Construction
 563 - Convert Sorted List to Binary Search Tree - BST / Middle-Node Construction
 564 - Delete Node in a BST - BST / Successor Replacement
 565 - Trim a Binary Search Tree - BST / Ordered Range Pruning
 566 - Range Sum of BST - BST / Ordered Range Pruning

Inorder as Sorted-Order Processing

567 - Kth Smallest Element in a BST - BST Inorder / Order Statistic
 568 - Minimum Distance Between BST Nodes - BST Inorder / Adjacent Difference
 569 - Find Mode in Binary Search Tree - BST Inorder / Run Counting
 570 - Convert BST to Greater Tree - BST / Reverse Inorder Accumulation
 571 - Increasing Order Search Tree - BST Inorder / Pointer Rewiring
 572 - Recover Binary Search Tree - BST Inorder / Detecting Swapped Values
 573 - All Elements in Two Binary Search Trees - BST / Merge Two Inorder Sequences

BST Queries and Iterators

574 - Lowest Common Ancestor of a BST - BST / Ordered Branching
 575 - Two Sum IV – Input Is a BST - BST / Two Iterators or Hashing
 576 - Closest Nodes Queries in a Binary Search Tree - BST / Floor and Ceiling
 577 - Binary Search Tree Iterator - BST / Lazy Inorder Stack
 578 - Closest Binary Search Tree Value II - BST / Predecessor and Successor Stacks

Advanced BST Construction and Counting

579 - Construct Binary Search Tree From Preorder Traversal - BST / Bounds-Based Construction
 580 - Serialize and Deserialize BST - BST / Preorder with Bounds
 581 - Balance a Binary Search Tree - BST / Inorder and Rebuild
 582 - Unique Binary Search Trees - BST DP / Catalan Recurrence
 583 - Number of Ways to Reorder Array to Get Same BST - BST and Combinatorics / Recursive Interleavings
 584 - Morris Traversal - Tree Threading / Constant-Space Traversal

Tries
Trie Foundations

585 - Implement Trie (Prefix Tree) - Trie / Insert, Search, and Prefix Search
 586 - Counting Words With a Given Prefix - Trie / Prefix Passage Counts
 587 - Sum of Prefix Scores of Strings - Trie / Accumulated Prefix Frequencies
 588 - Replace Words - Trie / Shortest Dictionary Prefix

Flexible and Approximate Search

589 - Design Add and Search Words Data Structure - Trie / Wildcard Search
 590 - Implement Magic Dictionary - Trie / Exactly One Character Modification
 591 - Extra Characters in a String - Trie and DP / Dictionary-Prefix Transitions

Prefix Ranking and Suggestions

592 - Search Suggestions System - Trie / Sorted Top-K Suggestions
 593 - Design Search Autocomplete System - Trie and Heap / Ranked Prefix Suggestions
 594 - Map Sum Pairs - Trie / Prefix Aggregate Values

Prefix and Suffix Relationships

595 - Count Prefix and Suffix Pairs I - String Matching / Prefix-Suffix Validation
 596 - Count Prefix and Suffix Pairs II - Trie / Combined Prefix-Suffix Counting
 597 - Stream of Characters - Reversed Trie / Streaming Suffix Queries
 598 - Palindrome Pairs - Trie / Reversed Words and Palindromic Remainders

Trie-Assisted Search and Hierarchical Structures

599 - Word Search II - Trie and Backtracking / Prefix-Pruned Board Search
 600 - Remove Sub-Folders From the Filesystem - Trie or Sorting / Ancestor Folder Detection
 601 - Design File System - Trie / Path Hierarchy
 602 - Design In-Memory File System - Trie / Directory and File Nodes

Heaps
Priority Queue Foundations

603 - Last Stone Weight - Max Heap / Repeated Selection
 604 - Take Gifts From the Richest Pile - Max Heap / Repeated Update
 605 - Final Array State After K Multiplication Operations I - Min Heap / Repeated Minimum Update
 606 - Kth Largest Element in a Stream - Min Heap / Fixed-Size Top K
 607 - Kth Largest Element in an Array - Min Heap / Fixed-Size Top K
 608 - Find the Kth Largest Integer in the Array - Heap / Large Numeric String Ordering
 609 - High Five - Heap / Per-Key Top K
 610 - Top K Frequent Elements - Hashing and Heap / Frequency Top K
 611 - Top K Frequent Words - Heap / Frequency and Lexicographic Ordering
 612 - Least Number of Unique Integers After K Removals - Min Heap / Remove Smallest Frequencies

Multiway Merge

613 - Merge K Sorted Lists - Heap / Multiway Linked-List Merge
 614 - K Smallest Pairs - Heap / Sorted Pair Frontier
 615 - Find K Pairs With Smallest Sums - Heap / Sorted Pair Frontier
 616 - Find the Kth Smallest Sum of a Matrix With Sorted Rows - Heap / Repeated Multiway Combination
 617 - Smallest Range Covering Elements From K Lists - Heap / Multiway Range Tracking

Greedy Selection with Heaps

618 - Minimum Cost to Connect Sticks - Min Heap / Repeated Cheapest Merge
 619 - Furthest Building You Can Reach - Min Heap / Allocate Limited Resources
 620 - Maximum Subsequence Score - Heap / Select K Under a Minimum Multiplier
 621 - Maximum Performance of a Team - Heap / Efficiency-Ordered Team Selection
 622 - IPO - Two Heaps / Capital-Constrained Profit Selection
 623 - Minimum Cost to Hire K Workers - Heap / Ratio-Ordered Selection
 624 - Campus Bikes - Heap or Sorted Events / Minimum-Distance Assignment

Scheduling and Resource Allocation

625 - Task Scheduler - Heap / Cooldown Scheduling
 626 - Reorganize String - Heap / Prevent Adjacent Equal Characters
 627 - Rearrange String K Distance Apart - Heap and Queue / Cooldown Separation
 628 - Longest Happy String - Heap / Avoiding Consecutive Repetition
 629 - Single-Threaded CPU - Heap / Available-Task Scheduling
 630 - Seat Reservation Manager - Min Heap / Smallest Available Resource
 631 - Process Tasks Using Servers - Two Heaps / Free and Busy Resources
 632 - The Number of the Smallest Unoccupied Chair - Two Heaps / Resource Arrival and Release
 633 - Meeting Rooms II - Heap / Minimum Concurrent Rooms
 634 - Meeting Rooms III - Two Heaps / Delayed Room Scheduling
 635 - Divide Intervals Into Minimum Number of Groups - Heap / Interval Resource Allocation
 636 - Car Pooling - Heap or Difference Array / Active Capacity

Streaming and Stateful Heap Design

637 - Find Median From Data Stream - Two Heaps / Lower-Upper Balance
 638 - Sliding Window Median - Two Heaps / Lazy Deletion
 639 - Stock Price Fluctuation - Heaps and Hashing / Lazy Stale-Entry Removal
 640 - Design a Food Rating System - Heap and Hashing / Category Ranking with Lazy Deletion
 641 - Design Twitter - Heap / Merging User Activity Streams
 642 - Maximum Frequency Stack - Frequency Buckets / Priority by Frequency and Recency

Monotonic and Optimization Heaps

643 - Minimize Deviation in Array - Heap / Normalize and Reduce Maximum
 644 - Constrained Subsequence Sum - Heap or Deque / Bounded DP Maximum
 645 - Find Building Where Alice and Bob Can Meet - Heap and Offline Queries / Earliest Valid Height
 646 - Number of Flowers in Full Bloom - Heap or Sweep Line / Active Intervals
 647 - Range Sum of Sorted Subarray Sums - Heap / Enumerating Ordered Subarray Sums

Graph and Matrix Heaps

648 - K Closest Points to Origin - Heap / Geometric Top K
 649 - Kth Smallest Element in a Sorted Matrix - Heap / Matrix Multiway Merge
 650 - Trapping Rain Water II - Heap and BFS / Expanding Boundary
 651 - Swim in Rising Water - Minimax Dijkstra / Minimum Possible Maximum Elevation
 652 - Path With Minimum Effort - Minimax Dijkstra / Minimum Bottleneck Path
 653 - Prim’s Minimum Spanning Tree - Heap and Graph / Cheapest Frontier Edge

Heap-Based Sequence Generation

654 - Ugly Number II - Heap or Multi-Pointer DP / Ordered Generated Sequence
 655 - Super Ugly Number - Heap or Multi-Pointer DP / Multi-Prime Sequence

Graphs
Graph Representation and Basic Traversal

656 - Find if Path Exists in Graph - Graph / Basic DFS and BFS
 657 - Keys and Rooms - Graph DFS / Reachability
 658 - Clone Graph - Graph Traversal / Visited Map and Deep Copy
 659 - Number of Provinces - Graph / Connected Components
 660 - Reorder Routes to Make All Paths Lead to the City Zero - Graph DFS / Edge Direction Tracking
 661 - Minimum Score of a Path Between Two Cities - Graph Traversal / Component-Wide Minimum Edge
 662 - Maximum Candies You Can Get From Boxes - Graph BFS / Unlockable State Processing

Bipartite Graphs and Coloring

663 - Is Graph Bipartite? - Graph Coloring / Two-Color Invariant
 664 - Possible Bipartition - Graph Coloring / Constraint Graph
 665 - Divide Nodes Into the Maximum Number of Groups - Bipartite Graph / Component Diameter and Layering

Grid Traversal Foundations

666 - Flood Fill - Grid DFS and BFS / Component Recoloring
 667 - Island Perimeter - Grid / Boundary Contribution
 668 - Number of Islands - Grid DFS and BFS / Connected Components
 669 - Max Area of Island - Grid DFS / Component Aggregation
 670 - Find All Groups of Farmland - Grid DFS / Component Bounding Rectangle
 671 - Count Sub Islands - Grid DFS / Component Containment
 672 - Number of Enclaves - Grid DFS / Boundary Reachability
 673 - Surrounded Regions - Grid DFS / Boundary-First Marking
 674 - Pacific Atlantic Water Flow - Grid Traversal / Reverse Reachability
 675 - Detect Cycles in 2D Grid - Grid DFS / Parent-Aware Cycle Detection
 676 - Shortest Bridge - Grid DFS and BFS / Component Marking and Expansion

Multi-Source Grid BFS

677 - Walls and Gates - Multi-Source BFS / Nearest Source Distance
 678 - Rotting Oranges - Multi-Source BFS / Layered Time Propagation
 679 - 01 Matrix - Multi-Source BFS / Nearest Zero Distance
 680 - As Far From Land as Possible - Multi-Source BFS / Maximum Nearest-Source Distance
 681 - Map of Highest Peak - Multi-Source BFS / Distance-Based Construction

Unweighted Shortest Paths

682 - Nearest Exit From Entrance in Maze - BFS / Shortest Unweighted Path
 683 - Shortest Path in Binary Matrix - BFS / Eight-Directional Shortest Path
 684 - Open the Lock - BFS / Implicit State Graph
 685 - Minimum Operations to Convert Number - BFS / Integer State Graph
 686 - Minimum Number of Operations to Make X and Y Equal - BFS / Reverse Integer Transformations
 687 - Snakes and Ladders - BFS / Board-to-Graph Mapping
 688 - Sliding Puzzle - BFS / Encoded State Graph
 689 - Jump Game III - BFS / Index State Graph
 690 - Jump Game IV - BFS / Value-Bucket Optimization
 691 - Bus Routes - BFS / Route-to-Route Graph
 692 - Shortest Path With Alternating Colors - BFS / Node-and-Edge-Color State
 693 - Second Minimum Time to Reach Destination - BFS / Two Arrival Times per Node

Word Transformation BFS

694 - Word Ladder - BFS / Shortest Transformation Sequence
 695 - Word Ladder II - BFS and Backtracking / All Shortest Transformation Paths

BFS with Expanded State

696 - Shortest Path to Get All Keys - Bitmask BFS / Position-and-Key State
 697 - Escape the Spreading Fire - Multi-Source BFS / Competing Arrival Times
 698 - Shortest Path Visiting All Nodes - Bitmask BFS / Node-and-Visited State [introduced at #507]

Disjoint Set Union Foundations

699 - Number of Provinces - Disjoint Set Union / Component Counting [alternative to #659]
 700 - Redundant Connection - Disjoint Set Union / First Cycle Edge
 701 - Make Network Connected - Disjoint Set Union / Components and Spare Edges
 702 - Satisfiability of Equality Equations - Disjoint Set Union / Equality Components
 703 - Accounts Merge - Disjoint Set Union / Entity Resolution
 704 - Smallest String With Swaps - Disjoint Set Union / Component-Wise Reordering
 705 - Most Stones Removed With Same Row or Column - Disjoint Set Union / Shared-Coordinate Components
 706 - Evaluate Division - Weighted Disjoint Set Union / Multiplicative Relationships

Advanced Disjoint Set Union

707 - Making a Large Island - Disjoint Set Union / Component Sizes After One Change
 708 - Find Latest Group of Size M - Disjoint Set Union / Dynamic Component Sizes
 709 - GCD Sort of an Array - Disjoint Set Union / Factor Connectivity
 710 - Checking Existence of Edge Length Limited Paths - Offline DSU / Sorted Edges and Queries
 711 - Remove Max Number of Edges to Keep Graph Fully Traversable - Disjoint Set Union / Shared and Exclusive Edges
 712 - Last Day Where You Can Still Cross - Binary Search and DSU / Dynamic Connectivity
 713 - Bricks Falling When Hit - Reverse Processing and DSU / Restored Connectivity
 714 - Rank Transform of a Matrix - Disjoint Set Union and DAG / Equal-Value Components
 715 - Redundant Connection II - Disjoint Set Union / Directed Parent and Cycle Cases

Topological Sort Foundations

716 - Course Schedule - Topological Sort / Directed Cycle Detection
 717 - Course Schedule II - Topological Sort / Producing a Valid Order
 718 - Find All Possible Recipes From Given Supplies - Topological Sort / Dependency Availability
 719 - All Ancestors of a Node in a Directed Acyclic Graph - DAG / Ancestor Propagation
 720 - Course Schedule IV - DAG / Transitive Reachability
 721 - Loud and Rich - DAG / Dominance Propagation

Topological Dynamic Programming

722 - Largest Color Value in a Directed Graph - Topological DP / Per-Color Path Counts
 723 - Parallel Courses III - Topological DP / Longest Completion Path
 724 - Number of Increasing Paths in a Grid - DAG DP / Height-Ordered Paths
 725 - Longest Increasing Path in a Matrix - DAG DP / Longest Height-Increasing Path

Multiple Dependency Orders

726 - Build a Matrix With Conditions - Topological Sort / Independent Row and Column Orders
 727 - Sort Items by Groups Respecting Dependencies - Topological Sort / Nested Dependency Graphs
 728 - Parallel Courses II - Topological Sort and Bitmask DP / Semester Selection

Weighted Graph Foundations

729 - Network Delay Time - Dijkstra / Single-Source Shortest Paths
 730 - Path With Maximum Probability - Modified Dijkstra / Maximum Product Path
 731 - Path With Minimum Effort - Minimax Dijkstra / Minimum Bottleneck Path [introduced at #652]
 732 - Swim in Rising Water - Minimax Dijkstra / Minimum Maximum Elevation [introduced at #651]
 733 - Number of Ways to Arrive at Destination - Dijkstra / Counting Shortest Paths
 734 - Reachable Nodes in Subdivided Graph - Dijkstra / Distance Budget Accounting
 735 - Design Graph With Shortest Path Calculator - Dijkstra / Mutable Weighted Graph API

Restricted and Layered Shortest Paths

736 - Cheapest Flights Within K Stops - Bellman-Ford DP / Edge-Limited Shortest Path
 737 - Minimum Cost to Make at Least One Valid Path in a Grid - 0-1 BFS / Zero-or-One Edge Costs
 738 - Number of Restricted Paths From First to Last Node - Dijkstra and DP / Decreasing-Distance Paths
 739 - Find the City With the Smallest Number of Neighbors at a Threshold Distance - Floyd-Warshall / All-Pairs Shortest Paths

Minimum Spanning Trees

740 - Min Cost to Connect All Points - Minimum Spanning Tree / Prim or Kruskal
 741 - Prim’s Minimum Spanning Tree - MST Template / Cheapest Frontier Edge
 742 - Find Critical and Pseudo-Critical Edges in Minimum Spanning Tree - MST / Edge Sensitivity Analysis

Cycle Detection and Functional Graphs

743 - Longest Cycle in a Graph - Functional Graph / Directed Cycle Length
 744 - Maximum Employees to Be Invited to a Meeting - Functional Graph / Cycles and Incoming Chains
 745 - Shortest Cycle in a Graph - BFS / Undirected Cycle Length

Eulerian Paths

746 - Reconstruct Itinerary - Eulerian Path / Lexicographic Hierholzer Algorithm
 747 - Valid Arrangement of Pairs - Eulerian Path / Directed Multigraph Trail

Bridges and Articulation Points

748 - Critical Connections in a Network - Tarjan’s Algorithm / Bridges
 749 - Minimum Number of Days to Disconnect Island - Tarjan’s Algorithm / Articulation Points

Advanced Graph State and Game Problems

750 - Cat and Mouse - Graph Game / Retrograde BFS and State DP
 751 - Number of Possible Sets of Closing Branches - Graph Enumeration / Subset Validation
 752 - Find the Shortest Superstring - Graph-Like Bitmask DP / Overlap Transitions

Range Queries

The progression below moves from immutable prefix queries to mutable Fenwick trees, segment trees, lazy propagation, persistence, and offline query processing.

Static One-Dimensional Queries

753 - Static Range Sum Queries - Prefix Sum / Immutable Range Sum [introduced at #73]
 754 - Static Range Minimum Queries - Sparse Table / Immutable Range Minimum
 755 - Range XOR Queries - Prefix XOR / Immutable Range XOR
 756 - Range Interval Queries - Sparse Table / Idempotent Range Query
 757 - Movie Festival Queries - Binary Lifting / Repeated Next-Interval Queries

Static Two-Dimensional Queries

758 - Forest Queries - 2D Prefix Sum / Immutable Rectangle Sum [introduced at #88]
 759 - Matrix Block Sum - 2D Prefix Sum / Fixed-Radius Rectangle Query [introduced at #87]

Fenwick Tree Foundations

760 - Dynamic Range Sum Queries - Fenwick Tree / Point Update and Range Sum
 761 - Count of Smaller Numbers After Self - Fenwick Tree / Coordinate Compression and Reverse Sweep
 762 - Inversion Count - Fenwick Tree / Prefix Frequency Counting
 763 - List Removals - Fenwick Tree / K-th Active Position
 764 - Salary Queries - Fenwick Tree / Dynamic Frequency Ranges
 765 - Distinct Values Queries - Offline Fenwick Tree / Last-Occurrence Updates

Difference Arrays and Range Updates

766 - Range Update Queries - Difference Array or Fenwick Tree / Range Add and Point Query
 767 - Increment Submatrices by One - 2D Difference Array / Rectangle Update [introduced at #89]
 768 - Forest Queries II - 2D Fenwick Tree / Point Toggle and Rectangle Sum

Segment Tree Foundations

769 - Dynamic Range Minimum Queries - Segment Tree / Point Update and Range Minimum
 770 - Subarray Sum Queries - Segment Tree / Maximum Subarray Metadata
 771 - Prefix Sum Queries - Segment Tree / Maximum Prefix Sum
 772 - Hotel Queries - Segment Tree / First Position Meeting a Threshold
 773 - Pizzeria Queries - Segment Tree / Transformed Distance Minimum
 774 - Subtree Queries - Euler Tour and Segment Tree / Subtree Sum
 775 - Path Queries - Euler Tour and Fenwick Tree / Root-to-Node Path Sum

Segment-Tree Node Composition

776 - Visible Buildings Queries - Segment Tree / Merging Visibility Information
 777 - Subarray Sum Queries II - Segment Tree / Extended Subarray Metadata
 778 - Distinct Values Queries II - Segment Tree / Dynamic Distinct Counting
 779 - Increasing Array Queries - Segment Tree / Monotonic Repair Cost
 780 - Missing Coin Sum Queries - Segment Tree / Reachable Prefix-Coverage Metadata

Lazy Propagation

781 - Range Updates and Sums - Lazy Segment Tree / Range Add, Assign, and Sum
 782 - Polynomial Queries - Lazy Segment Tree / Arithmetic-Progression Updates
 783 - Range Module - Dynamic Segment Tree / Coverage Updates and Queries [introduced at #297]
 784 - My Calendar III - Dynamic Segment Tree / Maximum Overlap [introduced at #295]

Persistence and Versioned Queries

785 - Range Queries and Copies - Persistent Segment Tree / Versioned Arrays
 786 - Snapshot Array - Versioned Storage / Per-Index Binary Search

Order Statistics and Offline Query Processing

787 - K-th Order Statistic in a Dynamic Multiset - Fenwick Tree / Frequency Selection
 788 - Offline Range Counting by Threshold - Fenwick Tree / Sorted Events and Queries
 789 - Count Number of Rectangles Containing Each Point - Offline Queries / Sorting and Fenwick Tree
 790 - Checking Existence of Edge Length Limited Paths - Offline Queries and DSU / Threshold Connectivity [introduced at #710]

Tree Range Queries

791 - Subordinates - Rooted Tree / Subtree Size
 792 - Tree Diameter - Tree DP / Two Longest Downward Paths
 793 - Tree Distances I - Tree DP / Farthest Distance per Node
 794 - Tree Distances II - Rerooting DP / Sum of Distances
 795 - Tree Matching - Tree DP / Maximum Matching
 796 - Company Queries I - Binary Lifting / K-th Ancestor
 797 - Company Queries II - Binary Lifting / Lowest Common Ancestor
 798 - Distance Queries - LCA / Tree Distance Formula
 799 - Counting Paths - LCA and Tree Difference / Path Frequency
 800 - Distinct Colors - Euler Tour and Offline Queries / Distinct Values in Subtrees
 801 - Path Queries II - Heavy-Light Decomposition / Path Maximum
 802 - Finding a Centroid - Tree / Subtree-Size Balancing
 803 - Fixed-Length Paths I - Centroid Decomposition / Exact-Distance Pair Counting
 804 - Fixed-Length Paths II - Centroid Decomposition / Distance-Range Pair Counting

Dynamic Programming
1. One-Dimensional Recurrence Foundations

805 - Climbing Stairs - Dynamic Programming / Basic One-Dimensional Recurrence
 806 - Min Cost Climbing Stairs - Dynamic Programming / Minimum-Cost Recurrence
 807 - House Robber - Dynamic Programming / Take-or-Skip Recurrence
 808 - 2 Keys Keyboard - Dynamic Programming / Factorization and State Transitions
 809 - Maximum Subarray - Dynamic Programming / Kadane’s Algorithm
 810 - Maximum Product Subarray - Dynamic Programming / Maximum and Minimum Ending States
 811 - Maximum Subarray Sum With One Deletion - Dynamic Programming / Used-Deletion State
 812 - Wiggle Subsequence - Dynamic Programming / Alternating Up and Down States
 813 - Longest Turbulent Subarray - Dynamic Programming / Alternating Comparison States
 814 - K-Concatenation Maximum Sum - Dynamic Programming / Kadane with Prefix and Suffix Contributions
 815 - Maximize Total Cost of Alternating Subarrays - Dynamic Programming / Alternating-Sign States
 816 - Constrained Subsequence Sum - Dynamic Programming and Monotonic Deque / Bounded Maximum Transition [introduced at #200]

2. Basic Counting and Unbounded Transitions

817 - Combination Sum IV - Dynamic Programming / Ordered Combination Counting
 818 - Number of Dice Rolls With Target Sum - Dynamic Programming / Bounded Sum Counting
 819 - Count Sorted Vowel Strings - Dynamic Programming / Nondecreasing Sequence Counting
 820 - Count Vowels Permutation - Dynamic Programming / Finite-State Transitions
 821 - Knight Dialer - Dynamic Programming / Graph-Based State Transitions
 822 - Student Attendance Record I - State Validation / Attendance Constraints
 823 - Student Attendance Record II - Dynamic Programming / Finite-State Sequence Counting
 824 - Dice Roll Simulation - Dynamic Programming / Run-Length-Constrained States
 825 - Number of Music Playlists - Dynamic Programming / Used-Song and Replay States
 826 - Build Array Where You Can Find the Maximum Exactly K Comparisons - Dynamic Programming / Length, Maximum, and Search-Cost State

3. Knapsack Foundations

827 - 0/1 Knapsack - Dynamic Programming Template / Use Each Item at Most Once
 828 - Partition Equal Subset Sum - 0/1 Knapsack / Subset-Sum Feasibility
 829 - Target Sum - 0/1 Knapsack / Sign Assignment Reduced to Subset Sum
 830 - Last Stone Weight II - 0/1 Knapsack / Minimum Partition Difference
 831 - Ones and Zeroes - Two-Dimensional 0/1 Knapsack / Dual Resource Constraints
 832 - Profitable Schemes - Multi-Dimensional Knapsack / People and Profit States
 833 - Rod Cutting - Unbounded Knapsack Template / Reusable Pieces
 834 - Coin Change - Unbounded Knapsack / Minimum Number of Items
 835 - Coin Change II - Unbounded Knapsack / Combination Counting
 836 - Minimum Number of Coins for Fruits - Dynamic Programming / Minimum Purchase Cost
 837 - Count of Sub-Multisets With Bounded Sum - Bounded Knapsack / Multiplicity-Aware Counting

4. State-Compressed Resource Search

838 - Shopping Offers - Memoized Dynamic Programming / Quantity-State Compression
 839 - Stickers to Spell Word - Memoized Dynamic Programming / Remaining-Character State
 840 - Smallest Sufficient Team - Bitmask DP / Minimum Set Cover [introduced at #505]
 841 - Distribute Repeating Integers - Bitmask DP / Assigning Customer Demands [introduced at #461]
 842 - Find Minimum Time to Finish All Jobs - Bitmask DP / Worker Assignment
 843 - Maximum Compatibility Score Sum - Bitmask DP / Person-to-Seat Assignment [introduced at #457]
 844 - Minimum XOR Sum of Two Arrays - Bitmask DP / Minimum-Cost Assignment [introduced at #504]
 845 - Number of Ways to Wear Different Hats to Each Other - Bitmask DP / Item-to-Person Assignment
 846 - Minimum Cost to Connect Two Groups of Points - Bitmask DP / Bipartite Coverage
 847 - Maximum Students Taking Exam - Bitmask DP / Valid Row Configurations
 848 - Maximum Number of Achievable Transfer Requests - Bitmask Enumeration / Net-Zero Balance
 849 - Maximize Grid Happiness - Profile DP / Row-State Compression
 850 - Shortest Path Visiting All Nodes - Bitmask State Search / Visited-Set DP [introduced at #507]

5. Longest Increasing Subsequence Family

851 - Longest Increasing Subsequence - Dynamic Programming / Quadratic LIS
 852 - Longest Increasing Subsequence - Binary Search / Patience Sorting Optimization
 853 - Number of Longest Increasing Subsequence - Dynamic Programming / Length and Count States
 854 - Maximum Length of Pair Chain - Dynamic Programming and Greedy / Ordered Pair Chains
 855 - Largest Divisible Subset - Dynamic Programming / Divisibility Predecessors
 856 - Russian Doll Envelopes - LIS / Sort One Dimension and Optimize the Other
 857 - Make Array Strictly Increasing - Dynamic Programming / Replacement-State Pruning
 858 - Longest String Chain - Dynamic Programming / Predecessor Deletion
 859 - Longest Unequal Adjacent Groups Subsequence II - Dynamic Programming / Constrained Predecessors
 860 - Find the Maximum Length of a Good Subsequence II - Dynamic Programming / Limited-Change State
 861 - Find the Maximum Length of Valid Subsequence II - Dynamic Programming / Remainder-Pair State

6. Arithmetic and Monotonic Subsequences

862 - Arithmetic Slices - Dynamic Programming / Contiguous Arithmetic Runs
 863 - Longest Arithmetic Subsequence of Given Difference - Dynamic Programming and Hashing / Fixed-Difference Predecessor
 864 - Longest Arithmetic Subsequence - Dynamic Programming and Hashing / Difference State
 865 - Find the Count of Monotonic Pairs I - Dynamic Programming / Monotonic Pair Decomposition
 866 - Find the Count of Monotonic Pairs II - Optimized Dynamic Programming / Prefix-Accumulated Transitions
 867 - K Inverse Pairs Array - Dynamic Programming / Prefix-Optimized Counting

7. Stock-State Dynamic Programming

868 - Best Time to Buy and Sell Stock - Dynamic Programming / One Transaction
 869 - Best Time to Buy and Sell Stock II - Dynamic Programming / Unlimited Transactions
 870 - Best Time to Buy and Sell Stock With Transaction Fee - Dynamic Programming / Hold and Cash States
 871 - Best Time to Buy and Sell Stock With Cooldown - Dynamic Programming / Hold, Sold, and Rest States
 872 - Best Time to Buy and Sell Stock III - Dynamic Programming / At Most Two Transactions
 873 - Best Time to Buy and Sell Stock IV - Dynamic Programming / At Most K Transactions

8. Grid Path Dynamic Programming

874 - Unique Paths - Grid DP / Counting Paths
 875 - Unique Paths II - Grid DP / Paths with Obstacles
 876 - Minimum Path Sum - Grid DP / Minimum Additive Path
 877 - Minimum Falling Path Sum - Grid DP / Adjacent-Column Transitions
 878 - Minimum Falling Path Sum II - Grid DP / Excluding the Same Column
 879 - Maximum Number of Moves in a Grid - Grid DAG DP / Increasing Paths
 880 - Where Will the Ball Fall - Grid DP or Simulation / Column Transition
 881 - Out of Boundary Paths - Grid DP / Step-Limited Boundary Exits
 882 - Maximum Non-Negative Product in a Matrix - Grid DP / Maximum and Minimum Product States
 883 - Dungeon Game - Reverse Grid DP / Minimum Required Health
 884 - Number of Ways of Cutting a Pizza - Grid DP and Prefix Sum / Valid Piece Cuts

9. Grid Shape Dynamic Programming

885 - Count Square Submatrices With All Ones - Grid DP / Minimum of Three Neighbors
 886 - Maximal Square - Grid DP / Largest All-One Square
 887 - Largest 1-Bordered Square - Prefix Sums / Valid Border Length
 888 - Largest Plus Sign - Directional DP / Four-Arm Minimum
 889 - Matrix Block Sum - 2D Prefix Sum / Rectangle Aggregation [introduced at #87]
 890 - Maximal Rectangle - Histogram DP and Monotonic Stack [introduced at #396]
 891 - Number of Submatrices That Sum to Target - Row Compression and Prefix Hashing [introduced at #105]
 892 - Max Sum of Rectangle No Larger Than K - Row Compression and Ordered Prefix Sums [introduced at #107]

10. Palindromic Dynamic Programming

893 - Longest Palindromic Substring - Interval DP / Palindromic Range Recognition
 894 - Count Palindromic Substrings - Interval DP / Counting Palindromic Ranges
 895 - Palindrome Partitioning - Backtracking with Palindrome DP [introduced at #446]
 896 - Longest Palindromic Subsequence - Interval DP / Matching Ends
 897 - Minimum Insertion Steps to Make a String Palindrome - Interval DP / Palindromic Completion
 898 - Palindrome Partitioning II - Dynamic Programming / Minimum Palindromic Cuts
 899 - Palindrome Partitioning III - Dynamic Programming / Minimum Changes Across K Parts
 900 - Minimum Changes to Make K Semi-Palindromes - Partition DP / Segment Conversion Cost
 901 - Longest Chunked Palindrome Decomposition - Dynamic Programming or Greedy / Matching Outer Chunks

11. Two-String Dynamic Programming

902 - Longest Common Subsequence - Two-String DP / Match-or-Skip Recurrence
 903 - Delete Operation for Two Strings - LCS Reduction / Minimum Deletions
 904 - Minimum ASCII Delete Sum for Two Strings - Two-String DP / Weighted Deletions
 905 - Shortest Common Supersequence - LCS Reconstruction / Merging Around Matches
 906 - Edit Distance - Two-String DP / Insert, Delete, and Replace
 907 - Interleaving String - Two-String DP / Prefix Interleaving
 908 - Max Dot Product of Two Subsequences - Two-Sequence DP / Forced Nonempty Matching
 909 - Apply Operations to Make Two Strings Equal - Two-String DP / Pairing Mismatch Costs
 910 - Minimum Swaps to Make Sequences Increasing - Dynamic Programming / Keep-or-Swap States

12. Pattern-Matching Dynamic Programming

911 - Regular Expression Matching - Dynamic Programming / Dot and Star Semantics
 912 - Wildcard Matching - Dynamic Programming / Question Mark and Star Semantics

13. Word Segmentation and Dictionary DP

913 - Word Break - Dynamic Programming / Prefix Segmentation
 914 - Word Break II - Dynamic Programming and Backtracking / Enumerating Segmentations
 915 - Extra Characters in a String - Dynamic Programming and Trie / Minimum Unmatched Characters
 916 - Concatenated Words - Dynamic Programming or Trie / Multiword Segmentation
 917 - Unique Substrings in Wraparound String - Dynamic Programming / Maximum Valid Suffix per Character

14. Distinct Subsequences and String Counting

918 - Distinct Subsequences - Two-String DP / Counting Target Formation
 919 - Distinct Subsequences II - Dynamic Programming / Removing Duplicate Subsequences
 920 - Number of Ways to Form a Target String Given a Dictionary - Dynamic Programming / Column-Based Character Selection
 921 - Find All Good Strings - Automaton DP / Length, Bounds, and Forbidden-Pattern State

15. Partition Dynamic Programming

922 - Partition Array for Maximum Sum - Partition DP / Best Final Segment
 923 - Filling Bookcase Shelves - Partition DP / Last-Shelf Enumeration
 924 - Video Stitching - Prefix DP / Minimum Clips [greedy version introduced at #288]
 925 - Allocate Mailboxes - Partition DP / Median Segment Cost
 926 - Min Cost to Split an Array - Partition DP / Duplicate Penalty
 927 - Minimum Sum of Values by Dividing Array - Partition DP / Segment AND State
 928 - String Compression II - Dynamic Programming / Delete-or-Keep Compression State

16. Interval Dynamic Programming Foundations

929 - Matrix Chain Multiplication - Interval DP Template / Choosing the Final Split
 930 - Minimum Score Triangulation of Polygon - Interval DP / Choosing the Final Triangle
 931 - Minimum Cost Tree From Leaf Values - Interval DP / Segment Maximum Combination
 932 - Burst Balloons - Interval DP / Choosing the Last Balloon
 933 - Minimum Cost to Cut a Stick - Interval DP / Choosing the Next Cut
 934 - Minimum Cost to Merge Stones - Interval DP / Merge Feasibility and Group Count
 935 - Remove Boxes - Interval DP / Carrying Equal Boxes Across a Range
 936 - Strange Printer - Interval DP / Merging Matching Print Operations

17. Complex Positional and Circular DP

937 - Freedom Trail - Dynamic Programming / Ring Position Transitions
 938 - Paint House III - Dynamic Programming / Position, Color, and Neighborhood State
 939 - Pizza With 3n Slices - Circular DP / Nonadjacent Fixed-Count Selection
 940 - Maximum Sum of 3 Non-Overlapping Subarrays - Dynamic Programming / Fixed Windows and Reconstruction [introduced at #170]

18. Probability Dynamic Programming

941 - Soup Servings - Probability DP / Serving-State Recurrence
 942 - New 21 Game - Probability DP / Sliding-Window Probability Sum
 943 - Champagne Tower - Probability DP / Overflow Distribution
 944 - Probability of a Two Boxes Having the Same Number of Distinct Balls - Combinatorial DP / Distribution with Equal Distinct Counts

19. Digit Dynamic Programming Foundations

945 - Count Numbers With Unique Digits - Digit DP / Used-Digit State
 946 - Non-Negative Integers Without Consecutive Ones - Digit DP / Previous-Bit Constraint
 947 - Numbers At Most N Given Digit Set - Digit DP / Restricted Digit Alphabet
 948 - Numbers With Repeated Digits - Digit DP / Complement of Unique-Digit Counts
 949 - Number of Digit One - Digit DP / Positional Digit Contribution
 950 - Number of Beautiful Integers in the Range - Digit DP / Balance and Divisibility State
 951 - Count the Number of Powerful Integers - Digit DP / Bounds, Suffix, and Digit Limit
 952 - Kth Smallest Instructions - Combinatorics / Lexicographic Path Counting

20. Tree Dynamic Programming

953 - House Robber III - Tree DP / Rob-or-Skip State [introduced at #528]
 954 - Longest ZigZag Path in a Binary Tree - Tree DP / Directional Downward States
 955 - Maximum Sum BST in Binary Tree - Tree DP / BST Metadata [introduced at #529]
 956 - Number of Ways to Reorder Array to Get Same BST - Tree DP and Combinatorics [introduced at #583]
 957 - Sum of Distances in Tree - Rerooting DP / Subtree-to-Global Transition
 958 - Count Paths That Can Form a Palindrome in a Tree - Tree DP / Path-Parity Masks
 959 - Find Number of Coins to Place in Tree Nodes - Tree DP / Extreme Subtree Values
 960 - Minimize the Total Price of the Trips - Tree DP / Path Frequencies and Independent Selection
 961 - Time Taken to Mark All Nodes - Rerooting DP / Direction-Dependent Edge Costs
 962 - Maximum Points After Collecting Coins From All Nodes - Tree DP / Operation Choice and Halving State
 963 - Maximum Score After Applying Operations on a Tree - Tree DP / Preserve-One-Path Constraint

21. Game Dynamic Programming

964 - Predict the Winner - Interval Game DP / Maximum Score Difference
 965 - Stone Game - Interval Game DP / Optimal Score Difference
 966 - Stone Game VII - Interval Game DP / Remove-One-End Scoring
 967 - Stone Game V - Interval DP / Valid Split and Score
 968 - Can I Win - Bitmask Game DP / Winning-State Search [introduced at #456]

22. Advanced Recurrence and Optimization

969 - Super Egg Drop - Dynamic Programming / Moves-to-Cover Recurrence
 970 - Race Car - Dynamic Programming / Overshoot-and-Reverse Decisions
 971 - Least Operators to Express Number - Digit DP / Base-X Representation Decisions
 972 - Super Washing Machines - Prefix Imbalance / Global Movement Bound [introduced at #315]
 973 - Reduce Dishes - Dynamic Programming and Greedy / Weighted Suffix Contribution
 974 - Find the Maximum Length of a Good Subsequence II - Optimized DP / Best State per Change Count
 975 - Find the Count of Monotonic Pairs II - Prefix-Optimized DP / Accelerated Transitions

Advanced String Algorithms

This section comes after string DP because it replaces expensive substring comparison and transition work with reusable preprocessing structures.

23. Prefix Function and KMP

976 - Find the Index of the First Occurrence in a String - KMP / Basic Pattern Search
 977 - Implement KMP Pattern Matching - KMP / Prefix-Function Construction
 978 - Find All Occurrences of a Pattern in Text - KMP / Reusing Matched Prefix Length
 979 - Repeated Substring Pattern - KMP / Border and Period Detection
 980 - Longest Happy Prefix - KMP / Longest Proper Prefix-Suffix
 981 - Shortest Palindrome - KMP / Longest Palindromic Prefix
 982 - Minimum Time to Revert Word to Initial State II - KMP or Z-Algorithm / Valid Shift Detection

24. Z-Algorithm

983 - Implement Z-Algorithm Pattern Matching - Z-Algorithm / Prefix-Match Lengths
 984 - Find All Pattern Occurrences Using pattern#text - Z-Algorithm / Pattern Matching
 985 - Sum of Scores of Built Strings - Z-Algorithm / Sum of Prefix Matches
 986 - Minimum Time to Revert Word to Initial State I - Z-Algorithm / Periodic Prefix Comparison

25. Rolling Hash

987 - Rabin-Karp Pattern Matching - Rolling Hash / Constant-Time Window Hash
 988 - Longest Duplicate Substring - Binary Search and Rolling Hash / Duplicate-Length Predicate
 989 - Distinct Echo Substrings - Rolling Hash / Equal Adjacent Substrings
 990 - Repeated DNA Sequences - Rolling Hash / Fixed-Length Duplicate Windows
 991 - Find Substring With Given Hash Value - Rolling Hash / Reverse Window Maintenance
 992 - Longest Common Subpath - Binary Search and Rolling Hash / Common Subarray Hashes

26. Manacher’s Algorithm

993 - Longest Palindromic Substring - Manacher’s Algorithm / Linear-Time Palindrome Radii
 994 - Count Palindromic Substrings - Manacher’s Algorithm / Summing Palindrome Radii
 995 - Maximum Product of the Length of Two Palindromic Substrings - Manacher and Prefix-Suffix Maxima / Disjoint Palindromes

27. Trie-Based Advanced String Matching

996 - Implement Trie (Prefix Tree) - Trie / Core Prefix Operations [introduced at #585]
 997 - Word Search II - Trie and Backtracking / Prefix-Pruned Search [introduced at #599]
 998 - Stream of Characters - Reversed Trie / Online Suffix Matching [introduced at #597]
 999 - Palindrome Pairs - Trie / Reversed Words and Palindromic Remainders [introduced at #598]
 1000 - Design Search Autocomplete System - Trie / Ranked Prefix Retrieval [introduced at #593]

28. Aho–Corasick Automaton

1001 - Implement Aho–Corasick Automaton - Multi-Pattern Matching / Trie Failure Links
 1002 - Multi-Pattern Occurrence Counting - Aho–Corasick / Failure-Link Aggregation
 1003 - Find All Good Strings - Automaton DP / Forbidden-Pattern Matching [introduced at #921]

29. Suffix Array and LCP

1004 - Construct a Suffix Array - Advanced Strings / Sorted Suffix Ranking
 1005 - Kasai’s Algorithm - Advanced Strings / Linear LCP Construction
 1006 - Count Distinct Substrings - Suffix Array and LCP / Total Minus Shared Prefixes
 1007 - Longest Duplicate Substring - Suffix Array and LCP / Maximum Adjacent LCP
 1008 - Longest Repeating Substring - Suffix Array and LCP / Maximum Repeated Prefix
 1009 - Longest Common Substring - Generalized Suffix Array / Cross-String Adjacent Suffixes

30. Suffix Automaton

1010 - Construct a Suffix Automaton - Advanced Strings / End-Position Equivalence States
 1011 - Count Distinct Substrings - Suffix Automaton / Transition-Length Contributions
 1012 - Count Occurrences of a Query String - Suffix Automaton / End-Position Counts
 1013 - Longest Common Substring - Suffix Automaton / Matching-State Traversal
 1014 - Longest Repeated Substring - Suffix Automaton / State Occurrence Counts

31. Advanced Palindrome Structures

1015 - Construct a Palindromic Tree - Eertree / Distinct Palindromic Substrings
 1016 - Count Distinct Palindromic Substrings - Eertree / One Node per Palindrome
 1017 - Count Occurrences of Every Palindrome - Eertree / Suffix-Link Propagation

32. Composite Advanced String Problems

1018 - Basic Calculator - Recursive Parsing / Nested Expression Grammar
 1019 - Basic Calculator III - Recursive Descent / Precedence and Parentheses
 1020 - Number of Atoms - Parsing / Nested Groups and Multipliers
 1021 - Expression Add Operators - Backtracking Parser / Precedence-Carrying State
 1022 - Regular Expression Matching - String DP / Automaton-Like Matching
 1023 - Wildcard Matching - String DP / Wildcard State Transitions
 1024 - Remove Invalid Parentheses - BFS or Backtracking / Minimum Grammar Repair
 1025 - Integer to English Words - Recursive String Construction / Magnitude Decomposition

Master DSA Roadmap — Part 6

Continuation from #1025. This final section progresses from basic matching to max flow, min cut, min-cost flow, and then composite data structures. Previously introduced problems are not renumbered unless they provide an essential integration checkpoint.

Flow and Matching
Bipartite Matching Foundations

1026 - Maximum Bipartite Matching - Matching Template / Basic Augmenting Paths
 1027 - Kuhn’s Algorithm - Bipartite Matching / DFS-Based Augmentation
 1028 - Maximum Bipartite Matching on a Grid - Bipartite Matching / Checkerboard Partitioning
 1029 - Maximum Students Taking Exam - Bipartite Matching or Bitmask DP / Conflict Graph
 1030 - Campus Bikes - Bipartite Assignment / Greedy, Heap, and Matching Comparison
 1031 - Maximum Compatibility Score Sum - Assignment Matching / Exhaustive and Bitmask Approaches
 1032 - Minimum XOR Sum of Two Arrays - Weighted Assignment / Bitmask DP Baseline
 1033 - Minimum Cost to Connect Two Groups of Points - Weighted Bipartite Coverage / Bitmask DP

Hopcroft–Karp

1034 - Hopcroft–Karp Algorithm - Bipartite Matching / Layered Augmenting Paths
 1035 - Maximum Bipartite Matching on a Large Sparse Graph - Hopcroft–Karp / Batched Augmentation
 1036 - Grid Pairing With Obstacles - Hopcroft–Karp / Sparse Grid Matching
 1037 - Minimum Path Cover in a Directed Acyclic Graph - Bipartite Matching / Vertex Splitting
 1038 - Minimum Vertex Cover in a Bipartite Graph - Matching / Kőnig’s Theorem
 1039 - Maximum Independent Set in a Bipartite Graph - Matching / Complement of Minimum Vertex Cover

Network-Flow Foundations

1040 - Ford–Fulkerson Algorithm - Maximum Flow / Residual Graph and Augmenting Paths
 1041 - Edmonds–Karp Algorithm - Maximum Flow / BFS Shortest Augmenting Paths
 1042 - Maximum Number of Edge-Disjoint Paths - Maximum Flow / Unit Edge Capacities
 1043 - Maximum Number of Vertex-Disjoint Paths - Maximum Flow / Vertex Splitting
 1044 - Maximum Flow in a Directed Network - Maximum Flow / Capacity Constraints

Dinic’s Algorithm

1045 - Dinic’s Algorithm - Maximum Flow / Level Graph and Blocking Flow
 1046 - Download Speed - Dinic / Maximum Network Throughput
 1047 - Police Chase - Maximum Flow and Minimum Cut / Cut-Edge Reconstruction
 1048 - School Dance - Maximum Flow / Bipartite Matching Construction
 1049 - Distinct Routes - Maximum Flow / Edge-Disjoint Path Reconstruction
 1050 - Maximum Bipartite Matching With Capacities - Dinic / Capacitated Assignment

Minimum Cut Modeling

1051 - Minimum s-t Cut - Flow Duality / Reachability in the Residual Graph
 1052 - Min-Cut Partitioning - Maximum Flow / Binary Assignment Costs
 1053 - Project Selection - Minimum Cut / Profit and Dependency Modeling
 1054 - Maximum Weight Closure of a Directed Graph - Minimum Cut / Dependency-Constrained Selection
 1055 - Grid Separation - Minimum Cut / Cell and Adjacency Capacities
 1056 - Minimum Number of Days to Disconnect Island - Articulation Points and Min-Cut Comparison

Lower Bounds and Circulation

1057 - Flow With Lower and Upper Bounds - Circulation / Demand Balancing
 1058 - Feasible Circulation - Super-Source and Super-Sink / Lower-Bound Transformation
 1059 - Flow With Node Demands - Circulation / Supply and Demand Conservation
 1060 - Bipartite Matching With Required Assignments - Lower-Bounded Flow / Mandatory Edges

Min-Cost Maximum Flow

1061 - Successive Shortest Augmenting Path Algorithm - Min-Cost Max-Flow / Residual Costs
 1062 - Minimum-Cost Maximum-Flow With Potentials - Min-Cost Flow / Reduced-Cost Dijkstra
 1063 - Minimum-Cost Bipartite Assignment - Min-Cost Flow / Unit-Capacity Matching
 1064 - Assignment With Costs - Min-Cost Flow / Worker-to-Job Modeling
 1065 - Minimum-Cost Pair Connection - Min-Cost Flow / Capacitated Pairing
 1066 - Transportation Problem - Min-Cost Flow / Multi-Unit Supply and Demand
 1067 - Minimum Cost to Connect Two Groups of Points - Min-Cost Flow / Coverage-Constrained Assignment
 1068 - Hungarian Algorithm - Assignment / Minimum-Cost Perfect Matching

Composite Data-Structure Design
Hash Table Internals

1069 - Design HashSet - Design / Buckets, Collision Handling, and Resizing
 1070 - Design HashMap - Design / Key-Value Buckets and Load Factor
 1071 - Insert Delete GetRandom O(1) - Design / Hash Map and Dynamic Array
 1072 - Insert Delete GetRandom O(1) – Duplicates Allowed - Design / Hash Map of Index Sets
 1073 - Finding the Users Active Minutes - Design Warm-Up / Map of Sets and Histogram

Stack and Queue Composition

1074 - Min Stack - Design / Stack With Aggregate Metadata
 1075 - Implement Stack Using Queues - Design / LIFO Using FIFO Primitives
 1076 - Implement Queue Using Stacks - Design / Amortized Lazy Transfer
 1077 - Design Circular Queue - Design / Fixed-Capacity Ring Buffer
 1078 - Design Circular Deque - Design / Bidirectional Ring Buffer
 1079 - Design Front Middle Back Queue - Design / Two Balanced Deques
 1080 - Max Stack - Design / Stack, Doubly Linked List, and Ordered Index
 1081 - Maximum Frequency Stack - Design / Frequency Buckets and Recency

Iterator Design

1082 - Peeking Iterator - Iterator Design / Buffered Lookahead
 1083 - Flatten Nested List Iterator - Iterator Design / Lazy Stack Expansion
 1084 - Binary Search Tree Iterator - Iterator Design / Lazy Inorder Traversal

Streaming Counters

1085 - Logger Rate Limiter - Streaming Design / Timestamped Key Suppression
 1086 - Design Hit Counter - Streaming Design / Sliding Timestamp Window
 1087 - Number of Recent Calls - Streaming Design / Queue-Based Time Window
 1088 - Product of the Last K Numbers - Streaming Design / Reset-Aware Prefix Products
 1089 - Kth Largest Element in a Stream - Streaming Design / Fixed-Size Heap
 1090 - Find Median From Data Stream - Streaming Design / Balanced Heaps

Key-Value Versioning

1091 - Time Based Key-Value Store - Design / Versioned Values and Floor Search
 1092 - Snapshot Array - Design / Per-Index Version History
 1093 - Online Election - Design / Prefix Leaders and Historical Queries
 1094 - Stock Price Fluctuation - Design / Latest Value, Extremes, and Lazy Deletion

Encoding and Serialization

1095 - Encode and Decode Strings - Design / Length-Prefixed Framing
 1096 - Serialize and Deserialize Binary Tree - Design / Null-Aware Tree Encoding
 1097 - Serialize and Deserialize BST - Design / Compact Preorder and Bounds
 1098 - Validate Preorder Serialization of a Binary Tree - Serialization / Slot Accounting

Linked Structures and Navigation

1099 - Design Linked List - Design / Indexed Node Operations
 1100 - Design Browser History - Design / Bidirectional Navigation
 1101 - LRU Cache - Design / Hash Map and Doubly Linked List
 1102 - LFU Cache - Design / Frequency Buckets and Recency
 1103 - All O(1) Data Structure - Design / Ordered Frequency Buckets
 1104 - Design a Text Editor - Design / Cursor Buffer or Two-Stack Editing

Trie-Based Systems

1105 - Implement Trie (Prefix Tree) - Design / Prefix Tree Fundamentals
 1106 - Design Add and Search Words Data Structure - Design / Trie With Wildcards
 1107 - Map Sum Pairs - Design / Trie Prefix Aggregation
 1108 - Stream of Characters - Design / Reversed Trie and Streaming Suffixes
 1109 - Search Suggestions System - Design / Prefix-Based Top-K Retrieval
 1110 - Design Search Autocomplete System - Design / Trie Ranking and Updates

Ordered Sets and Interval Systems

1111 - My Calendar I - Design / Ordered Non-Overlapping Intervals
 1112 - My Calendar II - Design / Preventing Triple Overlaps
 1113 - My Calendar III - Design / Dynamic Maximum Overlap
 1114 - Data Stream as Disjoint Intervals - Design / Online Interval Merging
 1115 - Range Module - Design / Dynamic Coverage Maintenance

Ranking and Category Systems

1116 - Design a Number Container System - Design / Value-to-Ordered-Indices Mapping
 1117 - Design a Food Rating System - Design / Category Heaps and Lazy Deletion
 1118 - Seat Reservation Manager - Design / Ordered Available Resources
 1119 - The Number of the Smallest Unoccupied Chair - Design / Resource Release and Reuse

Social and Activity Feeds

1120 - Design Twitter - Design / Follow Graph and K-Way Feed Merge
 1121 - Design Search Autocomplete System - Design / Ranked Activity Retrieval
 1122 - Maximum Frequency Stack - Design / Frequency and Recency Priority

Hierarchical File Systems

1123 - Design File System - Design / Path Trie and Stored Values
 1124 - Design In-Memory File System - Design / Directory and File Tree
 1125 - Remove Sub-Folders From the Filesystem - Hierarchical Design / Ancestor Detection

Mutable Graph APIs

1126 - Design Graph With Shortest Path Calculator - Design / Mutable Weighted Graph and Dijkstra
 1127 - Evaluate Division - Design / Weighted Graph or Weighted Union-Find
 1128 - Accounts Merge - Design / Entity Connectivity and Canonical Identity

Final Composite Design Problems

1129 - Task Scheduler - Composite Design / Heap, Cooldown Queue, and Frequency State
 1130 - Reorganize String - Composite Design / Heap and Adjacency Invariant
 1131 - Rearrange String K Distance Apart - Composite Design / Heap and Cooldown Queue
 1132 - Sliding Window Median - Composite Design / Dual Heaps and Lazy Deletion
 1133 - Minimum Interval to Include Each Query - Composite Design / Offline Sorting and Active Heap
 1134 - Smallest Range Covering Elements From K Lists - Composite Design / Heap and Range Tracking
 1135 - Design Twitter - Composite Design / Graph, Heap, and Stream Merge
 1136 - Design In-Memory File System - Composite Design / Trie, Tree, and Mutable Content
 1137 - LFU Cache - Composite Design / Multiple Hash Maps and Frequency Lists
 1138 - All O(1) Data Structure - Composite Design / Hash Maps and Bucketed Linked List



