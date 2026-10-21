# Section 1 LeetCode Curriculum: 120 Questions

**Section 1 covers patterns 1–9:**

1. Array, String & Matrix Mechanics  
2. Fundamental Hashing & Frequency Counting  
3. Prefix Sums, Difference Arrays & Prefix-Sum Hashing  
4. Two-Pointer Foundations  
5. Sorting, Pair Search & Multipointer Expansion  
6. Bucket Sort  
7. Boyer-Moore Voting & Counting Sort  
8. Quickselect & Randomized Selection  
9. Divide and Conquer on Arrays and Merge-Sort Counting  

The official <Organization>LeetCode</Organization> problem set currently includes dedicated tags for arrays, hashing, matrices, two pointers, prefix sums, quickselect, bucket sort, counting sort, divide and conquer, and merge sort, so this curriculum deliberately mixes those categories instead of treating Section 1 as only “array questions.” 【1-a96d48】【2-706526】

## How to use this list

Do **not** treat all 120 questions as equally important.

- **P0:** Must solve and later re-solve without help.
- **P1:** Must understand thoroughly and solve independently.
- **P2:** Advanced coverage or a useful variation.
- **Stretch:** Harder boundary case for Google L5 preparation.
- **Premium:** Skip if you do not have access without feeling that your preparation is incomplete.

### Recommended completion target

- **First pass:** Questions 1–65
- **Second pass:** Questions 66–100
- **Advanced pass:** Questions 101–120
- Re-solve approximately **35–40 P0/P1 questions** from a blank editor.

---

# Pattern 1: Array, String & Matrix Mechanics

These establish mutation, traversal, indexing, simulation, matrix boundaries, and in-place transformations.

## Foundational

1. **LC 26 — Remove Duplicates from Sorted Array**  
   Difficulty: Easy | Priority: P0  
   Focus: Read/write pointers and in-place mutation.

2. **LC 27 — Remove Element**  
   Difficulty: Easy | Priority: P0  
   Focus: Stable and unstable removal strategies.

3. **LC 283 — Move Zeroes**  
   Difficulty: Easy | Priority: P0  
   Focus: In-place compaction and preserving relative order.

4. **LC 88 — Merge Sorted Array**  
   Difficulty: Easy | Priority: P0  
   Focus: Right-to-left array writing.

5. **LC 189 — Rotate Array**  
   Difficulty: Medium | Priority: P0  
   Focus: Reversal algorithm, cyclic replacement, and modular indices.

6. **LC 48 — Rotate Image**  
   Difficulty: Medium | Priority: P0  
   Focus: Matrix transposition followed by reversal.

7. **LC 54 — Spiral Matrix**  
   Difficulty: Medium | Priority: P0  
   Focus: Boundary-controlled matrix traversal.

8. **LC 59 — Spiral Matrix II**  
   Difficulty: Medium | Priority: P1  
   Focus: Constructive matrix simulation.

9. **LC 73 — Set Matrix Zeroes**  
   Difficulty: Medium | Priority: P0  
   Focus: Using the first row and column as state.

10. **LC 289 — Game of Life**  
    Difficulty: Medium | Priority: P1  
    Focus: Simultaneous in-place state transitions.

## Variations

11. **LC 498 — Diagonal Traverse**  
    Difficulty: Medium | Priority: P1  
    Focus: Direction changes and diagonal indexing.

12. **LC 867 — Transpose Matrix**  
    Difficulty: Easy | Priority: P1  
    Focus: Rectangular matrix transformation.

13. **LC 1572 — Matrix Diagonal Sum**  
    Difficulty: Easy | Priority: P1  
    Focus: Diagonal indexing and center-cell overlap.

14. **LC 2022 — Convert 1D Array Into 2D Array**  
    Difficulty: Easy | Priority: P2  
    Focus: Index mapping between representations.

15. **LC 6 — Zigzag Conversion**  
    Difficulty: Medium | Priority: P1  
    Focus: Directional string simulation.

### Pattern 1 mastery check

You should be able to explain:

- When mutation is safe.
- How to avoid overwriting unread values.
- How to encode temporary state in the original array.
- How to derive matrix index transformations.
- How to handle shrinking matrix boundaries without duplicating cells.

---

# Pattern 2: Fundamental Hashing & Frequency Counting

These cover membership, frequency maps, canonical representations, duplicate detection, grouping, and complements.

## Foundational

16. **LC 1 — Two Sum**  
    Difficulty: Easy | Priority: P0  
    Focus: Complement lookup.

17. **LC 217 — Contains Duplicate**  
    Difficulty: Easy | Priority: P0  
    Focus: Hash-set membership.

18. **LC 219 — Contains Duplicate II**  
    Difficulty: Easy | Priority: P0  
    Focus: Last-seen index tracking.

19. **LC 242 — Valid Anagram**  
    Difficulty: Easy | Priority: P0  
    Focus: Frequency equality.

20. **LC 49 — Group Anagrams**  
    Difficulty: Medium | Priority: P0  
    Focus: Canonical keys using sorting or frequency vectors.

21. **LC 128 — Longest Consecutive Sequence**  
    Difficulty: Medium | Priority: P0  
    Focus: Starting-point detection in an unordered set.

22. **LC 205 — Isomorphic Strings**  
    Difficulty: Easy | Priority: P1  
    Focus: Bidirectional mappings.

23. **LC 290 — Word Pattern**  
    Difficulty: Easy | Priority: P1  
    Focus: Bijective mapping between domains.

## Set and frequency operations

24. **LC 349 — Intersection of Two Arrays**  
    Difficulty: Easy | Priority: P1  
    Focus: Set intersection.

25. **LC 350 — Intersection of Two Arrays II**  
    Difficulty: Easy | Priority: P1  
    Focus: Multiset intersection.

26. **LC 383 — Ransom Note**  
    Difficulty: Easy | Priority: P1  
    Focus: Supply-versus-demand frequency counting.

27. **LC 387 — First Unique Character in a String**  
    Difficulty: Easy | Priority: P1  
    Focus: Frequency counting followed by ordered scanning.

28. **LC 409 — Longest Palindrome**  
    Difficulty: Easy | Priority: P1  
    Focus: Pair extraction from frequencies.

29. **LC 771 — Jewels and Stones**  
    Difficulty: Easy | Priority: P2  
    Focus: Membership-based counting.

## Advanced hashing

30. **LC 36 — Valid Sudoku**  
    Difficulty: Medium | Priority: P0  
    Focus: Multiple simultaneous uniqueness constraints.

31. **LC 454 — 4Sum II**  
    Difficulty: Medium | Priority: P0  
    Focus: Pair-sum aggregation and complement matching.

### Pattern 2 mastery check

You should recognize when the correct hash-table value is:

- A Boolean membership flag.
- A frequency.
- A last-seen index.
- A first-seen index.
- A list of positions.
- A canonical signature.
- A pair or tuple of state values.

---

# Pattern 3: Prefix Sums, Difference Arrays & Prefix-Sum Hashing

This is one of the most important parts of Section 1. Master the distinction between plain prefix sums, transformed prefix sums, modular prefix sums, prefix XOR, and difference arrays.

## Basic one-dimensional prefix sums

32. **LC 303 — Range Sum Query: Immutable**  
    Difficulty: Easy | Priority: P0  
    Focus: Prefix-array construction and range formulas.

33. **LC 724 — Find Pivot Index**  
    Difficulty: Easy | Priority: P0  
    Focus: Left sum versus right sum.

34. **LC 1480 — Running Sum of 1D Array**  
    Difficulty: Easy | Priority: P1  
    Focus: Prefix-sum mechanics.

35. **LC 1732 — Find the Highest Altitude**  
    Difficulty: Easy | Priority: P1  
    Focus: Prefix accumulation over differences.

36. **LC 1991 — Find the Middle Index in Array**  
    Difficulty: Easy | Priority: P1  
    Focus: Balance point detection.

37. **LC 2574 — Left and Right Sum Differences**  
    Difficulty: Easy | Priority: P1  
    Focus: Prefix and suffix aggregation.

38. **LC 238 — Product of Array Except Self**  
    Difficulty: Medium | Priority: P0  
    Focus: Prefix and suffix products without division.

## Two-dimensional prefix sums

39. **LC 304 — Range Sum Query 2D: Immutable**  
    Difficulty: Medium | Priority: P0  
    Focus: Inclusion-exclusion in a 2D prefix table.

## Prefix-sum hashing

40. **LC 560 — Subarray Sum Equals K**  
    Difficulty: Medium | Priority: P0  
    Focus: Counting earlier prefix sums equal to `current - k`.

41. **LC 523 — Continuous Subarray Sum**  
    Difficulty: Medium | Priority: P0  
    Focus: Prefix remainders and earliest indices.

42. **LC 525 — Contiguous Array**  
    Difficulty: Medium | Priority: P0  
    Focus: Transforming `0` into `-1`.

43. **LC 974 — Subarray Sums Divisible by K**  
    Difficulty: Medium | Priority: P0  
    Focus: Counting equal prefix remainders.

44. **LC 930 — Binary Subarrays With Sum**  
    Difficulty: Medium | Priority: P0  
    Focus: Exact-sum counting in binary arrays.

45. **LC 1248 — Count Number of Nice Subarrays**  
    Difficulty: Medium | Priority: P0  
    Focus: Transforming odd/even values into binary indicators.

## Prefix XOR

46. **LC 1310 — XOR Queries of a Subarray**  
    Difficulty: Medium | Priority: P1  
    Focus: Prefix XOR and range XOR formulas.

## Difference arrays

47. **LC 1109 — Corporate Flight Bookings**  
    Difficulty: Medium | Priority: P0  
    Focus: One-dimensional range updates.

48. **LC 1094 — Car Pooling**  
    Difficulty: Medium | Priority: P0  
    Focus: Difference events and capacity checking.

## Prefix/suffix partitioning

49. **LC 2256 — Minimum Average Difference**  
    Difficulty: Medium | Priority: P1  
    Focus: Prefix sums with partition-specific denominators.

### Pattern 3 mastery check

For every subarray question, ask:

1. Can each element be transformed into a numeric contribution?
2. Is the requirement based on an exact sum?
3. Do I need a count, existence result, or maximum length?
4. Should the map store a frequency or earliest index?
5. Is modulo involved?
6. Can negative values appear?
7. Is the input binary or transformable into binary?
8. Is this actually a range-update problem requiring a difference array?

---

# Pattern 4: Two-Pointer Foundations

These questions cover opposite-direction pointers, same-direction pointers, fast/slow traversal, partitioning, subsequence matching, and area-based movement proofs.

## Opposite-direction pointers

50. **LC 125 — Valid Palindrome**  
    Difficulty: Easy | Priority: P0  
    Focus: Filtered character comparison.

51. **LC 167 — Two Sum II: Input Array Is Sorted**  
    Difficulty: Medium | Priority: P0  
    Focus: Movement based on sum comparison.

52. **LC 344 — Reverse String**  
    Difficulty: Easy | Priority: P1  
    Focus: Symmetric in-place swaps.

53. **LC 345 — Reverse Vowels of a String**  
    Difficulty: Easy | Priority: P1  
    Focus: Conditional pointer movement.

54. **LC 680 — Valid Palindrome II**  
    Difficulty: Easy | Priority: P0  
    Focus: Branching after the first mismatch.

55. **LC 11 — Container With Most Water**  
    Difficulty: Medium | Priority: P0  
    Focus: Proof for moving the shorter boundary.

56. **LC 15 — 3Sum**  
    Difficulty: Medium | Priority: P0  
    Focus: Sorting, duplicate handling, and two-pointer search.

57. **LC 42 — Trapping Rain Water**  
    Difficulty: Hard | Priority: P0  
    Focus: Left/right maximum invariants.

## Same-direction pointers

58. **LC 392 — Is Subsequence**  
    Difficulty: Easy | Priority: P0  
    Focus: Ordered matching within another sequence.

59. **LC 977 — Squares of a Sorted Array**  
    Difficulty: Easy | Priority: P0  
    Focus: Filling output from the largest absolute value.

60. **LC 75 — Sort Colors**  
    Difficulty: Medium | Priority: P0  
    Focus: Dutch National Flag partitioning.

61. **LC 80 — Remove Duplicates from Sorted Array II**  
    Difficulty: Medium | Priority: P0  
    Focus: Generalized read/write overwrite conditions.

62. **LC 443 — String Compression**  
    Difficulty: Medium | Priority: P1  
    Focus: Read/write pointers over character runs.

## Greedy two pointers

63. **LC 881 — Boats to Save People**  
    Difficulty: Medium | Priority: P0  
    Focus: Pairing the heaviest person when possible.

## Paired interval pointers

64. **LC 986 — Interval List Intersections**  
    Difficulty: Medium | Priority: P0  
    Focus: Advancing the interval that ends first.

### Pattern 4 mastery check

You should be able to justify:

- Why moving one pointer cannot remove an optimal answer.
- Whether output must preserve relative order.
- How duplicates affect pointer movement.
- Whether a local mismatch permits one branch or several.
- Whether the algorithm is truly two-pointer or actually sliding window.

---

# Pattern 5: Sorting, Pair Search & Multipointer Expansion

These questions focus on sorting as a transformation that exposes order, adjacency, pairing, duplicate control, and monotonic pointer movement.

## Pair and tuple search

65. **LC 16 — 3Sum Closest**  
    Difficulty: Medium | Priority: P0  
    Focus: Closest-target multipointer search.

66. **LC 18 — 4Sum**  
    Difficulty: Medium | Priority: P0  
    Focus: K-sum reduction, duplicate control, and overflow safety.

67. **LC 611 — Valid Triangle Number**  
    Difficulty: Medium | Priority: P0  
    Focus: Counting valid pairs for a fixed largest side.

68. **LC 923 — 3Sum With Multiplicity**  
    Difficulty: Medium | Priority: P1  
    Focus: Duplicate-aware combinatorial counting.

69. **LC 1577 — Number of Ways Where Square of Number Is Equal to Product of Two Numbers**  
    Difficulty: Medium | Priority: P2  
    Focus: Pair-product counting.

## Sorting transformations

70. **LC 31 — Next Permutation**  
    Difficulty: Medium | Priority: P0  
    Focus: Pivot detection, successor selection, and suffix reversal.

71. **LC 56 — Merge Intervals**  
    Difficulty: Medium | Priority: P0  
    Focus: Sort-then-merge.

72. **LC 57 — Insert Interval**  
    Difficulty: Medium | Priority: P0  
    Focus: Before, overlap, and after phases.

73. **LC 532 — K-diff Pairs in an Array**  
    Difficulty: Medium | Priority: P1  
    Focus: Unique-pair counting and the `k = 0` case.

74. **LC 658 — Find K Closest Elements**  
    Difficulty: Medium | Priority: P0  
    Focus: Ordered expansion or boundary binary search.

75. **LC 826 — Most Profit Assigning Work**  
    Difficulty: Medium | Priority: P1  
    Focus: Sorting two related domains and maintaining a prefix optimum.

76. **LC 870 — Advantage Shuffle**  
    Difficulty: Medium | Priority: P1  
    Focus: Greedy matching after sorting.

77. **LC 948 — Bag of Tokens**  
    Difficulty: Medium | Priority: P1  
    Focus: Two-ended greedy exchange.

78. **LC 1498 — Number of Subsequences That Satisfy the Given Sum Condition**  
    Difficulty: Medium | Priority: P0  
    Focus: Sorted endpoints plus combinatorial counting.

79. **LC 1877 — Minimize Maximum Pair Sum in Array**  
    Difficulty: Medium | Priority: P1  
    Focus: Pairing extremes after sorting.

### Pattern 5 mastery check

Before sorting, state precisely what sorting gives you:

- Adjacent equal values.
- Monotonic sums.
- Ordered endpoints.
- A canonical ordering.
- The ability to greedily pair extremes.
- The ability to skip duplicates.
- A fixed left-to-right sweep.
- A monotonic decision boundary.

Do not sort automatically. Explain why the lost original order is irrelevant or recoverable.

---

# Pattern 6: Bucket Sort as a Pattern

Bucket techniques are useful when the answer is organized by frequency, value range, or a small bounded domain.

80. **LC 347 — Top K Frequent Elements**  
    Difficulty: Medium | Priority: P0  
    Focus: Frequency buckets and top-K extraction.

81. **LC 451 — Sort Characters By Frequency**  
    Difficulty: Medium | Priority: P0  
    Focus: Grouping values by frequency.

82. **LC 692 — Top K Frequent Words**  
    Difficulty: Medium | Priority: P0  
    Focus: Frequency ordering with lexicographic tie-breaking.

83. **LC 164 — Maximum Gap**  
    Difficulty: Medium | Priority: P1  
    Focus: Pigeonhole reasoning and numeric buckets.

84. **LC 912 — Sort an Array**  
    Difficulty: Medium | Priority: P0  
    Focus: Implement several sorting approaches and compare constraints.

85. **LC 1054 — Distant Barcodes**  
    Difficulty: Medium | Priority: P1  
    Focus: Frequency-driven rearrangement.

86. **LC 767 — Reorganize String**  
    Difficulty: Medium | Priority: P0  
    Focus: Feasibility from maximum frequency and safe reconstruction.

87. **LC 1636 — Sort Array by Increasing Frequency**  
    Difficulty: Easy | Priority: P1  
    Focus: Sorting with frequency-based composite keys.

### Pattern 6 mastery check

Know when to choose:

- Frequency bucket instead of a heap.
- Counting sort instead of comparison sort.
- A heap when tie-breaking or online extraction matters.
- Direct-index arrays instead of hash maps.
- Bucket boundaries instead of storing every element.

---

# Pattern 7: Boyer-Moore Voting & Counting Sort

This pattern combines two bounded-state families:

- Frequency cancellation without storing all frequencies.
- Sorting or ranking through a bounded value domain.

## Boyer-Moore and cancellation

88. **LC 169 — Majority Element**  
    Difficulty: Easy | Priority: P0  
    Focus: Single-candidate Boyer-Moore voting.

89. **LC 229 — Majority Element II**  
    Difficulty: Medium | Priority: P0  
    Focus: Generalization to at most two candidates.

## Counting and bounded-domain processing

90. **LC 274 — H-Index**  
    Difficulty: Medium | Priority: P0  
    Focus: Capped counting buckets.

91. **LC 1122 — Relative Sort Array**  
    Difficulty: Easy | Priority: P1  
    Focus: Counting sort with a custom primary order.

92. **LC 1051 — Height Checker**  
    Difficulty: Easy | Priority: P1  
    Focus: Bounded-value reconstruction.

93. **LC 561 — Array Partition**  
    Difficulty: Easy | Priority: P1  
    Focus: Sorted pairing and counting-sort alternative.

94. **LC 1338 — Reduce Array Size to the Half**  
    Difficulty: Medium | Priority: P1  
    Focus: Frequencies of frequencies.

95. **LC 1207 — Unique Number of Occurrences**  
    Difficulty: Easy | Priority: P1  
    Focus: Validating frequency uniqueness.

96. **LC 945 — Minimum Increment to Make Array Unique**  
    Difficulty: Medium | Priority: P1  
    Focus: Sorted placement or frequency propagation.

97. **LC 1005 — Maximize Sum of Array After K Negations**  
    Difficulty: Easy | Priority: P1  
    Focus: Bounded-value greedy counting.

### Pattern 7 mastery check

For Boyer-Moore, be able to explain:

- Why pair cancellation preserves the majority.
- Why the final candidate may require verification.
- Why there can be at most `k - 1` values occurring more than `n/k` times.
- How candidate selection differs from candidate validation.

---

# Pattern 8: Quickselect & Randomized Selection

The first five questions are the direct selection core. The remaining five strengthen order-statistic reasoning where binary search or heap alternatives may be preferable.

## Direct Quickselect applications

98. **LC 215 — Kth Largest Element in an Array**  
    Difficulty: Medium | Priority: P0  
    Focus: Quickselect partitioning and randomized pivots.

99. **LC 973 — K Closest Points to Origin**  
    Difficulty: Medium | Priority: P0  
    Focus: Partial selection without fully sorting.

100. **LC 1985 — Find the Kth Largest Integer in the Array**  
     Difficulty: Medium | Priority: P1  
     Focus: Numeric-string comparison and selection.

101. **LC 324 — Wiggle Sort II**  
     Difficulty: Medium | Priority: Stretch  
     Focus: Median selection and three-way virtual-index partitioning.

102. **LC 462 — Minimum Moves to Equal Array Elements II**  
     Difficulty: Medium | Priority: P0  
     Focus: Median as the minimizer of absolute deviation.

## Broader order-statistic problems

103. **LC 378 — Kth Smallest Element in a Sorted Matrix**  
     Difficulty: Medium | Priority: P0  
     Focus: Heap versus value-domain binary search.

104. **LC 668 — Kth Smallest Number in Multiplication Table**  
     Difficulty: Hard | Priority: Stretch  
     Focus: Counting values at or below a candidate.

105. **LC 719 — Find K-th Smallest Pair Distance**  
     Difficulty: Hard | Priority: Stretch  
     Focus: Binary search over distance and two-pointer counting.

106. **LC 786 — K-th Smallest Prime Fraction**  
     Difficulty: Medium | Priority: P2  
     Focus: Fraction ordering and selection alternatives.

107. **LC 1439 — Find the Kth Smallest Sum of a Matrix With Sorted Rows**  
     Difficulty: Hard | Priority: Stretch  
     Focus: Repeated partial selection and bounded candidate expansion.

### Pattern 8 mastery check

Implement Quickselect with:

- Randomized pivot selection.
- Correct partition boundaries.
- Duplicate-safe behavior.
- Zero-based target conversion.
- Expected `O(n)` reasoning.
- Worst-case `O(n²)` awareness.

Also know when a heap or binary search on answer is safer than Quickselect.

---

# Pattern 9: Divide and Conquer on Arrays & Merge-Sort Counting

The central invariant is that after recursively sorting both halves, cross-half relationships can be counted efficiently.

## Core merge-sort counting

108. **LC 315 — Count of Smaller Numbers After Self**  
     Difficulty: Hard | Priority: P0  
     Focus: Index-preserving merge-sort counting.

109. **LC 327 — Count of Range Sum**  
     Difficulty: Hard | Priority: Stretch  
     Focus: Prefix sums and counting valid cross-half ranges.

110. **LC 493 — Reverse Pairs**  
     Difficulty: Hard | Priority: P0  
     Focus: Cross-half inequality counting before merging.

111. **LC 1649 — Create Sorted Array through Instructions**  
     Difficulty: Hard | Priority: Stretch  
     Focus: Smaller/greater counts using Fenwick tree or merge-sort ideas.

112. **LC 2426 — Number of Pairs Satisfying Inequality**  
     Difficulty: Hard | Priority: Stretch  
     Focus: Algebraic transformation followed by ordered-pair counting.

113. **LC 2179 — Count Good Triplets in an Array**  
     Difficulty: Hard | Priority: Stretch  
     Focus: Permutation mapping and left/right ordered counts.

114. **LC 1395 — Count Number of Teams**  
     Difficulty: Medium | Priority: P1  
     Focus: Counting smaller and greater elements around each index.

115. **LC 1885 — Count Pairs in Two Arrays**  
     Difficulty: Medium | Priority: P2 | Premium  
     Focus: Difference transformation and pair inequality counting.

## Related divide-and-conquer exposure

116. **LC 2251 — Number of Flowers in Full Bloom**  
     Difficulty: Hard | Priority: P1  
     Focus: Offline counting through sorted starts and ends.

117. **LC 218 — The Skyline Problem**  
     Difficulty: Hard | Priority: Stretch  
     Focus: Divide-and-conquer merging or sweep-line processing.

118. **LC 23 — Merge k Sorted Lists**  
     Difficulty: Hard | Priority: P1  
     Focus: Pairwise divide-and-conquer merging.

119. **LC 53 — Maximum Subarray**  
     Difficulty: Medium | Priority: P0  
     Focus: Kadane’s algorithm and divide-and-conquer alternative.

120. **LC 241 — Different Ways to Add Parentheses**  
     Difficulty: Medium | Priority: P1  
     Focus: Divide at every operator and combine independent subresults.

### Pattern 9 mastery check

For merge-sort counting, you should be able to explain:

1. What relationships are counted entirely inside the left half?
2. What relationships are counted entirely inside the right half?
3. What cross-half relationships remain?
4. Why does sorting each half make cross-counting efficient?
5. Must counting happen before or during the merge?
6. Do original indices need to be preserved?
7. Can integer multiplication or subtraction overflow?

---

# Priority Summary

## P0: Master cold

These are the highest-value questions from the complete list:

- LC 1 — Two Sum
- LC 15 — 3Sum
- LC 18 — 4Sum
- LC 26 — Remove Duplicates from Sorted Array
- LC 31 — Next Permutation
- LC 36 — Valid Sudoku
- LC 42 — Trapping Rain Water
- LC 48 — Rotate Image
- LC 49 — Group Anagrams
- LC 54 — Spiral Matrix
- LC 56 — Merge Intervals
- LC 57 — Insert Interval
- LC 73 — Set Matrix Zeroes
- LC 75 — Sort Colors
- LC 80 — Remove Duplicates from Sorted Array II
- LC 88 — Merge Sorted Array
- LC 128 — Longest Consecutive Sequence
- LC 164 — Maximum Gap
- LC 167 — Two Sum II
- LC 169 — Majority Element
- LC 189 — Rotate Array
- LC 215 — Kth Largest Element in an Array
- LC 229 — Majority Element II
- LC 238 — Product of Array Except Self
- LC 274 — H-Index
- LC 304 — Range Sum Query 2D
- LC 315 — Count of Smaller Numbers After Self
- LC 347 — Top K Frequent Elements
- LC 451 — Sort Characters By Frequency
- LC 454 — 4Sum II
- LC 462 — Minimum Moves to Equal Array Elements II
- LC 493 — Reverse Pairs
- LC 523 — Continuous Subarray Sum
- LC 525 — Contiguous Array
- LC 560 — Subarray Sum Equals K
- LC 611 — Valid Triangle Number
- LC 658 — Find K Closest Elements
- LC 692 — Top K Frequent Words
- LC 881 — Boats to Save People
- LC 930 — Binary Subarrays With Sum
- LC 973 — K Closest Points to Origin
- LC 974 — Subarray Sums Divisible by K
- LC 986 — Interval List Intersections
- LC 1109 — Corporate Flight Bookings
- LC 1248 — Count Number of Nice Subarrays
- LC 1498 — Number of Subsequences That Satisfy the Given Sum Condition

---

# Suggested Solving Order

## Phase 1: Foundations

Solve approximately 30 questions:

- Array mutation and matrix traversal
- Hash-map fundamentals
- Basic prefix sums
- Basic two pointers
- Sorting-based pair search

Recommended starting sequence:

1. LC 1
2. LC 217
3. LC 242
4. LC 26
5. LC 27
6. LC 283
7. LC 88
8. LC 125
9. LC 167
10. LC 977
11. LC 303
12. LC 724
13. LC 238
14. LC 49
15. LC 128
16. LC 189
17. LC 48
18. LC 54
19. LC 73
20. LC 15
21. LC 56
22. LC 57
23. LC 75
24. LC 11
25. LC 31
26. LC 347
27. LC 169
28. LC 229
29. LC 560
30. LC 974

## Phase 2: Pattern variations

Next, solve:

- Prefix-sum hashing variations
- Difference arrays
- Duplicate-sensitive K-sum
- Frequency buckets
- Greedy two pointers
- Quickselect

High-value targets:

- LC 523
- LC 525
- LC 930
- LC 1248
- LC 1094
- LC 1109
- LC 16
- LC 18
- LC 611
- LC 923
- LC 1498
- LC 451
- LC 692
- LC 164
- LC 215
- LC 973
- LC 462

## Phase 3: L5 advanced coverage

Finish with:

- LC 42
- LC 164
- LC 218
- LC 315
- LC 324
- LC 327
- LC 493
- LC 668
- LC 719
- LC 1439
- LC 1649
- LC 2179
- LC 2426

---

# Completion Criteria

Section 1 is complete when you can:

- Solve at least **95 of the 120** questions.
- Solve at least **40 P0 questions** without hints.
- Re-solve the major P0 problems after a two-week gap.
- Implement Quickselect and merge sort from memory.
- Derive prefix-sum hashing instead of recalling it mechanically.
- Explain duplicate handling in 3Sum and 4Sum.
- Prove pointer movement in Container With Most Water.
- Explain Boyer-Moore cancellation mathematically.
- Use a difference array for range updates.
- Distinguish selection from full sorting.
- Recognize the cross-pair structure behind merge-sort counting.

The main improvement over a random 120-question grind is that this curriculum covers distinct scenarios. The list progresses from mechanics to invariants, then moves into selection and divide-and-conquer counting, with the hardest questions reserved for the final pass.# Sections 2–5: LeetCode Curriculum

This curriculum contains **200 questions**, divided into:

- **Section 2: Sliding Windows — 40 questions**
- **Section 3: Binary Search — 50 questions**
- **Section 4: Intervals & Greedy — 60 questions**
- **Section 5: Linked Lists — 50 questions**

The categorization intentionally overlaps when a problem teaches more than one pattern. For example, a problem may use both a sliding window and a monotonic deque, or both interval sorting and greedy selection. LeetCode currently maintains dedicated tags for sliding window, binary search, greedy, sorting, linked lists, heaps, and monotonic queues, which supports treating these as related but independently practiced families. 【1-ca4012】【2-67eac9】【3-2f7acb】【4-002cec】

## Priority legend

- **P0:** Master cold. Re-solve from a blank editor.
- **P1:** Must solve independently.
- **P2:** Important variation or lower-frequency scenario.
- **Stretch:** Advanced Google L5 boundary problem.
- **Premium:** Skip if inaccessible.

---

# Section 2: Sliding Windows

## Patterns covered

10. Fixed-Size Sliding Windows  
11. Variable-Size Sliding Windows  
12. Monotonic Sliding Windows  

**Total: 40 questions**

---

## Pattern 10: Fixed-Size Sliding Windows

1. **LC 643 — Maximum Average Subarray I**  
   Easy | P0  
   Focus: Basic fixed-window sum.

2. **LC 1456 — Maximum Number of Vowels in a Substring of Given Length**  
   Medium | P0  
   Focus: Add-right, remove-left character counting.

3. **LC 1343 — Number of Sub-arrays of Size K and Average ≥ Threshold**  
   Medium | P0  
   Focus: Fixed-window threshold counting.

4. **LC 1876 — Substrings of Size Three with Distinct Characters**  
   Easy | P1  
   Focus: Fixed-size frequency validation.

5. **LC 219 — Contains Duplicate II**  
   Easy | P0  
   Focus: Bounded-distance membership window.

6. **LC 438 — Find All Anagrams in a String**  
   Medium | P0  
   Focus: Fixed-window frequency equality.

7. **LC 567 — Permutation in String**  
   Medium | P0  
   Focus: Detecting a permutation within a fixed window.

8. **LC 1052 — Grumpy Bookstore Owner**  
   Medium | P0  
   Focus: Baseline value plus maximum recoverable window.

9. **LC 1423 — Maximum Points You Can Obtain from Cards**  
   Medium | P0  
   Focus: Convert “take from ends” into a complementary window.

10. **LC 1652 — Defuse the Bomb**  
    Easy | P1  
    Focus: Circular fixed-size windows.

11. **LC 2090 — K Radius Subarray Averages**  
    Medium | P1  
    Focus: Centered windows and output indexing.

12. **LC 2379 — Minimum Recolors to Get K Consecutive Black Blocks**  
    Easy | P1  
    Focus: Minimum invalid values in a fixed window.

13. **LC 2461 — Maximum Sum of Distinct Subarrays With Length K**  
    Medium | P0  
    Focus: Fixed window plus distinctness constraint.

14. **LC 2841 — Maximum Sum of Almost Unique Subarray**  
    Medium | P1  
    Focus: Fixed window requiring at least `m` distinct values.

15. **LC 3318 — Find X-Sum of All K-Long Subarrays I**  
    Easy | P2  
    Focus: Frequency-ranked values inside fixed windows.

---

## Pattern 11: Variable-Size Sliding Windows

16. **LC 3 — Longest Substring Without Repeating Characters**  
    Medium | P0  
    Focus: Last-seen index and duplicate removal.

17. **LC 76 — Minimum Window Substring**  
    Hard | P0  
    Focus: Minimum covering window.

18. **LC 209 — Minimum Size Subarray Sum**  
    Medium | P0  
    Focus: Minimum window under a monotonic sum condition.

19. **LC 424 — Longest Repeating Character Replacement**  
    Medium | P0  
    Focus: Window size minus maximum frequency.

20. **LC 904 — Fruit Into Baskets**  
    Medium | P0  
    Focus: Longest window containing at most two distinct values.

21. **LC 1004 — Max Consecutive Ones III**  
    Medium | P0  
    Focus: Longest window with at most `k` invalid elements.

22. **LC 1208 — Get Equal Substrings Within Budget**  
    Medium | P1  
    Focus: Longest window under a cost budget.

23. **LC 1493 — Longest Subarray of 1’s After Deleting One Element**  
    Medium | P0  
    Focus: Window with at most one zero and mandatory deletion.

24. **LC 2024 — Maximize the Confusion of an Exam**  
    Medium | P1  
    Focus: Longest window after replacing at most `k` characters.

25. **LC 2516 — Take K of Each Character From Left and Right**  
    Medium | P0  
    Focus: Complementary middle window.

