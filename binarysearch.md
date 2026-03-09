### 0) Template warm-up (no problem, just setup)

1.  **Master 3 templates**
    *   **Index-based** (`while l <= r`, mid, shrink by comparison)
    *   **Boundary/first/last** (leftmost/rightmost predicate true)
    *   **Value-domain / Search on answer** (monotonic feasibility `check(x)`)

***

### Tier 1 — Fundamentals (index & simple boundaries)

2.  **Search Insert Position** *(index)*
3.  **First Bad Version** *(boundary: first true)*
4.  **Sqrt(x)** *(value on integers, floor root)*
5.  **Find Smallest Letter Greater Than Target** *(boundary: first greater)*
6.  **Find First and Last Position of Element in Sorted Array** *(leftmost/rightmost)*
7.  **Kth Missing Positive Number** *(boundary with arithmetic missing count)*
8.  **H-Index II** *(boundary by definition check)*
9.  **K Closest Elements** *(binary search left bound of fixed-size window)*
10. **Search in a Sorted Array of Unknown Size** *(exponential expansion → index BS)*

***

### Tier 2 — Rotations + Parity tricks + Peaks

11. **Find Minimum in Rotated Sorted Array** *(rotation pivot)*
12. **Search in Rotated Sorted Array** *(split by sorted half)*
13. **Find Minimum in Rotated Sorted Array II** *(rotation with duplicates)*
14. **Search in Rotated Sorted Array II** *(rotation + duplicates edge handling)*
15. **Single Element in a Sorted Array** *(parity/paired indices, index BS)*

***

### Tier 3 — Peaks & Bitonic

16. **Find Peak Element** *(unimodal slope BS)*
17. **Find a Peak Element II** *(2D peak—reduce along one dimension)*
18. **Find in Mountain Array** *(bitonic: find peak, then two BS passes)*

***

### Tier 4 — 2D Matrices

19. **Search a 2D Matrix** *(treat as flattened or row+col gates)*
20. **Search a 2D Matrix II** *(staircase from top-right/bottom-left or BS per row)*

***

### Tier 5 — Value-domain (Search on Answer): capacity/rate/feasibility

21. **Koko Eating Bananas** *(rate → days monotone)*
22. **Capacity to Ship Packages Within D Days** *(capacity → days monotone)*
23. **Split Array Largest Sum** *(max subarray sum → #splits monotone)*
24. **Minimum Number of Days to Make M Bouquets** *(days → bouquets monotone)*
25. **Magnetic Force Between Two Balls** *(min distance monotone greedy check)*
26. **Minimum Limit of Balls in a Bag** *(max bag size → operations monotone)*
27. **Maximum Value at a Given Index in a Bounded Array** *(height → sum bound monotone)*
28. **Minimize the Maximum Distance to Gas Station** *(max gap → stations monotone)*

***

### Tier 6 — Selection via value-domain counting

29. **Kth Smallest Element in a Sorted Matrix** *(value-domain count ≤ mid)*
30. **Kth Smallest Number in Multiplication Table** *(value-domain count ≤ mid)*
31. **Find K-th Smallest Pair Distance** *(value-domain with two-pointer count)*

***

### Tier 7 — Mixed patterns (prefix+BS, hashing+BS, interval BS)

32. **Heaters** *(nearest heater via BS per house)*
33. **Find Right Interval** *(sort starts, BS for next ≥ end)*
34. **Plates Between Candles** *(prefix + nearest candle via BS)*
35. **Longest Subsequence With Limited Sum** *(sort + prefix + upper\_bound per query)*
36. **Successful Pairs of Spells and Potions** *(sort potions + lower\_bound per spell)*
37. **Time Based Key-Value Store** *(per key timestamps + BS)*
38. **Random Pick with Weight** *(prefix + upper\_bound on random)*
39. **Maximum Number of Removable Characters** *(search on answer k + subsequence check)*
40. **Find Duplicate Number** *(value-domain pigeonhole BS; note Floyd alternative)*

***
