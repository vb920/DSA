---
layout: simple
title: "Prefix Sum Patterns"
permalink: /pattern/prefix-sum
---

# Prefix Sum Patterns — Comprehensive Guide

Prefix sum is one of the most fundamental techniques in competitive programming. The core idea is **precomputation**: spend O(N) time building an auxiliary array so that subsequent range queries take O(1). But prefix sums go far beyond simple "range sum" — they combine with hash maps, modular arithmetic, difference arrays, 2D grids, XOR, and even trees to solve an enormous variety of problems.

---

## Quick Navigation: "I need to..."

| I need to... | Technique | Section |
|--------------|-----------|---------|
| Query **sum of subarray** in O(1) | 1D prefix sum | [1](#1-basic-1d-prefix-sum) |
| Query **sum of submatrix** in O(1) | 2D prefix sum | [2](#2-2d-prefix-sum) |
| Count subarrays with **sum = k** | Prefix sum + hash map | [3](#3-prefix-sum--hash-map) |
| Count subarrays **divisible by k** | Prefix sum + modular arithmetic | [4](#4-prefix-sum--modular-arithmetic) |
| Apply **range updates** efficiently | Difference array | [5](#5-difference-array-1d) |
| Apply **2D range updates** | 2D difference array | [6](#6-difference-array-2d) |
| Query **XOR of subarray** | Prefix XOR | [7](#7-prefix-xor) |
| Find **product of array except self** | Prefix & suffix products | [8](#8-prefix--suffix-products) |
| Query **path sums on trees** | Prefix sum on trees | [9](#9-prefix-sum-on-trees) |
| Find subarray with sum in **[lo, hi]** | Prefix sum + binary search / BIT | [10](#10-prefix-sum--binary-search) |
| Handle **multiple dimensions** / bitmask sums | Higher-dimensional prefix sums | [11](#11-higher-dimensional-prefix-sums) |

---

## Table of Contents

1. [Basic 1D Prefix Sum](#1-basic-1d-prefix-sum)
2. [2D Prefix Sum](#2-2d-prefix-sum)
3. [Prefix Sum + Hash Map](#3-prefix-sum--hash-map)
4. [Prefix Sum + Modular Arithmetic](#4-prefix-sum--modular-arithmetic)
5. [Difference Array (1D)](#5-difference-array-1d)
6. [Difference Array (2D)](#6-difference-array-2d)
7. [Prefix XOR](#7-prefix-xor)
8. [Prefix & Suffix Products](#8-prefix--suffix-products)
9. [Prefix Sum on Trees](#9-prefix-sum-on-trees)
10. [Prefix Sum + Binary Search](#10-prefix-sum--binary-search)
11. [Higher-Dimensional Prefix Sums](#11-higher-dimensional-prefix-sums)
12. [Common Patterns Collection](#12-common-patterns-collection)
13. [Pattern Recognition Cheat Sheet](#13-pattern-recognition-cheat-sheet)

---

## 1. Basic 1D Prefix Sum

### The Idea

Given an array `a[0..n-1]`, build a prefix sum array where:

```
pre[0] = 0
pre[i] = a[0] + a[1] + ... + a[i-1]
```

Then the sum of any subarray `a[l..r]` (inclusive) is:

```
sum(l, r) = pre[r+1] - pre[l]
```

### Visual Trace

```
Index:    0    1    2    3    4    5
Array:  [ 3,   1,   4,   1,   5,   9 ]

Prefix: [0, 3, 4, 8, 9, 14, 23]
         ^  ^  ^  ^  ^   ^   ^
         |  |  |  |  |   |   sum of all 6
         |  |  |  |  |   sum of first 5
         |  |  |  |  sum of first 4
         |  |  |  sum of first 3
         |  |  sum of first 2
         |  sum of first 1
         empty prefix (sum of 0 elements)

Query: sum(2, 4) = pre[5] - pre[2] = 14 - 4 = 10
                 = a[2] + a[3] + a[4] = 4 + 1 + 5 = 10  ✓
```

### Why `pre` has length `n+1`?

The extra `pre[0] = 0` handles the edge case where `l = 0`. Without it, you'd need a special case. With it, `sum(0, r) = pre[r+1] - pre[0] = pre[r+1]` — clean and uniform.

### Implementation

```java
public static int[] buildPrefix(int[] a) {
    int n = a.length;
    int[] pre = new int[n + 1];
    for (int i = 0; i < n; i++) pre[i + 1] = pre[i] + a[i];
    return pre;
}

public static int rangeSum(int[] pre, int l, int r) {
    return pre[r + 1] - pre[l];
}

```

### Complexity

| Operation | Time | Space |
|-----------|------|-------|
| Build | O(N) | O(N) |
| Query | O(1) | — |

### Classic Problems

1. **Static Range Sum Queries** — Direct application
2. **Maximum subarray sum** — Kadane's is better, but `max(pre[j] - pre[i])` for `j > i` also works
3. **Equilibrium index** — Find index where left sum = right sum

---

## 2. 2D Prefix Sum

### The Idea

For a 2D grid, precompute the sum of every rectangle from `(0,0)` to `(i,j)`. Then any sub-rectangle sum can be computed in O(1) using **inclusion-exclusion**.

### Building the 2D Prefix Sum

```
pre[i][j] = sum of all grid[r][c] where 0 ≤ r < i, 0 ≤ c < j
```

Formula (1-indexed prefix, 0-indexed grid):

```
pre[i+1][j+1] = grid[i][j] + pre[i][j+1] + pre[i+1][j] - pre[i][j]
```

### Querying a Sub-Rectangle

Sum of grid cells in rectangle `(r1, c1)` to `(r2, c2)` inclusive:

```
sum = pre[r2+1][c2+1] - pre[r1][c2+1] - pre[r2+1][c1] + pre[r1][c1]
```

### Visual — Inclusion-Exclusion

```
We want the shaded region:

    c1      c2
     v       v
r1 > ########
     ########
r2 > ########

pre[r2+1][c2+1] includes everything from (0,0) to (r2,c2):

    +-----------+---+
    |     A     | B |
    +-----------+---+  <- r1
    |     C     |###|
    |           |###|
    +-----------+---+  <- r2
         ^         ^
         c1        c2

Answer = Total - A - B - C + overlap(A∩B is empty, but top-left counted)
       = pre[r2+1][c2+1]            (everything)
       - pre[r1][c2+1]              (rows above r1)
       - pre[r2+1][c1]              (cols left of c1)
       + pre[r1][c1]                (top-left corner subtracted twice)
```

### Implementation

```java
public static int[][] build2DPrefix(int[][] grid) {
    int R = grid.length, C = grid[0].length;
    int[][] pre = new int[R + 1][C + 1];

    for (int i = 0; i < R; i++) {
        for (int j = 0; j < C; j++) {
            pre[i + 1][j + 1] = grid[i][j]
                + pre[i][j + 1]
                + pre[i + 1][j]
                - pre[i][j];
        }
    }
    return pre;
}

public static int rectSum(int[][] pre, int r1, int c1, int r2, int c2) {
    return pre[r2 + 1][c2 + 1]
         - pre[r1][c2 + 1]
         - pre[r2 + 1][c1]
         + pre[r1][c1];
}

```

### Complexity

| Operation | Time | Space |
|-----------|------|-------|
| Build | O(R × C) | O(R × C) |
| Query | O(1) | — |

### Classic Problems

1. **Forest Queries (CSES)** — Count trees in sub-rectangle
2. **Maximum sum sub-rectangle** — Combine with Kadane's (O(N³) for N×N)
3. **Counting 1s in binary matrix** — Direct application

---

## 3. Prefix Sum + Hash Map

### The Core Trick

To count subarrays with sum exactly `k`:

```
If pre[j] - pre[i] = k, then subarray a[i..j-1] has sum k.
So for each j, we need: how many earlier indices i have pre[i] = pre[j] - k?
```

Store prefix sum frequencies in a hash map as you iterate!

### Visual Trace

```
Array:  [1, 2, 3, -2, 5]    k = 3

Index:   0  1  2   3  4
pre:  [0, 1, 3, 6,  4, 9]

Step by step:
j=0: pre=0, need pre[i]=0-3=-3, count[−3]=0.  Store count[0]=1
j=1: pre=1, need pre[i]=1-3=-2, count[−2]=0.  Store count[1]=1
j=2: pre=3, need pre[i]=3-3=0,  count[0]=1 → found 1!  (subarray [1,2])
j=3: pre=6, need pre[i]=6-3=3,  count[3]=1 → found 1!  (subarray [-2,5]? No, [3])
j=4: pre=4, need pre[i]=4-3=1,  count[1]=1 → found 1!  (subarray [3,-2,5]? No, [2,3,-2])
j=5: pre=9, need pre[i]=9-3=6,  count[6]=1 → found 1!  (subarray [-2,5])

Wait, let me re-trace more carefully:

j=0: current_sum=0. Initialize count={0: 1}
After a[0]=1: current_sum=1, need 1-3=-2, count[-2]=0. count={0:1, 1:1}
After a[1]=2: current_sum=3, need 3-3=0,  count[0]=1 → +1. count={0:1, 1:1, 3:1}
After a[2]=3: current_sum=6, need 6-3=3,  count[3]=1 → +1. count={0:1, 1:1, 3:1, 6:1}
After a[3]=-2: current_sum=4, need 4-3=1, count[1]=1 → +1. count={0:1, 1:1, 3:1, 6:1, 4:1}
After a[4]=5: current_sum=9, need 9-3=6,  count[6]=1 → +1. count={..., 9:1}

Total = 4 subarrays with sum 3: [1,2], [3], [2,3,-2], [-2,5]  ✓
```

### Implementation

```java
public static int subarraySumCount(int[] a, int k) {
    Map<Integer, Integer> count = new HashMap<>();
    count.put(0, 1);

    int current = 0, result = 0;
    for (int x : a) {
        current += x;
        result += count.getOrDefault(current - k, 0);
        count.put(current, count.getOrDefault(current, 0) + 1);
    }
    return result;
}

```

### Variation: Longest Subarray with Sum k

```java
public static int longestSubarraySumK(int[] a, int k) {
    Map<Integer, Integer> first = new HashMap<>();
    first.put(0, -1);

    int current = 0, best = 0;
    for (int i = 0; i < a.length; i++) {
        current += a[i];
        if (first.containsKey(current - k)) {
            best = Math.max(best, i - first.get(current - k));
        }
        first.putIfAbsent(current, i);
    }
    return best;
}

```

### Variation: Count Subarrays with Sum in Range [lo, hi]

```java
public static long countSumInRange(int[] a, long lo, long hi) {
    return countAtMost(a, hi) - countAtMost(a, lo - 1);
}

private static long countAtMost(int[] a, long target) {
    long count = 0;
    long prefix = 0;

    // TreeMap: prefixSum -> frequency
    TreeMap<Long, Integer> map = new TreeMap<>();
    map.put(0L, 1); // empty prefix

    for (int x : a) {
        prefix += x;

        // We need previous prefix sums p such that:
        // prefix - p <= target  =>  p >= prefix - target
        long lower = prefix - target;

        // Get all prefix sums p >= lower
        for (long key : map.tailMap(lower, true).keySet()) {
            count += map.get(key);
        }

        map.put(prefix, map.getOrDefault(prefix, 0) + 1);
    }

    return count;
}
```

### Complexity

| Operation | Time | Space |
|-----------|------|-------|
| Count subarrays with sum k | O(N) | O(N) |
| Longest subarray with sum k | O(N) | O(N) |

### Why This Is So Powerful

The hash map transforms the "check all pairs (i, j)" approach from O(N²) to O(N). The key insight: **you don't need to enumerate pairs — you just need to count how many earlier prefixes had the right value.**

---

## 4. Prefix Sum + Modular Arithmetic

### The Idea

To count subarrays whose sum is **divisible by k**:

```
sum(l, r) % k == 0
⟺ (pre[r+1] - pre[l]) % k == 0
⟺ pre[r+1] % k == pre[l] % k
```

So we just count **pairs of equal remainders** in the prefix sum array!

### Visual Trace

```
Array:  [4, 5, 0, -2, -3, 1]    k = 5

Index:        0   1  2   3   4  5
prefix sums: [0,  4, 9,  9,  7, 4, 5]
      mod 5: [0,  4, 4,  4,  2, 4, 0]

Group by remainder:
  0: indices {0, 6} → C(2,2) = 1 pair  → subarrays with sum divisible by 5
  4: indices {1, 2, 3, 5} → C(4,2) = 6 pairs
  2: indices {4} → C(1,2) = 0 pairs

Total = 1 + 6 + 0 = 7  ✓
```

### Implementation

```java
public static int subarraysDivByK(int[] a, int k) {
    int[] count = new int[k];
    count[0] = 1;

    int current = 0, result = 0;
    for (int x : a) {
        current += x;
        int rem = ((current % k) + k) % k;
        result += count[rem];
        count[rem]++;
    }
    return result;
}

```

### ⚠️ Watch Out: Negative Remainders

In C++/Java, `-7 % 5 = -2`. You need `((x % k) + k) % k` to get a non-negative remainder. **Python handles this correctly** — `(-7) % 5 = 3`.

### Variation: Subarrays Divisible by k with Exactly m Elements

Combine the modular prefix sum with a sliding window or deque to add the length constraint.

### Classic Problems

1. **Subarray Divisibility (CSES)** — Direct application
2. **LeetCode 974: Subarray Sums Divisible by K** — Same pattern
3. **LeetCode 523: Continuous Subarray Sum** — Divisible by k with length ≥ 2

---

## 5. Difference Array (1D)

### The Idea

The **difference array** is the **inverse** of prefix sum. If prefix sum turns "point values" into "cumulative sums," then the difference array turns "range updates" into "point updates."

```
Prefix sum:     point values  →  range queries (O(1))
Difference:     range updates →  point updates (O(1))
```

Given an array `a`, its difference array is:

```
d[0] = a[0]
d[i] = a[i] - a[i-1]   for i ≥ 1
```

To **add value v to all elements in a[l..r]**:

```
d[l] += v
d[r+1] -= v
```

Then reconstruct `a` by taking prefix sums of `d`.

### Visual Trace

```
Initial: a = [0, 0, 0, 0, 0, 0]   (6 elements)

Operation 1: add 3 to a[1..4]
  d[1] += 3, d[5] -= 3
  d = [0, 3, 0, 0, 0, -3]
  a = [0, 3, 3, 3, 3, 0]  ✓

Operation 2: add 2 to a[0..2]
  d[0] += 2, d[3] -= 2
  d = [2, 3, 0, -2, 0, -3]
  a = [2, 5, 5, 3, 3, 0]  ✓

Operation 3: add -1 to a[2..5]
  d[2] += -1, d[6] -= -1  (d[6] is out of bounds, ignore or use n+1 array)
  d = [2, 3, -1, -2, 0, -3]
  a = [2, 5, 4, 2, 2, -1]  ✓

Reconstruction: prefix sum of d
  a[0] = 2
  a[1] = 2 + 3 = 5
  a[2] = 5 + (-1) = 4
  a[3] = 4 + (-2) = 2
  a[4] = 2 + 0 = 2
  a[5] = 2 + (-3) = -1  ✓
```

### Implementation

```java
public static void rangeAdd(int[] diff, int l, int r, int v) {
    diff[l] += v;
    if (r + 1 < diff.length) diff[r + 1] -= v;
}

public static int[] reconstruct(int[] diff) {
    int n = diff.length;
    int[] a = new int[n];
    a[0] = diff[0];
    for (int i = 1; i < n; i++) a[i] = a[i - 1] + diff[i];
    return a;
}


# Usage
n = 6
diff = [0] * n
range_add(diff, 1, 4, 3)    # add 3 to [1..4]
range_add(diff, 0, 2, 2)    # add 2 to [0..2]
range_add(diff, 2, 5, -1)   # add -1 to [2..5]
result = reconstruct(diff)   # [2, 5, 4, 2, 2, -1]
```

### Complexity

| Operation | Time |
|-----------|------|
| Single range update | O(1) |
| Q range updates + reconstruct | O(Q + N) |

### When to Use

- Many range updates, single final query
- "Sweep line" style problems (event start/end)
- Bus schedule problems (passengers boarding/exiting at stops)

### Classic Problems

1. **Range Update Queries (CSES)** — Direct application
2. **Corporate Flight Bookings (LC 1109)** — Range add, then prefix sum
3. **Car Pooling (LC 1094)** — Difference array on timeline

---

## 6. Difference Array (2D)

### The Idea

Extend the 1D difference trick to 2D. To add value `v` to all cells in rectangle `(r1, c1)` to `(r2, c2)`:

```
d[r1][c1]     += v
d[r1][c2+1]   -= v
d[r2+1][c1]   -= v
d[r2+1][c2+1] += v
```

Then reconstruct with a **2D prefix sum** over `d`.

### Visual — Why 4 Points?

```
Adding v to the shaded rectangle:

    c1        c2
     +v ...   -v
r1 > ########
     ########
r2 > ########
     -v ...   +v

The +v at (r1,c1) "starts" the addition.
The -v at (r1,c2+1) stops it from spreading right.
The -v at (r2+1,c1) stops it from spreading down.
The +v at (r2+1,c2+1) corrects the double-subtraction at the corner.
```

### Implementation

```java
public static void rangeAdd2D(int[][] diff, int r1, int c1, int r2, int c2, int v) {
    diff[r1][c1] += v;
    if (c2 + 1 < diff[0].length) diff[r1][c2 + 1] -= v;
    if (r2 + 1 < diff.length) diff[r2 + 1][c1] -= v;
    if (r2 + 1 < diff.length && c2 + 1 < diff[0].length)
        diff[r2 + 1][c2 + 1] += v;
}

public static int[][] reconstruct2D(int[][] diff) {
    int R = diff.length, C = diff[0].length;

    for (int i = 0; i < R; i++)
        for (int j = 1; j < C; j++)
            diff[i][j] += diff[i][j - 1];

    for (int j = 0; j < C; j++)
        for (int i = 1; i < R; i++)
            diff[i][j] += diff[i - 1][j];

    return diff;
}

```

### Complexity

| Operation | Time |
|-----------|------|
| Single rectangle update | O(1) |
| Q updates + reconstruct | O(Q + R × C) |

### Classic Problems

1. **Forest Queries** variant — Stamp rectangles, then count
2. **2D range increment** — Multiple rectangle operations

---

## 7. Prefix XOR

### The Idea

XOR has the beautiful property that `a ^ a = 0`. So prefix XOR works exactly like prefix sum:

```
pre_xor[0] = 0
pre_xor[i] = a[0] ^ a[1] ^ ... ^ a[i-1]

XOR(l, r) = pre_xor[r+1] ^ pre_xor[l]
```

This works because the common prefix `a[0] ^ ... ^ a[l-1]` cancels out.

### Visual Trace

```
Array:  [3, 1, 5, 2, 4]

Binary:  011  001  101  010  100

Prefix XOR: [000, 011, 010, 111, 101, 001]
             0    3    2    7    5    1

Query: XOR(1, 3) = pre[4] ^ pre[1] = 5 ^ 3 = 101 ^ 011 = 110 = 6
Check: 1 ^ 5 ^ 2 = 001 ^ 101 ^ 010 = 110 = 6  ✓
```

### Implementation

```java
public static int[] buildPrefixXor(int[] a) {
    int n = a.length;
    int[] pre = new int[n + 1];
    for (int i = 0; i < n; i++) pre[i + 1] = pre[i] ^ a[i];
    return pre;
}

public static int rangeXor(int[] pre, int l, int r) {
    return pre[r + 1] ^ pre[l];
}

```

### Pattern: Count Subarrays with XOR = k

Same hash map trick as sum = k:

```java
public static int countSubarraysXorK(int[] a, int k) {
    Map<Integer, Integer> count = new HashMap<>();
    count.put(0, 1);

    int current = 0, result = 0;
    for (int x : a) {
        current ^= x;
        result += count.getOrDefault(current ^ k, 0);
        count.put(current, count.getOrDefault(current, 0) + 1);
    }
    return result;
}

```

### Why `current_xor ^ k` Instead of `current_xor - k`?

For sums: `pre[j] - pre[i] = k → pre[i] = pre[j] - k`
For XOR: `pre[j] ^ pre[i] = k → pre[i] = pre[j] ^ k`

XOR is its own inverse! `x ^ k = y ⟺ x = y ^ k`.

### Classic Problems

1. **Range Xor Queries (CSES)** — Direct application
2. **LeetCode 1442: Subarray XOR Triplets** — Count (i,j,k) with XOR splits
3. **Maximum XOR subarray** — Combine with trie

---

## 8. Prefix & Suffix Products

### The Idea

Sometimes you need products instead of sums. The classic problem: **Product of Array Except Self** — compute an array where `result[i]` = product of all elements except `a[i]`, without division.

### Solution: Left and Right Products

```
left[i]  = a[0] × a[1] × ... × a[i-1]    (prefix product)
right[i] = a[i+1] × a[i+2] × ... × a[n-1] (suffix product)
result[i] = left[i] × right[i]
```

### Visual Trace

```
Array:   [1, 2, 3, 4]

Left:    [1, 1, 2, 6]
          ^  ^  ^  ^
          |  |  |  1×2×3
          |  |  1×2
          |  1
          empty product

Right:   [24, 12, 4, 1]
           ^   ^  ^  ^
           |   |  |  empty product
           |   |  4
           |   3×4
           2×3×4

Result:  [24, 12, 8, 6]
          1×24  1×12  2×4  6×1  ✓
```

### Implementation (O(1) Extra Space)

```java
public static int[] productExceptSelf(int[] a) {
    int n = a.length;
    int[] res = new int[n];
    int left = 1;

    for (int i = 0; i < n; i++) {
        res[i] = left;
        left *= a[i];
    }

    int right = 1;
    for (int i = n - 1; i >= 0; i--) {
        res[i] *= right;
        right *= a[i];
    }

    return res;
}

```

### Generalization: Prefix + Suffix for Any Associative Operation

This pattern works for any operation where you can combine left and right parts:
- **Sum except self**: `total_sum - a[i]`
- **Min except self**: `min(prefix_min[i-1], suffix_min[i+1])`
- **GCD except self**: `gcd(prefix_gcd[i-1], suffix_gcd[i+1])`

```java
import java.util.*;

public class GcdExceptSelf {

    // If using Java < 18, replace Math.gcd with this custom function:
    public static int gcd(int a, int b) {
        if (b == 0) return Math.abs(a);
        return gcd(b, a % b);
    }

    public static int[] gcdExceptSelf(int[] a) {
        int n = a.length;
        int[] prefix = new int[n];
        int[] suffix = new int[n];
        int[] result = new int[n];

        // Build prefix GCDs
        prefix[0] = a[0];
        for (int i = 1; i < n; i++) {
            prefix[i] = gcd(prefix[i - 1], a[i]);
        }

        // Build suffix GCDs
        suffix[n - 1] = a[n - 1];
        for (int i = n - 2; i >= 0; i--) {
            suffix[i] = gcd(a[i], suffix[i + 1]);
        }

        // Build result
        for (int i = 0; i < n; i++) {
            int left = (i > 0) ? prefix[i - 1] : 0;
            int right = (i < n - 1) ? suffix[i + 1] : 0;

            if (left == 0) result[i] = right;
            else if (right == 0) result[i] = left;
            else result[i] = gcd(left, right);
        }

        return result;
    }

    // For testing
    public static void main(String[] args) {
        int[] a = {12, 15, 18, 9};
        System.out.println(Arrays.toString(gcdExceptSelf(a)));
    }
}
```

---

## 9. Prefix Sum on Trees

### The Idea

On trees, we can use prefix sums along root-to-node paths to answer path queries. Two main approaches:

### Approach 1: Euler Tour + Range Prefix Sum

Flatten the tree with Euler tour, then use 1D prefix sums for **subtree** queries.

```
Tree:        0
           / | \
          1  2  3
         / \
        4   5

Euler tour (tin order): [0, 1, 4, 5, 2, 3]
tin:  [0, 1, 4, 2, 3, 5]  (index in euler order... simplified)

Subtree of node 1 = contiguous range in euler array
```

### Approach 2: Path Prefix Sum with LCA

For path queries `u → v` through LCA:

```
sum(u, v) = sum(root, u) + sum(root, v) - 2 × sum(root, LCA(u,v)) + val[LCA(u,v)]
```

### Approach 3: Difference on Tree (Edge/Node Counting)

To increment all nodes on path `u → v`:

```
diff[u] += 1
diff[v] += 1
diff[LCA(u,v)] -= 1
diff[parent[LCA(u,v)]] -= 1
```

Then DFS to accumulate from leaves to root (subtree sum = answer for each node).

### Implementation — Path Sum with DFS Prefix

```java
// LCA + prefix tree sum setup (simplified)
class TreePrefixSum {
    int LOG = 20;
    int n;
    List<Integer>[] adj;
    int[] depth, value, depthSum;
    int[][] parent;

    TreePrefixSum(int n, int[] values, List<Integer>[] adj) {
        this.n = n;
        this.adj = adj;
        this.value = values;

        depth = new int[n];
        depthSum = new int[n];
        parent = new int[LOG][n];

        bfsInit();
        buildParents();
    }

    void bfsInit() {
        boolean[] visited = new boolean[n];
        Queue<Integer> q = new ArrayDeque<>();

        visited[0] = true;
        q.add(0);
        depthSum[0] = value[0];
        parent[0][0] = -1;

        while (!q.isEmpty()) {
            int u = q.poll();
            for (int v : adj[u]) {
                if (!visited[v]) {
                    visited[v] = true;
                    depth[v] = depth[u] + 1;
                    depthSum[v] = depthSum[u] + value[v];
                    parent[0][v] = u;
                    q.add(v);
                }
            }
        }
    }

    void buildParents() {
        for (int k = 1; k < LOG; k++) {
            for (int v = 0; v < n; v++) {
                int p = parent[k - 1][v];
                parent[k][v] = p == -1 ? -1 : parent[k - 1][p];
            }
        }
    }

    int lca(int u, int v) {
        if (depth[u] < depth[v]) { int t = u; u = v; v = t; }

        int diff = depth[u] - depth[v];
        for (int k = 0; k < LOG; k++)
            if (((diff >> k) & 1) == 1) u = parent[k][u];

        if (u == v) return u;

        for (int k = LOG - 1; k >= 0; k--) {
            if (parent[k][u] != parent[k][v]) {
                u = parent[k][u];
                v = parent[k][v];
            }
        }
        return parent[0][u];
    }

    int pathSum(int u, int v) {
        int l = lca(u, v);
        return depthSum[u] + depthSum[v] - 2 * depthSum[l] + value[l];
    }
}

```

### Implementation — Difference on Tree (Counting Paths)

```java
public static int[] countPathsThroughNodes(
        int n,
        List<Integer>[] adj,
        int[][] parent,     // parent[k][v]
        int[][] paths,      // list of {u, v}
        java.util.function.BiFunction<Integer, Integer, Integer> lcaFunc
) {
    int[] diff = new int[n];

    // Apply difference marks for each path
    for (int[] p : paths) {
        int u = p[0];
        int v = p[1];

        int l = lcaFunc.apply(u, v);

        diff[u] += 1;
        diff[v] += 1;
        diff[l] -= 1;

        int parentOfL = parent[0][l];
        if (parentOfL != -1) {
            diff[parentOfL] -= 1;
        }
    }

    int[] answer = new int[n];
    dfsAccumulate(0, -1, adj, diff, answer);
    return answer;
}

private static void dfsAccumulate(
        int u, int par,
        List<Integer>[] adj,
        int[] diff,
        int[] answer
) {
    answer[u] = diff[u];
    for (int v : adj[u]) {
        if (v != par) {
            dfsAccumulate(v, u, adj, diff, answer);
            answer[u] += answer[v];
        }
    }
}
```

### Classic Problems

1. **Path Queries (CSES)** — Sum on root-to-node paths
2. **Counting Paths (CSES)** — Difference on tree
3. **Distance Queries (CSES)** — Path length using LCA + depth

---

## 10. Prefix Sum + Binary Search

### The Idea

When the array has **non-negative** values, prefix sums are **monotonically non-decreasing**. This means you can binary search on them!

### Pattern: Smallest Subarray with Sum ≥ Target

```java
public static int minSubarrayWithSumAtLeast(int[] a, int target) {
    int n = a.length;
    int[] pre = new int[n + 1];
    for (int i = 0; i < n; i++) pre[i + 1] = pre[i] + a[i];

    int best = Integer.MAX_VALUE;

    for (int j = 1; j <= n; j++) {
        int threshold = pre[j] - target;

        int i = Arrays.binarySearch(pre, 0, j, threshold + 1);
        if (i < 0) i = -i - 1;
        i--;

        if (i >= 0 && pre[j] - pre[i] >= target) best = Math.min(best, j - i);
    }

    return best == Integer.MAX_VALUE ? -1 : best;
}

```

### Pattern: Count Subarrays with Sum in [lo, hi] (Non-Negative)

```java
import java.util.Arrays;

public class SubarraySumRange {

    public static long countSubarraysSumInRange(int[] a, long lo, long hi) {
        int n = a.length;
        long[] pre = new long[n + 1];

        // Build prefix sums
        for (int i = 0; i < n; i++) {
            pre[i + 1] = pre[i] + a[i];
        }

        long count = 0;

        for (int j = 1; j <= n; j++) {
            long lowBound = pre[j] - hi;   // pre[i] >= lowBound
            long highBound = pre[j] - lo;  // pre[i] <= highBound

            // Count i in [0, j) where lowBound ≤ pre[i] ≤ highBound
            int left = lowerBound(pre, 0, j, lowBound);
            int right = upperBound(pre, 0, j, highBound);

            count += (right - left);
        }

        return count;
    }

    // Equivalent to bisect_left
    private static int lowerBound(long[] arr, int from, int to, long target) {
        int pos = Arrays.binarySearch(arr, from, to, target);
        if (pos < 0) {
            pos = -pos - 1;   // insertion point
        }
        return pos;
    }

    // Equivalent to bisect_right
    private static int upperBound(long[] arr, int from, int to, long target) {
        int pos = Arrays.binarySearch(arr, from, to, target);

        if (pos < 0) {
            pos = -pos - 1;   // insertion point
        } else {
            // Move past duplicates
            while (pos < to && arr[pos] == target) {
                pos++;
            }
        }
        return pos;
    }
}
    return count
```

### When Negatives Exist: Use SortedList or BIT

If the array can have negative values, prefix sums aren't sorted. Use a **balanced BST** (like `SortedList` from `sortedcontainers`) or a **BIT/Fenwick tree** with coordinate compression.

```java
import java.util.*;

public class SubarraySumRange {

    public static long countSubarraysSumInRange(int[] a, long lo, long hi) {
        TreeMap<Long, Integer> map = new TreeMap<>();
        
        // prefix sum = 0 occurs once
        map.put(0L, 1);

        long currentSum = 0;
        long count = 0;

        for (int x : a) {
            currentSum += x;

            long left = currentSum - hi;
            long right = currentSum - lo;

            // Get all prefix sums in range [left, right]
            NavigableMap<Long, Integer> sub = map.subMap(left, true, right, true);

            for (int freq : sub.values()) {
                count += freq;
            }

            // Insert current prefix sum
            map.put(currentSum, map.getOrDefault(currentSum, 0) + 1);
        }

        return count;
    }

    public static void main(String[] args) {
        int[] a = {2, -1, 3};
        long lo = 2, hi = 4;

        System.out.println(countSubarraysSumInRange(a, lo, hi));
    }
}
```

### Complexity

| Approach | Time | When |
|----------|------|------|
| Binary search on sorted prefix | O(N log N) | Non-negative arrays |
| SortedList | O(N log N) | Any array |
| BIT + coordinate compression | O(N log N) | Any array |

---

## 11. Higher-Dimensional Prefix Sums

### Sum over Subsets (SOS) — Bitmask Prefix Sum

The **Sum over Subsets (SOS) DP** computes, for each bitmask `x`:

```
sos[x] = Σ f[y]  for all y that are submasks of x  (y & x == y)
```

This is essentially a prefix sum in each bit dimension.

### Why Is This a Prefix Sum?

Think of a bitmask as coordinates in a multi-dimensional binary space. Each bit is a dimension with values {0, 1}. SOS DP is the N-dimensional analogue of the 2D prefix sum!

```
2D: pre[i][j] = Σ grid[r][c] for r ≤ i, c ≤ j

Bitmask (3 bits = 3D):
sos[101] = f[000] + f[001] + f[100] + f[101]
         = sum over all submasks of 101
```

### SOS DP Implementation

```java
public static int[] sosDP(int[] f, int bits) {
    int n = 1 << bits;
    int[] sos = Arrays.copyOf(f, n);

    for (int bit = 0; bit < bits; bit++) {
        for (int mask = 0; mask < n; mask++) {
            if ((mask & (1 << bit)) != 0)
                sos[mask] += sos[mask ^ (1 << bit)];
        }
    }
    return sos;
}

```

### Visual Trace (2 bits)

```
f = [f[00], f[01], f[10], f[11]] = [1, 2, 3, 4]

Process bit 0:
  mask=00: bit 0 not set, skip
  mask=01: bit 0 set → sos[01] += sos[00] → sos[01] = 2 + 1 = 3
  mask=10: bit 0 not set, skip
  mask=11: bit 0 set → sos[11] += sos[10] → sos[11] = 4 + 3 = 7

After bit 0: sos = [1, 3, 3, 7]

Process bit 1:
  mask=00: bit 1 not set, skip
  mask=01: bit 1 not set, skip
  mask=10: bit 1 set → sos[10] += sos[00] → sos[10] = 3 + 1 = 4
  mask=11: bit 1 set → sos[11] += sos[01] → sos[11] = 7 + 3 = 10

After bit 1: sos = [1, 3, 4, 10]

Verify: sos[11] = f[00] + f[01] + f[10] + f[11] = 1+2+3+4 = 10  ✓
        sos[10] = f[00] + f[10] = 1+3 = 4  ✓
        sos[01] = f[00] + f[01] = 1+2 = 3  ✓
```

### Complexity

| Operation | Time | Space |
|-----------|------|-------|
| SOS DP | O(N × 2^N) | O(2^N) |

### Classic Problems

1. **SOS DP (CSES)** — Direct application
2. **Compatible pairs** — For each mask, count masks with no overlapping bits
3. **Maximum AND/OR pair** — Find pair with maximum bitwise AND

---

## 12. Common Patterns Collection

### Pattern A: Running Sum / Cumulative Sum

The simplest form — just accumulate as you go.

```java
public static int canCompleteCircuit(int[] gas, int[] cost) {
    int n = gas.length;
    int total = 0, tank = 0, start = 0;

    for (int i = 0; i < n; i++) {
        int diff = gas[i] - cost[i];
        total += diff;
        tank += diff;
        if (tank < 0) {
            start = i + 1;
            tank = 0;
        }
    }
    return total >= 0 ? start : -1;
}

```

### Pattern B: Prefix Sum for Counting

Turn "count of X in range" into a prefix sum.

```java
public static int[] prefixCountZeros(int[] a) {
    int n = a.length;
    int[] count = new int[n + 1];
    for (int i = 0; i < n; i++) count[i + 1] = count[i] + (a[i] == 0 ? 1 : 0);
    return count;
}

```

### Pattern C: Prefix Sum for String Problems

Count character frequencies in ranges.

```java
public static int[][] buildCharPrefix(String s) {
    int n = s.length();
    int[][] pre = new int[n + 1][26];

    for (int i = 0; i < n; i++) {
        pre[i + 1] = Arrays.copyOf(pre[i], 26);
        pre[i + 1][s.charAt(i) - 'a']++;
    }
    return pre;
}

public static int countCharInRange(int[][] pre, int l, int r, char ch) {
    int c = ch - 'a';
    return pre[r + 1][c] - pre[l][c];
}

```

### Pattern D: Max/Min Prefix and Suffix

Track running maximum or minimum from both ends.

```java
public static int trapRainWater(int[] height) {
    int n = height.length;
    if (n == 0) return 0;

    int[] leftMax = new int[n];
    int[] rightMax = new int[n];

    // Build left max array
    leftMax[0] = height[0];
    for (int i = 1; i < n; i++) {
        leftMax[i] = Math.max(leftMax[i - 1], height[i]);
    }

    // Build right max array
    rightMax[n - 1] = height[n - 1];
    for (int i = n - 2; i >= 0; i--) {
        rightMax[i] = Math.max(rightMax[i + 1], height[i]);
    }

    // Calculate trapped water
    int water = 0;
    for (int i = 0; i < n; i++) {
        water += Math.min(leftMax[i], rightMax[i]) - height[i];
    }

    return water;
}
``
```

### Pattern E: Sweep Line + Difference Array

Count overlapping intervals using difference array.

```java
public static int maxOverlappingIntervals(int[][] intervals, int maxVal) {
    int[] diff = new int[maxVal + 2];

    // Apply difference array updates
    for (int[] interval : intervals) {
        int start = interval[0];
        int end = interval[1];

        diff[start] += 1;
        diff[end + 1] -= 1;
    }

    int maxOverlap = 0;
    int current = 0;

    // Prefix sum builds the actual active count at each point
    for (int i = 0; i <= maxVal; i++) {
        current += diff[i];
        maxOverlap = Math.max(maxOverlap, current);
    }

    return maxOverlap;
}
```

### Pattern F: Prefix Sum + Two Pointers

For non-negative arrays, find subarrays with exact sum.

```java
public static int[] subarrayWithSum(int[] a, int target) {
    int current = 0;
    int left = 0;

    for (int right = 0; right < a.length; right++) {
        current += a[right];

        while (current > target && left <= right) {
            current -= a[left];
            left++;
        }

        if (current == target) {
            return new int[]{left, right};
        }
    }

    return null; // no subarray found
}
```

---

## 13. Pattern Recognition Cheat Sheet

### Decision Flowchart

```
"I need to answer range queries..."
   │
   ├── Static array, sum/xor queries?
   │     → Prefix Sum / Prefix XOR — O(N) build, O(1) query
   │
   ├── Static 2D grid, rectangle queries?
   │     → 2D Prefix Sum — O(RC) build, O(1) query
   │
   ├── Many range updates, then read?
   │     → Difference Array — O(1) update, O(N) reconstruct
   │
   ├── Many 2D rectangle updates?
   │     → 2D Difference Array — O(1) update, O(RC) reconstruct
   │
   ├── Count subarrays with sum/xor = k?
   │     → Prefix Sum + Hash Map — O(N)
   │
   ├── Count subarrays divisible by k?
   │     → Prefix Sum mod k + Counting — O(N)
   │
   ├── Product except self?
   │     → Prefix + Suffix Products — O(N)
   │
   ├── Path queries on tree?
   │     → Prefix Sum on Tree + LCA — varies
   │
   ├── Non-negative array, subarray sum in range?
   │     → Prefix Sum + Binary Search — O(N log N)
   │
   └── Bitmask subset sums?
         → SOS DP — O(N × 2^N)
```

### Quick Reference Table

| Problem Type | Technique | Time | Key Insight |
|--------------|-----------|------|-------------|
| Range sum query | 1D prefix sum | O(1) | `pre[r+1] - pre[l]` |
| Rectangle sum | 2D prefix sum | O(1) | Inclusion-exclusion |
| # subarrays sum=k | Prefix + hash map | O(N) | Count `pre[j]-k` |
| # subarrays sum%k=0 | Prefix mod k | O(N) | Equal remainders pair |
| Range update (batch) | Difference array | O(1)/update | Inverse of prefix sum |
| 2D range update | 2D difference | O(1)/update | 4-corner trick |
| Range XOR | Prefix XOR | O(1) | `a^a = 0` cancellation |
| Product except self | Prefix × suffix | O(N) | Left pass + right pass |
| Tree path sum | Depth prefix + LCA | O(log N) | `sum[u]+sum[v]-2*sum[lca]+val[lca]` |
| Subset sums (bitmask) | SOS DP | O(N·2^N) | N-dimensional prefix sum |

### Combining Prefix Sum with Other Techniques

| Combo | Example |
|-------|---------|
| Prefix Sum + Binary Search | Min subarray length with sum ≥ k (non-negative) |
| Prefix Sum + Sliding Window | Two pointers with running sum |
| Prefix Sum + Monotonic Deque | Max subarray sum with length in [a, b] |
| Prefix Sum + Segment Tree | Dynamic range sum with point updates |
| Prefix Sum + BIT (Fenwick) | Online prefix sum with updates |
| Difference Array + Sweep Line | Event counting, interval overlap |
| Prefix Sum + Coordinate Compression | Count inversions, range counting |
| Prefix XOR + Trie | Maximum XOR subarray |

### Common Mistakes to Avoid

| Mistake | Fix |
|---------|-----|
| Off-by-one in prefix indexing | Use `n+1` size, `pre[0]=0` convention |
| Forgetting `count[0] = 1` in hash map approach | The empty prefix is a valid subarray start |
| Using prefix sum with updates | Use BIT/Fenwick or segment tree instead |
| Negative modulo in C++/Java | Use `((x % k) + k) % k` |
| Assuming sorted prefix with negatives | Only non-negative arrays give sorted prefix |
| Integer overflow in prefix products | Use modular arithmetic or check bounds |
| 2D inclusion-exclusion sign errors | Draw it out: `+total -top -left +corner` |

### Complexity Summary

| Technique | Build | Query | Update |
|-----------|-------|-------|--------|
| 1D Prefix Sum | O(N) | O(1) | ✗ (static) |
| 2D Prefix Sum | O(RC) | O(1) | ✗ (static) |
| 1D Difference | O(N) | O(N) reconstruct | O(1) |
| 2D Difference | O(RC) | O(RC) reconstruct | O(1) |
| Prefix + HashMap | O(N) | inline | — |
| SOS DP | O(N·2^N) | O(1) | ✗ (static) |
| BIT/Fenwick | O(N) | O(log N) | O(log N) |

---

**The prefix sum is the Swiss Army knife of competitive programming.** Almost every "range query" or "subarray counting" problem has a prefix sum hiding inside it. When you see "subarray," "range," "sum," "count," or "divisible" — think prefix sum first.