26. **LC 2779 — Maximum Beauty of an Array After Applying Operation**  
    Medium | P1  
    Focus: Sort followed by bounded-value window.

27. **LC 2958 — Length of Longest Subarray With at Most K Frequency**  
    Medium | P1  
    Focus: Per-value frequency limits.

28. **LC 2962 — Count Subarrays Where Max Element Appears at Least K Times**  
    Medium | P1  
    Focus: Counting valid windows after reaching a frequency threshold.

29. **LC 713 — Subarray Product Less Than K**  
    Medium | P0  
    Focus: Count valid positive-product windows.

30. **LC 930 — Binary Subarrays With Sum**  
    Medium | P0  
    Focus: `atMost(goal) - atMost(goal - 1)`.

31. **LC 992 — Subarrays with K Different Integers**  
    Hard | P0  
    Focus: `atMost(k) - atMost(k - 1)`.

32. **LC 1248 — Count Number of Nice Subarrays**  
    Medium | P0  
    Focus: Exact count through at-most subtraction.

33. **LC 1358 — Number of Substrings Containing All Three Characters**  
    Medium | P0  
    Focus: Counting all extensions of a valid window.

34. **LC 159 — Longest Substring with At Most Two Distinct Characters**  
    Medium | P1 | Premium  
    Focus: Bounded distinct-character window.

35. **LC 340 — Longest Substring with At Most K Distinct Characters**  
    Medium | P1 | Premium  
    Focus: Generalized bounded-distinct window.

---

## Pattern 12: Monotonic Sliding Windows

36. **LC 239 — Sliding Window Maximum**  
    Hard | P0  
    Focus: Canonical decreasing deque.

37. **LC 1438 — Longest Continuous Subarray With Absolute Diff ≤ Limit**  
    Medium | P0  
    Focus: Simultaneous maximum and minimum deques.

38. **LC 862 — Shortest Subarray with Sum at Least K**  
    Hard | P0  
    Focus: Monotonic deque over prefix sums.

39. **LC 1696 — Jump Game VI**  
    Medium | P1  
    Focus: Window maximum over dynamic-programming states.

40. **LC 2762 — Continuous Subarrays**  
    Medium | P1  
    Focus: Counting windows with bounded max-min difference.

---

## Section 2 mastery checklist

You should be able to:

- Distinguish fixed and variable windows immediately.
- Explain why a variable window condition is monotonic.
- Count exact constraints using `atMost(k) - atMost(k - 1)`.
- Count all subarrays ending at the current right boundary.
- Handle a required deletion or complementary window.
- Implement a monotonic deque from memory.
- Explain why expired and dominated deque elements can be removed.
- Recognize when negative numbers invalidate a normal sum window.

### P0 shortlist

- LC 3, 76, 209, 239
- LC 424, 438, 567
- LC 713, 904, 930, 992
- LC 1004, 1052, 1248
- LC 1358, 1423, 1438, 1493
- LC 2461, 2516
- LC 862

---

# Section 3: Binary Search

## Patterns covered

13. Exact Search with Boundaries  
14. Binary Search as a Sorted Lookup Tool  
15. Structural Binary Search  
16. Rotated Sorted Arrays  
17. Binary Search on Answer  
18. Counting Values at or Below a Candidate  

**Total: 50 questions**

---

## Pattern 13: Exact Search with Boundaries

1. **LC 704 — Binary Search**  
   Easy | P0  
   Focus: Canonical exact search.

2. **LC 35 — Search Insert Position**  
   Easy | P0  
   Focus: First position greater than or equal to target.

3. **LC 34 — Find First and Last Position of Element in Sorted Array**  
   Medium | P0  
   Focus: Lower and upper boundaries.

4. **LC 278 — First Bad Version**  
   Easy | P0  
   Focus: First-true binary search.

5. **LC 69 — Sqrt(x)**  
   Easy | P0  
   Focus: Last feasible integer and overflow safety.

6. **LC 367 — Valid Perfect Square**  
   Easy | P1  
   Focus: Exact numeric binary search.

7. **LC 744 — Find Smallest Letter Greater Than Target**  
   Easy | P1  
   Focus: Strict upper bound with wraparound.

8. **LC 374 — Guess Number Higher or Lower**  
   Easy | P1  
   Focus: Comparator-driven search.

9. **LC 2529 — Maximum Count of Positive Integer and Negative Integer**  
   Easy | P1  
   Focus: Lower-bound and upper-bound counting.

10. **LC 2089 — Find Target Indices After Sorting Array**  
    Easy | P2  
    Focus: Boundary positions after ordering.

---

## Pattern 14: Binary Search as a Sorted Lookup Tool

11. **LC 74 — Search a 2D Matrix**  
    Medium | P0  
    Focus: Treat a matrix as a flattened sorted array.

12. **LC 240 — Search a 2D Matrix II**  
    Medium | P0  
    Focus: Staircase elimination and row-wise search alternatives.

13. **LC 1539 — Kth Missing Positive Number**  
    Easy | P0  
    Focus: Missing-count function.

14. **LC 658 — Find K Closest Elements**  
    Medium | P0  
    Focus: Binary search for the best window start.

15. **LC 981 — Time Based Key-Value Store**  
    Medium | P0  
    Focus: Binary search in per-key timestamp histories.

16. **LC 1146 — Snapshot Array**  
    Medium | P1  
    Focus: Versioned values and historical lookup.

17. **LC 1150 — Check If a Number Is Majority Element in a Sorted Array**  
    Easy | P2 | Premium  
    Focus: Boundary positions and range length.

18. **LC 1060 — Missing Element in Sorted Array**  
    Medium | P1 | Premium  
    Focus: Binary search over accumulated missing values.

---

## Pattern 15: Structural Binary Search

19. **LC 162 — Find Peak Element**  
    Medium | P0  
    Focus: Using slope direction to retain a peak.

20. **LC 852 — Peak Index in a Mountain Array**  
    Medium | P0  
    Focus: Unimodal turning point.

21. **LC 1095 — Find in Mountain Array**  
    Hard | P1  
    Focus: Peak detection followed by two directional searches.

22. **LC 540 — Single Element in a Sorted Array**  
    Medium | P0  
    Focus: Pair-index parity invariant.

23. **LC 1901 — Find a Peak Element II**  
    Medium | P1  
    Focus: Column-based structural elimination.

24. **LC 4 — Median of Two Sorted Arrays**  
    Hard | P0 / Stretch  
    Focus: Partitioning two sorted arrays.

25. **LC 33 — Search in Rotated Sorted Array**  
    Medium | P0  
    Focus: Determining which half is sorted.

26. **LC 81 — Search in Rotated Sorted Array II**  
    Medium | P0  
    Focus: Duplicate ambiguity.

27. **LC 153 — Find Minimum in Rotated Sorted Array**  
    Medium | P0  
    Focus: Locating the rotation minimum.

28. **LC 154 — Find Minimum in Rotated Sorted Array II**  
    Hard | P1  
    Focus: Duplicate-safe minimum search.

---

## Pattern 17: Binary Search on Answer

29. **LC 875 — Koko Eating Bananas**  
    Medium | P0  
    Focus: Minimum feasible processing rate.

30. **LC 1011 — Capacity to Ship Packages Within D Days**  
    Medium | P0  
    Focus: Minimum feasible capacity.

31. **LC 410 — Split Array Largest Sum**  
    Hard | P0  
    Focus: Minimize the maximum partition sum.

32. **LC 1482 — Minimum Number of Days to Make m Bouquets**  
    Medium | P0  
    Focus: Minimum feasible day.

33. **LC 1552 — Magnetic Force Between Two Balls**  
    Medium | P0  
    Focus: Maximize the minimum separation.

34. **LC 1760 — Minimum Limit of Balls in a Bag**  
    Medium | P1  
    Focus: Minimum feasible maximum size.

35. **LC 2064 — Minimized Maximum of Products Distributed to Any Store**  
    Medium | P1  
    Focus: Minimize a maximum allocation.

36. **LC 2226 — Maximum Candies Allocated to K Children**  
    Medium | P1  
    Focus: Maximum feasible equal allocation.

37. **LC 1283 — Find the Smallest Divisor Given a Threshold**  
    Medium | P0  
    Focus: Minimum divisor satisfying a rounded-sum limit.

38. **LC 1870 — Minimum Speed to Arrive on Time**  
    Medium | P1  
    Focus: Feasibility with mixed rounded and real-valued time.

39. **LC 1898 — Maximum Number of Removable Characters**  
    Medium | P1  
    Focus: Maximum feasible removals while preserving a subsequence.

40. **LC 2141 — Maximum Running Time of N Computers**  
    Hard | Stretch  
    Focus: Resource-pooling feasibility.

41. **LC 774 — Minimize Max Distance to Gas Station**  
    Hard | P2 | Premium  
    Focus: Binary search over a real-valued answer.

42. **LC 1231 — Divide Chocolate**  
    Hard | P1 | Premium  
    Focus: Maximize the minimum partition value.

---

## Pattern 18: Count Values at or Below a Candidate

43. **LC 378 — Kth Smallest Element in a Sorted Matrix**  
    Medium | P0  
    Focus: Counting matrix values at most `mid`.

44. **LC 668 — Kth Smallest Number in Multiplication Table**  
    Hard | P0  
    Focus: Row-wise count at or below a candidate.

45. **LC 719 — Find K-th Smallest Pair Distance**  
    Hard | P0  
    Focus: Two-pointer counting of pairs within a distance.

46. **LC 786 — K-th Smallest Prime Fraction**  
    Medium | P1  
    Focus: Fraction counting or heap-based alternatives.

47. **LC 2040 — Kth Smallest Product of Two Sorted Arrays**  
    Hard | Stretch  
    Focus: Sign-aware counting of products.

48. **LC 1201 — Ugly Number III**  
    Medium | P1  
    Focus: Inclusion-exclusion counting under a candidate.

49. **LC 878 — Nth Magical Number**  
    Hard | P1  
    Focus: LCM-based counting.

50. **LC 1802 — Maximum Value at a Given Index in a Bounded Array**  
    Medium | P1  
    Focus: Feasibility using arithmetic-series bounds.

---

## Section 3 mastery checklist

You should be able to:

- Write exact search, first-true and last-true templates.
- Derive search bounds without guessing arbitrary values.
- Prevent midpoint and multiplication overflow.
- Distinguish index-domain search from answer-domain search.
- Prove that the feasibility predicate is monotonic.
- Handle duplicates in rotated arrays.
- Convert K-th-value problems into counting predicates.
- Search real-valued answers with a fixed iteration count or epsilon.

### P0 shortlist

- LC 4, 33, 34, 35, 69, 74
- LC 81, 153, 162, 240
- LC 278, 378, 410
- LC 540, 658, 668, 704, 719
- LC 852, 875, 981
- LC 1011, 1283, 1482, 1539, 1552

---

# Section 4: Intervals & Greedy

## Patterns covered

19. Interval Representation & Basic Manipulation  
20. Meeting & Occupancy Intervals  
21. Sweep-Line Events  
22. Interval Scheduling & Coverage  
23. Dynamic Interval Structures  
24. Direct Greedy Choices & Resource Invariance  
25. Reachability & Coverage Invariance  
26. Ordering & Constructive Strategies  
27. Scheduling with Heaps  
28. Advanced Greedy Transformations  

**Total: 60 questions**

---

## Pattern 19: Interval Representation & Manipulation

1. **LC 56 — Merge Intervals**  
   Medium | P0  
   Focus: Sort and merge overlapping intervals.

2. **LC 57 — Insert Interval**  
   Medium | P0  
   Focus: Before, overlap and after phases.

3. **LC 986 — Interval List Intersections**  
   Medium | P0  
   Focus: Two-list interval traversal.

4. **LC 228 — Summary Ranges**  
   Easy | P1  
   Focus: Consecutive-range construction.

5. **LC 163 — Missing Ranges**  
   Easy | P1 | Premium  
   Focus: Gap construction and boundary safety.

6. **LC 1288 — Remove Covered Intervals**  
   Medium | P0  
   Focus: Sorting by start ascending and end descending.

7. **LC 729 — My Calendar I**  
   Medium | P0  
   Focus: Detecting interval overlap.

8. **LC 731 — My Calendar II**  
   Medium | P1  
   Focus: Preventing triple overlap.

9. **LC 732 — My Calendar III**  
   Hard | Stretch  
   Focus: Maximum concurrent intervals.

---

## Pattern 20: Meetings & Occupancy

10. **LC 252 — Meeting Rooms**  
    Easy | P0 | Premium  
    Focus: Detecting overlap after sorting.

11. **LC 253 — Meeting Rooms II**  
    Medium | P0 | Premium  
    Focus: Minimum concurrent resources.

12. **LC 2402 — Meeting Rooms III**  
    Hard | P0 / Stretch  
    Focus: Available-room and occupied-room heaps.

13. **LC 1094 — Car Pooling**  
    Medium | P0  
    Focus: Occupancy through difference events.

14. **LC 1109 — Corporate Flight Bookings**  
    Medium | P1  
    Focus: Interval range additions.

15. **LC 1854 — Maximum Population Year**  
    Easy | P1  
    Focus: Difference-array occupancy.

16. **LC 1943 — Describe the Painting**  
    Medium | P1  
    Focus: Weighted event sweep.

17. **LC 2848 — Points That Intersect With Cars**  
    Easy | P2  
    Focus: Discrete interval union.

---

## Pattern 21: Sweep-Line Events

18. **LC 218 — The Skyline Problem**  
    Hard | P0 / Stretch  
    Focus: Event ordering and active-height multiset.

19. **LC 391 — Perfect Rectangle**  
    Hard | Stretch  
    Focus: Area, corner parity and sweep-line reasoning.

20. **LC 850 — Rectangle Area II**  
    Hard | Stretch  
    Focus: Sweep line with covered Y-length.

21. **LC 2251 — Number of Flowers in Full Bloom**  
    Hard | P0  
    Focus: Offline event or binary-search counting.

22. **LC 452 — Minimum Number of Arrows to Burst Balloons**  
    Medium | P0  
    Focus: Greedy intersection endpoints.

23. **LC 435 — Non-overlapping Intervals**  
    Medium | P0  
    Focus: Preserve the interval ending earliest.

24. **LC 646 — Maximum Length of Pair Chain**  
    Medium | P1  
    Focus: Interval scheduling.

---

## Pattern 22: Scheduling & Coverage

25. **LC 1024 — Video Stitching**  
    Medium | P0  
    Focus: Greedily extend the reachable boundary.

26. **LC 1326 — Minimum Number of Taps to Open to Water a Garden**  
    Hard | P0  
    Focus: Transform intervals into jump-style coverage.

27. **LC 45 — Jump Game II**  
    Medium | P0  
    Focus: Layered greedy coverage.

28. **LC 55 — Jump Game**  
    Medium | P0  
    Focus: Furthest reachable index.

29. **LC 134 — Gas Station**  
    Medium | P0  
    Focus: Total feasibility and candidate reset.

30. **LC 763 — Partition Labels**  
    Medium | P0  
    Focus: Close a partition at its furthest required endpoint.

31. **LC 678 — Valid Parenthesis String**  
    Medium | P0  
    Focus: Greedy lower and upper bounds.

32. **LC 330 — Patching Array**  
    Hard | Stretch  
    Focus: Maintain the complete representable range.

---

## Pattern 23: Dynamic Interval Structures

33. **LC 352 — Data Stream as Disjoint Intervals**  
    Hard | P1  
    Focus: Dynamically merging neighboring ranges.

34. **LC 715 — Range Module**  
    Hard | P0 / Stretch  
    Focus: Add, remove and query dynamic ranges.

35. **LC 436 — Find Right Interval**  
    Medium | P1  
    Focus: Ordered start-point lookup.

36. **LC 1272 — Remove Interval**  
    Medium | P1 | Premium  
    Focus: Interval subtraction.

---

## Pattern 24: Direct Greedy Choices

37. **LC 455 — Assign Cookies**  
    Easy | P0  
    Focus: Smallest sufficient resource.

38. **LC 860 — Lemonade Change**  
    Easy | P1  
    Focus: Preserve flexible denominations.

39. **LC 881 — Boats to Save People**  
    Medium | P0  
    Focus: Pair the heaviest person when possible.

40. **LC 1710 — Maximum Units on a Truck**  
    Easy | P1  
    Focus: Highest-value items first.

41. **LC 948 — Bag of Tokens**  
    Medium | P1  
    Focus: Exchange cheap resources for score and expensive score for power.

42. **LC 1005 — Maximize Sum of Array After K Negations**  
    Easy | P1  
    Focus: Consume the most beneficial sign changes first.

43. **LC 409 — Longest Palindrome**  
    Easy | P1  
    Focus: Maximize paired resource usage.

44. **LC 605 — Can Place Flowers**  
    Easy | P1  
    Focus: Safe local placement.

---

## Pattern 25: Reachability & Coverage Invariants

45. **LC 135 — Candy**  
    Hard | P0  
    Focus: Satisfy constraints from both directions.

46. **LC 406 — Queue Reconstruction by Height**  
    Medium | P0  
    Focus: Sort to neutralize future placement effects.

47. **LC 621 — Task Scheduler**  
    Medium | P0  
    Focus: Most-frequent-task lower bound.

48. **LC 659 — Split Array into Consecutive Subsequences**  
    Medium | P0  
    Focus: Extend existing sequences before creating new ones.

49. **LC 846 — Hand of Straights**  
    Medium | P0  
    Focus: Start groups from the smallest remaining value.

50. **LC 1296 — Divide Array in Sets of K Consecutive Numbers**  
    Medium | P1  
    Focus: Frequency-ordered group construction.

---

## Pattern 26: Ordering & Constructive Greedy

51. **LC 179 — Largest Number**  
    Medium | P0  
    Focus: Custom concatenation comparator.

52. **LC 316 — Remove Duplicate Letters**  
    Medium | P0  
    Focus: Lexicographically minimal monotonic construction.

53. **LC 738 — Monotone Increasing Digits**  
    Medium | P1  
    Focus: Repair the first order violation.

54. **LC 1505 — Minimum Possible Integer After at Most K Adjacent Swaps**  
    Hard | Stretch  
    Focus: Greedy digit choice with position accounting.

55. **LC 1663 — Smallest String With a Given Numeric Value**  
    Medium | P1  
    Focus: Reserve minimum value, then assign excess greedily.

56. **LC 2576 — Find the Maximum Number of Marked Indices**  
    Medium | P1  
    Focus: Sort and greedily pair small and large values.

---

## Pattern 27–28: Heap Scheduling & Advanced Transformations

57. **LC 630 — Course Schedule III**  
    Hard | P0  
    Focus: Replace the longest selected duration when necessary.

58. **LC 1642 — Furthest Building You Can Reach**  
    Medium | P0  
    Focus: Assign ladders to the largest climbs.

59. **LC 502 — IPO**  
    Hard | P0  
    Focus: Unlock feasible projects and select maximum profit.

60. **LC 857 — Minimum Cost to Hire K Workers**  
    Hard | Stretch  
    Focus: Sort by ratio and retain the smallest quality sum.

---

## Section 4 mastery checklist

You should be able to:

- Normalize closed and half-open interval conventions.
- Derive the exact overlap condition.
- Know when to sort by start and when to sort by end.
- Turn interval endpoints into sweep events.
- Define tie-breaking for events at the same coordinate.
- Prove earliest-finish-time interval scheduling.
- Maintain a furthest-reachable coverage invariant.
- Recognize replacement greedy patterns using a max-heap.
- Explain why a local greedy choice does not harm a future optimum.

### P0 shortlist

- LC 45, 55, 56, 57
- LC 134, 135, 179, 218
- LC 252, 253, 316, 406
- LC 435, 452, 502
- LC 621, 630, 659, 678
- LC 715, 729, 763
- LC 846, 881, 986
- LC 1024, 1094, 1288, 1326
- LC 1642, 2251, 2402

---

# Section 5: Linked Lists

## Patterns covered

29. Basic Traversal & Pointer Mechanics  
30. Cycle Detection  
31. Reversal & Structural Rewriting  
32. Deletion & Local Mutation  
33. Arithmetic, Merging & Sorting  
34. Lists with Additional Relationships  
35. Doubly Linked Lists & Stateful Design  

**Total: 50 questions**

---

## Pattern 29: Traversal & Pointer Mechanics

1. **LC 876 — Middle of the Linked List**  
   Easy | P0  
   Focus: Fast and slow pointers.

2. **LC 19 — Remove Nth Node From End of List**  
   Medium | P0  
   Focus: Fixed-distance two pointers and dummy nodes.

3. **LC 2095 — Delete the Middle Node of a Linked List**  
   Medium | P1  
   Focus: Middle detection with predecessor tracking.

4. **LC 328 — Odd Even Linked List**  
   Medium | P0  
   Focus: Splitting and reconnecting alternating positions.

5. **LC 725 — Split Linked List in Parts**  
   Medium | P1  
   Focus: Length calculation and balanced segmentation.

6. **LC 817 — Linked List Components**  
   Medium | P1  
   Focus: Counting connected runs.

7. **LC 2181 — Merge Nodes in Between Zeros**  
   Medium | P1  
   Focus: Segment accumulation and node reuse.

8. **LC 2807 — Insert Greatest Common Divisors in Linked List**  
   Medium | P2  
   Focus: Safe insertion during traversal.

---

## Pattern 30: Cycle Detection

9. **LC 141 — Linked List Cycle**  
   Easy | P0  
   Focus: Floyd’s tortoise-and-hare algorithm.

10. **LC 142 — Linked List Cycle II**  
    Medium | P0  
    Focus: Locating the cycle entry.

11. **LC 202 — Happy Number**  
    Easy | P1  
    Focus: Cycle detection in an implicit sequence.

12. **LC 287 — Find the Duplicate Number**  
    Medium | P0  
    Focus: Treating values as next pointers.

13. **LC 457 — Circular Array Loop**  
    Medium | P1  
    Focus: Direction-aware cycle detection.

---

## Pattern 31: Reversal & Structural Rewriting

14. **LC 206 — Reverse Linked List**  
    Easy | P0  
    Focus: Iterative and recursive reversal.

15. **LC 92 — Reverse Linked List II**  
    Medium | P0  
    Focus: Reversing an internal list segment.

16. **LC 25 — Reverse Nodes in k-Group**  
    Hard | P0 / Stretch  
    Focus: Repeated bounded-group reversal.

17. **LC 24 — Swap Nodes in Pairs**  
    Medium | P0  
    Focus: Local structural rewiring.

18. **LC 61 — Rotate List**  
    Medium | P0  
    Focus: Temporarily forming a cycle.

19. **LC 143 — Reorder List**  
    Medium | P0  
    Focus: Split, reverse and interleave.

20. **LC 234 — Palindrome Linked List**  
    Easy | P0  
    Focus: Reverse the second half and compare.

21. **LC 2130 — Maximum Twin Sum of a Linked List**  
    Medium | P1  
    Focus: Half reversal and paired traversal.

22. **LC 2074 — Reverse Nodes in Even Length Groups**  
    Medium | P2  
    Focus: Variable group boundaries.

23. **LC 1721 — Swapping Nodes in a Linked List**  
    Medium | P1  
    Focus: Symmetric positional lookup.

---

## Pattern 32: Deletion & Local Mutation

24. **LC 203 — Remove Linked List Elements**  
    Easy | P0  
    Focus: Sentinel-based repeated deletion.

25. **LC 83 — Remove Duplicates from Sorted List**  
    Easy | P0  
    Focus: Local duplicate skipping.

26. **LC 82 — Remove Duplicates from Sorted List II**  
    Medium | P0  
    Focus: Removing entire duplicate runs.

27. **LC 237 — Delete Node in a Linked List**  
    Medium | P1  
    Focus: Copy-next-node mutation.

28. **LC 1171 — Remove Zero Sum Consecutive Nodes from Linked List**  
    Medium | P0  
    Focus: Prefix sums over linked nodes.

29. **LC 2487 — Remove Nodes From Linked List**  
    Medium | P0  
    Focus: Reverse traversal or monotonic-stack reasoning.

30. **LC 1669 — Merge In Between Linked Lists**  
    Medium | P1  
    Focus: Cutting and splicing a list range.

31. **LC 3217 — Delete Nodes From Linked List Present in Array**  
    Medium | P1  
    Focus: Hash-set-guided deletion.

---

## Pattern 33: Arithmetic, Merging & Sorting

32. **LC 2 — Add Two Numbers**  
    Medium | P0  
    Focus: Digit arithmetic and carry propagation.

33. **LC 445 — Add Two Numbers II**  
    Medium | P0  
    Focus: Forward-order arithmetic using stacks or reversal.

34. **LC 21 — Merge Two Sorted Lists**  
    Easy | P0  
    Focus: Sentinel-based merge.

35. **LC 23 — Merge k Sorted Lists**  
    Hard | P0  
    Focus: Heap or divide-and-conquer merging.

36. **LC 148 — Sort List**  
    Medium | P0  
    Focus: Linked-list merge sort.

37. **LC 147 — Insertion Sort List**  
    Medium | P1  
    Focus: Sorted-position insertion.

38. **LC 86 — Partition List**  
    Medium | P0  
    Focus: Stable partition into two lists.

39. **LC 1019 — Next Greater Node In Linked List**  
    Medium | P1  
    Focus: Convert traversal order into monotonic-stack processing.

40. **LC 369 — Plus One Linked List**  
    Medium | P1 | Premium  
    Focus: Carry handling from the end.

41. **LC 1634 — Add Two Polynomials Represented as Linked Lists**  
    Medium | P2 | Premium  
    Focus: Merge by exponent.

---

## Pattern 34: Additional Relationships

42. **LC 138 — Copy List with Random Pointer**  
    Medium | P0  
    Focus: Hash mapping or interleaved-copy technique.

43. **LC 430 — Flatten a Multilevel Doubly Linked List**  
    Medium | P0  
    Focus: Flattening child relationships in place.

44. **LC 708 — Insert into a Sorted Circular Linked List**  
    Medium | P1 | Premium  
    Focus: Rotation boundary and all-equal cases.

45. **LC 160 — Intersection of Two Linked Lists**  
    Easy | P0  
    Focus: Pointer switching to equalize path lengths.

---

## Pattern 35: Doubly Linked Lists & Stateful Design

46. **LC 146 — LRU Cache**  
    Medium | P0  
    Focus: Hash map plus doubly linked list.

47. **LC 460 — LFU Cache**  
    Hard | P0 / Stretch  
    Focus: Key map, frequency buckets and recency lists.

48. **LC 707 — Design Linked List**  
    Medium | P1  
    Focus: Sentinel nodes and index-based operations.

49. **LC 641 — Design Circular Deque**  
    Medium | P1  
    Focus: Circular state and boundary management.

50. **LC 432 — All O`one Data Structure**  
    Hard | Stretch  
    Focus: Doubly linked frequency buckets and constant-time movement.

---

## Section 5 mastery checklist

You should be able to:

- Use a dummy head naturally.
- Draw pointer states before rewiring.
- Reverse a complete list and a bounded segment.
- Split a list into two halves correctly for even and odd lengths.
- Find the N-th node from the end in one pass.
- Explain Floyd’s cycle-entry proof.
- Merge lists without creating cycles or losing nodes.
- Implement linked-list merge sort.
- Copy random-pointer structures with and without extra space.
- Design an LRU cache from memory.
- Preserve head, tail, previous and next invariants in doubly linked lists.

### P0 shortlist

- LC 2, 19, 21, 23, 24, 25
- LC 61, 82, 83, 86, 92
- LC 138, 141, 142, 143, 146, 148
- LC 160, 203, 206, 234
- LC 287, 328, 430, 445, 460
- LC 876, 1171, 2487

---

# Recommended Completion Order

## Phase 1: Foundations

Complete these first:

### Sliding windows

- LC 643
- LC 1456
- LC 3
- LC 209
- LC 424
- LC 438
- LC 567
- LC 713
- LC 904
- LC 1004

### Binary search

- LC 704
- LC 35
- LC 34
- LC 69
- LC 278
- LC 74
- LC 153
- LC 162
- LC 33
- LC 875

### Intervals and greedy

- LC 56
- LC 57
- LC 986
- LC 252
- LC 253
- LC 435
- LC 452
- LC 55
- LC 45
- LC 134

### Linked lists

- LC 21
- LC 206
- LC 876
- LC 19
- LC 141
- LC 142
- LC 83
- LC 203
- LC 234
- LC 160

---

## Phase 2: Interview-standard variations

### Sliding windows

- LC 76
- LC 930
- LC 992
- LC 1248
- LC 1358
- LC 1423
- LC 1493
- LC 2461
- LC 2516

### Binary search

- LC 540
- LC 658
- LC 981
- LC 1011
- LC 1283
- LC 1482
- LC 1539
- LC 1552
- LC 378

### Intervals and greedy

- LC 218
- LC 406
- LC 621
- LC 630
- LC 659
- LC 678
- LC 715
- LC 729
- LC 763
- LC 1024
- LC 1326
- LC 1642

### Linked lists

- LC 2
- LC 23
- LC 24
- LC 61
- LC 82
- LC 86
- LC 92
- LC 138
- LC 143
- LC 148
- LC 328
- LC 445

---

## Phase 3: Google L5 advanced pass

1. LC 25 — Reverse Nodes in k-Group
2. LC 4 — Median of Two Sorted Arrays
3. LC 76 — Minimum Window Substring
4. LC 218 — The Skyline Problem
5. LC 239 — Sliding Window Maximum
6. LC 330 — Patching Array
7. LC 391 — Perfect Rectangle
8. LC 410 — Split Array Largest Sum
9. LC 432 — All O`one Data Structure
10. LC 460 — LFU Cache
11. LC 502 — IPO
12. LC 668 — Kth Smallest Number in Multiplication Table
13. LC 715 — Range Module
14. LC 719 — Find K-th Smallest Pair Distance
15. LC 732 — My Calendar III
16. LC 850 — Rectangle Area II
17. LC 857 — Minimum Cost to Hire K Workers
18. LC 862 — Shortest Subarray with Sum at Least K
19. LC 1095 — Find in Mountain Array
20. LC 1438 — Longest Continuous Subarray With Absolute Diff ≤ Limit
21. LC 2040 — Kth Smallest Product of Two Sorted Arrays
22. LC 2141 — Maximum Running Time of N Computers
23. LC 2402 — Meeting Rooms III

---

# Overall Completion Target

For Sections 2–5 combined:

- Solve at least **155 of the 200 questions**.
- Solve every accessible **P0** question.
- Re-solve at least **50 P0 questions** after a 10–14 day gap.
- Complete at least **15 Stretch problems**.
- Conduct mixed practice where the pattern name is hidden.

A strong final benchmark is:

- **Sliding window:** 20–25 minutes
- **Standard binary search:** 15–20 minutes
- **Binary search on answer:** 25–30 minutes
- **Standard interval/greedy:** 20–30 minutes
- **Standard linked list:** 20–25 minutes
- **Advanced hard problem:** 35–45 minutes with a correct explanation and implementation plan

The key improvement in this curriculum is scenario coverage. It includes not only canonical questions, but also complementary windows, exact-K counting, monotonic deques, structural binary search, K-th-value counting, sweep lines, dynamic intervals, heap-replacement greedy strategies, pointer rewiring, random relationships, and stateful linked-list design.# Sections 6–8: LeetCode Curriculum

This curriculum contains **150 questions**:

- **Section 6: Stacks & Queues — 55 questions**
- **Section 7: Recursion & Backtracking — 50 questions**
- **Section 8: Bit Manipulation — 45 questions**

The selection covers the full range of scenarios in your pattern sheet: stack reduction, parsing, monotonic structures, queue simulation, subset and permutation search, constrained construction, trie-assisted backtracking, XOR, bitmasks, binary construction, binary tries, and state-compressed DP.

LeetCode’s problem set currently includes dedicated classifications for stack, queue, monotonic stack, recursion, backtracking, bit manipulation, bitmask, trie, design, and simulation. 【1-a01405】【2-d0c088】【3-450a5c】【4-8d7272】【5-e02822】【6-7eab12】

## Priority legend

- **P0:** Master cold and re-solve from a blank editor.
- **P1:** Must solve independently.
- **P2:** Useful variation or comparatively lower-frequency scenario.
- **Stretch:** Advanced Google L5 boundary problem.
- **Premium:** Skip if inaccessible.

---

# Section 6: Stacks & Queues

## Patterns covered

36. Stack & Queue Fundamental Mechanics  
37. Adjacent Cancellation & Reduction  
38. Stack-Based Evaluation & Parsing  
39. Expression Parsing & Evaluation Trees  
40. Monotonic Stack Foundations  
41. Greedy Monotonic Stacks, Contributions & Histograms  
42. Stack & Queue Implementation  
43. Queue & Deque Simulation  
44. Monotonic Deque  
45. Specialized Stack & Iterator Design  

**Total: 55 questions**

---

## Pattern 36: Stack & Queue Fundamentals

1. **LC 20 — Valid Parentheses**  
   Easy | P0  
   Focus: Matching delimiters using a stack.

2. **LC 1047 — Remove All Adjacent Duplicates in String**  
   Easy | P0  
   Focus: Stack-based adjacent cancellation.

3. **LC 1544 — Make The String Great**  
   Easy | P1  
   Focus: Conditional adjacent cancellation.

4. **LC 844 — Backspace String Compare**  
   Easy | P0  
   Focus: Stack simulation and reverse two-pointer alternative.

5. **LC 682 — Baseball Game**  
   Easy | P1  
   Focus: Stack state with references to previous results.

6. **LC 1598 — Crawler Log Folder**  
   Easy | P2  
   Focus: Directory-depth stack simulation.

7. **LC 1700 — Number of Students Unable to Eat Lunch**  
   Easy | P1  
   Focus: Queue simulation and counting shortcut.

8. **LC 2073 — Time Needed to Buy Tickets**  
   Easy | P1  
   Focus: Queue simulation and direct counting.

---

## Pattern 37: Adjacent Cancellation & Reduction

9. **LC 1209 — Remove All Adjacent Duplicates in String II**  
   Medium | P0  
   Focus: Stack of character-frequency pairs.

10. **LC 2390 — Removing Stars From a String**  
    Medium | P0  
    Focus: Destructive stack operations.

11. **LC 735 — Asteroid Collision**  
    Medium | P0  
    Focus: Repeated collision resolution.

12. **LC 946 — Validate Stack Sequences**  
    Medium | P0  
    Focus: Simulating forced pops.

13. **LC 1249 — Minimum Remove to Make Valid Parentheses**  
    Medium | P0  
    Focus: Tracking unmatched parentheses.

14. **LC 921 — Minimum Add to Make Parentheses Valid**  
    Medium | P1  
    Focus: Unmatched opening and closing counts.

15. **LC 1963 — Minimum Number of Swaps to Make the String Balanced**  
    Medium | P1  
    Focus: Balance deficits and minimum correction.

16. **LC 856 — Score of Parentheses**  
    Medium | P1  
    Focus: Nested structural reduction.

17. **LC 1003 — Check If Word Is Valid After Substitutions**  
    Medium | P1  
    Focus: Repeated pattern reduction.

---

## Pattern 38: Evaluation & Parsing

18. **LC 150 — Evaluate Reverse Polish Notation**  
    Medium | P0  
    Focus: Operand ordering and postfix evaluation.

19. **LC 394 — Decode String**  
    Medium | P0  
    Focus: Nested parsing with count and string stacks.

20. **LC 71 — Simplify Path**  
    Medium | P0  
    Focus: Canonical path construction.

21. **LC 227 — Basic Calculator II**  
    Medium | P0  
    Focus: Operator precedence without parentheses.

22. **LC 224 — Basic Calculator**  
    Hard | P0  
    Focus: Parentheses, signs and recursive or stack parsing.

23. **LC 772 — Basic Calculator III**  
    Hard | Stretch | Premium  
    Focus: Parentheses and full arithmetic precedence.

24. **LC 636 — Exclusive Time of Functions**  
    Medium | P0  
    Focus: Call-stack simulation and timestamp boundaries.

25. **LC 726 — Number of Atoms**  
    Hard | Stretch  
    Focus: Nested grammar and multiplier propagation.

26. **LC 1106 — Parsing A Boolean Expression**  
    Hard | P1  
    Focus: Nested Boolean-expression reduction.

27. **LC 385 — Mini Parser**  
    Medium | P1  
    Focus: Recursive parsing of nested integer lists.

---

## Pattern 39: Expression Trees & Advanced Parsing

28. **LC 1597 — Build Binary Expression Tree From Infix Expression**  
    Hard | Stretch | Premium  
    Focus: Operator-precedence expression tree.

29. **LC 1628 — Design an Expression Tree With Evaluate Function**  
    Medium | P1 | Premium  
    Focus: Postfix expression-tree construction.

30. **LC 241 — Different Ways to Add Parentheses**  
    Medium | P0  
    Focus: Divide expressions and combine subresults.

31. **LC 439 — Ternary Expression Parser**  
    Medium | P1 | Premium  
    Focus: Right-associative expression parsing.

32. **LC 1087 — Brace Expansion**  
    Medium | P2 | Premium  
    Focus: Parsing choices and constructing combinations.

---

## Pattern 40: Monotonic Stack Foundations

33. **LC 496 — Next Greater Element I**  
    Easy | P0  
    Focus: Canonical next-greater-element stack.

34. **LC 503 — Next Greater Element II**  
    Medium | P0  
    Focus: Circular monotonic-stack traversal.

35. **LC 739 — Daily Temperatures**  
    Medium | P0  
    Focus: Next greater value by index distance.

36. **LC 1475 — Final Prices With a Special Discount in a Shop**  
    Easy | P1  
    Focus: Next smaller-or-equal element.

37. **LC 901 — Online Stock Span**  
    Medium | P0  
    Focus: Compressed previous-greater information.

38. **LC 1019 — Next Greater Node In Linked List**  
    Medium | P1  
    Focus: Monotonic processing after sequential traversal.

39. **LC 1944 — Number of Visible People in a Queue**  
    Hard | P1  
    Focus: Visibility and blocked monotonic relationships.

40. **LC 853 — Car Fleet**  
    Medium | P0  
    Focus: Sorted arrival-time stack.

---

## Pattern 41: Histograms, Contributions & Greedy Stacks

41. **LC 84 — Largest Rectangle in Histogram**  
    Hard | P0  
    Focus: Previous and next smaller boundaries.

42. **LC 85 — Maximal Rectangle**  
    Hard | P0  
    Focus: Repeated histogram reduction.

43. **LC 907 — Sum of Subarray Minimums**  
    Medium | P0  
    Focus: Per-element contribution and duplicate ownership.

44. **LC 2104 — Sum of Subarray Ranges**  
    Medium | P0  
    Focus: Maximum contribution minus minimum contribution.

45. **LC 316 — Remove Duplicate Letters**  
    Medium | P0  
    Focus: Lexicographically minimal greedy monotonic stack.

46. **LC 402 — Remove K Digits**  
    Medium | P0  
    Focus: Remove harmful preceding digits greedily.

47. **LC 456 — 132 Pattern**  
    Medium | P0  
    Focus: Reverse scan with a monotonic stack and middle candidate.

48. **LC 962 — Maximum Width Ramp**  
    Medium | P1  
    Focus: Candidate left boundaries and reverse matching.

---

## Pattern 42: Stack & Queue Implementation

49. **LC 225 — Implement Stack Using Queues**  
    Easy | P0  
    Focus: Rotating a queue to simulate LIFO.

50. **LC 232 — Implement Queue Using Stacks**  
    Easy | P0  
    Focus: Amortized two-stack queue.

51. **LC 622 — Design Circular Queue**  
    Medium | P1  
    Focus: Circular indexing and full/empty state.

52. **LC 641 — Design Circular Deque**  
    Medium | P1  
    Focus: Double-ended circular storage.

---

## Patterns 43–45: Deques, Specialized Stacks & Iterators

53. **LC 155 — Min Stack**  
    Medium | P0  
    Focus: Maintaining a secondary minimum invariant.

54. **LC 895 — Maximum Frequency Stack**  
    Hard | P0  
    Focus: Frequency buckets plus recency.

55. **LC 341 — Flatten Nested List Iterator**  
    Medium | P0  
    Focus: Lazy stack-based iterator traversal.

### Additional optional problems

- **LC 716 — Max Stack**
- **LC 1670 — Design Front Middle Back Queue**
- **LC 284 — Peeking Iterator**
- **LC 251 — Flatten 2D Vector**
- **LC 281 — Zigzag Iterator**
- **LC 239 — Sliding Window Maximum**
- **LC 862 — Shortest Subarray with Sum at Least K**
- **LC 1438 — Longest Continuous Subarray With Absolute Difference ≤ Limit**

These overlap with Sections 2 and 10, so they do not need to be counted twice.

---

## Section 6 mastery checklist

You should be able to:

- Recognize unresolved earlier elements as a stack signal.
- Implement next greater and next smaller templates.
- Choose strict versus non-strict comparisons for duplicates.
- Derive per-element contribution formulas.
- Parse nested structures safely.
- Distinguish operands from operators.
- Implement an amortized `O(1)` queue using two stacks.
- Implement lazy iterator traversal.
- Explain why elements removed from a monotonic structure never become useful again.
- Solve LC 84, 224, 316 and 907 from a blank editor.

### P0 shortlist

- LC 20, 71, 84, 85
- LC 150, 155, 224, 225, 227, 232
- LC 241, 316, 341, 394, 402
- LC 456, 496, 503, 636, 735, 739
- LC 853, 895, 901, 907, 946
- LC 1047, 1209, 1249, 2104, 2390

---

# Section 7: Recursion & Backtracking

## Patterns covered

46. Recursion & Backtracking Foundations  
47. Subsets & Combinations  
48. Permutations & Constructive Search  
49. Valid Sequence Construction & Grid Backtracking  
50. Graph & Trie-Assisted Backtracking  
51. Advanced Parsing & Expression Search  

**Total: 50 questions**

---

## Pattern 46: Recursion & Backtracking Foundations

1. **LC 509 — Fibonacci Number**  
   Easy | P1  
   Focus: Recursion tree, memoization and iterative conversion.

2. **LC 50 — Pow(x, n)**  
   Medium | P0  
   Focus: Divide-and-conquer recursion.

3. **LC 779 — K-th Symbol in Grammar**  
   Medium | P1  
   Focus: Recursive parent-state relationship.

4. **LC 390 — Elimination Game**  
   Medium | P2  
   Focus: Recursive direction and boundary transformation.

5. **LC 1545 — Find Kth Bit in Nth Binary String**  
   Medium | P1  
   Focus: Reflection and recursive index mapping.

6. **LC 894 — All Possible Full Binary Trees**  
   Medium | P1  
   Focus: Recursive structure generation and memoization.

---

## Pattern 47: Subsets & Combinations

7. **LC 78 — Subsets**  
   Medium | P0  
   Focus: Include/exclude and for-loop templates.

8. **LC 90 — Subsets II**  
   Medium | P0  
   Focus: Duplicate elimination after sorting.

9. **LC 77 — Combinations**  
   Medium | P0  
   Focus: Fixed-size selection.

10. **LC 39 — Combination Sum**  
    Medium | P0  
    Focus: Reusing the current candidate.

11. **LC 40 — Combination Sum II**  
    Medium | P0  
    Focus: Single use and same-level duplicate skipping.

12. **LC 216 — Combination Sum III**  
    Medium | P1  
    Focus: Bounded-value fixed-length combinations.

13. **LC 377 — Combination Sum IV**  
    Medium | P1  
    Focus: Recognizing when counting requires DP instead of enumeration.

14. **LC 491 — Non-decreasing Subsequences**  
    Medium | P1  
    Focus: Per-depth duplicate elimination without sorting.

15. **LC 17 — Letter Combinations of a Phone Number**  
    Medium | P0  
    Focus: Multi-choice recursive construction.

16. **LC 784 — Letter Case Permutation**  
    Medium | P1  
    Focus: Binary choices during construction.

---

## Pattern 48: Permutations & Constructive Search

17. **LC 46 — Permutations**  
    Medium | P0  
    Focus: Used-array and swap-based generation.

18. **LC 47 — Permutations II**  
    Medium | P0  
    Focus: Duplicate-sensitive permutation generation.

19. **LC 60 — Permutation Sequence**  
    Hard | P1  
    Focus: Factorial-group selection without generating all permutations.

20. **LC 31 — Next Permutation**  
    Medium | P0  
    Focus: Lexicographic successor construction.

21. **LC 526 — Beautiful Arrangement**  
    Medium | P1  
    Focus: Position-based pruning.

22. **LC 1079 — Letter Tile Possibilities**  
    Medium | P1  
    Focus: Frequency-based permutation generation.

23. **LC 1238 — Circular Permutation in Binary Representation**  
    Medium | P2  
    Focus: Gray-code construction.

24. **LC 1718 — Construct the Lexicographically Largest Valid Sequence**  
    Medium | P1  
    Focus: Placement constraints and descending-choice ordering.

---

## Pattern 49: Valid Sequences & Grid Backtracking

25. **LC 22 — Generate Parentheses**  
    Medium | P0  
    Focus: Prefix-valid sequence construction.

26. **LC 79 — Word Search**  
    Medium | P0  
    Focus: Grid DFS with temporary marking.

27. **LC 37 — Sudoku Solver**  
    Hard | P0  
    Focus: Constraint propagation and cell-choice ordering.

28. **LC 51 — N-Queens**  
    Hard | P0  
    Focus: Column and diagonal constraints.

29. **LC 52 — N-Queens II**  
    Hard | P1  
    Focus: Counting solutions and bitmask optimization.

30. **LC 1219 — Path with Maximum Gold**  
    Medium | P1  
    Focus: Grid-path enumeration with restoration.

31. **LC 980 — Unique Paths III**  
    Hard | P0  
    Focus: Visit-all-cells constraint.

32. **LC 1593 — Split a String Into the Max Number of Unique Substrings**  
    Medium | P1  
    Focus: Partition search with a uniqueness set.

33. **LC 1415 — The k-th Lexicographical String of All Happy Strings**  
    Medium | P1  
    Focus: Lexicographic generation and early termination.

---

## Pattern 50: Graph & Trie-Assisted Backtracking

34. **LC 212 — Word Search II**  
    Hard | P0  
    Focus: Trie pruning plus grid backtracking.

35. **LC 126 — Word Ladder II**  
    Hard | Stretch  
    Focus: BFS shortest layers followed by path reconstruction.

36. **LC 332 — Reconstruct Itinerary**  
    Hard | P0  
    Focus: Edge-consuming DFS and lexical ordering.

37. **LC 797 — All Paths From Source to Target**  
    Medium | P0  
    Focus: Path construction in a DAG.

38. **LC 638 — Shopping Offers**  
    Medium | P1  
    Focus: Memoized multidimensional decision search.

39. **LC 691 — Stickers to Spell Word**  
    Hard | Stretch  
    Focus: Frequency-state memoization and pruning.

40. **LC 473 — Matchsticks to Square**  
    Medium | P0  
    Focus: Symmetry pruning and capacity constraints.

41. **LC 698 — Partition to K Equal Sum Subsets**  
    Medium | P0  
    Focus: Bucket construction and duplicate-state pruning.

42. **LC 2305 — Fair Distribution of Cookies**  
    Medium | P1  
    Focus: Minimax bucket assignment and pruning.

---

## Pattern 51: Parsing & Expression Search

43. **LC 93 — Restore IP Addresses**  
    Medium | P0  
    Focus: Bounded string partitioning.

44. **LC 131 — Palindrome Partitioning**  
    Medium | P0  
    Focus: Partition search with palindrome validation.

45. **LC 282 — Expression Add Operators**  
    Hard | P0 / Stretch  
    Focus: Parsing operands and preserving multiplication precedence.

46. **LC 301 — Remove Invalid Parentheses**  
    Hard | Stretch  
    Focus: Minimum-removal search and duplicate output prevention.

47. **LC 842 — Split Array into Fibonacci Sequence**  
    Medium | P1  
    Focus: Numeric parsing, overflow and forced continuation.

48. **LC 306 — Additive Number**  
    Medium | P1  
    Focus: Enumerating initial numbers and validating the remainder.

49. **LC 967 — Numbers With Same Consecutive Differences**  
    Medium | P1  
    Focus: Digit-by-digit constructive search.

50. **LC 2698 — Find the Punishment Number of an Integer**  
    Medium | P2  
    Focus: Digit partitioning with a target sum.

---

## Section 7 mastery checklist

You should be able to define:

- The current state.
- The available choices.
- The validity condition.
- The base case.
- The undo operation.
- The duplicate-elimination rule.
- The pruning bound.
- The correct memoization key.

You should also be able to distinguish:

- Enumeration from counting.
- Backtracking from dynamic programming.
- Same-level duplicate elimination from global deduplication.
- Reusable candidates from single-use candidates.
- Grid marking from a separate visited structure.
- Path construction from reachability testing.

### P0 shortlist

- LC 17, 22, 31, 37, 39, 40
- LC 46, 47, 50, 51
- LC 77, 78, 79, 90, 93
- LC 131, 212, 282, 332
- LC 473, 698, 797, 980

### Hardest high-value problems

- LC 37 — Sudoku Solver
- LC 51 — N-Queens
- LC 126 — Word Ladder II
- LC 212 — Word Search II
- LC 282 — Expression Add Operators
- LC 301 — Remove Invalid Parentheses
- LC 691 — Stickers to Spell Word
- LC 698 — Partition to K Equal Sum Subsets

---

# Section 8: Bit Manipulation

## Patterns covered

52. Binary Representation Fundamentals  
53. Carry & Arithmetic  
54. XOR Calculation & Cancellation  
55. Prefix XOR & Reconstruction  
56. Range & Aggregate Bitwise Operations  
57. Binary Construction  
58. Binary Tries  
59. Bitmask Dynamic Programming  

**Total: 45 questions**

---

## Pattern 52: Binary Representation Fundamentals

1. **LC 191 — Number of 1 Bits**  
   Easy | P0  
   Focus: Bit scanning and `n & (n - 1)`.

2. **LC 338 — Counting Bits**  
   Easy | P0  
   Focus: Reuse results from smaller numbers.

3. **LC 190 — Reverse Bits**  
   Easy | P0  
   Focus: Fixed-width bit extraction and construction.

4. **LC 231 — Power of Two**  
   Easy | P0  
   Focus: Single-set-bit test.

5. **LC 342 — Power of Four**  
   Easy | P1  
   Focus: Single bit restricted to valid positions.

6. **LC 326 — Power of Three**  
   Easy | P2  
   Focus: Contrast arithmetic tests with bit-specific tests.

7. **LC 461 — Hamming Distance**  
   Easy | P0  
   Focus: XOR followed by popcount.

8. **LC 2220 — Minimum Bit Flips to Convert Number**  
   Easy | P1  
   Focus: Count differing bit positions.

9. **LC 693 — Binary Number with Alternating Bits**  
   Easy | P1  
   Focus: Shifted XOR patterns.

10. **LC 762 — Prime Number of Set Bits in Binary Representation**  
    Easy | P2  
    Focus: Popcount classification.

---

## Pattern 53: Carry & Arithmetic

11. **LC 371 — Sum of Two Integers**  
    Medium | P0  
    Focus: XOR as sum and AND-shift as carry.

12. **LC 29 — Divide Two Integers**  
    Medium | P0  
    Focus: Shift-based quotient construction and overflow handling.

13. **LC 67 — Add Binary**  
    Easy | P0  
    Focus: Explicit carry propagation.

14. **LC 989 — Add to Array-Form of Integer**  
    Easy | P1  
    Focus: Variable-length carry propagation.

15. **LC 405 — Convert a Number to Hexadecimal**  
    Easy | P1  
    Focus: Fixed-width representation of negative values.

16. **LC 89 — Gray Code**  
    Medium | P0  
    Focus: `i XOR (i >> 1)` construction.

---

## Pattern 54: XOR Cancellation

17. **LC 136 — Single Number**  
    Easy | P0  
    Focus: Pair cancellation.

18. **LC 137 — Single Number II**  
    Medium | P0  
    Focus: Bit counts modulo three or finite-state masks.

19. **LC 260 — Single Number III**  
    Medium | P0  
    Focus: Partition using the lowest differing bit.

20. **LC 268 — Missing Number**  
    Easy | P0  
    Focus: XOR of indices and values.

21. **LC 389 — Find the Difference**  
    Easy | P1  
    Focus: XOR cancellation across two strings.

22. **LC 1442 — Count Triplets That Can Form Two Arrays of Equal XOR**  
    Medium | P0  
    Focus: Equal prefix-XOR relationships.

23. **LC 1486 — XOR Operation in an Array**  
    Easy | P2  
    Focus: Direct XOR accumulation.

24. **LC 1720 — Decode XORed Array**  
    Easy | P0  
    Focus: Reconstruct values from adjacent XOR.

---

## Pattern 55: Prefix XOR & Reconstruction

25. **LC 1310 — XOR Queries of a Subarray**  
    Medium | P0  
    Focus: Prefix XOR range queries.

26. **LC 1734 — Decode XORed Permutation**  
    Medium | P1  
    Focus: Aggregate XOR and parity-index reconstruction.

27. **LC 1829 — Maximum XOR for Each Query**  
    Medium | P1  
    Focus: Iterative aggregate XOR and bounded complement.

28. **LC 2433 — Find The Original Array of Prefix XOR**  
    Medium | P0  
    Focus: Inverting prefix XOR.

29. **LC 2997 — Minimum Number of Operations to Make Array XOR Equal to K**  
    Medium | P1  
    Focus: Compare aggregate XOR with the target.

30. **LC 2429 — Minimize XOR**  
    Medium | P1  
    Focus: Preserve high-value shared bits, then fill low bits.

---

## Pattern 56: Range & Aggregate Bitwise Operations

31. **LC 201 — Bitwise AND of Numbers Range**  
    Medium | P0  
    Focus: Common binary prefix.

32. **LC 477 — Total Hamming Distance**  
    Medium | P0  
    Focus: Per-bit zero-one contribution.

33. **LC 898 — Bitwise ORs of Subarrays**  
    Medium | P0  
    Focus: Compress distinct OR states ending at each position.

34. **LC 1521 — Find a Value of a Mysterious Function Closest to Target**  
    Hard | Stretch  
    Focus: Compress distinct AND states over subarrays.

35. **LC 2411 — Smallest Subarrays With Maximum Bitwise OR**  
    Medium | P1  
    Focus: Track the latest occurrence of each bit.

36. **LC 2275 — Largest Combination With Bitwise AND Greater Than Zero**  
    Medium | P1  
    Focus: Count values containing each bit.

---

## Pattern 57: Binary Construction

37. **LC 421 — Maximum XOR of Two Numbers in an Array**  
    Medium | P0  
    Focus: Greedy prefix sets or a binary trie.

38. **LC 1707 — Maximum XOR With an Element From Array**  
    Hard | P0 / Stretch  
    Focus: Offline sorting plus binary-trie queries.

39. **LC 2935 — Maximum Strong Pair XOR II**  
    Hard | Stretch  
    Focus: Sliding constraints with a removable binary trie.

40. **LC 1238 — Circular Permutation in Binary Representation**  
    Medium | P1  
    Focus: Rotated Gray-code construction.

---

## Pattern 58–59: Bitmasks & Bitmask DP

41. **LC 473 — Matchsticks to Square**  
    Medium | P1  
    Focus: Subset-state search and symmetry.

42. **LC 698 — Partition to K Equal Sum Subsets**  
    Medium | P0  
    Focus: Used-mask search and memoization.

43. **LC 1125 — Smallest Sufficient Team**  
    Hard | P0  
    Focus: Skills represented as a bitmask.

44. **LC 847 — Shortest Path Visiting All Nodes**  
    Hard | P0  
    Focus: Multi-source BFS over `(node, visitedMask)`.

45. **LC 943 — Find the Shortest Superstring**  
    Hard | Stretch  
    Focus: Subset DP with last-string state and reconstruction.

---

## Additional optional bitmask-DP problems

These are highly valuable if you want stronger advanced coverage:

- **LC 464 — Can I Win**
- **LC 526 — Beautiful Arrangement**
- **LC 691 — Stickers to Spell Word**
- **LC 996 — Number of Squareful Arrays**
- **LC 1066 — Campus Bikes II**
- **LC 1255 — Maximum Score Words Formed by Letters**
- **LC 1349 — Maximum Students Taking Exam**
- **LC 1434 — Number of Ways to Wear Different Hats to Each Other**
- **LC 1494 — Parallel Courses II**
- **LC 1655 — Distribute Repeating Integers**
- **LC 1681 — Minimum Incompatibility**
- **LC 1723 — Find Minimum Time to Finish All Jobs**
- **LC 1799 — Maximize Score After N Operations**
- **LC 1879 — Minimum XOR Sum of Two Arrays**
- **LC 1986 — Minimum Number of Work Sessions to Finish the Tasks**
- **LC 2172 — Maximum AND Sum of Array**
- **LC 2305 — Fair Distribution of Cookies**

These overlap with DP and memoized decision search, so solve them during Section 8 or Section 13, but do not count them twice.

---

## Section 8 mastery checklist

You should be able to:

- Test, set, clear, toggle and extract a bit.
- Remove the lowest set bit.
- Isolate the lowest set bit.
- Count bits efficiently.
- Explain pair cancellation through XOR.
- Separate two unique values using a distinguishing bit.
- Derive prefix-XOR range queries.
- Explain why range AND keeps only the shared prefix.
- Calculate per-bit contributions.
- Build and query a binary trie.
- Encode a subset as a bitmask.
- Iterate through all submasks of a mask.
- Design DP over `(mask, last)` or `(mask, position)`.
- Reconstruct the selected solution from bitmask DP.

### P0 shortlist

- LC 29, 67, 89
- LC 1125
- LC 136, 137, 190, 191, 201
- LC 231, 260, 268, 338, 371
- LC 421, 461, 477
- LC 698, 847, 898
- LC 1310, 1442, 1707, 1720, 2433

---

# Recommended Completion Order

## Phase 1: Fundamentals

### Stacks and queues

1. LC 20
2. LC 1047
3. LC 844
4. LC 150
5. LC 71
6. LC 496
7. LC 739
8. LC 225
9. LC 232
10. LC 155
11. LC 946
12. LC 1209

### Recursion and backtracking

1. LC 50
2. LC 17
3. LC 78
4. LC 77
5. LC 39
6. LC 40
7. LC 46
8. LC 47
9. LC 22
10. LC 79
11. LC 93
12. LC 131

### Bit manipulation

1. LC 191
2. LC 338
3. LC 231
4. LC 461
5. LC 136
6. LC 268
7. LC 67
8. LC 371
9. LC 201
10. LC 1310
11. LC 1720
12. LC 2433

---

## Phase 2: Interview-standard variations

### Stacks and queues

- LC 84
- LC 85
- LC 224
- LC 227
- LC 316
- LC 394
- LC 402
- LC 456
- LC 503
- LC 636
- LC 735
- LC 853
- LC 901
- LC 907
- LC 1249

### Recursion and backtracking

- LC 37
- LC 51
- LC 52
- LC 60
- LC 90
- LC 212
- LC 241
- LC 332
- LC 473
- LC 526
- LC 638
- LC 698
- LC 797
- LC 980
- LC 1219

### Bit manipulation

- LC 29
- LC 89
- LC 137
- LC 260
- LC 421
- LC 477
- LC 698
- LC 847
- LC 898
- LC 1125
- LC 1442
- LC 1707
- LC 1734
- LC 1829
- LC 2429

---

## Phase 3: Google L5 advanced pass

1. **LC 37 — Sudoku Solver**
2. **LC 51 — N-Queens**
3. **LC 84 — Largest Rectangle in Histogram**
4. **LC 85 — Maximal Rectangle**
5. **LC 126 — Word Ladder II**
6. **LC 212 — Word Search II**
7. **LC 224 — Basic Calculator**
8. **LC 282 — Expression Add Operators**
9. **LC 301 — Remove Invalid Parentheses**
10. **LC 332 — Reconstruct Itinerary**
11. **LC 432 — All O`one Data Structure**
12. **LC 691 — Stickers to Spell Word**
13. **LC 698 — Partition to K Equal Sum Subsets**
14. **LC 726 — Number of Atoms**
15. **LC 772 — Basic Calculator III**
16. **LC 847 — Shortest Path Visiting All Nodes**
17. **LC 895 — Maximum Frequency Stack**
18. **LC 907 — Sum of Subarray Minimums**
19. **LC 943 — Find the Shortest Superstring**
20. **LC 1125 — Smallest Sufficient Team**
21. **LC 1597 — Build Binary Expression Tree**
22. **LC 1707 — Maximum XOR With an Element From Array**
23. **LC 1944 — Number of Visible People in a Queue**
24. **LC 2104 — Sum of Subarray Ranges**
25. **LC 2935 — Maximum Strong Pair XOR II**

---

# Combined Completion Target

For Sections 6–8:

- Solve at least **115 of the 150 primary questions**.
- Solve every accessible **P0** question.
- Re-solve at least **35 P0 questions** after a 10–14 day gap.
- Complete at least **12 Stretch problems**.
- Implement immutable templates from memory for:
  - Monotonic stack
  - Histogram boundaries
  - Recursive-descent expression parsing
  - Subsets
  - Permutations
  - Combination Sum
  - Grid backtracking
  - Binary trie
  - Bitmask DP
- Practice mixed sets where the underlying pattern is hidden.

## Strong final benchmark

- Standard stack problem: **15–20 minutes**
- Monotonic-stack problem: **20–30 minutes**
- Standard backtracking problem: **20–30 minutes**
- Advanced constrained search: **35–45 minutes**
- Standard XOR/bit problem: **15–25 minutes**
- Binary-trie problem: **25–35 minutes**
- Bitmask-DP problem: **35–45 minutes**

The most important conceptual progression is:

1. **Stack stores unresolved earlier state.**
2. **Backtracking explores choices while restoring state.**
3. **Bitmasks compress sets and Boolean state.**
4. **Memoization turns repeated backtracking states into DP.**
5. **Monotonic structures discard states that can never become optimal.**
6. **Tries greedily select the best opposing bit for XOR optimization.**# Section 9: Trees, BSTs & Tries

## Strict Google L5 Preparation Curriculum

Section 9 is large enough that a short list would leave important gaps. The curriculum below contains **130 primary questions**, plus optional extensions, covering all 17 patterns in your sheet:

60. Trees & BSTs — Basic Traversals  
61. Structural Comparison & Transformation  
62. Height-Based Post-Order Patterns  
63. Breadth-First Tree Traversal  
64. Root-to-Leaf Paths  
65. Ancestors, Distances & Relationships  
66. Tree Construction  
67. Serialization & Subtree Identity  
68. Binary Search Tree Fundamentals  
69. In-Order as Sorted-Order Processing  
70. BST Queries & Iterators  
71. Advanced BST Construction & Counting  
72. Trie Foundations  
73. Flexible & Approximate Search  
74. Prefix Ranking & Suggestions  
75. Prefix & Suffix Relationships  
76. Trie-Assisted Search & Hierarchical Structures  

The current <Organization>LeetCode</Organization> problem catalogue contains hundreds of tree and BFS/DFS problems, along with dedicated Binary Tree, BST and Trie classifications. For strict preparation, merely completing traversal questions is insufficient. You need structural recursion, path-state reasoning, tree construction, serialization, BST invariants, iterative traversal, trie design and composite search. 【1-c2aba1】【2-855619】【3-c34427】【4-866a14】

---

# Priority Legend

- **P0:** Master cold. Derive and implement without assistance.
- **P1:** Must solve independently after standard preparation.
- **P2:** Important variation, but lower expected frequency.
- **Stretch:** Advanced boundary for strict L5 preparation.
- **Premium:** Skip if inaccessible, or find an equivalent version.

---

# Pattern 60: Basic Tree Traversals

These establish recursive DFS, iterative DFS, stack frames, traversal order and N-ary tree handling.

## Core binary-tree traversal

1. **LC 144 — Binary Tree Preorder Traversal**  
   Easy | P0  
   Focus: Recursive and iterative root-left-right traversal.

2. **LC 94 — Binary Tree Inorder Traversal**  
   Easy | P0  
   Focus: Recursive traversal and explicit-stack simulation.

3. **LC 145 — Binary Tree Postorder Traversal**  
   Easy | P0  
   Focus: Recursive, two-stack and one-stack approaches.

4. **LC 102 — Binary Tree Level Order Traversal**  
   Medium | P0  
   Focus: Queue-based BFS and level boundaries.

5. **LC 104 — Maximum Depth of Binary Tree**  
   Easy | P0  
   Focus: Recursive return values and BFS alternative.

6. **LC 111 — Minimum Depth of Binary Tree**  
   Easy | P0  
   Focus: Correct handling of one-child nodes.

7. **LC 226 — Invert Binary Tree**  
   Easy | P0  
   Focus: Preorder, postorder and BFS structural mutation.

8. **LC 222 — Count Complete Tree Nodes**  
   Easy | P0  
   Focus: Basic traversal and complete-tree height optimization.

9. **LC 965 — Univalued Binary Tree**  
   Easy | P1  
   Focus: Global-value validation.

10. **LC 872 — Leaf-Similar Trees**  
    Easy | P1  
    Focus: Extracting traversal-derived sequences.

## N-ary traversal

11. **LC 589 — N-ary Tree Preorder Traversal**  
    Easy | P1  
    Focus: Child-order preservation in iterative traversal.

12. **LC 590 — N-ary Tree Postorder Traversal**  
    Easy | P1  
    Focus: Postorder over variable-degree nodes.

13. **LC 559 — Maximum Depth of N-ary Tree**  
    Easy | P1  
    Focus: Generalizing binary recursion.

14. **LC 429 — N-ary Tree Level Order Traversal**  
    Medium | P1  
    Focus: BFS over arbitrary child counts.

## Advanced traversal mechanics

15. **LC 114 — Flatten Binary Tree to Linked List**  
    Medium | P0  
    Focus: Reverse preorder, tail returns and iterative rewiring.

16. **LC 897 — Increasing Order Search Tree**  
    Easy | P1  
    Focus: Inorder reconstruction into a right-only tree.

17. **LC 156 — Binary Tree Upside Down**  
    Medium | P1 | Premium  
    Focus: Recursive structural rewiring.

18. **LC 536 — Construct Binary Tree from String**  
    Medium | P1 | Premium  
    Focus: Parsing combined with recursive construction.

### Mastery requirements

You should be able to write from memory:

- Recursive preorder, inorder and postorder.
- Iterative preorder and inorder.
- One-stack iterative postorder.
- BFS with a captured level size.
- Morris inorder traversal conceptually.
- DFS using explicit stack frames containing node and processing state.

---

# Pattern 61: Structural Comparison & Transformation

These questions ask whether two trees have the same shape, can be transformed into one another, or satisfy a recursive structural property.

19. **LC 100 — Same Tree**  
    Easy | P0  
    Focus: Simultaneous recursion over two trees.

20. **LC 101 — Symmetric Tree**  
    Easy | P0  
    Focus: Mirror-node comparison.

21. **LC 951 — Flip Equivalent Binary Trees**  
    Medium | P0  
    Focus: Matching with swapped and non-swapped child arrangements.

22. **LC 572 — Subtree of Another Tree**  
    Easy | P0  
    Focus: Candidate-root search plus structural equality.

23. **LC 617 — Merge Two Binary Trees**  
    Easy | P1  
    Focus: Structural combination with absent-node handling.

24. **LC 814 — Binary Tree Pruning**  
    Medium | P0  
    Focus: Postorder deletion based on subtree information.

25. **LC 1325 — Delete Leaves With a Given Value**  
    Medium | P0  
    Focus: Repeated leaf deletion naturally handled by postorder.

26. **LC 669 — Trim a Binary Search Tree**  
    Medium | P0  
    Focus: Structural pruning using the BST ordering invariant.

27. **LC 2331 — Evaluate Boolean Binary Tree**  
    Easy | P1  
    Focus: Recursive expression-tree evaluation.

28. **LC 2415 — Reverse Odd Levels of Binary Tree**  
    Medium | P1  
    Focus: Symmetric pair traversal or level-value replacement.

29. **LC 951 — Flip Equivalent Binary Trees**  
    Medium | P0  
    Focus: Exploring equivalent structural alignments.

30. **LC 971 — Flip Binary Tree To Match Preorder Traversal**  
    Medium | P1  
    Focus: Guided structural decisions using a target traversal.

### Strict-interview concern

For every structural comparison, decide whether the state is:

- One node.
- A pair of nodes.
- A node plus a target position.
- A node plus an external sequence index.
- A subtree property returned upward.

---

# Pattern 62: Height-Based Postorder Patterns

This is one of the highest-value tree families. The child subtrees are solved first, and the parent combines their returned information.

## Height and balance

31. **LC 110 — Balanced Binary Tree**  
    Easy | P0  
    Focus: Return height or a failure sentinel.

32. **LC 543 — Diameter of Binary Tree**  
    Easy | P0  
    Focus: Downward height versus through-node answer.

33. **LC 124 — Binary Tree Maximum Path Sum**  
    Hard | P0  
    Focus: Best downward gain versus globally best path.

34. **LC 687 — Longest Univalue Path**  
    Medium | P0  
    Focus: Extend only compatible child paths.

35. **LC 1372 — Longest ZigZag Path in a Binary Tree**  
    Medium | P0  
    Focus: Direction-specific downward states.

36. **LC 1026 — Maximum Difference Between Node and Ancestor**  
    Medium | P0  
    Focus: Carry ancestor extrema downward or aggregate extrema upward.

37. **LC 563 — Binary Tree Tilt**  
    Easy | P1  
    Focus: Return subtree sum and accumulate local differences.

38. **LC 129 — Sum Root to Leaf Numbers**  
    Medium | P0  
    Focus: Path-number state.

39. **LC 1339 — Maximum Product of Splitted Binary Tree**  
    Medium | P1  
    Focus: Subtree sums and global total.

40. **LC 1038 — Binary Search Tree to Greater Sum Tree**  
    Medium | P0  
    Focus: Reverse inorder cumulative state.

## Subtree aggregation

41. **LC 508 — Most Frequent Subtree Sum**  
    Medium | P1  
    Focus: Postorder aggregation with frequency counting.

42. **LC 366 — Find Leaves of Binary Tree**  
    Medium | P0 | Premium  
    Focus: Classify nodes by distance from the lowest leaf.

43. **LC 250 — Count Univalue Subtrees**  
    Medium | P1 | Premium  
    Focus: Boolean subtree validation and counting.

44. **LC 333 — Largest BST Subtree**  
    Medium | P0 | Premium  
    Focus: Return BST validity, range and size.

45. **LC 1373 — Maximum Sum BST in Binary Tree**  
    Hard | P0  
    Focus: Composite postorder state containing validity, range and sum.

46. **LC 968 — Binary Tree Cameras**  
    Hard | P0  
    Focus: Three-state greedy postorder DP.

47. **LC 979 — Distribute Coins in Binary Tree**  
    Medium | P0  
    Focus: Subtree surplus and movement cost.

48. **LC 337 — House Robber III**  
    Medium | P0  
    Focus: Return take and skip states.

49. **LC 1457 — Pseudo-Palindromic Paths in a Binary Tree**  
    Medium | P1  
    Focus: Parity mask along root-to-leaf paths.

50. **LC 2458 — Height of Binary Tree After Subtree Removal Queries**  
    Hard | Stretch  
    Focus: Subtree heights, depth levels and outside-subtree alternatives.

### Essential postorder distinction

For each question, explicitly identify:

1. What is returned to the parent?
2. What is the answer passing through the current node?
3. Is there a separate global answer?
4. Can failure be encoded as a sentinel?
5. Does the returned state need height, sum, range, count or several fields?
6. Can the answer be computed in one postorder traversal?

---

# Pattern 63: Breadth-First Tree Traversal

These cover levels, views, width, completeness, parent links and horizontal ordering.

51. **LC 102 — Binary Tree Level Order Traversal**  
    Medium | P0  
    Focus: Canonical level-order traversal.

52. **LC 107 — Binary Tree Level Order Traversal II**  
    Medium | P1  
    Focus: Reversing level output.

53. **LC 103 — Binary Tree Zigzag Level Order Traversal**  
    Medium | P0  
    Focus: Directional level construction.

54. **LC 199 — Binary Tree Right Side View**  
    Medium | P0  
    Focus: Last node of every BFS level or right-first DFS.

55. **LC 515 — Find Largest Value in Each Tree Row**  
    Medium | P1  
    Focus: Per-level aggregation.

56. **LC 637 — Average of Levels in Binary Tree**  
    Easy | P1  
    Focus: Numeric level aggregation.

57. **LC 116 — Populating Next Right Pointers in Each Node**  
    Medium | P0  
    Focus: Perfect-tree next-pointer traversal.

58. **LC 117 — Populating Next Right Pointers in Each Node II**  
    Medium | P0  
    Focus: Constant-space construction over sparse levels.

59. **LC 662 — Maximum Width of Binary Tree**  
    Medium | P0  
    Focus: Normalized complete-tree indices.

60. **LC 958 — Check Completeness of a Binary Tree**  
    Medium | P0  
    Focus: No non-null node after the first missing child.

61. **LC 1609 — Even Odd Tree**  
    Medium | P1  
    Focus: Per-level parity and ordering constraints.

62. **LC 1302 — Deepest Leaves Sum**  
    Medium | P1  
    Focus: Final-level aggregation.

63. **LC 1161 — Maximum Level Sum of a Binary Tree**  
    Medium | P1  
    Focus: Level numbering and maximum sum.

64. **LC 993 — Cousins in Binary Tree**  
    Easy | P1  
    Focus: Equal depth with different parents.

65. **LC 863 — All Nodes Distance K in Binary Tree**  
    Medium | P0  
    Focus: Convert the tree into an undirected neighborhood graph.

66. **LC 314 — Binary Tree Vertical Order Traversal**  
    Medium | P1 | Premium  
    Focus: BFS with horizontal coordinates.

67. **LC 987 — Vertical Order Traversal of a Binary Tree**  
    Hard | P0  
    Focus: Row, column and value tie-breaking.

---

# Pattern 64: Root-to-Leaf Paths

These require careful distinction between:

- Path state.
- Path existence.
- Path enumeration.
- Path counting.
- Prefix-state counting.
- Leaf-only versus any-node endpoints.

68. **LC 112 — Path Sum**  
    Easy | P0  
    Focus: Root-to-leaf existence.

69. **LC 113 — Path Sum II**  
    Medium | P0  
    Focus: Root-to-leaf path enumeration with backtracking.

70. **LC 437 — Path Sum III**  
    Medium | P0  
    Focus: Prefix-sum hashing over root-to-current paths.

71. **LC 257 — Binary Tree Paths**  
    Easy | P1  
    Focus: String-based path construction.

72. **LC 129 — Sum Root to Leaf Numbers**  
    Medium | P0  
    Focus: Incremental numeric path state.

73. **LC 988 — Smallest String Starting From Leaf**  
    Medium | P1  
    Focus: Reverse path representation and lexicographic comparison.

74. **LC 1022 — Sum of Root To Leaf Binary Numbers**  
    Easy | P1  
    Focus: Binary-value accumulation.

75. **LC 1448 — Count Good Nodes in Binary Tree**  
    Medium | P0  
    Focus: Path maximum passed downward.

76. **LC 1457 — Pseudo-Palindromic Paths in a Binary Tree**  
    Medium | P0  
    Focus: Parity mask and one-set-bit test.

77. **LC 1530 — Number of Good Leaf Nodes Pairs**  
    Medium | P0  
    Focus: Return leaf distances and count cross-subtree pairs.

78. **LC 2096 — Step-By-Step Directions From a Binary Tree Node to Another**  
    Medium | P0  
    Focus: Paths to nodes, LCA and direction conversion.

79. **LC 666 — Path Sum IV**  
    Medium | P2 | Premium  
    Focus: Implicit tree representation.

80. **LC 298 — Binary Tree Longest Consecutive Sequence**  
    Medium | P1 | Premium  
    Focus: Parent-child path-state propagation.

81. **LC 549 — Binary Tree Longest Consecutive Sequence II**  
    Medium | Stretch | Premium  
    Focus: Increasing and decreasing paths joined at a node.

---

# Pattern 65: Ancestors, Distances & Relationships

## Lowest common ancestor

82. **LC 236 — Lowest Common Ancestor of a Binary Tree**  
    Medium | P0  
    Focus: Bottom-up recursive LCA.

83. **LC 235 — Lowest Common Ancestor of a Binary Search Tree**  
    Medium | P0  
    Focus: Use ordered branching.

84. **LC 1644 — Lowest Common Ancestor of a Binary Tree II**  
    Medium | P0 | Premium  
    Focus: Verify that both target nodes exist.

85. **LC 1650 — Lowest Common Ancestor of a Binary Tree III**  
    Medium | P1 | Premium  
    Focus: Parent-pointer intersection.

86. **LC 1676 — Lowest Common Ancestor of a Binary Tree IV**  
    Medium | P1 | Premium  
    Focus: Generalize LCA to a target set.

87. **LC 1740 — Find Distance in a Binary Tree**  
    Medium | P1 | Premium  
    Focus: LCA plus individual depths.

## Relationship queries

88. **LC 863 — All Nodes Distance K in Binary Tree**  
    Medium | P0  
    Focus: Parent mapping or distance-returning DFS.

89. **LC 2385 — Amount of Time for Binary Tree to Be Infected**  
    Medium | P0  
    Focus: Graph conversion or diameter-style recursion.

90. **LC 742 — Closest Leaf in a Binary Tree**  
    Medium | P1 | Premium  
    Focus: Parent links and multi-direction BFS.

91. **LC 993 — Cousins in Binary Tree**  
    Easy | P1  
    Focus: Parent and depth relationships.

92. **LC 1261 — Find Elements in a Contaminated Binary Tree**  
    Medium | P1  
    Focus: Reconstruct implicit node values and support membership lookup.

93. **LC 2277 — Closest Node to Path in Tree**  
    Hard | Stretch | Premium  
    Focus: LCA relationships and path-distance queries.

### Strict L5 extension

For one-off LCA queries, recursive LCA is enough. For repeated queries, know:

- Parent and depth preprocessing.
- Binary lifting.
- Euler tour plus RMQ conceptually.
- Distance formula:

`distance(u, v) = depth[u] + depth[v] - 2 × depth[lca(u, v)]`

Binary lifting is formally included in your later Section 18, but the conceptual connection should be understood here.

---

# Pattern 66: Tree Construction

Construction questions test whether you understand exactly what information makes a tree uniquely recoverable.

94. **LC 105 — Construct Binary Tree from Preorder and Inorder Traversal**  
    Medium | P0  
    Focus: Root selection and inorder partitioning.

95. **LC 106 — Construct Binary Tree from Inorder and Postorder Traversal**  
    Medium | P0  
    Focus: Reverse root processing and interval boundaries.

96. **LC 889 — Construct Binary Tree from Preorder and Postorder Traversal**  
    Medium | P0  
    Focus: Non-unique reconstruction and subtree sizing.

97. **LC 1008 — Construct Binary Search Tree from Preorder Traversal**  
    Medium | P0  
    Focus: Bounds-driven linear construction.

98. **LC 654 — Maximum Binary Tree**  
    Medium | P0  
    Focus: Recursive maximum partition and monotonic-stack optimization.

99. **LC 998 — Maximum Binary Tree II**  
    Medium | P1  
    Focus: Right-spine insertion.

100. **LC 1028 — Recover a Tree From Preorder Traversal**  
     Hard | P0  
     Focus: Depth-encoded parsing.

101. **LC 2196 — Create Binary Tree From Descriptions**  
     Medium | P0  
     Focus: Node creation, child attachment and root identification.

102. **LC 108 — Convert Sorted Array to Binary Search Tree**  
     Easy | P0  
     Focus: Balanced divide-and-conquer construction.

103. **LC 109 — Convert Sorted List to Binary Search Tree**  
     Medium | P0  
     Focus: Slow/fast splitting or simulated inorder construction.

104. **LC 1382 — Balance a Binary Search Tree**  
     Medium | P1  
     Focus: Inorder extraction followed by balanced construction.

105. **LC 536 — Construct Binary Tree from String**  
     Medium | P1 | Premium  
     Focus: Recursive parsing and negative values.

106. **LC 1628 — Design an Expression Tree With Evaluate Function**  
     Medium | P1 | Premium  
     Focus: Build a tree from postfix notation.

### Construction mastery requirements

For every traversal-construction problem, explain:

- Where the root comes from.
- How the left-subtree size is determined.
- Whether values are unique.
- Whether reconstruction is unique.
- How to avoid copying subarrays.
- Whether an index map reduces complexity.
- Whether recursion depth can reach `O(n)`.

---

# Pattern 67: Serialization & Subtree Identity

107. **LC 297 — Serialize and Deserialize Binary Tree**  
     Hard | P0  
     Focus: Preserve structure using null markers.

108. **LC 449 — Serialize and Deserialize BST**  
     Medium | P0  
     Focus: Compact serialization using BST bounds.

109. **LC 652 — Find Duplicate Subtrees**  
     Medium | P0  
     Focus: Canonical subtree IDs or serialized signatures.

110. **LC 428 — Serialize and Deserialize N-ary Tree**  
     Hard | P1 | Premium  
     Focus: Encode variable child counts.

111. **LC 431 — Encode N-ary Tree to Binary Tree**  
     Hard | Stretch | Premium  
     Focus: Left-child/right-sibling representation.

112. **LC 606 — Construct String from Binary Tree**  
     Easy | P1  
     Focus: Minimal parentheses while preserving structure.

113. **LC 1948 — Delete Duplicate Folders in System**  
     Hard | Stretch  
     Focus: Hierarchical trie serialization and duplicate-subtree removal.

114. **LC 572 — Subtree of Another Tree**  
     Easy | P0  
     Focus: Structural equality; serialization or tree hashing alternatives.

### Serialization failure cases

Your encoding must distinguish:

- A missing left child from a missing right child.
- Negative and multi-digit values.
- Delimiter collisions.
- Duplicate node values.
- An empty tree.
- Skewed trees.
- N-ary nodes with zero versus several children.

For subtree identity, prefer assigning an integer ID to each tuple:

`(node value, left subtree ID, right subtree ID)`

This avoids repeatedly constructing long serialization strings.

---

# Pattern 68: Binary Search Tree Fundamentals

115. **LC 98 — Validate Binary Search Tree**  
     Medium | P0  
     Focus: Strict lower/upper bounds or inorder ordering.

116. **LC 700 — Search in a Binary Search Tree**  
     Easy | P0  
     Focus: Ordered traversal.

117. **LC 701 — Insert into a Binary Search Tree**  
     Medium | P0  
     Focus: Preserve the BST invariant.

118. **LC 450 — Delete Node in a BST**  
     Medium | P0  
     Focus: Leaf, one-child and two-child deletion.

119. **LC 669 — Trim a Binary Search Tree**  
     Medium | P0  
     Focus: Entire discarded subtrees.

120. **LC 235 — Lowest Common Ancestor of a BST**  
     Medium | P0  
     Focus: Split-point reasoning.

121. **LC 938 — Range Sum of BST**  
     Easy | P0  
     Focus: Pruning by value range.

122. **LC 783 — Minimum Distance Between BST Nodes**  
     Easy | P1  
     Focus: Adjacent inorder values.

123. **LC 530 — Minimum Absolute Difference in BST**  
     Easy | P1  
     Focus: Previous inorder value.

124. **LC 653 — Two Sum IV — Input is a BST**  
     Easy | P0  
     Focus: Hashing, inorder two pointers or dual iterators.

125. **LC 1373 — Maximum Sum BST in Binary Tree**  
     Hard | P0  
     Focus: BST validation within an arbitrary binary tree.

### Critical validation warning

Do not validate a BST by checking only:

`node.left.val < node.val < node.right.val`

The ordering condition applies to the entire left and right subtrees. Use:

- Recursive lower and upper bounds.
- Strictly increasing inorder traversal.
- Postorder subtree ranges.

Also handle integer boundaries without unsafe sentinel assumptions.

---

# Pattern 69: Inorder as Sorted-Order Processing

126. **LC 230 — Kth Smallest Element in a BST**  
     Medium | P0  
     Focus: Stop inorder traversal at the K-th value.

127. **LC 173 — Binary Search Tree Iterator**  
     Medium | P0  
     Focus: Controlled inorder traversal with `O(h)` state.

128. **LC 99 — Recover Binary Search Tree**  
     Medium | P0  
     Focus: Detect one or two inorder inversions.

129. **LC 501 — Find Mode in Binary Search Tree**  
     Easy | P1  
     Focus: Run-length counting in sorted order.

130. **LC 897 — Increasing Order Search Tree**  
     Easy | P1  
     Focus: Rebuild while processing sorted values.

131. **LC 1038 — Binary Search Tree to Greater Sum Tree**  
     Medium | P0  
     Focus: Reverse inorder accumulation.

132. **LC 538 — Convert BST to Greater Tree**  
     Medium | P1  
     Focus: Same reverse-inorder invariant.

133. **LC 1305 — All Elements in Two Binary Search Trees**  
     Medium | P0  
     Focus: Merge two sorted inorder streams.

134. **LC 1214 — Two Sum BSTs**  
     Medium | P1 | Premium  
     Focus: Search one BST using values from another.

135. **LC 1932 — Merge BSTs to Create Single BST**  
     Hard | Stretch  
     Focus: Leaf-root matching plus global-bound validation.

### Required mental model

Inorder traversal of a valid BST is a sorted stream. Once you see that, ask whether the problem becomes:

- K-th element selection.
- Adjacent-value comparison.
- Two-pointer search.
- Stream merging.
- Run-length counting.
- Prefix or suffix accumulation.
- Detection of ordering inversions.

---

# Pattern 70: BST Queries & Iterators

136. **LC 173 — Binary Search Tree Iterator**  
     Medium | P0  
     Focus: Lazy `O(h)` iterator.

137. **LC 1586 — Binary Search Tree Iterator II**  
     Medium | P1 | Premium  
     Focus: Bidirectional iterator with history.

138. **LC 285 — Inorder Successor in BST**  
     Medium | P0 | Premium  
     Focus: Successor candidate while searching.

139. **LC 510 — Inorder Successor in BST II**  
     Medium | P1 | Premium  
     Focus: Parent-pointer successor.

140. **LC 270 — Closest Binary Search Tree Value**  
     Easy | P0 | Premium  
     Focus: Ordered descent with closest candidate.

141. **LC 272 — Closest Binary Search Tree Value II**  
     Hard | Stretch | Premium  
     Focus: Predecessor and successor stacks.

142. **LC 938 — Range Sum of BST**  
     Easy | P0  
     Focus: Range-pruned traversal.

143. **LC 2476 — Closest Nodes Queries in a Binary Search Tree**  
     Medium | P0  
     Focus: Inorder array plus lower and upper bounds.

144. **LC 653 — Two Sum IV — Input is a BST**  
     Easy | P0  
     Focus: Set-based search or two directional iterators.

145. **LC 1305 — All Elements in Two Binary Search Trees**  
     Medium | P0  
     Focus: Simultaneous lazy inorder iteration.

### Iterator mastery

Implement:

- `pushLeft(node)`
- `next()`
- `hasNext()`

Then generalize to:

- Reverse inorder.
- Predecessor iterator.
- Successor iterator.
- Two-iterator Two Sum without flattening the entire tree.
- Bidirectional iteration with cached history.

---

# Pattern 71: Advanced BST Construction & Counting

146. **LC 95 — Unique Binary Search Trees II**  
     Medium | P0  
     Focus: Construct all root-left-right combinations.

147. **LC 96 — Unique Binary Search Trees**  
     Medium | P0  
     Focus: Catalan recurrence.

148. **LC 1569 — Number of Ways to Reorder Array to Get Same BST**  
     Hard | Stretch  
     Focus: Recursive left/right partitioning and combinatorics.

149. **LC 315 — Count of Smaller Numbers After Self**  
     Hard | P0  
     Focus: Augmented BST, merge sort or Fenwick tree.

150. **LC 220 — Contains Duplicate III**  
     Hard | P0  
     Focus: Ordered-set predecessor/successor queries.

151. **LC 493 — Reverse Pairs**  
     Hard | P1  
     Focus: Ordered counting, merge sort or augmented BST.

152. **LC 1649 — Create Sorted Array through Instructions**  
     Hard | Stretch  
     Focus: Counts of smaller and larger values.

153. **LC 1008 — Construct BST from Preorder Traversal**  
     Medium | P0  
     Focus: Bounds and monotonic construction.

154. **LC 449 — Serialize and Deserialize BST**  
     Medium | P0  
     Focus: Reconstruction using ordered bounds.

155. **LC 1382 — Balance a Binary Search Tree**  
     Medium | P1  
     Focus: Sorted inorder values and balanced rebuilding.

### Strict L5 expectation

Understand augmentation even if you implement the final solution with a Fenwick tree:

- `subtreeSize`
- Number of duplicates
- Rank of a value
- K-th smallest retrieval
- Count less than a candidate
- Count in a value range

You should be able to explain why an unbalanced plain BST can degrade to `O(n)` per operation.

---

# Pattern 72: Trie Foundations

156. **LC 208 — Implement Trie (Prefix Tree)**  
     Medium | P0  
     Focus: Insert, exact search and prefix search.

157. **LC 211 — Design Add and Search Words Data Structure**  
     Medium | P0  
     Focus: Wildcard branching.

158. **LC 648 — Replace Words**  
     Medium | P0  
     Focus: Stop at the shortest matching prefix.

159. **LC 677 — Map Sum Pairs**  
     Medium | P0  
     Focus: Prefix aggregation and value updates.

160. **LC 1268 — Search Suggestions System**  
     Medium | P0  
     Focus: Prefix traversal plus lexicographic top-K suggestions.

161. **LC 720 — Longest Word in Dictionary**  
     Medium | P1  
     Focus: Every prefix must be a valid word.

162. **LC 1804 — Implement Trie II (Prefix Tree)**  
     Medium | P0 | Premium  
     Focus: Exact counts, prefix counts and erase.

163. **LC 1858 — Longest Word With All Prefixes**  
     Medium | P1 | Premium  
     Focus: Valid-prefix chain.

164. **LC 2416 — Sum of Prefix Scores of Strings**  
     Hard | P0  
     Focus: Prefix frequency counts.

165. **LC 3043 — Find the Length of the Longest Common Prefix**  
     Medium | P1  
     Focus: Numeric-string trie or prefix hashing.

### Trie implementation checklist

Each node may need:

- Child references.
- End-of-word flag.
- Number of words ending at the node.
- Number of words passing through the node.
- Aggregate prefix value.
- Stored candidates or top-K suggestions.
- Index or metadata associated with a word.

Know the tradeoffs between:

- Fixed-size child arrays.
- Hash maps.
- Compressed edges.
- Storing results at every node.
- Generating results through bounded DFS.

---

# Pattern 73: Flexible & Approximate Search

166. **LC 211 — Design Add and Search Words Data Structure**  
     Medium | P0  
     Focus: Dot wildcard matching.

167. **LC 676 — Implement Magic Dictionary**  
     Medium | P0  
     Focus: Exactly one character modification.

168. **LC 820 — Short Encoding of Words**  
     Medium | P0  
     Focus: Reverse trie and suffix elimination.

169. **LC 1023 — Camelcase Matching**  
     Medium | P1  
     Focus: Structured subsequence matching.

170. **LC 745 — Prefix and Suffix Search**  
     Hard | P0  
     Focus: Combined prefix-suffix trie keys.

171. **LC 425 — Word Squares**  
     Hard | P0 | Premium  
     Focus: Prefix-indexed candidate generation.

172. **LC 212 — Word Search II**  
     Hard | P0  
     Focus: Trie-guided grid search and branch pruning.

173. **LC 336 — Palindrome Pairs**  
     Hard | Stretch  
     Focus: Trie or hashing with palindrome remainders.

174. **LC 1032 — Stream of Characters**  
     Hard | P0  
     Focus: Reverse trie over a bounded suffix stream.

175. **LC 3093 — Longest Common Suffix Queries**  
     Hard | P1  
     Focus: Reverse trie with tie-breaking metadata.

### Approximate-search state

A flexible trie search may need:

- Current trie node.
- Position in the query.
- Number of edits used.
- Search direction.
- Grid coordinates.
- Visited state.
- Remaining prefix or suffix.
- Candidate ranking state.

Control exponential branching by pruning immediately when:

- A child does not exist.
- The edit budget is exceeded.
- No words remain under a trie node.
- The current path cannot beat the best result.
- The required prefix is absent.

---

# Pattern 74: Prefix Ranking & Suggestions

176. **LC 1268 — Search Suggestions System**  
     Medium | P0  
     Focus: Top three lexicographic suggestions for each prefix.

177. **LC 642 — Design Search Autocomplete System**  
     Hard | P0 | Premium  
     Focus: Frequency ranking, lexical tie-breaking and online updates.

178. **LC 677 — Map Sum Pairs**  
     Medium | P0  
     Focus: Mutable prefix-score aggregation.

179. **LC 2416 — Sum of Prefix Scores of Strings**  
     Hard | P0  
     Focus: Count strings sharing each prefix.

180. **LC 1898-style prefix ranking variants**  
     Optional  
     Focus: Keep ranking data near prefix nodes when query frequency is high.

181. **LC 588 — Design In-Memory File System**  
     Hard | P0 | Premium  
     Focus: Hierarchical trie with lexical listing.

182. **LC 1166 — Design File System**  
     Medium | P1 | Premium  
     Focus: Path validation and parent existence.

183. **LC 1233 — Remove Sub-Folders from the Filesystem**  
     Medium | P0  
     Focus: Terminal folder nodes stop deeper traversal.

184. **LC 1948 — Delete Duplicate Folders in System**  
     Hard | Stretch  
     Focus: Canonical signatures for hierarchical structures.

### Ranking design questions

Be prepared to discuss:

- Store top-K candidates at every node or compute them on demand?
- How are rankings updated after insertion?
- How are ties broken?
- Can deleted or stale candidates remain lazily?
- What is the memory cost of duplicating top-K lists?
- What changes when queries vastly outnumber updates?

---

# Pattern 75: Prefix & Suffix Relationships

185. **LC 745 — Prefix and Suffix Search**  
     Hard | P0  
     Focus: Combined-key trie or dual tries plus index sets.

186. **LC 820 — Short Encoding of Words**  
     Medium | P0  
     Focus: Reverse words to convert suffixes into prefixes.

187. **LC 3045 — Count Prefix and Suffix Pairs II**  
     Hard | Stretch  
     Focus: Paired-character trie or border reasoning.

188. **LC 3042 — Count Prefix and Suffix Pairs I**  
     Easy | P1  
     Focus: Fundamental prefix-and-suffix relation.

189. **LC 3093 — Longest Common Suffix Queries**  
     Hard | P1  
     Focus: Reverse trie with shortest-index tie-breaking.

190. **LC 336 — Palindrome Pairs**  
     Hard | Stretch  
     Focus: Prefix/suffix palindrome decomposition.

191. **LC 1032 — Stream of Characters**  
     Hard | P0  
     Focus: Match recent stream suffixes using a reverse trie.

192. **LC 2088-style prefix/suffix variants**  
     Optional  
     Focus: Recognize when reversing strings converts suffix queries into prefix queries.

### Required transformation

When the question asks about suffixes, immediately consider:

- Reverse every word.
- Use a standard prefix trie afterward.
- Store original indices or metadata.
- Limit retained stream length to the longest dictionary word.

---

# Pattern 76: Trie-Assisted Search & Hierarchical Structures

193. **LC 212 — Word Search II**  
     Hard | P0  
     Focus: Trie plus grid DFS.

194. **LC 425 — Word Squares**  
     Hard | P0 | Premium  
     Focus: Prefix-generated backtracking candidates.

195. **LC 472 — Concatenated Words**  
     Hard | P0  
     Focus: Trie or word-break search with multiple component words.

196. **LC 140 — Word Break II**  
     Hard | P0  
     Focus: Trie-assisted sentence construction with memoization.

197. **LC 139 — Word Break**  
     Medium | P0  
     Focus: Trie-guided segmentation DP.

198. **LC 648 — Replace Words**  
     Medium | P0  
     Focus: Shortest terminal prefix.

199. **LC 588 — Design In-Memory File System**  
     Hard | P0 | Premium  
     Focus: Hierarchical path trie.

200. **LC 1166 — Design File System**  
     Medium | P1 | Premium  
     Focus: Path hierarchy and parent validation.

201. **LC 1233 — Remove Sub-Folders from the Filesystem**  
     Medium | P0  
     Focus: Terminal nodes dominate descendants.

202. **LC 1948 — Delete Duplicate Folders in System**  
     Hard | Stretch  
     Focus: Trie plus canonical subtree serialization.

203. **LC 1268 — Search Suggestions System**  
     Medium | P0  
     Focus: Retrieval from prefix nodes.

204. **LC 642 — Design Search Autocomplete System**  
     Hard | P0 | Premium  
     Focus: Stateful ranking and updates.

205. **LC 1804 — Implement Trie II**  
     Medium | P0 | Premium  
     Focus: Mutable multiplicities.

206. **LC 676 — Implement Magic Dictionary**  
     Medium | P0  
     Focus: Limited-edit trie search.

207. **LC 677 — Map Sum Pairs**  
     Medium | P0  
     Focus: Prefix aggregation with overwritten keys.

---

# Deduplicated Primary Curriculum

Several questions intentionally appear under multiple patterns because they teach multiple invariants. For example:

- LC 212 belongs to both backtracking and trie-assisted search.
- LC 1373 belongs to both postorder aggregation and advanced BST validation.
- LC 863 belongs to BFS and ancestor/relationship modeling.
- LC 1038 belongs to BST transformation and reverse inorder.
- LC 1948 belongs to serialization and hierarchical tries.

After deduplication, this curriculum contains approximately **130 unique primary problems**.

Do not solve duplicate entries twice during the initial pass. Revisit them later under the second conceptual lens.

---

# Strict P0 Core: Master Cold

These are the questions I would require for strict L5 readiness.

## Tree traversal and structure

- LC 94 — Binary Tree Inorder Traversal
- LC 98 — Validate Binary Search Tree
- LC 100 — Same Tree
- LC 101 — Symmetric Tree
- LC 102 — Binary Tree Level Order Traversal
- LC 103 — Binary Tree Zigzag Level Order Traversal
- LC 104 — Maximum Depth of Binary Tree
- LC 105 — Construct Tree from Preorder and Inorder
- LC 106 — Construct Tree from Inorder and Postorder
- LC 110 — Balanced Binary Tree
- LC 114 — Flatten Binary Tree to Linked List
- LC 116 — Populating Next Right Pointers
- LC 117 — Populating Next Right Pointers II
- LC 124 — Binary Tree Maximum Path Sum
- LC 144 — Preorder Traversal
- LC 145 — Postorder Traversal
- LC 199 — Binary Tree Right Side View
- LC 226 — Invert Binary Tree

## Paths and relationships

- LC 112 — Path Sum
- LC 113 — Path Sum II
- LC 129 — Sum Root to Leaf Numbers
- LC 236 — Lowest Common Ancestor
- LC 437 — Path Sum III
- LC 543 — Diameter of Binary Tree
- LC 863 — All Nodes Distance K
- LC 987 — Vertical Order Traversal
- LC 1448 — Count Good Nodes
- LC 1530 — Number of Good Leaf Node Pairs
- LC 2096 — Directions From One Node to Another
- LC 2385 — Time to Infect a Binary Tree

## Tree DP and postorder aggregation

- LC 337 — House Robber III
- LC 687 — Longest Univalue Path
- LC 968 — Binary Tree Cameras
- LC 979 — Distribute Coins
- LC 1026 — Maximum Difference Between Node and Ancestor
- LC 1339 — Maximum Product of Split Binary Tree
- LC 1372 — Longest ZigZag Path
- LC 1373 — Maximum Sum BST

## Construction and serialization

- LC 108 — Sorted Array to BST
- LC 109 — Sorted List to BST
- LC 297 — Serialize and Deserialize Binary Tree
- LC 449 — Serialize and Deserialize BST
- LC 652 — Find Duplicate Subtrees
- LC 654 — Maximum Binary Tree
- LC 889 — Construct Tree from Preorder and Postorder
- LC 1008 — BST from Preorder
- LC 1028 — Recover Tree from Preorder
- LC 2196 — Create Binary Tree from Descriptions

## BST

- LC 95 — Unique BSTs II
- LC 96 — Unique BSTs
- LC 99 — Recover BST
- LC 173 — BST Iterator
- LC 230 — Kth Smallest in BST
- LC 235 — LCA of BST
- LC 450 — Delete Node in BST
- LC 653 — Two Sum IV
- LC 669 — Trim BST
- LC 700 — Search in BST
- LC 701 — Insert into BST
- LC 938 — Range Sum of BST
- LC 1038 — BST to Greater Sum Tree
- LC 1305 — Merge Elements from Two BSTs

## Trie and hierarchical search

- LC 139 — Word Break
- LC 140 — Word Break II
- LC 208 — Implement Trie
- LC 211 — Add and Search Word
- LC 212 — Word Search II
- LC 336 — Palindrome Pairs
- LC 425 — Word Squares
- LC 472 — Concatenated Words
- LC 588 — In-Memory File System
- LC 642 — Autocomplete System
- LC 648 — Replace Words
- LC 676 — Magic Dictionary
- LC 677 — Map Sum Pairs
- LC 745 — Prefix and Suffix Search
- LC 820 — Short Encoding of Words
- LC 1032 — Stream of Characters
- LC 1233 — Remove Sub-Folders
- LC 1268 — Search Suggestions System
- LC 1804 — Implement Trie II
- LC 1948 — Delete Duplicate Folders
- LC 2416 — Sum of Prefix Scores

---

# Recommended Study Order

## Phase 1: Traversal fluency

Complete first:

1. LC 104
2. LC 100
3. LC 101
4. LC 226
5. LC 94
6. LC 144
7. LC 145
8. LC 102
9. LC 199
10. LC 111
11. LC 112
12. LC 257

Goal: recursion and traversal mechanics should require almost no conscious effort.

---

## Phase 2: Postorder information flow

1. LC 110
2. LC 543
3. LC 687
4. LC 563
5. LC 337
6. LC 979
7. LC 1372
8. LC 124
9. LC 968
10. LC 1373

Goal: distinguish the value returned upward from the globally accumulated answer.

---

## Phase 3: Paths and relationships

1. LC 113
2. LC 129
3. LC 437
4. LC 1448
5. LC 1457
6. LC 236
7. LC 863
8. LC 1530
9. LC 2096
10. LC 2385

Goal: choose correctly among backtracking, prefix hashing, LCA, graph conversion and postorder distance aggregation.

---

## Phase 4: Construction and serialization

1. LC 105
2. LC 106
3. LC 108
4. LC 109
5. LC 654
6. LC 889
7. LC 1008
8. LC 1028
9. LC 297
10. LC 449
11. LC 652

Goal: understand what information uniquely identifies structure.

---

## Phase 5: BST mastery

1. LC 98
2. LC 700
3. LC 701
4. LC 450
5. LC 230
6. LC 235
7. LC 173
8. LC 99
9. LC 653
10. LC 938
11. LC 1038
12. LC 1305
13. LC 95
14. LC 96

Goal: use ordering for pruning, streaming and construction rather than treating a BST as a generic tree.

---

## Phase 6: Trie foundations

1. LC 208
2. LC 211
3. LC 648
4. LC 677
5. LC 720
6. LC 820
7. LC 1268
8. LC 1804
9. LC 2416

Goal: confidently change trie-node metadata to fit a new API.

---

## Phase 7: Trie-assisted composite search

1. LC 212
2. LC 425
3. LC 472
4. LC 745
5. LC 1032
6. LC 1233
7. LC 1948
8. LC 336
9. LC 642
10. LC 588

Goal: combine tries with backtracking, ranking, serialization and hierarchical design.

---

# Advanced Google L5 Final Set

Complete these under timed conditions after finishing the main curriculum:

1. **LC 99 — Recover Binary Search Tree**
2. **LC 124 — Binary Tree Maximum Path Sum**
3. **LC 140 — Word Break II**
4. **LC 212 — Word Search II**
5. **LC 220 — Contains Duplicate III**
6. **LC 297 — Serialize and Deserialize Binary Tree**
7. **LC 336 — Palindrome Pairs**
8. **LC 425 — Word Squares**
9. **LC 431 — Encode N-ary Tree to Binary Tree**
10. **LC 449 — Serialize and Deserialize BST**
11. **LC 472 — Concatenated Words**
12. **LC 588 — Design In-Memory File System**
13. **LC 642 — Design Search Autocomplete System**
14. **LC 652 — Find Duplicate Subtrees**
15. **LC 745 — Prefix and Suffix Search**
16. **LC 863 — All Nodes Distance K**
17. **LC 968 — Binary Tree Cameras**
18. **LC 987 — Vertical Order Traversal**
19. **LC 1028 — Recover a Tree From Preorder Traversal**
20. **LC 1032 — Stream of Characters**
21. **LC 1373 — Maximum Sum BST**
22. **LC 1530 — Number of Good Leaf Node Pairs**
23. **LC 1569 — Number of Ways to Reorder Array to Get Same BST**
24. **LC 1932 — Merge BSTs to Create Single BST**
25. **LC 1948 — Delete Duplicate Folders in System**
26. **LC 2096 — Directions From One Tree Node to Another**
27. **LC 2277 — Closest Node to Path in Tree**
28. **LC 2416 — Sum of Prefix Scores**
29. **LC 2458 — Height After Subtree Removal Queries**
30. **LC 3045 — Count Prefix and Suffix Pairs II**

---

# Interview Templates You Must Internalize

## 1. Basic recursive DFS

Know where work occurs:

- Before child recursion: preorder.
- Between left and right: inorder.
- After both children: postorder.

## 2. Postorder with composite return state

Typical return fields:

- `isValid`
- `height`
- `sum`
- `minimum`
- `maximum`
- `size`
- `bestDownwardPath`

## 3. Path backtracking

The sequence is:

1. Add the current node.
2. Test the terminal condition.
3. Recurse into children.
4. Remove the current node.

## 4. Tree prefix sum

Maintain frequencies of prefix sums along only the active root-to-current recursion path.

Increment before descending and decrement while backtracking.

## 5. Iterative inorder

Maintain a stack containing the unprocessed path of left ancestors.

## 6. LCA

Return:

- The current node if it is a target.
- The non-null child result if only one side contains a target.
- The current node if both sides return non-null.

## 7. Tree construction

Prefer traversal intervals and shared indices. Avoid copying array slices.

## 8. BST bounds

Every node must satisfy a range inherited from all its ancestors.

## 9. Trie wildcard search

The state is:

`(trie node, query index)`

For a wildcard, recurse into every available child.

## 10. Trie-assisted backtracking

Temporarily mark the board, follow only existing trie edges, emit words at terminal nodes and prune exhausted trie branches.

---

# Strict Completion Criteria

Section 9 is complete only when you can:

## Traversals

- Write recursive and iterative preorder, inorder and postorder.
- Write BFS with levels.
- Explain Morris traversal conceptually.
- Avoid recursion-state leakage between test cases.

## Recursive state

- Separate downward-return state from the global answer.
- Design composite subtree return values.
- Detect when a top-down state is better than bottom-up state.
- Avoid recomputing subtree height or sums.

## Paths

- Distinguish root-to-leaf, ancestor-to-descendant and arbitrary-node paths.
- Use prefix sums for downward path counting.
- Use backtracking for path enumeration.
- Use LCA or postorder composition for arbitrary-node relationships.

## Construction

- Construct trees from traversal pairs.
- Explain uniqueness requirements.
- Avoid `O(n²)` index searching.
- Handle skewed trees and recursion depth.

## Serialization

- Preserve null structure.
- Handle delimiters, signs and duplicate values.
- Assign canonical subtree IDs.
- Explain deterministic encoding.

## BSTs

- Validate using global bounds.
- Insert, search and delete.
- Implement a lazy iterator.
- Recover two swapped values.
- Use reverse inorder.
- Use ordered pruning.
- Explain augmentation for rank queries.

## Tries

- Implement insert, search, prefix search, count and erase.
- Support wildcard branching.
- Store prefix aggregates.
- Build lexicographic suggestions.
- Reverse strings for suffix queries.
- Combine a trie with grid DFS.
- Model file systems and folders as hierarchical tries.
- Discuss memory versus query-speed tradeoffs.

---

# Quantitative Target

For strict preparation:

- Solve **105–115 of the approximately 130 unique primary questions**.
- Solve every accessible **P0** problem.
- Re-solve at least **35 P0 problems** after a two-week gap.
- Complete at least **15 advanced or Stretch problems**.
- Implement the standard tree and trie templates from memory.
- Conduct at least **four mixed Section 9 mock sessions**.
- Include one tree-design or trie-design problem in every second mock.

## Expected timing

- Easy tree traversal: **10–15 minutes**
- Standard medium tree problem: **20–25 minutes**
- Tree construction or LCA variation: **25–30 minutes**
- Advanced postorder-state problem: **30–40 minutes**
- Trie design problem: **25–35 minutes**
- Trie plus backtracking problem: **35–45 minutes**
- Hard composite problem: **40–50 minutes**, including proof and edge-case discussion

The most important objective is not memorizing 130 solutions. It is learning to identify what information flows **down the tree**, what information flows **up the tree**, what must remain **global**, and what can be compressed into a reusable subtree or trie state.# Section 11: Graphs

## Strict Google L5 Preparation Curriculum

Section 11 should be treated as one of the highest-priority sections in the complete sheet. A strict interview may move rapidly from basic graph representation into grid modeling, state-expanded BFS, DSU, topological ordering, weighted shortest paths, MST, cycle analysis, bridges, or game-state search.

This curriculum contains approximately **145 unique primary questions**, with additional optional extensions. It covers all Section 11 patterns:

85. Graph Representation & Basic Traversal  
86. Bipartite Graphs & Coloring  
87. Grid Traversal Foundations  
88. Multi-Source Grid BFS  
89. Unweighted Shortest Path  
90. Word Transformation BFS  
91. BFS with Expanded States  
92. Disjoint Set Union Foundations  
93. Advanced Disjoint Set Union  
94. Topological Sort Foundations  
95. Topological Dynamic Programming  
96. Multi-Dependency Ordering  
97. Weighted Graph Foundations  
98. Restricted & Layered Shortest Paths  
99. Minimum Spanning Tree  
100. Functional Graph Cycles + Bridges/Articulation Points  
101. Advanced Graph State & Game Problems  

The current <Organization>LeetCode</Organization> catalogue maintains substantial dedicated collections for Graph, DFS, BFS, Union Find, Topological Sort, Shortest Path, Minimum Spanning Tree, Strongly Connected Components, Eulerian Circuits, and biconnected-component problems. 【1-5cece2】【2-8d15fe】【3-770683】【4-805942】【5-8f9f36】【6-96dff1】

---

# Priority Legend

- **P0:** Master cold. Derive, prove and implement without assistance.
- **P1:** Must solve independently after normal practice.
- **P2:** Important variation or a lower-frequency scenario.
- **Stretch:** Advanced boundary for strict Google L5 preparation.
- **Premium:** Skip if inaccessible, or solve a structurally equivalent problem.

---

# Pattern 85: Graph Representation & Basic Traversal

The first goal is to become fluent in converting an informal relationship into a graph.

You should recognize:

- Directed versus undirected edges.
- Weighted versus unweighted edges.
- Explicit versus implicit graphs.
- Sparse versus dense graphs.
- Node values versus node identities.
- Adjacency lists versus adjacency matrices.
- DFS recursion versus iterative DFS.
- Component counting versus reachability.

## Core traversal

1. **LC 133 — Clone Graph**  
   Medium | P0  
   Focus: Graph traversal with old-node to new-node mapping.

2. **LC 1971 — Find if Path Exists in Graph**  
   Easy | P0  
   Focus: Basic undirected reachability.

3. **LC 841 — Keys and Rooms**  
   Medium | P0  
   Focus: Directed reachability from a fixed source.

4. **LC 547 — Number of Provinces**  
   Medium | P0  
   Focus: Connected components in an adjacency matrix.

5. **LC 323 — Number of Connected Components in an Undirected Graph**  
   Medium | P0 | Premium  
   Focus: DFS, BFS and DSU alternatives.

6. **LC 261 — Graph Valid Tree**  
   Medium | P0 | Premium  
   Focus: Connectivity plus absence of cycles.

7. **LC 684 — Redundant Connection**  
   Medium | P0  
   Focus: Detect the edge that closes an undirected cycle.

8. **LC 685 — Redundant Connection II**  
   Hard | P0 / Stretch  
   Focus: Directed graph with a two-parent conflict and cycle conflict.

9. **LC 785 — Is Graph Bipartite?**  
   Medium | P0  
   Focus: Component-aware graph coloring.

10. **LC 797 — All Paths From Source to Target**  
    Medium | P0  
    Focus: Enumerating all paths in a DAG.

11. **LC 1466 — Reorder Routes to Make All Paths Lead to the City Zero**  
    Medium | P0  
    Focus: Preserve original edge direction during undirected traversal.

12. **LC 1319 — Number of Operations to Make Network Connected**  
    Medium | P0  
    Focus: Components and redundant edges.

13. **LC 1791 — Find Center of Star Graph**  
    Easy | P1  
    Focus: Degree structure.

14. **LC 1557 — Minimum Number of Vertices to Reach All Nodes**  
    Medium | P1  
    Focus: Zero-indegree nodes in a DAG.

15. **LC 997 — Find the Town Judge**  
    Easy | P1  
    Focus: In-degree and out-degree accounting.

16. **LC 1436 — Destination City**  
    Easy | P2  
    Focus: Terminal node through degree information.

17. **LC 1615 — Maximal Network Rank**  
    Medium | P1  
    Focus: Degree sums corrected for direct connectivity.

18. **LC 2492 — Minimum Score of a Path Between Two Cities**  
    Medium | P1  
    Focus: Component traversal with minimum edge aggregation.

19. **LC 2316 — Count Unreachable Pairs of Nodes in an Undirected Graph**  
    Medium | P0  
    Focus: Component sizes and cross-component pair counting.

20. **LC 2685 — Count the Number of Complete Components**  
    Medium | P1  
    Focus: Component size and internal edge count.

21. **LC 2368 — Reachable Nodes With Restrictions**  
    Medium | P1  
    Focus: Traversal with forbidden nodes.

22. **LC 2092 — Find All People With Secret**  
    Hard | P0  
    Focus: Time-batched connectivity.

23. **LC 2392 — Build a Matrix With Conditions**  
    Hard | P0  
    Focus: Two independent ordering graphs.

24. **LC 924 — Minimize Malware Spread**  
    Hard | P1  
    Focus: Component ownership and impact analysis.

### Representation mastery

For every problem, decide whether you need:

- `graph[u] -> list of v`
- `graph[u] -> list of (v, weight)`
- Reverse adjacency.
- In-degree or out-degree arrays.
- Edge IDs.
- Parent edge tracking.
- A matrix rather than an adjacency list.
- An implicit neighbor-generation function.
- A map because node labels are sparse or non-numeric.

---

# Pattern 86: Bipartite Graphs & Coloring

Bipartite problems often appear disguised as:

- Divide people into two groups.
- Assign opposite labels to conflicting entities.
- Check whether constraints of the form “different from” are consistent.
- Match entities from two separate classes.
- Detect an odd cycle.

25. **LC 785 — Is Graph Bipartite?**  
    Medium | P0  
    Focus: Two-color every connected component.

26. **LC 886 — Possible Bipartition**  
    Medium | P0  
    Focus: Convert dislike constraints into an undirected graph.

27. **LC 1042 — Flower Planting With No Adjacent**  
    Medium | P1  
    Focus: Bounded-degree graph coloring.

28. **LC  bipartite variants with equality constraints**  
    Conceptual  
    Focus: Determine whether ordinary coloring or parity DSU is more appropriate.

29. **LC 2493 — Divide Nodes Into the Maximum Number of Groups**  
    Hard | P0 / Stretch  
    Focus: Bipartite validation plus component diameter through BFS layering.

30. **LC 1349 — Maximum Students Taking Exam**  
    Hard | Stretch  
    Focus: Bipartite matching or state-compressed DP.

31. **LC 1820 — Maximum Number of Accepted Invitations**  
    Medium | P1 | Premium  
    Focus: DFS-based augmenting paths for bipartite matching.

32. **LC 1947 — Maximum Compatibility Score Sum**  
    Medium | P2  
    Focus: Assignment through permutation, bitmask DP or matching.

33. **LC 2123 — Minimum Operations to Remove Adjacent Ones in Matrix**  
    Hard | P2 | Premium  
    Focus: Grid bipartite matching and minimum vertex cover connection.

### Coloring mastery

You should be able to explain:

- Why BFS levels naturally alternate colors.
- Why every disconnected component must be processed.
- Why a same-color edge proves the existence of an odd cycle.
- Why a self-loop immediately violates bipartiteness.
- When two-coloring is insufficient because the problem requires matching.
- How parity DSU can maintain same/different relationships dynamically.

---

# Pattern 87: Grid Traversal Foundations

A grid is usually an implicit graph:

- Each cell is a node.
- Neighboring cells define edges.
- Obstacles remove nodes or edges.
- Cell values may define traversal rules.
- Mutating the grid can replace a separate visited matrix.

## Core islands and components

34. **LC 200 — Number of Islands**  
    Medium | P0  
    Focus: Canonical grid component traversal.

35. **LC 695 — Max Area of Island**  
    Medium | P0  
    Focus: Component-size aggregation.

36. **LC 463 — Island Perimeter**  
    Easy | P0  
    Focus: Count exposed boundaries.

37. **LC 733 — Flood Fill**  
    Easy | P0  
    Focus: Grid traversal and safe recoloring.

38. **LC 130 — Surrounded Regions**  
    Medium | P0  
    Focus: Boundary-connected components.

39. **LC 417 — Pacific Atlantic Water Flow**  
    Medium | P0  
    Focus: Reverse reachability from multiple boundaries.

40. **LC 1020 — Number of Enclaves**  
    Medium | P0  
    Focus: Remove boundary-reachable land.

41. **LC 1254 — Number of Closed Islands**  
    Medium | P0  
    Focus: Boundary contact versus enclosed components.

42. **LC 1905 — Count Sub Islands**  
    Medium | P0  
    Focus: Validate components against a second grid.

43. **LC 827 — Making A Large Island**  
    Hard | P0  
    Focus: Label components and combine neighboring component sizes.

44. **LC 934 — Shortest Bridge**  
    Medium | P0  
    Focus: DFS one component, then BFS expansion.

45. **LC 694 — Number of Distinct Islands**  
    Medium | P0 | Premium  
    Focus: Shape normalization using relative coordinates.

46. **LC 711 — Number of Distinct Islands II**  
    Hard | Stretch | Premium  
    Focus: Canonical shape under rotations and reflections.

47. **LC 529 — Minesweeper**  
    Medium | P1  
    Focus: Conditional recursive expansion.

48. **LC 1034 — Coloring A Border**  
    Medium | P1  
    Focus: Identify component boundary cells.

49. **LC 1219 — Path with Maximum Gold**  
    Medium | P1  
    Focus: Grid backtracking rather than simple visitation.

50. **LC 1559 — Detect Cycles in 2D Grid**  
    Medium | P0  
    Focus: Undirected cycle detection with parent tracking.

51. **LC 1391 — Check if There is a Valid Path in a Grid**  
    Medium | P1  
    Focus: Direction-compatible edges.

52. **LC 1992 — Find All Groups of Farmland**  
    Medium | P1  
    Focus: Rectangular components and boundary extraction.

53. **LC 2658 — Maximum Number of Fish in a Grid**  
    Medium | P1  
    Focus: Weighted component aggregation.

54. **LC 1021-style grid traversal variants**  
    Optional  
    Focus: Separate traversal state from cell content when mutation is unsafe.

### Grid mastery

Before coding, settle:

- Four or eight directions?
- Can movement wrap around?
- Is the graph directed because movement rules differ by direction?
- Can the grid be mutated?
- Is revisiting with a different state meaningful?
- Is this component traversal, shortest path or backtracking?
- Are source and destination cells traversable?
- Does entering a cell carry a cost?

---

# Pattern 88: Multi-Source Grid BFS

Multi-source BFS begins with every source in the queue at distance zero.

It is the correct pattern when asking:

- Distance to the nearest source.
- Time until a process spreads everywhere.
- Simultaneous growth, infection, fire or decay.
- Voronoi-like nearest-source assignment in an unweighted graph.

55. **LC 994 — Rotting Oranges**  
    Medium | P0  
    Focus: Simultaneous level-by-level spread.

56. **LC 542 — 01 Matrix**  
    Medium | P0  
    Focus: Distance from every cell to the nearest zero.

57. **LC 286 — Walls and Gates**  
    Medium | P0 | Premium  
    Focus: Start BFS from all gates.

58. **LC 1765 — Map of Highest Peak**  
    Medium | P0  
    Focus: Multi-source distance labeling.

59. **LC 1162 — As Far from Land as Possible**  
    Medium | P0  
    Focus: Maximum distance from any source.

60. **LC 1926 — Nearest Exit from Entrance in Maze**  
    Medium | P1  
    Focus: Boundary target and BFS distance.

61. **LC 2146 — K Highest Ranked Items Within a Price Range**  
    Medium | P1  
    Focus: BFS distance plus ranking tie-breakers.

62. **LC 2258 — Escape the Spreading Fire**  
    Hard | Stretch  
    Focus: Fire arrival times plus feasibility search.

63. **LC 2812 — Find the Safest Path in a Grid**  
    Medium | P0  
    Focus: Multi-source danger distance followed by maximum-bottleneck search.

64. **LC 317 — Shortest Distance from All Buildings**  
    Hard | P0 | Premium  
    Focus: Repeated BFS and aggregate reachability.

65. **LC 1263 — Minimum Moves to Move a Box to Their Target Location**  
    Hard | Stretch  
    Focus: Player reachability nested inside state-space search.

### Multi-source BFS invariant

When a node is first discovered, it has the minimum distance from **any** source, provided:

- Every edge has equal cost.
- All sources begin at distance zero.
- Nodes are enqueued only when their best distance is established.

---

# Pattern 89: Unweighted Shortest Path

For equal-cost edges, BFS computes shortest path by number of edges.

66. **LC 1091 — Shortest Path in Binary Matrix**  
    Medium | P0  
    Focus: Eight-direction BFS.

67. **LC 752 — Open the Lock**  
    Medium | P0  
    Focus: Implicit graph over configurations.

68. **LC 127 — Word Ladder**  
    Hard | P0  
    Focus: Implicit word graph and shortest transformation length.

69. **LC 433 — Minimum Genetic Mutation**  
    Medium | P0  
    Focus: Small-alphabet transformation graph.

70. **LC 815 — Bus Routes**  
    Hard | P0  
    Focus: Correct graph modeling between stops and routes.

71. **LC 1345 — Jump Game IV**  
    Hard | P0  
    Focus: Same-value teleport edges and one-time adjacency expansion.

72. **LC 1654 — Minimum Jumps to Reach Home**  
    Medium | P1  
    Focus: Direction-sensitive state and bounded search space.

73. **LC 1311 — Get Watched Videos by Your Friends**  
    Medium | P1  
    Focus: Exact BFS-level retrieval.

74. **LC 1129 — Shortest Path with Alternating Colors**  
    Medium | P0  
    Focus: State includes the previous edge color.

75. **LC 1376 — Time Needed to Inform All Employees**  
    Medium | P1  
    Focus: Rooted directed graph and path-time accumulation.

76. **LC 1928 — Minimum Cost to Reach Destination in Time**  
    Hard | Stretch  
    Focus: Multi-objective state, not ordinary BFS.

77. **LC 847 — Shortest Path Visiting All Nodes**  
    Hard | P0  
    Focus: Multi-source BFS over node and visited mask.

78. **LC 1293 — Shortest Path in a Grid with Obstacles Elimination**  
    Hard | P0  
    Focus: Position plus remaining eliminations.

79. **LC 864 — Shortest Path to Get All Keys**  
    Hard | P0  
    Focus: Position plus collected-key mask.

80. **LC 909 — Snakes and Ladders**  
    Medium | P0  
    Focus: Index conversion and forced transitions.

### Shortest-path reconstruction

In addition to distance, be prepared to return the actual path by storing:

- `parent[node]`
- `parent[state]`
- The action used to reach the state
- The last edge or transformation

Do not overwrite parent state after the shortest visit is finalized.

---

# Pattern 90: Word Transformation BFS

Word transformation deserves separate practice because neighbor generation often dominates the runtime.

81. **LC 127 — Word Ladder**  
    Hard | P0  
    Focus: Pattern buckets, direct mutation and bidirectional BFS.

82. **LC 126 — Word Ladder II**  
    Hard | P0 / Stretch  
    Focus: Shortest-layer graph followed by path reconstruction.

83. **LC 433 — Minimum Genetic Mutation**  
    Medium | P0  
    Focus: Fixed-character substitutions.

84. **LC 752 — Open the Lock**  
    Medium | P0  
    Focus: Similar transformation-space modeling.

85. **LC 1553-style transformation minimization variants**  
    Optional  
    Focus: Decide whether BFS, bidirectional BFS or memoized recursion is more suitable.

### Word-ladder mastery

You should know three neighbor-generation methods:

1. Try every character at every position.
2. Precompute wildcard pattern buckets.
3. Use bidirectional BFS from the smaller frontier.

For Word Ladder II:

- BFS determines minimum distances.
- Stop adding deeper layers after the shortest target depth.
- Store predecessor relationships or a shortest-path DAG.
- Backtrack only through valid shortest-path edges.

---

# Pattern 91: BFS with Expanded States

The node is not just a location. It may be:

- `(position, remaining resource)`
- `(node, visitedMask)`
- `(row, column, keysMask)`
- `(node, lastEdgeColor)`
- `(position, direction)`
- `(position, speed)`
- `(boxPosition, playerPosition)`
- `(node, stopsUsed)`

86. **LC 847 — Shortest Path Visiting All Nodes**  
    Hard | P0  
    Focus: `(node, visitedMask)`.

87. **LC 864 — Shortest Path to Get All Keys**  
    Hard | P0  
    Focus: Grid location plus key mask.

88. **LC 1293 — Shortest Path in a Grid with Obstacles Elimination**  
    Hard | P0  
    Focus: Location plus remaining eliminations.

89. **LC 1129 — Shortest Path with Alternating Colors**  
    Medium | P0  
    Focus: Node plus last edge color.

90. **LC 1210 — Minimum Moves to Reach Target with Rotations**  
    Hard | P0  
    Focus: Location plus snake orientation.

91. **LC 1654 — Minimum Jumps to Reach Home**  
    Medium | P1  
    Focus: Position plus whether the previous move was backward.

92. **LC 2059 — Minimum Operations to Convert Number**  
    Medium | P1  
    Focus: Numeric configuration graph.

93. **LC 1263 — Minimum Moves to Move a Box**  
    Hard | Stretch  
    Focus: Box and player positions.

94. **LC 2290 — Minimum Obstacle Removal to Reach Corner**  
    Hard | P0  
    Focus: 0-1 BFS.

95. **LC 1368 — Minimum Cost to Make at Least One Valid Path in a Grid**  
    Hard | P0  
    Focus: 0-1 BFS over preferred and changed directions.

96. **LC 2608 — Shortest Cycle in a Graph**  
    Hard | P1  
    Focus: BFS from each source with parent-aware cycle detection.

97. **LC 1824 — Minimum Sideway Jumps**  
    Medium | P1  
    Focus: Position and lane state.

98. **LC 818 — Race Car**  
    Hard | Stretch  
    Focus: Position and speed state.

99. **LC 773 — Sliding Puzzle**  
    Hard | P0  
    Focus: Encoded board configuration.

100. **LC 909 — Snakes and Ladders**  
     Medium | P0  
     Focus: Board position with forced transition.

### Dominance pruning

Two states at the same location are not always equally useful.

For example:

- More remaining obstacle eliminations dominates fewer.
- Lower cost at the same time state may dominate higher cost.
- Same node with a superset of keys may dominate a subset only under careful conditions.
- Fewer stops does not necessarily dominate lower cost.

You must prove dominance before discarding expanded states.

---

# Pattern 92: Disjoint Set Union Foundations

A DSU supports:

- `find(x)`
- `union(a, b)`
- Connectivity queries
- Component-size tracking
- Component-count tracking

Implement both:

- Path compression
- Union by size or rank

## Core DSU problems

101. **LC 547 — Number of Provinces**  
     Medium | P0  
     Focus: DSU over an adjacency matrix.

102. **LC 684 — Redundant Connection**  
     Medium | P0  
     Focus: First edge connecting already-connected nodes.

103. **LC 261 — Graph Valid Tree**  
     Medium | P0 | Premium  
     Focus: Exactly `n - 1` edges plus connectivity.

104. **LC 323 — Number of Connected Components**  
     Medium | P0 | Premium  
     Focus: Component count after unions.

105. **LC 1319 — Number of Operations to Make Network Connected**  
     Medium | P0  
     Focus: Redundant cables and component count.

106. **LC 721 — Accounts Merge**  
     Medium | P0  
     Focus: Union entities through shared attributes.

107. **LC 990 — Satisfiability of Equality Equations**  
     Medium | P0  
     Focus: Process equality before inequality.

108. **LC 1061 — Lexicographically Smallest Equivalent String**  
     Medium | P0  
     Focus: Select a canonical component representative.

109. **LC 1971 — Find if Path Exists in Graph**  
     Easy | P1  
     Focus: Basic connectivity query.

110. **LC 2685 — Count Complete Components**  
     Medium | P1  
     Focus: DSU or traversal plus component edge counts.

111. **LC 2316 — Count Unreachable Pairs of Nodes**  
     Medium | P0  
     Focus: Component sizes and pair counting.

112. **LC 1202 — Smallest String With Swaps**  
     Medium | P0  
     Focus: Group indices by components and assign sorted characters.

113. **LC 839 — Similar String Groups**  
     Hard | P1  
     Focus: Pairwise relation construction and DSU.

114. **LC 947 — Most Stones Removed with Same Row or Column**  
     Medium | P0  
     Focus: Components over rows and columns.

115. **LC 959 — Regions Cut By Slashes**  
     Medium | P0  
     Focus: Expand each cell into subregions or use corner connectivity.

---

# Pattern 93: Advanced Disjoint Set Union

Advanced DSU frequently requires:

- Metadata per root.
- Weighted relationships.
- Time-ordered union.
- Rollback or temporary connectivity.
- Activating nodes dynamically.
- Merging identifiers from different domains.

116. **LC 685 — Redundant Connection II**  
     Hard | P0 / Stretch  
     Focus: Directed parent conflict plus cycle.

117. **LC 399 — Evaluate Division**  
     Medium | P0  
     Focus: Weighted DSU or weighted graph traversal.

118. **LC 952 — Largest Component Size by Common Factor**  
     Hard | P0  
     Focus: Union numbers through prime factors.

119. **LC 924 — Minimize Malware Spread**  
     Hard | P1  
     Focus: Component infection ownership.

120. **LC 928 — Minimize Malware Spread II**  
     Hard | Stretch  
     Focus: Influence after node removal.

121. **LC 1101 — The Earliest Moment When Everyone Become Friends**  
     Medium | P1 | Premium  
     Focus: Time-sorted union events.

122. **LC 1631 — Path With Minimum Effort**  
     Medium | P0  
     Focus: Sort edges and union until endpoints connect.

123. **LC 1697 — Checking Existence of Edge Length Limited Paths**  
     Hard | P0  
     Focus: Offline queries sorted by weight limit.

124. **LC 2092 — Find All People With Secret**  
     Hard | P0  
     Focus: Time-batched temporary connectivity.

125. **LC 2421 — Number of Good Paths**  
     Hard | P0  
     Focus: Activate nodes by value and merge eligible components.

126. **LC 827 — Making A Large Island**  
     Hard | P0  
     Focus: Component-size metadata.

127. **LC 305 — Number of Islands II**  
     Hard | P0 | Premium  
     Focus: Dynamic activation and component counting.

128. **LC 803 — Bricks Falling When Hit**  
     Hard | Stretch  
     Focus: Reverse operations and roof connectivity.

129. **LC 1579 — Remove Max Number of Edges to Keep Graph Fully Traversable**  
     Hard | P0  
     Focus: Shared edges before user-specific edges.

130. **LC 1722 — Minimize Hamming Distance After Swap Operations**  
     Medium | P1  
     Focus: Frequency comparison inside components.

### Weighted DSU invariant

For division-like relationships, store a weight representing a node’s relationship to its parent.

After path compression, update the weight so that it directly represents the relationship to the root.

Be able to derive the formula rather than memorize it blindly.

---

# Pattern 94: Topological Sort Foundations

Topological sorting applies to directed acyclic graphs.

It supports:

- Dependency resolution.
- Valid execution order.
- Cycle detection.
- Layered processing.
- Course or task scheduling.
- Lexicographically smallest valid order.

## Core problems

131. **LC 207 — Course Schedule**  
     Medium | P0  
     Focus: Directed-cycle detection through Kahn’s algorithm or DFS colors.

132. **LC 210 — Course Schedule II**  
     Medium | P0  
     Focus: Produce a valid topological order.

133. **LC 269 — Alien Dictionary**  
     Hard | P0 | Premium  
     Focus: Infer edges from adjacent words and detect invalid prefix cases.

134. **LC 1136 — Parallel Courses**  
     Medium | P0 | Premium  
     Focus: BFS layers in a DAG.

135. **LC 1203 — Sort Items by Groups Respecting Dependencies**  
     Hard | Stretch  
     Focus: Two-level topological ordering.

136. **LC 2115 — Find All Possible Recipes from Given Supplies**  
     Medium | P0  
     Focus: Supplies as initially available zero-requirement resources.

137. **LC 2392 — Build a Matrix With Conditions**  
     Hard | P0  
     Focus: Independent row and column topological orders.

138. **LC 802 — Find Eventual Safe States**  
     Medium | P0  
     Focus: Reverse graph and terminal-node topological elimination.

139. **LC 310 — Minimum Height Trees**  
     Medium | P0  
     Focus: Repeated leaf removal.

140. **LC 444 — Sequence Reconstruction**  
     Medium | P1 | Premium  
     Focus: Uniqueness of a topological order.

141. **LC 1462 — Course Schedule IV**  
     Medium | P1  
     Focus: Transitive prerequisite reachability.

142. **LC 2192 — All Ancestors of a Node in a DAG**  
     Medium | P0  
     Focus: Propagate ancestor sets through topological order.

143. **LC 851 — Loud and Rich**  
     Medium | P1  
     Focus: Dependency graph and best ancestor propagation.

### Kahn’s algorithm mastery

Maintain:

- Adjacency list.
- In-degree array.
- Queue of zero-indegree nodes.
- Processed-node count.
- Optional priority queue for lexical ordering.
- Optional level count for parallel execution time.

A directed graph contains a cycle if fewer than `n` nodes are processed.

---

# Pattern 95: Topological Dynamic Programming

In a DAG, topological order converts cyclic-looking dependencies into one-directional transitions.

144. **LC 329 — Longest Increasing Path in a Matrix**  
     Hard | P0  
     Focus: Memoized DFS or topological layers.

145. **LC 2050 — Parallel Courses III**  
     Hard | P0  
     Focus: Earliest finish time in a dependency DAG.

146. **LC 1857 — Largest Color Value in a Directed Graph**  
     Hard | P0  
     Focus: Topological DP with a color-frequency vector.

147. **LC 2328 — Number of Increasing Paths in a Grid**  
     Hard | P0  
     Focus: DAG path counting.

148. **LC 2376-style dependency DP variants**  
     Optional  
     Focus: Count or optimize over acyclic state transitions.

149. **LC 2192 — All Ancestors of a Node in a DAG**  
     Medium | P0  
     Focus: Set propagation.

150. **LC 851 — Loud and Rich**  
     Medium | P1  
     Focus: Best-answer propagation.

151. **LC 1976 — Number of Ways to Arrive at Destination**  
     Medium | P0  
     Focus: Shortest-path DAG counting after Dijkstra relaxation.

152. **LC 1786 — Number of Restricted Paths From First to Last Node**  
     Medium | P0  
     Focus: Dijkstra distances define an acyclic restriction.

153. **LC 1514-style path optimization variants**  
     Optional  
     Focus: Recognize when ordering by distance or value creates a DAG.

### DAG DP design

For each node, determine whether DP means:

- Best path ending at the node.
- Best path starting at the node.
- Number of paths reaching the node.
- Earliest completion time.
- Set of reachable ancestors.
- Per-category best count.
- Reconstruction parent.

---

# Pattern 96: Multi-Dependency Ordering

These problems add grouping, uniqueness, nested dependencies or inferred ordering.

154. **LC 269 — Alien Dictionary**  
     Hard | P0 | Premium  
     Focus: Infer only the first differing-character constraint.

155. **LC 1203 — Sort Items by Groups Respecting Dependencies**  
     Hard | Stretch  
     Focus: Group DAG plus item DAG.

156. **LC 444 — Sequence Reconstruction**  
     Medium | P1 | Premium  
     Focus: Exactly one valid topological choice at every step.

157. **LC 2115 — Find All Possible Recipes**  
     Medium | P0  
     Focus: Ingredients, recipes and supplies.

158. **LC 2392 — Build a Matrix With Conditions**  
     Hard | P0  
     Focus: Compose two valid orderings.

159. **LC 1462 — Course Schedule IV**  
     Medium | P1  
     Focus: Transitive dependencies.

160. **LC 1916 — Count Ways to Build Rooms in an Ant Colony**  
     Hard | Stretch  
     Focus: Tree dependencies plus combinatorics.

161. **LC 1591 — Strange Printer II**  
     Hard | Stretch  
     Focus: Infer ordering constraints between colors.

### Alien Dictionary failure cases

You must explicitly handle:

- A longer word appearing before its exact prefix.
- Characters with no edges.
- Duplicate edges.
- Multiple valid orders.
- Directed cycles.
- Empty or one-word input.
- Lexicographic requirements, if requested.

---

# Pattern 97: Weighted Graph Foundations

For non-negative weighted edges, Dijkstra is the default shortest-path algorithm.

You should also know:

- Bellman-Ford for negative edges.
- Floyd-Warshall for all-pairs shortest paths on small graphs.
- 0-1 BFS for edge weights in `{0, 1}`.
- DAG shortest path for acyclic graphs.
- Maximum-probability Dijkstra variants.
- Bottleneck-path variants.

## Dijkstra core

162. **LC 743 — Network Delay Time**  
     Medium | P0  
     Focus: Canonical single-source Dijkstra.

163. **LC 1514 — Path with Maximum Probability**  
     Medium | P0  
     Focus: Max-heap Dijkstra with multiplicative path value.

164. **LC 1631 — Path With Minimum Effort**  
     Medium | P0  
     Focus: Minimize the maximum edge cost.

165. **LC 778 — Swim in Rising Water**  
     Hard | P0  
     Focus: Minimize maximum cell elevation.

166. **LC 1976 — Number of Ways to Arrive at Destination**  
     Medium | P0  
     Focus: Dijkstra with shortest-path counts.

167. **LC 1786 — Number of Restricted Paths**  
     Medium | P0  
     Focus: Dijkstra followed by distance-ordered DP.

168. **LC 882 — Reachable Nodes In Subdivided Graph**  
     Hard | P1  
     Focus: Weighted distances plus partially traversed edges.

169. **LC 1334 — Find the City With the Smallest Number of Neighbors**  
     Medium | P0  
     Focus: Floyd-Warshall or repeated Dijkstra.

170. **LC 2642 — Design Graph With Shortest Path Calculator**  
     Hard | P0  
     Focus: Dynamic edge insertion and shortest-path queries.

171. **LC 2203 — Minimum Weighted Subgraph With Required Paths**  
     Hard | Stretch  
     Focus: Dijkstra from two sources and once on the reverse graph.

## Special weight structures

172. **LC 1368 — Minimum Cost to Make at Least One Valid Path**  
     Hard | P0  
     Focus: 0-1 BFS.

173. **LC 2290 — Minimum Obstacle Removal to Reach Corner**  
     Hard | P0  
     Focus: 0-1 BFS.

174. **LC 787 — Cheapest Flights Within K Stops**  
     Medium | P0  
     Focus: Bellman-Ford layers or stateful shortest path.

175. **LC 1129 — Shortest Path with Alternating Colors**  
     Medium | P0  
     Focus: State expansion rather than standard Dijkstra.

176. **LC 399 — Evaluate Division**  
     Medium | P0  
     Focus: Weighted graph traversal.

177. **LC 1462 — Course Schedule IV**  
     Medium | P1  
     Focus: Floyd-Warshall-style transitive closure alternative.

### Dijkstra correctness requirements

You must explain:

- Why finalized minimum-distance nodes are safe with non-negative edges.
- Why negative edges invalidate ordinary Dijkstra.
- Why stale priority-queue entries may be skipped.
- Why marking visited at insertion can be incorrect.
- How to reconstruct shortest paths.
- How to count multiple shortest paths.
- How to modify relaxation for minimax or maximum-probability paths.

---

# Pattern 98: Restricted & Layered Shortest Paths

The lowest raw distance is not enough when constraints include:

- Maximum stops.
- Time budget.
- Discounts.
- Limited free edges.
- Edge-color alternation.
- Disappearing nodes.
- Resource consumption.
- Multiple optimization dimensions.

178. **LC 787 — Cheapest Flights Within K Stops**  
     Medium | P0  
     Focus: Cost plus number of edges used.

179. **LC 1928 — Minimum Cost to Reach Destination in Time**  
     Hard | Stretch  
     Focus: Time and cost state.

180. **LC 2093 — Minimum Cost to Reach City With Discounts**  
     Medium | P0 | Premium  
     Focus: Node plus discounts used.

181. **LC 2714 — Find Shortest Path with K Hops**  
     Hard | P1 | Premium  
     Focus: Layered state graph.

182. **LC 2045 — Second Minimum Time to Reach Destination**  
     Hard | P0  
     Focus: First and second arrival times plus synchronized signals.

183. **LC 3123 — Find Edges in Shortest Paths**  
     Hard | P0  
     Focus: Distances from source and destination.

184. **LC 3112 — Minimum Time to Visit Disappearing Nodes**  
     Medium | P1  
     Focus: Arrival constraints during Dijkstra.

185. **LC 2662 — Minimum Cost of a Path With Special Roads**  
     Medium | P0  
     Focus: Compress relevant coordinates into a weighted graph.

186. **LC 1293 — Shortest Path with Obstacles Elimination**  
     Hard | P0  
     Focus: Remaining resource state.

187. **LC 864 — Shortest Path to Get All Keys**  
     Hard | P0  
     Focus: Acquired-resource mask.

188. **LC 1697 — Edge Length Limited Paths**  
     Hard | P0  
     Focus: Offline DSU instead of per-query shortest paths.

### State-space warning

A visited array indexed only by node is incorrect when reaching the same node with different:

- Remaining resources.
- Stops used.
- Key sets.
- Last-edge types.
- Arrival times.
- Costs under another constraint.

---

# Pattern 99: Minimum Spanning Tree

An MST connects every vertex with minimum total edge weight.

Know both:

- **Kruskal:** sort edges and union components.
- **Prim:** grow a tree using the cheapest crossing edge.

189. **LC 1584 — Min Cost to Connect All Points**  
     Medium | P0  
     Focus: Prim and Kruskal on a complete graph.

190. **LC 1135 — Connecting Cities With Minimum Cost**  
     Medium | P0 | Premium  
     Focus: Canonical MST.

191. **LC 1168 — Optimize Water Distribution in a Village**  
     Hard | P0 | Premium  
     Focus: Add a virtual source for well-building choices.

192. **LC 1489 — Find Critical and Pseudo-Critical Edges in MST**  
     Hard | Stretch  
     Focus: Force or exclude individual edges.

193. **LC 1579 — Remove Max Number of Edges to Keep Graph Fully Traversable**  
     Hard | P0  
     Focus: Shared connectivity before exclusive edges.

194. **LC 1631 — Path With Minimum Effort**  
     Medium | P0  
     Focus: MST bottleneck interpretation.

195. **LC 778 — Swim in Rising Water**  
     Hard | P0  
     Focus: Connectivity threshold interpretation.

196. **LC 1697 — Edge Length Limited Paths**  
     Hard | P0  
     Focus: Kruskal-style offline connectivity.

197. **LC 1724 — Checking Existence of Edge Length Limited Paths II**  
     Hard | Stretch | Premium  
     Focus: Persistent or advanced connectivity, optional.

### MST mastery

Be able to answer:

- Does the graph need to be connected initially?
- How do you detect failure to form an MST?
- Are duplicate and negative-weight edges allowed?
- Why does selecting the cheapest non-cycle edge work?
- Why is Prim preferable for dense implicit graphs?
- Why is Kruskal convenient when edges are already available?
- What is a critical versus pseudo-critical MST edge?
- How can a virtual node transform “build locally or connect externally” choices?

---

# Pattern 100: Functional Graph Cycles, Bridges & Articulation Points

A functional graph has at most one outgoing edge from each node.

Common tasks include:

- Detecting cycles.
- Finding cycle length.
- Counting nodes leading into cycles.
- Computing visits before repetition.
- Combining inbound chains with cycles.

## Functional graphs

198. **LC 2360 — Longest Cycle in a Graph**  
     Hard | P0  
     Focus: Traversal timestamps or topological pruning.

199. **LC 2127 — Maximum Employees to Be Invited to a Meeting**  
     Hard | P0 / Stretch  
     Focus: Cycles plus inbound chains into mutual pairs.

200. **LC 287 — Find the Duplicate Number**  
     Medium | P0  
     Focus: Floyd cycle detection in an implicit functional graph.

201. **LC 457 — Circular Array Loop**  
     Medium | P1  
     Focus: Direction-consistent cycle detection.

202. **LC 2359 — Find Closest Node to Given Two Nodes**  
     Medium | P0  
     Focus: Distances along functional paths.

203. **LC 2876 — Count Visited Nodes in a Directed Graph**  
     Hard | Stretch  
     Focus: Cycle sizes plus reverse propagation to inbound nodes.

## Bridges and articulation concepts

204. **LC 1192 — Critical Connections in a Network**  
     Hard | P0  
     Focus: Tarjan low-link values and bridges.

205. **LC 1568 — Minimum Number of Days to Disconnect Island**  
     Hard | P0 / Stretch  
     Focus: Articulation-point reasoning or bounded brute force.

206. **LC 928 — Minimize Malware Spread II**  
     Hard | Stretch  
     Focus: Removal impact and graph separation.

207. **LC 2360-style cycle decomposition variants**  
     Optional  
     Focus: Separate cyclic core from inbound trees.

### Tarjan bridge invariant

During DFS, maintain:

- `discovery[u]`: the time node `u` was first visited.
- `low[u]`: the earliest discovery time reachable from `u` using tree edges and at most one back edge.

A DFS tree edge `u -> v` is a bridge when:

`low[v] > discovery[u]`

Be careful with:

- The parent edge.
- Parallel edges.
- Disconnected graphs.
- Edge IDs.
- Updating low-link values from already-visited neighbors.

---

# Pattern 101: Advanced Graph State & Game Problems

These problems combine graphs with masks, minimax reasoning, retrograde analysis, probability, or evolving state.

208. **LC 847 — Shortest Path Visiting All Nodes**  
     Hard | P0  
     Focus: BFS over node and visited mask.

209. **LC 864 — Shortest Path to Get All Keys**  
     Hard | P0  
     Focus: Grid graph plus inventory mask.

210. **LC 913 — Cat and Mouse**  
     Hard | Stretch  
     Focus: Retrograde game-state analysis.

211. **LC 1728 — Cat and Mouse II**  
     Hard | Stretch  
     Focus: Turn-based game states and bounded move count.

212. **LC 802 — Find Eventual Safe States**  
     Medium | P0  
     Focus: Terminal-state propagation.

213. **LC 1125 — Smallest Sufficient Team**  
     Hard | P1  
     Focus: State compression over skill coverage.

214. **LC 943 — Find the Shortest Superstring**  
     Hard | Stretch  
     Focus: Complete directed overlap graph plus mask DP.

215. **LC 1494 — Parallel Courses II**  
     Hard | Stretch  
     Focus: Dependency graph plus subset transitions.

216. **LC 1349 — Maximum Students Taking Exam**  
     Hard | Stretch  
     Focus: Grid conflict graph and state-compressed DP.

217. **LC 1928 — Minimum Cost to Reach Destination in Time**  
     Hard | Stretch  
     Focus: Multi-dimensional optimization state.

218. **LC 1263 — Minimum Moves to Move a Box**  
     Hard | Stretch  
     Focus: Nested reachability inside BFS.

219. **LC 818 — Race Car**  
     Hard | Stretch  
     Focus: Infinite-looking configuration graph with bounded exploration.

220. **LC 773 — Sliding Puzzle**  
     Hard | P0  
     Focus: Permutation-state BFS.

221. **LC 301-style state-search variants**  
     Optional  
     Focus: BFS when minimum number of transformations is required.

222. **LC 1514 — Path with Maximum Probability**  
     Medium | P0  
     Focus: Semiring-style path optimization.

223. **LC 882 — Reachable Nodes in Subdivided Graph**  
     Hard | P1  
     Focus: Weighted reachability plus partial edge usage.

224. **LC 2065 — Maximum Path Quality of a Graph**  
     Hard | Stretch  
     Focus: Time-bounded revisiting and backtracking.

225. **LC 2242 — Maximum Score of a Node Sequence**  
     Hard | P1  
     Focus: Retain only a bounded number of best neighbors.

### Game-state modeling

A game state may include:

- Positions of all players.
- Whose turn it is.
- Remaining resources.
- Collected items.
- Move count.
- Terminal winner.
- Draw or unresolved status.

For finite deterministic games, retrograde analysis begins from known terminal states and propagates wins and losses backward.

---

# Additional Strongly Recommended Graph Problems

These are useful for additional coverage or mixed revision.

226. **LC 332 — Reconstruct Itinerary**  
     Hard | P0  
     Focus: Eulerian path with lexical edge ordering.

227. **LC 2097 — Valid Arrangement of Pairs**  
     Hard | P0  
     Focus: Directed Eulerian trail.

228. **LC 753 — Cracking the Safe**  
     Hard | Stretch  
     Focus: Eulerian cycle in a De Bruijn graph.

229. **LC 753-style edge-consumption problems**  
     Optional  
     Focus: Use every edge exactly once.

230. **LC 753 / LC 332 / LC 2097 together**  
     Required comparative study  
     Focus: Distinguish node visitation from edge consumption.

Although Eulerian traversal is listed in your added Section 18, it should be practiced beside graph traversal because it violates the standard “mark every node visited once” instinct.

---

# Deduplicated Coverage

Many problems intentionally appear in more than one pattern:

- **LC 847** belongs to unweighted shortest path, expanded-state BFS and advanced state search.
- **LC 864** belongs to grid BFS, bitmasks and expanded-state search.
- **LC 1631** supports Dijkstra, binary-search feasibility, DSU and MST interpretations.
- **LC 1697** supports offline queries, DSU and Kruskal-style processing.
- **LC 2092** combines time batching and temporary connectivity.
- **LC 2392** combines topological sorting and constructive matrix placement.
- **LC 802** can be solved using reverse topological processing or DFS coloring.
- **LC 2127** combines functional graph cycles with tree-depth aggregation.
- **LC 126** combines BFS shortest layers with backtracking.

After removing repeats, the main curriculum is approximately **145 unique problems**.

Do not blindly solve duplicate entries twice in the first pass. Revisit them later and implement a different valid approach.

---

# Strict P0 Core: Master Cold

## Traversal and graph modeling

- LC 133 — Clone Graph
- LC 200 — Number of Islands
- LC 261 — Graph Valid Tree
- LC 323 — Connected Components
- LC 417 — Pacific Atlantic Water Flow
- LC 547 — Number of Provinces
- LC 684 — Redundant Connection
- LC 685 — Redundant Connection II
- LC 695 — Max Area of Island
- LC 785 — Is Graph Bipartite?
- LC 797 — All Paths From Source to Target
- LC 827 — Making A Large Island
- LC 841 — Keys and Rooms
- LC 934 — Shortest Bridge
- LC 1020 — Number of Enclaves
- LC 1319 — Make Network Connected
- LC 1466 — Reorder Routes
- LC 1905 — Count Sub Islands
- LC 2316 — Count Unreachable Pairs

## BFS and state-space search

- LC 127 — Word Ladder
- LC 126 — Word Ladder II
- LC 286 — Walls and Gates
- LC 542 — 01 Matrix
- LC 752 — Open the Lock
- LC 773 — Sliding Puzzle
- LC 815 — Bus Routes
- LC 847 — Shortest Path Visiting All Nodes
- LC 864 — Shortest Path to Get All Keys
- LC 909 — Snakes and Ladders
- LC 994 — Rotting Oranges
- LC 1091 — Shortest Path in Binary Matrix
- LC 1129 — Alternating Colors
- LC 1162 — As Far from Land as Possible
- LC 1210 — Minimum Moves to Reach Target With Rotations
- LC 1293 — Shortest Path with Obstacles Elimination
- LC 1345 — Jump Game IV
- LC 1368 — Minimum Cost Grid Path
- LC 1765 — Map of Highest Peak
- LC 2290 — Minimum Obstacle Removal

## DSU

- LC 305 — Number of Islands II
- LC 399 — Evaluate Division
- LC 684 — Redundant Connection
- LC 685 — Redundant Connection II
- LC 721 — Accounts Merge
- LC 947 — Most Stones Removed
- LC 952 — Largest Component by Common Factor
- LC 959 — Regions Cut By Slashes
- LC 990 — Equality Equations
- LC 1061 — Smallest Equivalent String
- LC 1202 — Smallest String With Swaps
- LC 1579 — Remove Maximum Edges
- LC 1697 — Edge Length Limited Paths
- LC 2092 — Find All People With Secret
- LC 2421 — Number of Good Paths

## Topological sorting and DAG DP

- LC 207 — Course Schedule
- LC 210 — Course Schedule II
- LC 269 — Alien Dictionary
- LC 310 — Minimum Height Trees
- LC 329 — Longest Increasing Path
- LC 802 — Eventual Safe States
- LC 1136 — Parallel Courses
- LC 1203 — Sort Items by Groups
- LC 1857 — Largest Color Value
- LC 2050 — Parallel Courses III
- LC 2115 — Find All Possible Recipes
- LC 2192 — All Ancestors in a DAG
- LC 2328 — Number of Increasing Paths
- LC 2392 — Build a Matrix With Conditions

## Weighted paths

- LC 743 — Network Delay Time
- LC 778 — Swim in Rising Water
- LC 787 — Cheapest Flights Within K Stops
- LC 1334 — Find the City
- LC 1514 — Maximum Probability Path
- LC 1631 — Path With Minimum Effort
- LC 1786 — Restricted Paths
- LC 1976 — Number of Shortest Paths
- LC 2045 — Second Minimum Time
- LC 2203 — Minimum Weighted Subgraph
- LC 2642 — Design Graph
- LC 2662 — Special Roads
- LC 3112 — Disappearing Nodes
- LC 3123 — Edges in Shortest Paths

## MST, cycles and connectivity structure

- LC 1135 — Connecting Cities
- LC 1168 — Optimize Water Distribution
- LC 1192 — Critical Connections
- LC 1489 — Critical and Pseudo-Critical MST Edges
- LC 1584 — Min Cost to Connect Points
- LC 2127 — Maximum Employees to Invite
- LC 2360 — Longest Cycle
- LC 2876 — Count Visited Nodes

---

# Recommended Study Order

## Phase 1: Representation and traversal

Solve first:

1. LC 1971
2. LC 547
3. LC 133
4. LC 200
5. LC 695
6. LC 733
7. LC 841
8. LC 323
9. LC 261
10. LC 684
11. LC 130
12. LC 417
13. LC 785
14. LC 886
15. LC 1466

Goal: convert prose into a graph and traverse it without implementation mistakes.

---

## Phase 2: BFS and shortest unweighted paths

1. LC 994
2. LC 542
3. LC 286
4. LC 1091
5. LC 752
6. LC 433
7. LC 127
8. LC 815
9. LC 909
10. LC 934
11. LC 1162
12. LC 1345

Goal: recognize single-source, multi-source and implicit-graph BFS.

---

## Phase 3: Expanded states

1. LC 1129
2. LC 1654
3. LC 1293
4. LC 864
5. LC 847
6. LC 1210
7. LC 773
8. LC 1368
9. LC 2290
10. LC 1263

Goal: define the actual state precisely before creating `visited`.

---

## Phase 4: DSU

1. LC 547
2. LC 684
3. LC 261
4. LC 721
5. LC 990
6. LC 1061
7. LC 1202
8. LC 947
9. LC 959
10. LC 1319
11. LC 1579
12. LC 1697
13. LC 2092
14. LC 2421

Goal: extend DSU from Boolean connectivity into component metadata and offline processing.

---

## Phase 5: Topological sorting and DAG DP

1. LC 207
2. LC 210
3. LC 802
4. LC 1136
5. LC 2115
6. LC 269
7. LC 310
8. LC 329
9. LC 2050
10. LC 2192
11. LC 2392
12. LC 1857
13. LC 1203

Goal: move from cycle detection into ordered state propagation.

---

## Phase 6: Weighted shortest paths

1. LC 743
2. LC 1514
3. LC 1631
4. LC 778
5. LC 787
6. LC 1334
7. LC 1976
8. LC 1786
9. LC 1368
10. LC 2290
11. LC 2045
12. LC 2203
13. LC 2642

Goal: choose correctly among BFS, 0-1 BFS, Dijkstra, Bellman-Ford and Floyd-Warshall.

---

## Phase 7: MST and structural graph algorithms

1. LC 1584
2. LC 1135
3. LC 1168
4. LC 1489
5. LC 1192
6. LC 1568
7. LC 2360
8. LC 2127
9. LC 2876
10. LC 332
11. LC 2097

Goal: understand connectivity beyond ordinary reachability.

---

# Advanced Google L5 Final Set

Complete these under timed conditions after the main curriculum:

1. **LC 126 — Word Ladder II**
2. **LC 269 — Alien Dictionary**
3. **LC 305 — Number of Islands II**
4. **LC 329 — Longest Increasing Path**
5. **LC 685 — Redundant Connection II**
6. **LC 753 — Cracking the Safe**
7. **LC 778 — Swim in Rising Water**
8. **LC 803 — Bricks Falling When Hit**
9. **LC 815 — Bus Routes**
10. **LC 827 — Making A Large Island**
11. **LC 847 — Shortest Path Visiting All Nodes**
12. **LC 864 — Shortest Path to Get All Keys**
13. **LC 913 — Cat and Mouse**
14. **LC 928 — Minimize Malware Spread II**
15. **LC 952 — Largest Component Size by Common Factor**
16. **LC 1192 — Critical Connections**
17. **LC 1203 — Sort Items by Groups**
18. **LC 1263 — Minimum Moves to Move a Box**
19. **LC 1293 — Shortest Path with Obstacles Elimination**
20. **LC 1368 — Minimum Cost Grid Path**
21. **LC 1489 — Critical and Pseudo-Critical MST Edges**
22. **LC 1568 — Minimum Days to Disconnect Island**
23. **LC 1579 — Remove Maximum Number of Edges**
24. **LC 1697 — Edge Length Limited Paths**
25. **LC 1728 — Cat and Mouse II**
26. **LC 1857 — Largest Color Value**
27. **LC 1928 — Minimum Cost Within Time**
28. **LC 2092 — Find All People With Secret**
29. **LC 2127 — Maximum Employees to Invite**
30. **LC 2203 — Minimum Weighted Subgraph**
31. **LC 2258 — Escape the Spreading Fire**
32. **LC 2392 — Build a Matrix With Conditions**
33. **LC 2421 — Number of Good Paths**
34. **LC 2493 — Divide Nodes Into Maximum Groups**
35. **LC 2876 — Count Visited Nodes**
36. **LC 3123 — Find Edges in Shortest Paths**

---

# Algorithms You Must Implement From Memory

## 1. DFS

Both recursive and iterative forms, with:

- Parent tracking.
- Component counting.
- Entry and exit processing.
- Three-color state for directed cycles.

## 2. BFS

Including:

- Level-by-level BFS.
- Multi-source BFS.
- Parent reconstruction.
- Bidirectional BFS.
- Expanded-state BFS.

## 3. DSU

With:

- Path compression.
- Union by size.
- Component count.
- Component size.
- Canonical representative selection.
- Weighted relationship extension.

## 4. Topological sort

Both:

- Kahn’s BFS algorithm.
- DFS postorder with cycle colors.

## 5. Dijkstra

With:

- Weighted adjacency list.
- Stale-entry check.
- Distance relaxation.
- Parent reconstruction.
- Shortest-path counting variation.

## 6. 0-1 BFS

Use a deque:

- Zero-cost edge goes to the front.
- One-cost edge goes to the back.

## 7. Bellman-Ford

Know:

- `n - 1` relaxation rounds.
- Early stopping.
- Negative-cycle detection.
- Layer-limited variation for a maximum number of edges.

## 8. Floyd-Warshall

Understand:

- All-pairs shortest paths.
- Intermediate-node progression.
- Transitive closure variation.
- Small-graph applicability.

## 9. Prim and Kruskal

Implement both and explain when each is preferable.

## 10. Tarjan bridges

Maintain discovery and low-link values correctly.

## 11. Eulerian traversal

Perform postorder edge consumption and reverse the resulting path.

---

# Strict Completion Criteria

Section 11 is complete only when you can:

## Graph modeling

- Determine whether edges are directed.
- Identify the actual nodes and transitions.
- Build reverse graphs when useful.
- Preserve edge IDs when parallel edges matter.
- Convert grids and configurations into implicit graphs.

## Traversal

- Detect components.
- Detect cycles in directed and undirected graphs.
- Handle disconnected graphs.
- Avoid mistaking path-local visitation for global visitation.
- Return or reconstruct paths when requested.

## BFS

- Use BFS only when edge costs support it.
- Initialize multiple sources correctly.
- Define an expanded state without losing necessary information.
- Apply dominance pruning only after proving it.
- Use bidirectional BFS when branching is large and endpoints are known.

## DSU

- Implement path compression and union by size.
- Maintain root metadata.
- Process offline queries in sorted order.
- Handle dynamic node activation.
- Understand weighted DSU.
- Recognize when unions must be temporary or reset by time group.

## Topological sorting

- Detect cycles.
- Produce an order.
- Detect uniqueness.
- Process topological layers.
- Perform DP over a DAG.
- Handle inferred constraints and invalid-prefix cases.

## Weighted shortest paths

- Select BFS, 0-1 BFS, Dijkstra, Bellman-Ford or Floyd-Warshall appropriately.
- Explain why Dijkstra requires non-negative edges.
- Count shortest paths.
- Reconstruct shortest paths.
- Handle layered resource states.
- Solve minimax and maximum-probability variations.

## MST and structural algorithms

- Implement Kruskal and Prim.
- Use virtual nodes.
- Identify critical edges.
- Compute bridges.
- Analyze functional graphs.
- Separate cycles from inbound trees.
- Recognize Eulerian edge-consumption problems.

---

# Quantitative Target

For strict Google L5 preparation:

- Solve **115–125 of the approximately 145 unique primary questions**.
- Solve every accessible **P0** problem.
- Re-solve at least **40 P0 problems** after a 10–14 day gap.
- Complete at least **18 Stretch problems**.
- Implement all core algorithms from a blank editor.
- Complete at least **six mixed graph mock sessions**.
- Include one advanced state-space or weighted-graph problem in every second mock.
- Revisit at least five problems using an alternative algorithm.

## Expected timing

- Basic DFS/BFS: **15–20 minutes**
- Grid traversal: **20–25 minutes**
- Standard multi-source BFS: **20–25 minutes**
- DSU problem: **20–30 minutes**
- Topological-sort problem: **20–30 minutes**
- Standard Dijkstra: **25–30 minutes**
- Restricted shortest path: **30–40 minutes**
- MST problem: **25–35 minutes**
- Bridge or functional-graph problem: **35–45 minutes**
- Advanced graph-state problem: **40–50 minutes**

The central skill is not memorizing graph algorithms independently. It is correctly answering four questions before implementation:

1. **What exactly is a node or state?**
2. **What transition creates an edge?**
3. **What information changes the future, and therefore belongs in the state?**
4. **Which ordering or invariant makes the search correct and efficient?**

If those four decisions are correct, most graph implementations become standard templates. If any one of them is wrong, even flawless BFS, DFS or Dijkstra code will solve the wrong graph.# Section 13: Dynamic Programming

## Strict Google L5 Deep-Coverage Curriculum

Dynamic programming is arguably the most demanding section because success depends less on recalling an algorithm and more on constructing the correct mathematical state.

This curriculum covers all Section 13 patterns:

110. Dynamic Programming Foundations  
111. 1D Dynamic Programming  
112. Basic Counting & Unbounded Transitions  
113. Knapsack Foundations  
114. State-Compressed Tree DP  
115. Longest Increasing Subsequence Family  
116. Arithmetic & Monotonic Subsequences  
117. Stack-State Dynamic Programming  
118. Grid-Path Dynamic Programming  
119. Grid-Shaped Dynamic Programming  
120. Palindromic Dynamic Programming  
121. Two-String Dynamic Programming  
122. Interleaving & Shuffle Reconstruction  
123. Pattern-Matching Dynamic Programming  
124. Word Segmentation & Dictionary DP  
125. Distance-Based Subsequences & String Counting  
126. Partition Dynamic Programming  
127. Interval Dynamic Programming  
128. Complex Positional & Circular DP  
129. Probability Dynamic Programming  
130. Digit Dynamic Programming  
131. Tree Dynamic Programming  
132. Memoized Decision Search & Game DP  
133. Nim & Grundy Numbers  
134. Matrix Exponentiation & Fast Recurrence  
135. Advanced Recurrence & DP Optimization  

The curriculum contains approximately **190 primary entries**, with overlaps intentionally retained where a problem teaches multiple DP formulations.

---

# Priority Legend

- **P0:** Master cold. Derive the state and transition without hints.
- **P1:** Must solve independently after normal preparation.
- **P2:** Important variation or lower-frequency technique.
- **Stretch:** Advanced Google L5 boundary.
- **Premium:** Skip if inaccessible or replace with an equivalent problem.

---

# The DP Derivation Framework

For every problem, write these seven items before coding:

1. **State**
   - What does `dp[...]` mean exactly?
   - Use a complete sentence.

2. **Decision**
   - What choices are available from this state?

3. **Transition**
   - How does the current state depend on smaller states?

4. **Base cases**
   - What are the smallest valid states?
   - What represents an impossible state?

5. **Evaluation order**
   - Which dependencies must already be computed?

6. **Answer location**
   - Is the answer `dp[n]`, `dp[0]`, a maximum over states, or a sum?

7. **Complexity**
   - Number of states × transition cost per state.

Do not code until the state meaning is precise.

---

# Pattern 110: Dynamic Programming Foundations

These questions establish the fundamental recurrence-building process.

## Linear recurrence foundations

1. **LC 70 — Climbing Stairs**  
   Easy | P0  
   State: Number of ways to reach step `i`.  
   Focus: Fibonacci-style recurrence and space compression.

2. **LC 746 — Min Cost Climbing Stairs**  
   Easy | P0  
   State: Minimum cost to reach or leave position `i`.  
   Focus: State-definition alternatives.

3. **LC 509 — Fibonacci Number**  
   Easy | P1  
   Focus: Recursion, memoization, tabulation and constant-space iteration.

4. **LC 1137 — N-th Tribonacci Number**  
   Easy | P1  
   Focus: Higher-order recurrence.

5. **LC 198 — House Robber**  
   Medium | P0  
   State: Best value using houses through index `i`.  
   Focus: Take versus skip.

6. **LC 213 — House Robber II**  
   Medium | P0  
   Focus: Convert a circular dependency into two linear cases.

7. **LC 740 — Delete and Earn**  
   Medium | P0  
   Focus: Aggregate by value and reduce to House Robber.

8. **LC 256 — Paint House**  
   Medium | P0 | Premium  
   Focus: Position plus previous-category constraint.

9. **LC 265 — Paint House II**  
   Hard | P1 | Premium  
   Focus: Optimize transitions using smallest and second-smallest previous values.

10. **LC 276 — Paint Fence**  
    Medium | P1 | Premium  
    Focus: Track equal and different ending states.

11. **LC 91 — Decode Ways**  
    Medium | P0  
    Focus: One-character and two-character transitions.

12. **LC 639 — Decode Ways II**  
    Hard | P0 / Stretch  
    Focus: Weighted transitions for wildcard characters.

13. **LC 650 — 2 Keys Keyboard**  
    Medium | P1  
    Focus: Factorization or state including clipboard contents.

14. **LC 991 — Broken Calculator**  
    Medium | P2  
    Focus: Compare greedy reverse reasoning with DP-like forward state.

15. **LC 1025 — Divisor Game**  
    Easy | P1  
    Focus: Winning-state recurrence and mathematical simplification.

## Foundation mastery

You must be able to:

- Convert naive recursion into memoization.
- Identify repeated subproblems.
- Remove irrelevant state variables.
- Convert top-down memoization into bottom-up tabulation.
- Compress memory only after validating dependencies.
- Distinguish number of ways from minimum cost and maximum value.

---

# Pattern 111: One-Dimensional Dynamic Programming

The index usually represents a prefix, position, day or endpoint.

## Maximum and minimum value

16. **LC 53 — Maximum Subarray**  
    Medium | P0  
    State: Best subarray ending exactly at `i`.  
    Focus: Extend versus restart.

17. **LC 152 — Maximum Product Subarray**  
    Medium | P0  
    State: Maximum and minimum products ending at `i`.  
    Focus: Negative values swap extrema.

18. **LC 918 — Maximum Sum Circular Subarray**  
    Medium | P0  
    Focus: Maximum ordinary subarray versus total minus minimum subarray.

19. **LC 1567 — Maximum Length of Subarray With Positive Product**  
    Medium | P1  
    Focus: Positive and negative ending-length states.

20. **LC 1749 — Maximum Absolute Sum of Any Subarray**  
    Medium | P1  
    Focus: Track maximum and minimum ending sums.

21. **LC 1186 — Maximum Subarray Sum with One Deletion**  
    Medium | P0  
    State: Best ending sum with zero or one deletion used.

22. **LC 2321 — Maximum Score of Spliced Array**  
    Hard | P1  
    Focus: Convert one selected segment into a maximum-gain subarray.

23. **LC 2606 — Find the Substring With Maximum Cost**  
    Medium | P1  
    Focus: Kadane on transformed character weights.

## Reachability and minimum operations

24. **LC 55 — Jump Game**  
    Medium | P0  
    Focus: DP reachability and greedy reduction.

25. **LC 45 — Jump Game II**  
    Medium | P0  
    Focus: Minimum jumps; compare quadratic DP, BFS layers and greedy.

26. **LC 322 — Coin Change**  
    Medium | P0  
    State: Minimum coins required for each amount.

27. **LC 279 — Perfect Squares**  
    Medium | P0  
    Focus: Minimum unbounded transitions.

28. **LC 983 — Minimum Cost For Tickets**  
    Medium | P0  
    Focus: Day-index or travel-index state.

29. **LC 1340 — Jump Game V**  
    Hard | P1  
    Focus: Ordered DFS memoization over valid jumps.

30. **LC 1696 — Jump Game VI**  
    Medium | P0  
    Focus: DP transition optimized by monotonic deque.

31. **LC 1871 — Jump Game VII**  
    Medium | P0  
    Focus: Reachability window optimized by prefix counts or sliding window.

32. **LC 2361 — Minimum Costs Using the Train Line**  
    Hard | P1  
    Focus: Two-mode positional DP.

33. **LC 2147 — Number of Ways to Divide a Long Corridor**  
    Hard | P1  
    Focus: Structural counting after identifying forced groups.

## Counting sequences

34. **LC 377 — Combination Sum IV**  
    Medium | P0  
    Focus: Ordered sequence counting.

35. **LC 1269 — Number of Ways to Stay in the Same Place After Some Steps**  
    Hard | P1  
    Focus: Step and position DP with bounded useful width.

36. **LC 2466 — Count Ways To Build Good Strings**  
    Medium | P0  
    Focus: Forward counting with two allowed increments.

37. **LC 2266 — Count Number of Texts**  
    Medium | P1  
    Focus: Run-specific recurrence.

38. **LC 1416 — Restore The Array**  
    Hard | P0  
    Focus: Prefix parsing with numeric bounds.

39. **LC 600 — Non-negative Integers without Consecutive Ones**  
    Hard | P1  
    Focus: Fibonacci counting and digit-DP interpretation.

---

# Pattern 112: Basic Counting & Unbounded Transitions

The same action may be used repeatedly.

The most important distinction is loop order:

- Iterate amounts outside, choices inside to count ordered sequences.
- Iterate choices outside, amounts inside to count unordered combinations.

40. **LC 322 — Coin Change**  
    Medium | P0  
    Focus: Minimize item count with unlimited reuse.

41. **LC 518 — Coin Change II**  
    Medium | P0  
    Focus: Count unordered combinations.

42. **LC 377 — Combination Sum IV**  
    Medium | P0  
    Focus: Count ordered compositions.

43. **LC 279 — Perfect Squares**  
    Medium | P0  
    Focus: Unbounded minimum-item recurrence.

44. **LC 343 — Integer Break**  
    Medium | P0  
    Focus: Product maximization through partition.

45. **LC 1449 — Form Largest Integer With Digits That Add up to Target**  
    Hard | P0  
    Focus: Unbounded value maximization with lexicographic reconstruction.

46. **LC 1155 — Number of Dice Rolls With Target Sum**  
    Medium | P0  
    Focus: Bounded repeated transitions.

47. **LC 494 — Target Sum**  
    Medium | P0  
    Focus: Sign assignment reduced to subset-sum counting.

48. **LC 879 — Profitable Schemes**  
    Hard | P0  
    Focus: Two-dimensional bounded knapsack with capped profit.

49. **LC 2585 — Number of Ways to Earn Points**  
    Hard | P1  
    Focus: Bounded multiplicity transitions.

50. **LC 2902 — Count of Sub-Multisets With Bounded Sum**  
    Hard | Stretch  
    Focus: Frequency-compressed bounded knapsack.

---

# Pattern 113: Knapsack Foundations

## 0/1 knapsack

Each item may be selected at most once.

51. **LC 416 — Partition Equal Subset Sum**  
    Medium | P0  
    Focus: Boolean subset-sum reachability.

52. **LC 494 — Target Sum**  
    Medium | P0  
    Focus: Algebraic reduction to subset count.

53. **LC 474 — Ones and Zeroes**  
    Medium | P0  
    Focus: Two-capacity 0/1 knapsack.

54. **LC 1049 — Last Stone Weight II**  
    Medium | P0  
    Focus: Partition values into two nearly equal groups.

55. **LC 879 — Profitable Schemes**  
    Hard | P0  
    Focus: Capacity plus capped objective dimension.

56. **LC 956 — Tallest Billboard**  
    Hard | P0 / Stretch  
    Focus: Difference-state knapsack.

57. **LC 1755 — Closest Subsequence Sum**  
    Hard | Stretch  
    Focus: Meet-in-the-middle alternative to large-capacity DP.

58. **LC 2035 — Partition Array Into Two Arrays to Minimize Sum Difference**  
    Hard | Stretch  
    Focus: Meet-in-the-middle grouped by selected-item count.

59. **LC 805 — Split Array With Same Average**  
    Hard | Stretch  
    Focus: Cardinality-sensitive subset sum.

60. **LC 1774 — Closest Dessert Cost**  
    Medium | P1  
    Focus: Base selection plus bounded toppings.

## Knapsack implementation rules

For one-dimensional 0/1 knapsack:

- Iterate capacity backward.
- Backward iteration prevents reusing the same item.

For unbounded knapsack:

- Iterate capacity forward.
- Forward iteration allows reuse of the current item.

For two-dimensional capacities:

- Both capacity dimensions generally iterate backward for 0/1 selection.

---

# Pattern 114: State-Compressed Tree DP

This pattern includes trees where each node returns a small vector of states.

61. **LC 337 — House Robber III**  
    Medium | P0  
    State: Best result when taking or skipping the node.

62. **LC 968 — Binary Tree Cameras**  
    Hard | P0  
    State: Has camera, covered, or requires coverage.

63. **LC 979 — Distribute Coins in Binary Tree**  
    Medium | P0  
    State: Subtree balance returned to the parent.

64. **LC 124 — Binary Tree Maximum Path Sum**  
    Hard | P0  
    Focus: Downward contribution versus global answer.

65. **LC 1373 — Maximum Sum BST in Binary Tree**  
    Hard | P0  
    State: Validity, minimum, maximum and sum.

66. **LC 1519 — Number of Nodes in the Sub-Tree With the Same Label**  
    Medium | P0  
    Focus: Merge label-frequency vectors.

67. **LC 2246 — Longest Path With Different Adjacent Characters**  
    Hard | P0  
    Focus: Keep the two best compatible child chains.

68. **LC 2925 — Maximum Score After Applying Operations on a Tree**  
    Medium/Hard | P1  
    Focus: Preserve a required contribution in every root-to-leaf path.

69. **LC 834 — Sum of Distances in Tree**  
    Hard | P0  
    Focus: Subtree DP plus rerooting.

70. **LC 2458 — Height of Binary Tree After Subtree Removal Queries**  
    Hard | Stretch  
    Focus: Inside-subtree and outside-subtree information.

---

# Pattern 115: Longest Increasing Subsequence Family

You must know both:

- `O(n²)` DP.
- `O(n log n)` tails-array method.

The tails array does not necessarily represent an actual subsequence. It stores the smallest possible tail for each length.

## Core LIS

71. **LC 300 — Longest Increasing Subsequence**  
    Medium | P0  
    Focus: Quadratic DP and binary-search optimization.

72. **LC 673 — Number of Longest Increasing Subsequences**  
    Medium | P0  
    State: Best length and count ending at each position.

73. **LC 354 — Russian Doll Envelopes**  
    Hard | P0  
    Focus: Sort width ascending and height descending before LIS.

74. **LC 646 — Maximum Length of Pair Chain**  
    Medium | P0  
    Focus: LIS-style DP versus interval greedy.

75. **LC 1027 — Longest Arithmetic Subsequence**  
    Medium | P0  
    Focus: DP indexed by endpoint and difference.

76. **LC 1218 — Longest Arithmetic Subsequence of Given Difference**  
    Medium | P0  
    Focus: Hash-map DP by value.

77. **LC 368 — Largest Divisible Subset**  
    Medium | P0  
    Focus: Sorted DAG and predecessor reconstruction.

78. **LC 1048 — Longest String Chain**  
    Medium | P0  
    Focus: Ordered DAG by word length.

79. **LC 1964 — Find the Longest Valid Obstacle Course at Each Position**  
    Hard | P0  
    Focus: Non-decreasing LIS using upper bound.

80. **LC 1626 — Best Team With No Conflicts**  
    Medium | P0  
    Focus: Sorting removes one constraint before LIS-style DP.

81. **LC 1691 — Maximum Height by Stacking Cuboids**  
    Hard | P1  
    Focus: Normalize dimensions and perform multidimensional LIS.

82. **LC 2407 — Longest Increasing Subsequence II**  
    Hard | Stretch  
    Focus: Segment-tree-optimized LIS with bounded value difference.

## Reconstruction requirement

For LIS reconstruction, store:

- Best length ending at each index.
- Predecessor index.
- Index where the global best sequence ends.

Be prepared to return an actual subsequence, not just its length.

---

# Pattern 116: Arithmetic & Monotonic Subsequences

83. **LC 1027 — Longest Arithmetic Subsequence**  
    Medium | P0  
    Focus: Endpoint plus difference.

84. **LC 1218 — Longest Arithmetic Subsequence of Given Difference**  
    Medium | P0  
    Focus: Value-indexed transition.

85. **LC 446 — Arithmetic Slices II: Subsequence**  
    Hard | P0  
    Focus: Count arithmetic subsequences ending at each index.

86. **LC 413 — Arithmetic Slices**  
    Medium | P0  
    Focus: Contiguous arithmetic runs.

87. **LC 376 — Wiggle Subsequence**  
    Medium | P0  
    Focus: Up and down states; greedy equivalence.

88. **LC 978 — Longest Turbulent Subarray**  
    Medium | P1  
    Focus: Alternating comparison state.

89. **LC 873 — Length of Longest Fibonacci Subsequence**  
    Medium | P0  
    Focus: Pair endpoints and predecessor lookup.

90. **LC 2111 — Minimum Operations to Make the Array K-Increasing**  
    Hard | P1  
    Focus: Split by residue classes and solve non-decreasing LIS.

91. **LC 960 — Delete Columns to Make Sorted III**  
    Hard | P1  
    Focus: LIS over columns under row-wise compatibility.

92. **LC 1671 — Minimum Number of Removals to Make Mountain Array**  
    Hard | P0  
    Focus: LIS from both directions.

---

# Pattern 117: Stack-State Dynamic Programming

These problems include a state representing an open count, unmatched structures, or stack-like unresolved choices.

93. **LC 32 — Longest Valid Parentheses**  
    Hard | P0  
    Focus: DP by valid suffix ending at each position.

94. **LC 678 — Valid Parenthesis String**  
    Medium | P0  
    Focus: Open-count DP and greedy bounds.

95. **LC 1541 — Minimum Insertions to Balance a Parentheses String**  
    Medium | P1  
    Focus: Required-closing state.

96. **LC 2116 — Check if a Parentheses String Can Be Valid**  
    Medium | P0  
    Focus: Position and balance feasibility; greedy interval alternative.

97. **LC 1963 — Minimum Number of Swaps to Make String Balanced**  
    Medium | P1  
    Focus: Balance deficits.

98. **LC 301 — Remove Invalid Parentheses**  
    Hard | Stretch  
    Focus: Decision search and balance state.

99. **LC 1000 — Minimum Cost to Merge Stones**  
    Hard | P0 / Stretch  
    Focus: Interval DP with pile-count state.

100. **LC 1130 — Minimum Cost Tree From Leaf Values**  
     Medium | P0  
     Focus: Interval DP and monotonic-stack alternative.

---

# Pattern 118: Grid-Path Dynamic Programming

Movement is usually directional, making the grid a DAG.

## Basic grid paths

101. **LC 62 — Unique Paths**  
     Medium | P0  
     Focus: Count paths from top-left to bottom-right.

102. **LC 63 — Unique Paths II**  
     Medium | P0  
     Focus: Obstacles reset reachability.

103. **LC 64 — Minimum Path Sum**  
     Medium | P0  
     Focus: Minimize accumulated path cost.

104. **LC 120 — Triangle**  
     Medium | P0  
     Focus: Bottom-up rolling DP.

105. **LC 931 — Minimum Falling Path Sum**  
     Medium | P0  
     Focus: Previous-row neighborhood.

106. **LC 1289 — Minimum Falling Path Sum II**  
     Hard | P0  
     Focus: Smallest and second-smallest previous-row values.

107. **LC 2304 — Minimum Path Cost in a Grid**  
     Medium | P1  
     Focus: Value-dependent transition costs.

108. **LC 1301 — Number of Paths with Max Score**  
     Hard | P1  
     Focus: Optimize score and count optimal paths simultaneously.

109. **LC 2267 — Check if There Is a Valid Parentheses String Path**  
     Hard | P0  
     Focus: Grid position plus balance state.

110. **LC 174 — Dungeon Game**  
     Hard | P0  
     Focus: Minimum required health working backward.

111. **LC 741 — Cherry Pickup**  
     Hard | P0 / Stretch  
     Focus: Two synchronized walkers.

112. **LC 1463 — Cherry Pickup II**  
     Hard | P0  
     Focus: Row plus two column positions.

113. **LC 2435 — Paths in Matrix Whose Sum Is Divisible by K**  
     Hard | P0  
     Focus: Position plus modulo state.

114. **LC 2328 — Number of Increasing Paths in a Grid**  
     Hard | P0  
     Focus: Grid converted into a DAG by value ordering.

---

# Pattern 119: Grid-Shaped Dynamic Programming

This category includes rectangles, squares, neighborhood states and row masks.

115. **LC 221 — Maximal Square**  
     Medium | P0  
     Focus: Largest square ending at each cell.

116. **LC  maximal rectangle alternative**  
     Study with LC 85  
     Focus: Row histograms and stack, not pure DP.

117. **LC 1277 — Count Square Submatrices with All Ones**  
     Medium | P0  
     Focus: Square-size recurrence.

118. **LC  maximal plus-sign variants: LC 764 — Largest Plus Sign**  
     Medium | P1  
     Focus: Four directional run lengths.

119. **LC 562 — Longest Line of Consecutive One in Matrix**  
     Medium | P1 | Premium  
     Focus: Four direction-specific states.

120. **LC 2684 — Maximum Number of Moves in a Grid**  
     Medium | P1  
     Focus: Column-ordered reachability.

121. **LC 329 — Longest Increasing Path in a Matrix**  
     Hard | P0  
     Focus: Memoized DAG DP.

122. **LC 1349 — Maximum Students Taking Exam**  
     Hard | Stretch  
     Focus: Row-mask DP with inter-row compatibility.

123. **LC 1659 — Maximize Grid Happiness**  
     Hard | Stretch  
     Focus: Profile DP with encoded previous-row state.

124. **LC 1931 — Painting a Grid With Three Different Colors**  
     Hard | Stretch  
     Focus: Enumerate valid column masks and compatibility.

125. **LC 1723-style profile assignment variants**  
     Optional  
     Focus: Compress small-width grid state rather than whole grid history.

---

# Pattern 120: Palindromic Dynamic Programming

Distinguish:

- Palindromic substring: contiguous.
- Palindromic subsequence: not necessarily contiguous.
- Count all palindromes.
- Minimum cuts.
- Minimum insertions or deletions.
- Enumerate partitions.

## Substrings and partitions

126. **LC 5 — Longest Palindromic Substring**  
     Medium | P0  
     Focus: Interval DP and center expansion.

127. **LC 647 — Palindromic Substrings**  
     Medium | P0  
     Focus: Count all palindromic intervals.

128. **LC 131 — Palindrome Partitioning**  
     Medium | P0  
     Focus: Palindrome preprocessing plus backtracking.

129. **LC 132 — Palindrome Partitioning II**  
     Hard | P0  
     Focus: Minimum cuts over palindromic suffixes.

130. **LC 1278 — Palindrome Partitioning III**  
     Hard | P0  
     Focus: Interval conversion cost plus partition DP.

131. **LC 1745 — Palindrome Partitioning IV**  
     Hard | P1  
     Focus: Three-part feasibility.

132. **LC 2472 — Maximum Number of Non-overlapping Palindrome Substrings**  
     Hard | P1  
     Focus: Palindrome detection plus prefix optimization.

## Subsequences

133. **LC 516 — Longest Palindromic Subsequence**  
     Medium | P0  
     Focus: Interval DP or LCS with reversed string.

134. **LC 1312 — Minimum Insertion Steps to Make a String Palindrome**  
     Hard | P0  
     Focus: `n - LPS` or direct interval DP.

135. **LC 730 — Count Different Palindromic Subsequences**  
     Hard | Stretch  
     Focus: Duplicate-sensitive interval counting.

136. **LC 1771 — Maximize Palindrome Length From Subsequences**  
     Hard | Stretch  
     Focus: LPS across a concatenated boundary.

137. **LC 1682 — Longest Palindromic Subsequence II**  
     Hard | Stretch | Premium  
     Focus: Interval state with outer-character restrictions.

---

# Pattern 121: Two-String Dynamic Programming

Typically:

`dp[i][j] = answer for a prefix or suffix of string A and string B`

## LCS family

138. **LC 1143 — Longest Common Subsequence**  
     Medium | P0  
     Focus: Canonical two-string DP.

139. **LC 583 — Delete Operation for Two Strings**  
     Medium | P0  
     Focus: Reduce to LCS or direct edit recurrence.

140. **LC 712 — Minimum ASCII Delete Sum for Two Strings**  
     Medium | P0  
     Focus: Weighted deletions.

141. **LC 1092 — Shortest Common Supersequence**  
     Hard | P0  
     Focus: LCS-guided reconstruction.

142. **LC 1035 — Uncrossed Lines**  
     Medium | P0  
     Focus: LCS interpretation.

143. **LC 1458 — Max Dot Product of Two Subsequences**  
     Hard | P0  
     Focus: Matching weighted elements with non-empty enforcement.

## Edit distance family

144. **LC 72 — Edit Distance**  
     Medium | P0  
     Focus: Insert, delete and replace.

145. **LC 161 — One Edit Distance**  
     Medium | P1 | Premium  
     Focus: Boundary case analysis and direct solution.

146. **LC 115 — Distinct Subsequences**  
     Hard | P0  
     Focus: Count ways one string forms another.

147. **LC 392 — Is Subsequence**  
     Easy | P1  
     Focus: Two-pointer baseline.

148. **LC 524 — Longest Word in Dictionary through Deleting**  
     Medium | P1  
     Focus: Repeated subsequence checking.

149. **LC 727 — Minimum Window Subsequence**  
     Hard | P0 | Premium  
     Focus: Subsequence-aligned window DP.

150. **LC 97 — Interleaving String**  
     Medium | P0  
     Focus: Prefix lengths from two strings.

---

# Pattern 122: Interleaving & Shuffle Reconstruction

151. **LC 97 — Interleaving String**  
     Medium | P0  
     State: Whether prefixes of two strings form a target prefix.

152. **LC 87 — Scramble String**  
     Hard | P0 / Stretch  
     State: Two starts plus substring length.

153. **LC 44-style shuffle matching variants**  
     Optional  
     Focus: Branching over two source sequences.

154. **LC 1092 — Shortest Common Supersequence**  
     Hard | P0  
     Focus: Reconstruct a sequence preserving both input orders.

155. **LC 727 — Minimum Window Subsequence**  
     Hard | P0 | Premium  
     Focus: Locate the shortest target-preserving source interval.

156. **LC 115 — Distinct Subsequences**  
     Hard | P0  
     Focus: Count alignment choices.

### Scramble String mastery

For `Scramble String`, know:

- State `(i, j, length)`.
- Split into swapped and non-swapped cases.
- Character-frequency pruning.
- Why exponential recursion becomes polynomial with memoization.
- Why substring creation can add avoidable overhead.

---

# Pattern 123: Pattern-Matching Dynamic Programming

157. **LC 10 — Regular Expression Matching**  
     Hard | P0  
     Focus: `.` and `*` with zero-or-more interpretation.

158. **LC 44 — Wildcard Matching**  
     Hard | P0  
     Focus: `?` and `*` matching arbitrary sequences.

159. **LC 139 — Word Break**  
     Medium | P0  
     Focus: Prefix segmentation.

160. **LC 97 — Interleaving String**  
     Medium | P0  
     Focus: Match target through two sources.

161. **LC 678 — Valid Parenthesis String**  
     Medium | P1  
     Focus: Pattern uncertainty represented as a range of balances.

162. **LC 1639 — Number of Ways to Form a Target String Given a Dictionary**  
     Hard | P0  
     Focus: Column frequencies plus target-prefix DP.

163. **LC 2060 — Check if an Original String Exists Given Two Encoded Strings**  
     Hard | Stretch  
     Focus: Position pair plus unmatched decoded-length difference.

### Regex warning

In LC 10:

- `*` modifies the preceding token.
- It does not independently match arbitrary characters.
- The transition must permit both:
  - Zero occurrences.
  - One or more occurrences when the token matches.

---

# Pattern 124: Word Segmentation & Dictionary DP

164. **LC 139 — Word Break**  
     Medium | P0  
     Focus: Boolean segmentation.

165. **LC 140 — Word Break II**  
     Hard | P0  
     Focus: Enumerate valid segmentations with memoized suffix results.

166. **LC 472 — Concatenated Words**  
     Hard | P0  
     Focus: Repeated dictionary segmentation.

167. **LC 1048 — Longest String Chain**  
     Medium | P0  
     Focus: Words ordered by length and predecessor deletion.

168. **LC 2707 — Extra Characters in a String**  
     Medium | P0  
     Focus: Minimize uncovered characters.

169. **LC 1449 — Form Largest Integer With Digits That Add up to Target**  
     Hard | P0  
     Focus: String-valued reconstruction under cost constraints.

170. **LC 1639 — Ways to Form a Target String**  
     Hard | P0  
     Focus: Dictionary-column aggregation.

171. **LC 1713 — Minimum Operations to Make a Subsequence**  
     Hard | P0  
     Focus: Map target values to indices and solve LIS.

172. **LC 1255 — Maximum Score Words Formed by Letters**  
     Hard | P1  
     Focus: Subset decision with letter capacities.

---

# Pattern 125: Distance-Based Subsequences & String Counting

173. **LC 115 — Distinct Subsequences**  
     Hard | P0  
     Focus: Count source-to-target alignments.

174. **LC 940 — Distinct Subsequences II**  
     Hard | P0  
     Focus: Correct duplicate overcounting through last occurrence.

175. **LC 1639 — Ways to Form a Target String**  
     Hard | P0  
     Focus: Position-aligned counting.

176. **LC 2262 — Total Appeal of A String**  
     Hard | P0  
     Focus: Contribution of the most recent occurrence.

177. **LC 828 — Count Unique Characters of All Substrings**  
     Hard | P0  
     Focus: Previous and next occurrence contribution.

178. **LC 1930 — Unique Length-3 Palindromic Subsequences**  
     Medium | P1  
     Focus: Boundary occurrence and middle-character counting.

179. **LC 730 — Count Different Palindromic Subsequences**  
     Hard | Stretch  
     Focus: Duplicate-sensitive interval counting.

180. **LC 1220 — Count Vowels Permutation**  
     Hard | P0  
     Focus: Small finite-state transition system.

181. **LC 2466 — Count Ways To Build Good Strings**  
     Medium | P0  
     Focus: Length-based counting.

---

# Pattern 126: Partition Dynamic Programming

Partition DP usually has the form:

`dp[i] = best answer for the first i elements`

Transition:

`dp[i] = best over all valid previous cut positions j`

## Core partitioning

182. **LC 139 — Word Break**  
     Medium | P0  
     Focus: Boolean prefix partition.

183. **LC 132 — Palindrome Partitioning II**  
     Hard | P0  
     Focus: Minimum cuts.

184. **LC 1278 — Palindrome Partitioning III**  
     Hard | P0  
     Focus: Exactly `k` partitions with conversion costs.

185. **LC 1043 — Partition Array for Maximum Sum**  
     Medium | P0  
     Focus: Bounded last-segment length.

186. **LC 1335 — Minimum Difficulty of a Job Schedule**  
     Hard | P0  
     Focus: Prefix partition by days.

187. **LC 410 — Split Array Largest Sum**  
     Hard | P0  
     Focus: Minimax partition DP and binary-search alternative.

188. **LC 813 — Largest Sum of Averages**  
     Medium | P0  
     Focus: Exact or at-most group partitioning.

189. **LC 1105 — Filling Bookcase Shelves**  
     Medium | P0  
     Focus: Last-shelf partition.

190. **LC 1478 — Allocate Mailboxes**  
     Hard | P0  
     Focus: Segment cost preprocessing plus partition DP.

191. **LC 1959 — Minimum Total Space Wasted With K Resizing Operations**  
     Hard | P1  
     Focus: Segment waste plus number of resizes.

192. **LC 2547 — Minimum Cost to Split an Array**  
     Hard | P0  
     Focus: Incrementally maintain segment duplicate cost.

193. **LC 2478 — Number of Beautiful Partitions**  
     Hard | Stretch  
     Focus: Constrained cut positions and optimized counting.

194. **LC 2463 — Minimum Total Distance Traveled**  
     Hard | P0  
     Focus: Assign ordered robots to ordered factories.

### Partition-DP optimization

When trying all previous cuts is too slow, investigate:

- Prefix-sum segment costs.
- Incremental maintenance while extending the final segment backward.
- Monotonic queue.
- Divide-and-conquer optimization.
- Convex Hull Trick.
- A binary-search transformation when the objective is minimax feasibility.

---

# Pattern 127: Interval Dynamic Programming

State is usually based on an interval:

`dp[l][r]`

Evaluation order typically increases interval length.

## Core interval problems

195. **LC 516 — Longest Palindromic Subsequence**  
     Medium | P0  
     Focus: Match or discard interval endpoints.

196. **LC 312 — Burst Balloons**  
     Hard | P0  
     Focus: Choose the last balloon burst inside an interval.

197. **LC 1039 — Minimum Score Triangulation of Polygon**  
     Medium | P0  
     Focus: Choose a split vertex.

198. **LC 1000 — Minimum Cost to Merge Stones**  
     Hard | P0 / Stretch  
     Focus: Interval plus remaining pile count.

199. **LC 1547 — Minimum Cost to Cut a Stick**  
     Hard | P0  
     Focus: Choose the first or last cut inside an interval.

200. **LC 1130 — Minimum Cost Tree From Leaf Values**  
     Medium | P0  
     Focus: Partition interval and combine maxima.

201. **LC 375 — Guess Number Higher or Lower II**  
     Medium | P0  
     Focus: Minimize worst-case cost.

202. **LC 486 — Predict the Winner**  
     Medium | P0  
     Focus: Score-difference interval DP.

203. **LC 877 — Stone Game**  
     Medium | P1  
     Focus: Difference recurrence and mathematical shortcut.

204. **LC 1140 — Stone Game II**  
     Medium | P0  
     Focus: Position plus dynamic maximum-take parameter.

205. **LC 1406 — Stone Game III**  
     Hard | P0  
     Focus: Score-difference suffix DP.

206. **LC 1510 — Stone Game IV**  
     Hard | P1  
     Focus: Winning-state recurrence.

207. **LC 1690 — Stone Game VII**  
     Medium | P0  
     Focus: Interval sum and score difference.

208. **LC 1686 — Stone Game VI**  
     Medium | P1  
     Focus: Recognize greedy rather than forcing interval DP.

209. **LC 1770 — Maximum Score from Performing Multiplication Operations**  
     Medium | P0  
     Focus: Number taken from left determines the right endpoint.

210. **LC 546 — Remove Boxes**  
     Hard | Stretch  
     Focus: Interval state with carried equal boxes.

211. **LC 664 — Strange Printer**  
     Hard | P0 / Stretch  
     Focus: Merge print operations for matching characters.

212. **LC 730 — Count Different Palindromic Subsequences**  
     Hard | Stretch  
     Focus: Duplicate-aware interval recurrence.

### Interval-DP recognition

Look for:

- Removing or processing endpoints.
- Choosing the final operation.
- Splitting a range at every possible pivot.
- Merging adjacent groups.
- Optimal parenthesization.
- A game where players choose from either end.
- A polygon, chain or sequence partition.

---

# Pattern 128: Complex Positional & Circular DP

## Circular structures

213. **LC 213 — House Robber II**  
     Medium | P0  
     Focus: Exclude first or exclude last.

214. **LC 918 — Maximum Sum Circular Subarray**  
     Medium | P0  
     Focus: Non-wrapping versus wrapping case.

215. **LC 1388 — Pizza With 3n Slices**  
     Hard | P0  
     Focus: Circular exact-cardinality selection.

216. **LC 1888 — Minimum Number of Flips to Make Binary String Alternating**  
     Medium | P1  
     Focus: Duplicate the string and use a fixed-size window.

## Multi-position state

217. **LC 1770 — Maximum Score from Multiplication Operations**  
     Medium | P0  
     Focus: Operation index plus number taken from the left.

218. **LC 1463 — Cherry Pickup II**  
     Hard | P0  
     Focus: Two positions on each row.

219. **LC 741 — Cherry Pickup**  
     Hard | Stretch  
     Focus: Synchronize two walkers by total steps.

220. **LC 1771 — Maximize Palindrome Length From Subsequences**  
     Hard | Stretch  
     Focus: Interval DP with cross-string requirement.

221. **LC 1263-style multi-agent problems**  
     Optional  
     Focus: Determine whether state should include two positions.

222. **LC 935 — Knight Dialer**  
     Medium | P0  
     Focus: Position and move count.

223. **LC 1220 — Count Vowels Permutation**  
     Hard | P0  
     Focus: Small transition graph.

224. **LC 576 — Out of Boundary Paths**  
     Medium | P0  
     Focus: Position and moves remaining.

225. **LC 688 — Knight Probability in Chessboard**  
     Medium | P0  
     Focus: Probability mass by position and step.

---

# Pattern 129: Probability Dynamic Programming

Probability DP requires careful definition of whether state stores:

- Probability of reaching a state.
- Probability of eventual success.
- Expected value.
- Distribution over outcomes.
- Count of equally likely outcomes.

226. **LC 688 — Knight Probability in Chessboard**  
     Medium | P0  
     Focus: Propagate probability mass over moves.

227. **LC 837 — New 21 Game**  
     Medium | P0  
     Focus: Sliding-window optimization of probability recurrence.

228. **LC 808 — Soup Servings**  
     Medium | P0  
     Focus: Memoized probability with state scaling and asymptotic cutoff.

229. **LC 1230 — Toss Strange Coins**  
     Medium | P0 | Premium  
     Focus: Exact number of successes.

230. **LC 1227 — Airplane Seat Assignment Probability**  
     Medium | P2  
     Focus: Mathematical simplification.

231. **LC 1467 — Probability of a Two Boxes Having The Same Number of Distinct Balls**  
     Hard | Stretch  
     Focus: Combinatorial probability DP.

232. **LC 1514 — Path with Maximum Probability**  
     Medium | P1  
     Focus: Graph optimization rather than ordinary probability DP.

233. **LC 1143-style expectation variants**  
     Optional  
     Focus: Clearly distinguish expected value from direct probability.

### Probability-DP checks

- Do probabilities leaving a state sum to one?
- Are outcomes equally likely?
- Is a combinatorial coefficient required?
- Is the answer conditional on a terminal event?
- Can continuous-looking quantities be discretized?
- Can negligible tail states be bounded safely?

---

# Pattern 130: Digit Dynamic Programming

Digit DP counts integers satisfying digit-based constraints without enumerating every integer.

Typical state:

`dp[position][tight][started][additional state]`

Additional state may include:

- Digit sum.
- Modulo remainder.
- Used-digit mask.
- Previous digit.
- Count of a particular digit.
- Whether a forbidden pattern has appeared.

## Foundational digit DP

234. **LC 233 — Number of Digit One**  
     Hard | P0  
     Focus: Count occurrences of digit `1` up to `n`.

235. **LC 357 — Count Numbers with Unique Digits**  
     Medium | P1  
     Focus: Used-digit tracking and combinatorics.

236. **LC 600 — Non-negative Integers without Consecutive Ones**  
     Hard | P0  
     Focus: Binary digit DP with previous-bit state.

237. **LC 788 — Rotated Digits**  
     Medium | P1  
     Focus: Digit category state.

238. **LC 902 — Numbers At Most N Given Digit Set**  
     Hard | P0  
     Focus: Tight prefix and shorter-length counting.

239. **LC 1012 — Numbers With Repeated Digits**  
     Hard | P0  
     Focus: Count unique-digit numbers and subtract.

240. **LC 1397 — Find All Good Strings**  
     Hard | Stretch  
     Focus: Digit DP over characters plus KMP automaton state.

241. **LC 2376 — Count Special Integers**  
     Hard | P0  
     Focus: Used-digit mask.

242. **LC 2719 — Count of Integers**  
     Hard | P0  
     Focus: Digit sum bounded within a range.

243. **LC 2801 — Count Stepping Numbers in Range**  
     Hard | P0  
     Focus: Previous digit and string-bounded range.

244. **LC 2827 — Number of Beautiful Integers in the Range**  
     Hard | P0  
     Focus: Modulo plus odd/even digit balance.

245. **LC 2999 — Count the Number of Powerful Integers**  
     Hard | P1  
     Focus: Digit bounds plus required suffix.

246. **LC 3352 — Count K-Reducible Numbers Less Than N**  
     Hard | Stretch  
     Focus: Binary digits, popcount and reduction depth.

### Digit-DP mastery

You should be able to explain:

- `tight`: whether the current prefix equals the bound’s prefix.
- `started`: whether a non-leading-zero digit has been placed.
- Why leading zeros should usually not enter a used-digit mask.
- How to compute a range answer as `count(R) - count(L - 1)`.
- When the number zero requires special handling.
- How to memoize only non-tight states, or include tight in the state.
- How to combine digit DP with an automaton for forbidden substrings.

---

# Pattern 131: Tree Dynamic Programming

## Basic subtree DP

247. **LC 337 — House Robber III**  
     Medium | P0  
     Focus: Take and skip states.

248. **LC 968 — Binary Tree Cameras**  
     Hard | P0  
     Focus: Three-state coverage.

249. **LC 979 — Distribute Coins**  
     Medium | P0  
     Focus: Subtree surplus.

250. **LC 124 — Binary Tree Maximum Path Sum**  
     Hard | P0  
     Focus: Best downward branch and global path.

251. **LC 1373 — Maximum Sum BST in Binary Tree**  
     Hard | P0  
     Focus: Composite subtree information.

## General tree DP and rerooting

252. **LC 834 — Sum of Distances in Tree**  
     Hard | P0  
     Focus: Subtree sizes, initial answer and reroot transition.

253. **LC 310 — Minimum Height Trees**  
     Medium | P0  
     Focus: Tree centers through leaf peeling.

254. **LC 1245 — Tree Diameter**  
     Medium | P0 | Premium  
     Focus: Two BFS/DFS passes or subtree DP.

255. **LC 2246 — Longest Path With Different Adjacent Characters**  
     Hard | P0  
     Focus: Two best child paths.

256. **LC 1519 — Number of Nodes in Sub-Tree With Same Label**  
     Medium | P0  
     Focus: Frequency-vector subtree aggregation.

257. **LC 2049 — Count Nodes With the Highest Score**  
     Medium | P0  
     Focus: Component sizes after removing a node.

258. **LC 1617 — Count Subtrees With Max Distance Between Cities**  
     Hard | Stretch  
     Focus: Subset enumeration plus diameter.

259. **LC 2925 — Maximum Score After Applying Operations on a Tree**  
     Hard | P1  
     Focus: Root-to-leaf validity and minimum preserved sum.

260. **LC 2538 — Difference Between Maximum and Minimum Price Sum**  
     Hard | Stretch  
     Focus: Multiple downward path states.

261. **LC 2646 — Minimize the Total Price of the Trips**  
     Hard | Stretch  
     Focus: Path-frequency aggregation plus tree independent-set DP.

262. **LC 1483 — Kth Ancestor of a Tree Node**  
     Hard | P1  
     Focus: Binary lifting rather than ordinary tree DP.

### Rerooting derivation

For LC 834:

1. Compute subtree sizes.
2. Compute the answer for one root.
3. Move the root across edge `u-v`.
4. Nodes inside `v`’s subtree become one step closer.
5. Other nodes become one step farther.

The transition is:

`answer[v] = answer[u] - subtreeSize[v] + (n - subtreeSize[v])`

Do not memorize this without understanding the two affected node groups.

---

# Pattern 132: Memoized Decision Search & Game DP

The state represents a decision position, and the result may be:

- Winning or losing.
- Best achievable score.
- Score difference.
- Minimum worst-case cost.
- Maximum guaranteed reward.

## Decision search

263. **LC 464 — Can I Win**  
     Medium | P0  
     Focus: Used-number mask and remaining target.

264. **LC 473 — Matchsticks to Square**  
     Medium | P0  
     Focus: Bucket construction and symmetry pruning.

265. **LC 698 — Partition to K Equal Sum Subsets**  
     Medium | P0  
     Focus: Used-mask memoization.

266. **LC 638 — Shopping Offers**  
     Medium | P0  
     Focus: Remaining-needs vector as a memoization key.

267. **LC 691 — Stickers to Spell Word**  
     Hard | P0 / Stretch  
     Focus: Canonical remaining-demand state.

268. **LC 1723 — Find Minimum Time to Finish All Jobs**  
     Hard | Stretch  
     Focus: Assignment search or subset DP.

269. **LC 1986 — Minimum Number of Work Sessions**  
     Medium | P0  
     Focus: Mask with current-session usage or subset partition.

270. **LC 1655 — Distribute Repeating Integers**  
     Hard | Stretch  
     Focus: Customer subset allocation.

## Game DP

271. **LC 486 — Predict the Winner**  
     Medium | P0  
     Focus: Maximum score difference.

272. **LC 877 — Stone Game**  
     Medium | P1  
     Focus: DP formulation and parity shortcut.

273. **LC 1140 — Stone Game II**  
     Medium | P0  
     Focus: Position and changing parameter `M`.

274. **LC 1406 — Stone Game III**  
     Hard | P0  
     Focus: Suffix score difference.

275. **LC 1510 — Stone Game IV**  
     Hard | P1  
     Focus: Winning-state recurrence.

276. **LC 1690 — Stone Game VII**  
     Medium | P0  
     Focus: Interval score difference.

277. **LC 1872 — Stone Game VIII**  
     Hard | Stretch  
     Focus: Prefix transformation and optimized recurrence.

278. **LC 2029 — Stone Game IX**  
     Medium | P1  
     Focus: Remainder counts and game-state reasoning.

279. **LC 913 — Cat and Mouse**  
     Hard | Stretch  
     Focus: Retrograde graph-game DP.

### Game-state principle

A particularly useful state stores:

`maximum score current player can achieve relative to the opponent`

Then:

`current advantage = immediate gain - opponent's best future advantage`

This often avoids storing both players’ scores.

---

# Pattern 133: Nim & Grundy Numbers

This section should remain lower priority than standard DP, but strict preparation should include recognition.

280. **LC 292 — Nim Game**  
     Easy | P0  
     Focus: Losing positions under fixed move rules.

281. **LC 877 — Stone Game**  
     Medium | P1  
     Focus: Understand why it is not ordinary Nim.

282. **LC 464 — Can I Win**  
     Medium | P0  
     Focus: Finite-state impartial game solved by memoization.

283. **LC 1025 — Divisor Game**  
     Easy | P1  
     Focus: Winning and losing positions.

284. **LC 1510 — Stone Game IV**  
     Hard | P1  
     Focus: Square-removal game.

285. **LC 1908 — Game of Nim**  
     Medium | P2 | Premium  
     Focus: XOR invariant across piles.

286. **LC 294 — Flip Game II**  
     Medium | P1 | Premium  
     Focus: Memoized winning-state search and Grundy decomposition concept.

287. **LC 1563 — Stone Game V**  
     Hard | Stretch  
     Focus: Partition game DP, not pure Nim.

### Grundy knowledge level

Understand:

- A terminal state has Grundy value zero.
- A state’s Grundy value is the minimum excluded value of its successors.
- Multiple independent games combine through XOR.
- A combined state is losing when the XOR of Grundy values is zero.

Do not overinvest in full Sprague-Grundy theory before mastering mainstream DP.

---

# Pattern 134: Matrix Exponentiation & Fast Recurrence

Matrix exponentiation converts a fixed linear recurrence into exponentiation of a transition matrix.

288. **LC 509 — Fibonacci Number**  
     Easy | P0 concept  
     Focus: Represent Fibonacci using a 2×2 matrix.

289. **LC 70 — Climbing Stairs**  
     Easy | P1 concept  
     Focus: Same recurrence structure.

290. **LC 1137 — Tribonacci Number**  
     Easy | P1 concept  
     Focus: Higher-dimensional transition matrix.

291. **LC 1220 — Count Vowels Permutation**  
     Hard | P1  
     Focus: Small finite-state transition matrix.

292. **LC 935 — Knight Dialer**  
     Medium | P1  
     Focus: Graph transition matrix.

293. **LC 552 — Student Attendance Record II**  
     Hard | P0 / Stretch  
     Focus: Finite automaton DP and matrix-exponentiation extension.

### Matrix-exponentiation mastery

Know:

- How to encode a linear recurrence as a state vector.
- How to derive the transition matrix.
- Why exponentiation by squaring takes `O(log n)` matrix multiplications.
- How modular arithmetic is applied.
- Why matrix exponentiation is useful only when transitions are fixed and linear.
- Why ordinary iterative DP is preferable when `n` is modest.

---

# Pattern 135: Advanced Recurrence & DP Optimization

This is the advanced boundary. Master recognition first, then implementation.

## Monotonic queue optimization

294. **LC 1696 — Jump Game VI**  
     Medium | P0  
     Focus: Sliding maximum over previous DP states.

295. **LC 1425 — Constrained Subsequence Sum**  
     Hard | P0  
     Focus: Maximum positive transition in a bounded window.

296. **LC 862 — Shortest Subarray with Sum at Least K**  
     Hard | P0  
     Focus: Monotonic deque over prefix sums.

297. **LC 2944 — Minimum Number of Coins for Fruits**  
     Medium | P1  
     Focus: Range-minimum transition optimization.

## Prefix/suffix transition optimization

298. **LC 1937 — Maximum Number of Points with Cost**  
     Medium | P0  
     Focus: Left and right sweeps replace quadratic transitions.

299. **LC 1289 — Minimum Falling Path Sum II**  
     Hard | P0  
     Focus: Smallest and second-smallest previous states.

300. **LC 265 — Paint House II**  
     Hard | P1 | Premium  
     Focus: Smallest and second-smallest colors.

301. **LC 689 — Maximum Sum of 3 Non-Overlapping Subarrays**  
     Hard | P0  
     Focus: Prefix best and suffix best reconstruction.

302. **LC 1235 — Maximum Profit in Job Scheduling**  
     Hard | P0  
     Focus: Sort, binary search and prefix-optimal DP.

303. **LC 1751 — Maximum Number of Events That Can Be Attended II**  
     Hard | P0  
     Focus: Event index, remaining selections and binary-search jump.

## Convex Hull Trick / line optimization

304. **LC 1478-style quadratic transition optimization**  
     Conceptual  
     Focus: Identify recurrences with linear-function comparisons.

305. **LC  CHT practice equivalents**  
     Optional  
     Focus: Slopes, intercepts and monotonic query order.

For Google L5, conceptual recognition is usually more important than memorizing a sophisticated arbitrary-order Li Chao tree.

## Divide-and-conquer DP optimization

306. **Partition-cost optimization family**  
     Conceptual  
     Focus: Recurrence of the form:

     `dp[g][i] = min over j < i of dp[g-1][j] + cost(j+1, i)`

Know that monotonicity of the optimal split can reduce transition complexity.

## State reduction and mathematical optimization

307. **LC 1186 — Maximum Subarray Sum With One Deletion**  
     Medium | P0  
     Focus: Reduce full history to two scalar states.

308. **LC 1223 — Dice Roll Simulation**  
     Hard | P1  
     Focus: Run-length state and prefix-total optimization.

309. **LC 1269 — Number of Ways to Stay in Same Place**  
     Hard | P1  
     Focus: Bound the position dimension by the number of steps.

310. **LC 1866 — Number of Ways to Rearrange Sticks With K Sticks Visible**  
     Hard | P1  
     Focus: Combinatorial recurrence.

311. **LC 920 — Number of Music Playlists**  
     Hard | P0  
     Focus: Number used and playlist length.

312. **LC 629 — K Inverse Pairs Array**  
     Hard | P0 / Stretch  
     Focus: Prefix sums optimize a range-sum recurrence.

313. **LC 879 — Profitable Schemes**  
     Hard | P0  
     Focus: Cap profit state at the required threshold.

314. **LC 1639 — Ways to Form Target String**  
     Hard | P0  
     Focus: Precompute column frequencies.

315. **LC 2478 — Number of Beautiful Partitions**  
     Hard | Stretch  
     Focus: Prefix sums over valid previous cuts.

---

# Strict P0 Core: Master Cold

## Foundational DP

- LC 53 — Maximum Subarray
- LC 70 — Climbing Stairs
- LC 91 — Decode Ways
- LC 198 — House Robber
- LC 213 — House Robber II
- LC 279 — Perfect Squares
- LC 322 — Coin Change
- LC 343 — Integer Break
- LC 377 — Combination Sum IV
- LC 518 — Coin Change II
- LC 740 — Delete and Earn
- LC 746 — Min Cost Climbing Stairs
- LC 983 — Minimum Cost for Tickets

## Knapsack and subset DP

- LC 416 — Partition Equal Subset Sum
- LC 474 — Ones and Zeroes
- LC 494 — Target Sum
- LC 879 — Profitable Schemes
- LC 956 — Tallest Billboard
- LC 1049 — Last Stone Weight II

## Sequence DP

- LC 300 — Longest Increasing Subsequence
- LC 354 — Russian Doll Envelopes
- LC 368 — Largest Divisible Subset
- LC 376 — Wiggle Subsequence
- LC 446 — Arithmetic Slices II
- LC 673 — Number of LIS
- LC 873 — Longest Fibonacci Subsequence
- LC 1027 — Longest Arithmetic Subsequence
- LC 1048 — Longest String Chain
- LC 1218 — Arithmetic Subsequence of Given Difference
- LC 1626 — Best Team With No Conflicts
- LC 1671 — Minimum Removals for Mountain Array
- LC 1964 — Longest Valid Obstacle Course

## Grid DP

- LC 62 — Unique Paths
- LC 63 — Unique Paths II
- LC 64 — Minimum Path Sum
- LC 120 — Triangle
- LC 174 — Dungeon Game
- LC 221 — Maximal Square
- LC 741 — Cherry Pickup
- LC 931 — Minimum Falling Path Sum
- LC 1277 — Count Square Submatrices
- LC 1289 — Minimum Falling Path Sum II
- LC 1463 — Cherry Pickup II
- LC 2267 — Valid Parentheses Path
- LC 2435 — Paths With Sum Divisible by K

## String DP

- LC 5 — Longest Palindromic Substring
- LC 10 — Regular Expression Matching
- LC 44 — Wildcard Matching
- LC 72 — Edit Distance
- LC 87 — Scramble String
- LC 97 — Interleaving String
- LC 115 — Distinct Subsequences
- LC 132 — Palindrome Partitioning II
- LC 139 — Word Break
- LC 140 — Word Break II
- LC 516 — Longest Palindromic Subsequence
- LC 583 — Delete Operation for Two Strings
- LC 647 — Palindromic Substrings
- LC 712 — Minimum ASCII Delete Sum
- LC 940 — Distinct Subsequences II
- LC 1092 — Shortest Common Supersequence
- LC 1143 — Longest Common Subsequence
- LC 1278 — Palindrome Partitioning III
- LC 1312 — Minimum Insertions for Palindrome
- LC 1458 — Maximum Dot Product
- LC 1639 — Ways to Form Target String

## Partition and interval DP

- LC 312 — Burst Balloons
- LC 375 — Guess Number II
- LC 486 — Predict the Winner
- LC 546 — Remove Boxes
- LC 664 — Strange Printer
- LC 813 — Largest Sum of Averages
- LC 1000 — Minimum Cost to Merge Stones
- LC 1039 — Polygon Triangulation
- LC 1043 — Partition Array for Maximum Sum
- LC 1105 — Filling Bookcase Shelves
- LC 1130 — Minimum Cost Tree From Leaf Values
- LC 1140 — Stone Game II
- LC 1335 — Job Schedule Difficulty
- LC 1406 — Stone Game III
- LC 1478 — Allocate Mailboxes
- LC 1547 — Minimum Cost to Cut a Stick
- LC 1690 — Stone Game VII
- LC 1770 — Maximum Score from Multiplication
- LC 2547 — Minimum Cost to Split an Array

## Tree and state-compressed DP

- LC 124 — Binary Tree Maximum Path Sum
- LC 337 — House Robber III
- LC 834 — Sum of Distances in Tree
- LC 968 — Binary Tree Cameras
- LC 979 — Distribute Coins
- LC 1373 — Maximum Sum BST
- LC 1519 — Subtree Labels
- LC 2246 — Longest Path With Different Adjacent Characters

## Decision and game DP

- LC 464 — Can I Win
- LC 638 — Shopping Offers
- LC 691 — Stickers to Spell Word
- LC 698 — Partition to K Equal Sum Subsets
- LC 1140 — Stone Game II
- LC 1406 — Stone Game III
- LC 1690 — Stone Game VII
- LC 1986 — Minimum Work Sessions

## Advanced and optimized DP

- LC 629 — K Inverse Pairs
- LC 689 — Three Non-Overlapping Subarrays
- LC 837 — New 21 Game
- LC 920 — Music Playlists
- LC 1220 — Count Vowels Permutation
- LC 1235 — Job Scheduling
- LC 1289 — Falling Path Sum II
- LC 1425 — Constrained Subsequence Sum
- LC 1696 — Jump Game VI
- LC 1751 — Maximum Events II
- LC 1937 — Maximum Points With Cost

## Digit DP

- LC 233 — Number of Digit One
- LC 600 — No Consecutive Ones
- LC 902 — Numbers At Most N
- LC 1012 — Numbers With Repeated Digits
- LC 2376 — Count Special Integers
- LC 2719 — Count of Integers
- LC 2801 — Count Stepping Numbers
- LC 2827 — Beautiful Integers

---

# Recommended Study Order

## Phase 1: Recurrence fluency

Solve:

1. LC 70
2. LC 746
3. LC 198
4. LC 213
5. LC 740
6. LC 53
7. LC 152
8. LC 91
9. LC 322
10. LC 518
11. LC 377
12. LC 983

Goal: define prefix and endpoint states naturally.

---

## Phase 2: Knapsack

1. LC 416
2. LC 494
3. LC 474
4. LC 1049
5. LC 879
6. LC 956
7. LC 805
8. LC 1755
9. LC 2035

Goal: master loop direction, capacity dimensions and subset transformations.

---

## Phase 3: Sequence DP

1. LC 300
2. LC 673
3. LC 354
4. LC 368
5. LC 376
6. LC 1027
7. LC 1218
8. LC 873
9. LC 1048
10. LC 1626
11. LC 1671
12. LC 1964

Goal: recognize ordered DAGs and reconstruct optimal subsequences.

---

## Phase 4: Grid DP

1. LC 62
2. LC 63
3. LC 64
4. LC 120
5. LC 931
6. LC 221
7. LC 1277
8. LC 174
9. LC 1289
10. LC 1463
11. LC 2435
12. LC 741

Goal: move from simple directional dependencies to multi-agent states.

---

## Phase 5: String DP

1. LC 1143
2. LC 72
3. LC 115
4. LC 97
5. LC 516
6. LC 1312
7. LC 1092
8. LC 5
9. LC 647
10. LC 132
11. LC 10
12. LC 44
13. LC 87
14. LC 940
15. LC 1639

Goal: become comfortable with `dp[i][j]`, interval strings and reconstruction.

---

## Phase 6: Partition and interval DP

1. LC 1043
2. LC 1105
3. LC 813
4. LC 1335
5. LC 1278
6. LC 1478
7. LC 312
8. LC 1039
9. LC 1547
10. LC 375
11. LC 486
12. LC 1000
13. LC 664
14. LC 546

Goal: derive transitions over cut positions and interval pivots.

---

## Phase 7: Tree and game DP

1. LC 337
2. LC 979
3. LC 124
4. LC 968
5. LC 1373
6. LC 834
7. LC 2246
8. LC 464
9. LC 698
10. LC 1140
11. LC 1406
12. LC 1690

Goal: design compact return vectors and adversarial score states.

---

## Phase 8: Digit and advanced DP

1. LC 600
2. LC 902
3. LC 1012
4. LC 2376
5. LC 2719
6. LC 2801
7. LC 2827
8. LC 1696
9. LC 1425
10. LC 1937
11. LC 629
12. LC 1235
13. LC 1751
14. LC 920

Goal: handle tight bounds, transition optimization and larger composite states.

---

# Advanced Google L5 Final Set

Complete these under timed conditions:

1. LC 10 — Regular Expression Matching
2. LC 32 — Longest Valid Parentheses
3. LC 44 — Wildcard Matching
4. LC 72 — Edit Distance
5. LC 87 — Scramble String
6. LC 115 — Distinct Subsequences
7. LC 124 — Binary Tree Maximum Path Sum
8. LC 132 — Palindrome Partitioning II
9. LC 140 — Word Break II
10. LC 174 — Dungeon Game
11. LC 233 — Number of Digit One
12. LC 312 — Burst Balloons
13. LC 446 — Arithmetic Slices II
14. LC 464 — Can I Win
15. LC 546 — Remove Boxes
16. LC 552 — Student Attendance Record II
17. LC 600 — No Consecutive Ones
18. LC 629 — K Inverse Pairs
19. LC 639 — Decode Ways II
20. LC 664 — Strange Printer
21. LC 691 — Stickers to Spell Word
22. LC 698 — Partition to K Equal Sum Subsets
23. LC 730 — Count Different Palindromic Subsequences
24. LC 741 — Cherry Pickup
25. LC 805 — Split Array With Same Average
26. LC 834 — Sum of Distances in Tree
27. LC 879 — Profitable Schemes
28. LC 920 — Music Playlists
29. LC 940 — Distinct Subsequences II
30. LC 956 — Tallest Billboard
31. LC 968 — Binary Tree Cameras
32. LC 1000 — Minimum Cost to Merge Stones
33. LC 1092 — Shortest Common Supersequence
34. LC 1278 — Palindrome Partitioning III
35. LC 1335 — Job Schedule Difficulty
36. LC 1349 — Maximum Students Taking Exam
37. LC 1397 — Find All Good Strings
38. LC 1458 — Maximum Dot Product
39. LC 1463 — Cherry Pickup II
40. LC 1478 — Allocate Mailboxes
41. LC 1639 — Ways to Form Target String
42. LC 1659 — Maximize Grid Happiness
43. LC 1755 — Closest Subsequence Sum
44. LC 1931 — Painting a Grid
45. LC 2035 — Partition Array to Minimize Difference
46. LC 2060 — Encoded String Equivalence
47. LC 2267 — Valid Parentheses Path
48. LC 2407 — LIS II
49. LC 2478 — Beautiful Partitions
50. LC 2646 — Minimize Total Price of Trips
51. LC 2719 — Count of Integers
52. LC 2801 — Stepping Numbers
53. LC 2827 — Beautiful Integers

---

# Templates You Must Internalize

## 1. Take-or-skip DP

State describes the best result from or through an index.

Transition compares:

- Skip current item.
- Take current item and jump to the next compatible state.

## 2. Knapsack

State contains processed items and remaining or used capacity.

Know:

- 0/1 loop direction.
- Unbounded loop direction.
- Boolean, count, minimum and maximum variants.
- Multi-capacity compression.

## 3. Two-string DP

State contains prefix lengths or starting indices.

Typical transitions:

- Match both characters.
- Skip from the first string.
- Skip from the second.
- Replace, insert or delete.

## 4. Interval DP

Process intervals by increasing length.

Transition tries:

- Endpoints.
- Split positions.
- Last operation.
- First operation.

## 5. Partition DP

State is the answer for a prefix and possibly a number of groups.

Transition selects the final segment.

## 6. Tree DP

Each child returns a compact state vector.

The parent:

- Combines child states.
- Updates a global answer if needed.
- Returns only information useful to its own parent.

## 7. Bitmask DP

State includes a subset mask, often with a final item or position.

Complexity is commonly:

- `O(2^n × n)`
- `O(2^n × n²)`
- `O(3^n)` when enumerating all submasks for every mask.

## 8. Digit DP

State includes:

- Position.
- Tightness.
- Whether the number has started.
- Problem-specific state.

## 9. Game DP

Store whether the current player can win or the maximum score difference achievable.

## 10. Optimized transition DP

Start with the correct slow recurrence.

Then identify whether the transition is:

- Range maximum or minimum.
- Range sum.
- Best previous compatible index.
- Linear function evaluation.
- Repeated subset calculation.

Only optimize after establishing correctness.

---

# Common DP Failure Modes

## 1. State is not semantically complete

If future decisions depend on information absent from the state, memoization merges non-equivalent situations.

## 2. State contains unnecessary history

Carrying the full chosen sequence or path often creates exponential state when only a count, mask, balance or endpoint is needed.

## 3. Wrong iteration direction

Especially dangerous for knapsack:

- Backward for 0/1.
- Forward for unlimited reuse.

## 4. In-place compression destroys dependencies

Before changing a 2D table into one row, determine whether the current transition needs:

- Previous row.
- Current row.
- Left-to-right values.
- Right-to-left values.

## 5. Impossible states use unsafe values

For maximization, do not initialize impossible states to zero when zero could become a valid competitor.

Use a sufficiently negative sentinel.

## 6. Overflow before modulo

Use a sufficiently wide numeric type before performing addition or multiplication.

## 7. Counting duplicates incorrectly

Common in:

- Distinct subsequences.
- Palindromic subsequences.
- Coin-change combinations.
- Dictionary construction.
- Repeated values in subset DP.

## 8. Returning the wrong state

The answer may be:

- Best state ending anywhere.
- State covering the entire input.
- Maximum among terminal states.
- Sum of terminal states.
- Difference between two players.

## 9. Premature optimization

A wrong `O(n)` recurrence is worse than a correct `O(n²)` recurrence.

Derive the baseline first.

## 10. Memorizing transitions without deriving them

A slightly changed constraint will break memorized code. Always reconstruct the meaning of each dimension.

---

# Strict Completion Criteria

Section 13 is complete only when you can:

## State design

- Define every DP state in one precise sentence.
- Remove irrelevant dimensions.
- Identify sufficient state without carrying full history.
- Recognize when sorting creates a DAG.

## Recurrence

- Enumerate all legal final decisions.
- Prove that transitions cover every valid solution.
- Prove that no solution is counted incorrectly.
- Handle impossible states safely.

## Implementation

- Write top-down and bottom-up versions.
- Compress space correctly.
- Reconstruct an optimal solution.
- Use modulo and wide numeric types safely.
- Estimate states × transitions before implementation.

## Pattern recognition

- Distinguish subsequence from substring.
- Distinguish partition DP from interval DP.
- Distinguish knapsack combinations from permutations.
- Recognize tree DP return vectors.
- Recognize digit DP from bounded-number counting.
- Recognize state-expanded DP and bitmask DP.
- Recognize when a greedy or graph solution is better than DP.

## Optimization

- Optimize bounded transition windows with a deque.
- Optimize compatible-position transitions with binary search.
- Use prefix sums for range-sum transitions.
- Use smallest and second-smallest values for “all except one” transitions.
- Recognize matrix exponentiation for fixed linear recurrences.
- Understand divide-and-conquer optimization and Convex Hull Trick conceptually.

---

# Quantitative Preparation Target

For strict Google L5 preparation:

- Solve **140–155 unique problems** from this curriculum.
- Solve every accessible **P0** problem.
- Re-solve at least **50 P0 problems** after a 10–14 day gap.
- Complete at least **25 Hard or Stretch problems**.
- Implement at least 15 problems both top-down and bottom-up.
- Reconstruct the actual solution for at least 10 problems.
- Optimize at least 8 slow recurrences after first implementing the baseline.
- Complete at least **eight mixed DP mock sessions**.
- Include a string, interval, tree, digit or bitmask DP in every second mock.

## Expected timing

- Basic 1D DP: **15–20 minutes**
- Standard knapsack: **20–30 minutes**
- LIS variation: **25–35 minutes**
- Grid DP: **20–30 minutes**
- Two-string DP: **25–35 minutes**
- Partition DP: **30–40 minutes**
- Interval DP: **35–45 minutes**
- Tree DP: **30–40 minutes**
- Bitmask DP: **35–45 minutes**
- Digit DP: **40–50 minutes**
- Advanced optimized DP: **45–55 minutes**

---

# Final Standard for Strict L5 Readiness

For an unseen DP problem, you should be able to do the following within approximately ten minutes:

1. Explain the brute-force decision tree.
2. Identify the repeated subproblems.
3. Define a complete minimal state.
4. Write the recurrence.
5. Identify base and impossible states.
6. Choose top-down or bottom-up evaluation.
7. Calculate time and space complexity.
8. Explain whether reconstruction is possible.
9. Identify likely optimizations.
10. Discuss edge cases and overflow.

The decisive skill is not remembering hundreds of recurrences. It is learning to describe the future using the smallest sufficient state and then proving that every transition moves to a strictly smaller, already solvable subproblem.
