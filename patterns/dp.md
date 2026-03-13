# Dynamic Programming — Comprehensive Pattern Guide

---

## What Is DP?

Dynamic Programming is a technique for solving problems that have two properties:

1. **Optimal substructure**: The optimal solution can be built from optimal solutions of subproblems
2. **Overlapping subproblems**: The same subproblems are solved repeatedly

DP = **recursion + memoization** (or equivalently, building a table bottom-up).

```
Fibonacci WITHOUT DP:              Fibonacci WITH DP:

       fib(5)                          fib(5)
      /      \                        /      \
   fib(4)   fib(3)                fib(4)   fib(3) <- cached!
   /    \    /    \               /    \
fib(3) fib(2) fib(2) fib(1)  fib(3) fib(2) <- cached!
 ...    ...    ...              /    \          fib(2) fib(1) <- cached!

Calls: 15 (exponential)        Calls: 5 (linear)
```

---

## Table of Contents

1. [How to Approach DP Problems](#1-how-to-approach-dp-problems)
2. [Top-Down vs Bottom-Up](#2-top-down-vs-bottom-up)
3. [Linear DP](#3-linear-dp)
4. [Grid DP](#4-grid-dp)
5. [Knapsack Family](#5-knapsack-family)
6. [Longest Increasing Subsequence](#6-longest-increasing-subsequence)
7. [Longest Common Subsequence](#7-longest-common-subsequence)
8. [Interval DP](#8-interval-dp)
9. [State Machine DP](#9-state-machine-dp)
10. [Tree DP](#10-tree-dp)
11. [Bitmask DP](#11-bitmask-dp)
12. [Digit DP](#12-digit-dp)
13. [Probability / Expected Value DP](#13-probability--expected-value-dp)
14. [DP on DAGs](#14-dp-on-dags)
15. [DP Optimizations](#15-dp-optimizations)
16. [Pattern Recognition Cheat Sheet](#16-pattern-recognition-cheat-sheet)

---

## 1. How to Approach DP Problems

### The 5-Step Framework

Every DP problem can be solved with this framework:

```
Step 1: DEFINE THE STATE
        "What information do I need to describe a subproblem?"
        -> dp[i] = ..., dp[i][j] = ...

Step 2: DEFINE THE TRANSITION
        "How do I build the answer from smaller subproblems?"
        -> dp[i] = some function of dp[i-1], dp[i-2], ...

Step 3: DEFINE THE BASE CASE
        "What are the smallest subproblems I know the answer to?"
        -> dp[0] = ..., dp[1] = ...

Step 4: DEFINE THE ANSWER
        "Which state gives me the final answer?"
        -> return dp[n], or max(dp), or dp[n][target]

Step 5: OPTIMIZE SPACE (optional)
        "Do I only need the last row/few states?"
        -> reduce from O(n^2) space to O(n)
```

### Recognizing DP Problems

| Signal | Example |
|--------|---------|
| "Count the number of ways" | How many paths from top-left to bottom-right? |
| "Minimum/maximum cost" | Minimum coins to make change |
| "Is it possible?" | Can we partition into two equal-sum subsets? |
| "Longest/shortest" | Longest increasing subsequence |
| Choices at each step | Take or skip each item |
| Problem has optimal substructure | Shortest path through a grid |

### Common Mistakes

| Mistake | Fix |
|---------|-----|
| Missing state | Add dimensions until subproblems are unique |
| Wrong transition direction | Ensure you only use already-computed states |
| Off-by-one in base cases | Trace through smallest examples manually |
| Not considering "do nothing" | Often dp[i] = dp[i-1] is a valid transition |
| Forgetting modular arithmetic | Apply MOD at every addition/multiplication |

---

## 2. Top-Down vs Bottom-Up

### Top-Down (Memoization)

Start from the final answer, recurse into subproblems, cache results.

```java
import java.util.*;
public class Fibonacci {
    private Map<Integer, Long> memo = new HashMap<>();
    public long fib(int n) {
        if (n <= 1) {
            return n;
        }

        if (memo.containsKey(n)) {
            return memo.get(n);
        }

        long value = fib(n - 1) + fib(n - 2);
        memo.put(n, value);

        return value;
    }
}
```

### Bottom-Up (Tabulation)

Start from base cases, fill the table iteratively.

```java
public class FibonacciDP {

    public long fib(int n) {
        if (n <= 1) {
            return n;
        }

        long[] dp = new long[n + 1];
        dp[1] = 1;

        for (int i = 2; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }

        return dp[n];
    }
}
```

### When to Use Which

| | Top-Down | Bottom-Up |
|--|----------|-----------|
| **Pros** | Natural to think recursively; only computes needed states | No recursion overhead; easier to optimize space |
| **Cons** | Recursion limit; function call overhead | Must figure out correct iteration order; computes all states |
| **Best for** | Complex state spaces; sparse states | Simple iteration order; when you need all states |
| **Contest tip** | Start with top-down, convert if TLE | Preferred for performance-critical problems |

### Space Optimization

If `dp[i]` only depends on `dp[i-1]` (and possibly `dp[i-2]`), you don't need the full array:

```java
# Before: O(n) space
long[] dp = new long[n + 1];
dp[1] = 1;
for (int i = 2; i <= n; i++) {
    dp[i] = dp[i - 1] + dp[i - 2];
}
return dp[n];

# After: O(1) space
public long fib(int n) {
    if (n == 0) return 0;
    if (n == 1) return 1;

    long a = 0;
    long b = 1;

    for (int i = 2; i <= n; i++) {
        long temp = b;
        b = a + b;  // new b
        a = temp;   // new a = old b
    }

    return b;
}

```

---

## 3. Linear DP

The simplest DP pattern: states form a 1D sequence.

### Pattern

```
dp[i] = answer considering elements 0..i (or i..n-1)
dp[i] depends on dp[i-1], dp[i-2], ..., or dp[j] for j < i
```

### Example: Maximum Subarray Sum (Kadane's Algorithm)

**Problem**: Find the contiguous subarray with the largest sum.

```
Array:  [-2, 1, -3, 4, -1, 2, 1, -5, 4]

State:  dp[i] = maximum subarray sum ENDING at index i

Transition:
  dp[i] = max(arr[i], dp[i-1] + arr[i])
          ^           ^
          start new   extend previous

Base: dp[0] = arr[0]
Answer: max(dp)
```

```java
public class MaxSubarray {
    public int maxSubarray(int[] arr) {
        int dp = arr[0];    // max ending here
        int best = arr[0];  // global max

        for (int i = 1; i < arr.length; i++) {
            dp = Math.max(arr[i], dp + arr[i]);  // extend or restart
            best = Math.max(best, dp);           // update global best
        }

        return best;
    }
}
```

### Example: Coin Combinations (Count Ways)

**Problem**: Given coins `[1, 3, 5]`, how many ways to make sum `n`?

```
State:  dp[s] = number of ways to form sum s

Transition:
  dp[s] = sum(dp[s - coin] for coin in coins if s >= coin)

Base: dp[0] = 1 (one way to make sum 0: use no coins)
Answer: dp[n]
```

```java
public class CoinWays {
    public long coinWays(int[] coins, int n) {
        long[] dp = new long[n + 1];
        dp[0] = 1;  // 1 way to form sum 0 (choose nothing)

        for (int s = 1; s <= n; s++) {
            for (int coin : coins) {
                if (s >= coin) {  dp[s] += dp[s - coin];
                }
            }
        }

        return dp[n];
    }
}
```

### Example: House Robber

**Problem**: Rob houses in a line, can't rob two adjacent. Maximize total.

```
Houses: [2, 7, 9, 3, 1]

State:  dp[i] = max money from houses 0..i

Transition:
  dp[i] = max(dp[i-1],          # skip house i
              dp[i-2] + arr[i])  # rob house i

Base: dp[0] = arr[0], dp[1] = max(arr[0], arr[1])
Answer: dp[n-1]
```

```java
public class HouseRobber {
  public int rob(int[] nums) {
      if (nums.length == 1) {
          return nums[0];
      }
      int a = nums[0];                     // dp[i-2]
      int b = Math.max(nums[0], nums[1]);  // dp[i-1]

      for (int i = 2; i < nums.length; i++) {
          int newB = Math.max(b, a + nums[i]);  // max(rob previous, rob this + dp[i-2])
          a = b;
          b = newB;
      }

      return b;   // dp[n-1]
  }
}
```

---

## 4. Grid DP

States are 2D positions in a grid.

### Pattern

```
dp[i][j] = answer for cell (i, j)
dp[i][j] depends on dp[i-1][j], dp[i][j-1], dp[i-1][j-1], etc.
```

### Example: Unique Paths

**Problem**: Count paths from top-left to bottom-right, moving only right or down.

```
Grid 3x3:

dp[0][0]=1  dp[0][1]=1  dp[0][2]=1
dp[1][0]=1  dp[1][1]=2  dp[1][2]=3
dp[2][0]=1  dp[2][1]=3  dp[2][2]=6

Transition: dp[i][j] = dp[i-1][j] + dp[i][j-1]      (from above) + (from left)
Answer: dp[m-1][n-1] = 6
```

```java
public class UniquePaths {
  public int uniquePaths(int m, int n) {
      int[][] dp = new int[m][n];
      // Initialize first row and first column to 1
      for (int i = 0; i < m; i++) {
          dp[i][0] = 1;
      }
      for (int j = 0; j < n; j++) {
          dp[0][j] = 1;
      }

      // Fill the DP table
      for (int i = 1; i < m; i++) {
          for (int j = 1; j < n; j++) {
              dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
          }
      }

      return dp[m - 1][n - 1];
  }
}
``
```

### Example: Minimum Path Sum

**Problem**: Find the path from top-left to bottom-right with minimum sum.

```
Grid:
1  3  1
1  5  1
4  2  1

dp:
1  4  5
2  7  6
6  8  7

Transition: dp[i][j] = grid[i][j] + min(dp[i-1][j], dp[i][j-1])
Answer: dp[m-1][n-1] = 7  (path: 1->3->1->1->1)
```

```java
public class MinPathSum {
  public int minPathSum(int[][] grid) {
      int m = grid.length;
      int n = grid[0].length;
      int[][] dp = new int[m][n];
      // Start
      dp[0][0] = grid[0][0];

      // First column
      for (int i = 1; i < m; i++) {
          dp[i][0] = dp[i - 1][0] + grid[i][0];
      }

      // First row
      for (int j = 1; j < n; j++) {
          dp[0][j] = dp[0][j - 1] + grid[0][j];
      }

      // Fill DP table
      for (int i = 1; i < m; i++) {
          for (int j = 1; j < n; j++) {
              dp[i][j] = grid[i][j] +Math.min(dp[i - 1][j], dp[i][j - 1]);
          }
      }

      return dp[m - 1][n - 1];
  }
}
```

### Space Optimization for Grid DP

Since each row only depends on the previous row:

```java
public class MinPathSumOptimized {
  public int minPathSumOptimized(int[][] grid) {
    int m = grid.length;
    int n = grid[0].length;

    int[] dp = new int[n];

    // Initialize first row
    dp[0] = grid[0][0];
    for (int j = 1; j < n; j++) {
        dp[j] = dp[j - 1] + grid[0][j];
    }
    // Process remaining rows
    for (int i = 1; i < m; i++) {

        // Update first column
        dp[0] += grid[i][0];

        // Update inner cells
        for (int j = 1; j < n; j++) {
            dp[j] = grid[i][j] + Math.min(dp[j], dp[j - 1]);
            //                          ↑ old dp[j]   ↑ left dp[j-1]
        }
    }
    return dp[n - 1];
  }
}
```

---

## 5. Knapsack Family

The most important DP family. Three major variants.

### 5.1 0/1 Knapsack

**Problem**: N items, each with weight and value. Pick items to maximize value without exceeding capacity W. Each item used **at most once**.

```
State:  dp[i][w] = max value using items 0..i-1 with capacity w

Transition:
  dp[i][w] = max(
      dp[i-1][w],                    # don't take item i
      dp[i-1][w - weight[i]] + val[i]  # take item i (if w >= weight[i])
  )

Base: dp[0][w] = 0 for all w
Answer: dp[n][W]
```

```java
public class Knapsack01 {
  public int knapsack01(int[] weights, int[] values, int W) {
      int n = weights.length;
      int[][] dp = new int[n + 1][W + 1];
      for (int i = 1; i <= n; i++) {
          int wt = weights[i - 1];
          int val = values[i - 1];

          for (int w = 0; w <= W; w++) {

              // Don't take item i
              dp[i][w] = dp[i - 1][w];

              // Try taking item i (if it fits)
              if (w >= wt) {dp[i][w] = Math.max(dp[i][w],dp[i - 1][w - wt] + val);
              }
          }
      }
      return dp[n][W];
  }
}
```

**Space-optimized** (iterate w in reverse to avoid using item twice):

```java
public class Knapsack01Optimized {
  public int knapsack01Optimized(int[] weights, int[] values, int W) {
      int[] dp = new int[W + 1];
      for (int i = 0; i < weights.length; i++) {
          int wt = weights[i];
          int val = values[i];

          // Reverse loop is CRITICAL to avoid reusing an item more than once.
          for (int w = W; w >= wt; w--) {
              dp[w] = Math.max(dp[w], dp[w - wt] + val);
          }
      }
      return dp[W];
  }
}
```

**Why reverse?** Forward iteration would let `dp[w - weights[i]]` use the current item's contribution (already updated in this iteration), effectively using the item multiple times. Reverse ensures we only use `dp` values from the previous iteration.

### 5.2 Unbounded Knapsack

**Problem**: Same as 0/1, but each item can be used **unlimited times**.

```java
public class KnapsackUnbounded {
  public int knapsackUnbounded(int[] weights, int[] values, int W) {
      int[] dp = new int[W + 1];

      for (int i = 0; i < weights.length; i++) {
          int wt = weights[i];
          int val = values[i];

          // FORWARD loop → allows reusing the same item unlimited times
          for (int w = wt; w <= W; w++) {
              dp[w] = Math.max(dp[w], dp[w - wt] + val);
          }
      }
      return dp[W];
  }
}
```

Forward iteration naturally allows reuse: `dp[w - weights[i]]` may already include item `i`.

### 5.3 Bounded Knapsack

**Problem**: Item i can be used at most `count[i]` times.

**Approach**: Convert each item with count `c` into binary groups: 1, 2, 4, ..., remainder. This reduces to 0/1 knapsack with O(N log C) items.

```java
public class BoundedKnapsack {
  public int knapsackBounded(int[] weights, int[] values, int[] counts, int W) {
      // Step 1: Expand bounded items using binary grouping
      // Each (weight, count) becomes items with weights: w*1, w*2, w*4, ..., w*rem
      List<int[]> items = new ArrayList<>(); // each element: {w_item, v_item}

      for (int i = 0; i < weights.length; i++) {
          int w = weights[i];
          int v = values[i];
          int c = counts[i];

          int k = 1;
          while (k <= c) {
              items.add(new int[]{w * k, v * k});
              c -= k;
              k <<= 1;  // k *= 2
          }
          if (c > 0) {
              // remainder chunk
              items.add(new int[]{w * c, v * c});
          }
      }

      // Step 2: Solve as 0/1 knapsack
      int[] dp = new int[W + 1];

      for (int[] item : items) {
          int wItem = item[0];
          int vItem = item[1];

          // REVERSE loop for standard 0/1 knapsack
          for (int w = W; w >= wItem; w--) {
              dp[w] = Math.max(dp[w], dp[w - wItem] + vItem);
          }
      }
      return dp[W];
  }
}

```

### Knapsack Variant Summary

| Variant | Item usage | Iteration direction | Time |
|---------|-----------|-------------------|------|
| 0/1 | At most once | **Reverse** w | O(NW) |
| Unbounded | Unlimited | **Forward** w | O(NW) |
| Bounded | At most c[i] | Binary grouping + reverse | O(NW log C) |

### Common Knapsack Disguises

| Problem | Knapsack form |
|---------|--------------|
| Subset Sum | 0/1 knapsack, values = weights, check dp[target] > 0 |
| Partition Equal Subset | 0/1 knapsack with target = total_sum / 2 |
| Coin Change (min coins) | Unbounded, minimize count instead of maximize value |
| Coin Change (count ways) | Unbounded, count instead of max |
| Target Sum (+/-) | 0/1 knapsack, target = (sum + target) / 2 |

---

## 6. Longest Increasing Subsequence

### Problem

Find the length of the longest strictly increasing subsequence.

```
Array: [10, 9, 2, 5, 3, 7, 101, 18]
LIS:   [2, 3, 7, 101] or [2, 3, 7, 18] or [2, 5, 7, 101] ...
Length: 4
```

### O(N^2) DP Solution

```
State:  dp[i] = length of LIS ending at index i

Transition:
  dp[i] = 1 + max(dp[j] for j < i if arr[j] < arr[i])

Base: dp[i] = 1 for all i (each element is a subsequence of length 1)
Answer: max(dp)
```

```java
public class LIS {
  public int lisN2(int[] arr) {
      int n = arr.length;
      int[] dp = new int[n];
      Arrays.fill(dp, 1);
      for (int i = 1; i < n; i++) {
          for (int j = 0; j < i; j++) {
              if (arr[j] < arr[i]) {       // strictly increasing
                  dp[i] = Math.max(dp[i], dp[j] + 1);
              }
          }
      }

      int best = 1;
      for (int len : dp) {
          best = Math.max(best, len);
      }

      return best;
  }
}
```

### O(N log N) with Binary Search

Maintain a list `tails` where `tails[k]` = smallest ending element of all increasing subsequences of length `k+1`.

```java
import java.util.*;
public class LISnlogn {
  public int lisNlogN(int[] arr) {
      // tails[i] = the smallest ending value of any subsequence of length i+1
      int[] tails = new int[arr.length];
      int size = 0;
      for (int x : arr) {
          // binary search in tails[0:size)
          int pos = Arrays.binarySearch(tails, 0, size, x);

          if (pos < 0) {
              pos = -(pos + 1);   // convert to insertion index
          }

          tails[pos] = x;

          if (pos == size) {
              size++;             // extended longest subsequence
          }
      }

      return size;
  }
}
```

### Trace

```
arr = [10, 9, 2, 5, 3, 7, 101, 18]

x=10:  tails = [10]
x=9:   tails = [9]           (9 replaces 10 at pos 0)
x=2:   tails = [2]           (2 replaces 9)
x=5:   tails = [2, 5]        (5 extends)
x=3:   tails = [2, 3]        (3 replaces 5 at pos 1)
x=7:   tails = [2, 3, 7]     (7 extends)
x=101: tails = [2, 3, 7, 101] (101 extends)
x=18:  tails = [2, 3, 7, 18]  (18 replaces 101 at pos 3)

Length = 4
```

Note: `tails` is NOT the actual LIS. It's a working structure. To reconstruct the actual LIS, track parent pointers.

### Variations
| Variation                          | Java Explanation                                           |
| ---------------------------------- | ---------------------------------------------------------- |
| **Non‑decreasing LIS**             | Use `upperBound` (first index > x) instead of `lowerBound` |
| **Longest Decreasing Subsequence** | Use LIS on `-nums[i]` or reverse + LIS                     |
| **Count of LIS**                   | Maintain two arrays: `dp[i]` and `count[i]`                |
| **Min deletions for sorted array** | `n - LIS`                                                  |

---

## 7. Longest Common Subsequence

### Problem

Find the length of the longest subsequence common to two strings.

```
s1 = "ABCBDAB"
s2 = "BDCAB"
LCS = "BCAB" (length 4)
```

### Implementation

```
State:  dp[i][j] = LCS of s1[0..i-1] and s2[0..j-1]

Transition:
  If s1[i-1] == s2[j-1]:
      dp[i][j] = dp[i-1][j-1] + 1     # characters match, extend
  Else:
      dp[i][j] = max(dp[i-1][j],       # skip from s1
                      dp[i][j-1])       # skip from s2

Base: dp[0][j] = dp[i][0] = 0
Answer: dp[m][n]
```

```java
public class LCS {
  public int lcs(String s1, String s2) {
      int m = s1.length();
      int n = s2.length();
      int[][] dp = new int[m + 1][n + 1];
      for (int i = 1; i <= m; i++) {
          for (int j = 1; j <= n; j++) {
              if (s1.charAt(i - 1) == s2.charAt(j - 1)) {dp[i][j] = dp[i - 1][j - 1] + 1;
              } else {dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
              }
          }
      }

      return dp[m][n];
  }
}

```

### Reconstruct the LCS

```java
public class LCSString {

    public String lcsString(String s1, String s2) {
        int m = s1.length();
        int n = s2.length();

        // DP table: dp[i][j] = LCS length for s1[:i], s2[:j]
        int[][] dp = new int[m + 1][n + 1];

        // Fill DP
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (s1.charAt(i - 1) == s2.charAt(j - 1)) {  dp[i][j] = dp[i - 1][j - 1] + 1;
                } else {  dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                }
            }
        }

        // Backtrack to build LCS string
        StringBuilder result = new StringBuilder();
        int i = m, j = n;

        while (i > 0 && j > 0) {
            if (s1.charAt(i - 1) == s2.charAt(j - 1)) {
                result.append(s1.charAt(i - 1));   // match → part of LCS
                i--;
                j--;
            } else if (dp[i - 1][j] > dp[i][j - 1]) {
                i--;  // move up
            } else {
                j--;  // move left
            }
        }

        return result.reverse().toString();
    }
}
```

### Space Optimization for LCS

The full 2D table uses O(MN) space. Since each row `dp[i]` only depends on `dp[i-1]`, we can reduce to **O(min(M,N))** using two rows (or a single row with a saved variable):

```java
public class LCSOptimized {

    public int lcsOptimized(String s1, String s2) {
        // Ensure s2 is the shorter string to minimize space
        if (s1.length() < s2.length()) {
            String temp = s1;
            s1 = s2;
            s2 = temp;
        }

        int m = s1.length();
        int n = s2.length();

        int[] prev = new int[n + 1];

        for (int i = 1; i <= m; i++) {
            int[] curr = new int[n + 1];

            for (int j = 1; j <= n; j++) {
                if (s1.charAt(i - 1) == s2.charAt(j - 1)) {  curr[j] = prev[j - 1] + 1;    // match
                } else {  curr[j] = Math.max(prev[j], curr[j - 1]); // skip one side
                }
            }

            prev = curr;
        }
      return prev[n];
    }
}
```

**Single-row trick** (saves one allocation, but trickier):

```java
public class LCSSingleRow {
  public int lcsSingleRow(String s1, String s2) {
      // Ensure s2 is shorter for minimal space
      if (s1.length() < s2.length()) {
          String temp = s1;
          s1 = s2;
          s2 = temp;
      }
      int m = s1.length();
      int n = s2.length();
      int[] dp = new int[n + 1];
      for (int i = 1; i <= m; i++) {
          int prevDiag = 0;  // stores dp[j-1] from previous row (dp[i-1][j-1])

          for (int j = 1; j <= n; j++) {

              int temp = dp[j];  // this is dp[i-1][j] before overwrite

              if (s1.charAt(i - 1) == s2.charAt(j - 1)) {dp[j] = prevDiag + 1;
              } else {dp[j] = Math.max(dp[j], dp[j - 1]);
              }

              prevDiag = temp;  // update for next column
          }
      }
      return dp[n];
  }
}

```

**Caveat**: With O(N) space you can compute the LCS **length**, but **not reconstruct** the actual LCS string. Reconstruction requires the full 2D table (or Hirschberg's algorithm for O(N) space reconstruction in O(MN) time).

### LCS Family

| Problem | Relation to LCS |
|---------|----------------|
| Edit Distance | Similar DP table, different transition |
| Shortest Common Supersequence | `len(s1) + len(s2) - LCS` |
| Longest Palindromic Subsequence | LCS of string and its reverse |
| Diff (version control) | LCS = unchanged lines |

---

## 8. Interval DP

### Pattern

Problems where the answer for a range `[i, j]` depends on sub-ranges.

```
State:  dp[i][j] = answer for the subarray/substring from i to j

Transition:
  dp[i][j] = best over all split points k in [i, j-1]:
              combine(dp[i][k], dp[k+1][j])

Iteration: by increasing length of interval
Base: dp[i][i] = base value (single element)
Answer: dp[0][n-1]
```

### Example: Matrix Chain Multiplication

**Problem**: Given matrices A1 x A2 x ... x An, find the order of multiplication that minimizes total scalar multiplications.

```
dimensions = [10, 30, 5, 60]
Matrices: A1(10x30), A2(30x5), A3(5x60)

(A1*A2)*A3 = 10*30*5 + 10*5*60 = 1500 + 3000 = 4500
A1*(A2*A3) = 30*5*60 + 10*30*60 = 9000 + 18000 = 27000

Optimal: (A1*A2)*A3 = 4500
```

```java
public class MatrixChainMultiplication {

    public int matrixChain(int[] dims) {
        int n = dims.length - 1;   // number of matrices
        int[][] dp = new int[n][n];

        // length = chain length
        for (int length = 2; length <= n; length++) {
            for (int i = 0; i <= n - length; i++) {
                int j = i + length - 1;
                dp[i][j] = Integer.MAX_VALUE;

                for (int k = i; k < j; k++) {
  int cost = dp[i][k]           + dp[k + 1][j]           + dims[i] * dims[k + 1] * dims[j + 1];
  dp[i][j] = Math.min(dp[i][j], cost);
                }
            }
        }

        return dp[0][n - 1];
    }
}
```

### Example: Burst Balloons

**Problem**: Burst balloons in an order to maximize coins. Bursting balloon i gives `nums[left] * nums[i] * nums[right]`.

```java
import java.util.*;
public class BurstBalloons {
    public int maxCoins(int[] nums) {
      // Step 1: pad nums with 1 on both ends
      int n = nums.length + 2;
      int[] arr = new int[n];
      arr[0] = 1;
      arr[n - 1] = 1;

      for (int i = 0; i < nums.length; i++) {
          arr[i + 1] = nums[i];
      }

      // Step 2: DP table
      int[][] dp = new int[n][n];

      // Step 3: interval length from 2 to n-1
      for (int length = 2; length < n; length++) {
          for (int i = 0; i + length < n; i++) {
              int j = i + length;

              // Try every possible k as the last balloon to burst
              for (int k = i + 1; k < j; k++) {dp[i][j] = Math.max(    dp[i][j],    dp[i][k] + dp[k][j] + arr[i] * arr[k] * arr[j]);
              }
          }
      }

      return dp[0][n - 1];
    }
}
```

### Space Optimization for Interval DP

Interval DP generally **cannot** be space-optimized below O(N^2). Unlike linear or grid DP where each row depends only on the previous row, interval DP entries `dp[i][j]` depend on arbitrary sub-intervals `dp[i][k]` and `dp[k+1][j]` — you need the full table.

**Exception**: Some interval-like problems (e.g., palindrome partitioning) can be reformulated as linear DP, reducing space to O(N). See below.

### Example: Palindrome Partitioning (Min Cuts)

**Problem**: Minimum cuts to partition a string into palindromes.

```java
public class MinCutPalindrome {
  public int minCut(String s) {
      int n = s.length();
      char[] arr = s.toCharArray();

      // Step 1: Precompute palindrome table
      boolean[][] isPal = new boolean[n][n];

      for (int i = n - 1; i >= 0; i--) {
          for (int j = i; j < n; j++) {
              if (arr[i] == arr[j] && (j - i <= 2 || isPal[i + 1][j - 1])) {isPal[i][j] = true;
              }
          }
      }

      // Step 2: dp[i] = minimum cuts for substring s[0..i]
      int[] dp = new int[n];
      for (int i = 0; i < n; i++) {
          dp[i] = i; // worst case: cut before every character
      }

      for (int i = 1; i < n; i++) {

          // If entire prefix s[0..i] is a palindrome → 0 cuts
          if (isPal[0][i]) {
              dp[i] = 0;
              continue;
          }

          // Otherwise try all valid partitions
          for (int j = 1; j <= i; j++) {
              if (isPal[j][i]) {dp[i] = Math.min(dp[i], dp[j - 1] + 1);
              }
          }
      }

      return dp[n - 1];
  }
}
```

---

## 9. State Machine DP

### Pattern

The problem has distinct **states** you can be in, with transitions between them. Each step, you transition between states.

```
State Machine:

   ┌──────┐    buy     ┌──────┐
   │ NOT  │ ──────────> │ HOLD │
   │HOLDING│ <────────── │  ING │
   └──────┘    sell     └──────┘
```

### Example: Best Time to Buy and Sell Stock with Cooldown

**Problem**: Buy and sell stocks, but after selling you must wait one day.

```
States: REST (not holding, can buy)
        HOLD (holding stock, can sell)
        COOL (just sold, must wait)

Transitions:
  rest[i] = max(rest[i-1], cool[i-1])       # do nothing or finish cooldown
  hold[i] = max(hold[i-1], rest[i-1] - p[i]) # keep holding or buy
  cool[i] = hold[i-1] + p[i]                 # sell

Answer: max(rest[n-1], cool[n-1])
```

```java
public class MaxProfitCooldown {
  public int maxProfitCooldown(int[] prices) {
      if (prices.length == 0) {
          return 0;
      }
      int n = prices.length;
      int[] rest = new int[n];
      int[] hold = new int[n];
      int[] cool = new int[n];

      hold[0] = -prices[0];

      for (int i = 1; i < n; i++) {
          rest[i] = Math.max(rest[i - 1], cool[i - 1]);
          hold[i] = Math.max(hold[i - 1], rest[i - 1] - prices[i]);
          cool[i] = hold[i - 1] + prices[i];
      }

      return Math.max(rest[n - 1], cool[n - 1]);
  }
}
```

### Space Optimization for State Machine DP

Since each state at step `i` only depends on step `i-1`, replace arrays with variables — O(N) space → O(1):

```java
public class MaxProfitCooldownOptimized {
  public int maxProfitCooldownOptimized(int[] prices) {
      if (prices.length == 0) {
          return 0;
      }
      int rest = 0;
      int hold = -prices[0];
      int cool = 0;

      for (int i = 1; i < prices.length; i++) {
          int newRest = Math.max(rest, cool);
          int newHold = Math.max(hold, rest - prices[i]);
          int newCool = hold + prices[i];

          rest = newRest;
          hold = newHold;
          cool = newCool;
      }

      return Math.max(rest, cool);
  }
}
```

**Key**: Update all states simultaneously (use `new_` variables or tuple unpacking) to avoid using partially-updated values from the current step.

### Example: Best Time to Buy and Sell Stock with K Transactions

```java
public class MaxProfitK {
  public int maxProfitK(int[] prices, int k) {
      int n = prices.length;
      if (n == 0) return 0;

      // Unlimited transactions case (k >= n/2)
      if (k >= n / 2) {
          int profit = 0;
          for (int i = 1; i < n; i++) {
              if (prices[i] > prices[i - 1]) {profit += prices[i] - prices[i - 1];
              }
          }
          return profit;
      }

      // dp[t][i] = max profit using at most t transactions on days 0..i
      int[][] dp = new int[k + 1][n];

      for (int t = 1; t <= k; t++) {
          int bestBuy = -prices[0];  // best dp[t-1][i] - prices[i] seen so far

          for (int i = 1; i < n; i++) {
              dp[t][i] = Math.max(dp[t][i - 1],         // no sell today
                  bestBuy + prices[i]   // sell today
              );

              bestBuy = Math.max(bestBuy,dp[t - 1][i] - prices[i]   // buy today
              );
          }
      }
    return dp[k][n - 1];
  }
}
```

### Stock Problem Family

| Variant | States | Extra |
|---------|--------|-------|
| One transaction | buy price tracking | O(n) greedy |
| Unlimited transactions | hold/not-hold | O(n) |
| K transactions | k x hold/not-hold | O(nk) |
| With cooldown | rest/hold/cool | 3 states |
| With transaction fee | hold/not-hold, subtract fee on sell | 2 states |

---

## 10. Tree DP

### Pattern

DP on a rooted tree where each node's value depends on its children.

```
State:  dp[node] = answer for the subtree rooted at node
Transition: dp[node] = combine(dp[child1], dp[child2], ...)
Direction: bottom-up (leaves -> root), naturally done via post-order DFS
```

### Example: Maximum Independent Set

**Problem**: Select nodes with maximum total weight such that no two adjacent nodes are selected.

```
         1 (w=10)
        / \
   (w=20)2  3(w=30)
      /
  (w=40)4

dp[node][0] = max weight NOT selecting node
dp[node][1] = max weight selecting node

Transitions:
  dp[node][0] = sum(max(dp[child][0], dp[child][1]) for child)
                # if we don't select node, children can be either
  dp[node][1] = weight[node] + sum(dp[child][0] for child)
                # if we select node, children must NOT be selected
```

```java
class Solution {

    private int[][] dp;        // dp[node][0 or 1]
    private List<List<Integer>> graph;
    private int[] weight;

    public int maxIndependentSet(int n, int[][] edges, int[] weight) {
        this.weight = weight;

        graph = new ArrayList<>();
        for (int i = 0; i < n; i++) graph.add(new ArrayList<>());

        for (int[] e : edges) {
            graph.get(e[0]).add(e[1]);
            graph.get(e[1]).add(e[0]);
        }

        dp = new int[n][2];  // [not_selected, selected]

        dfs(0, -1);
        return Math.max(dp[0][0], dp[0][1]);
    }

    private void dfs(int node, int parent) {
        dp[node][1] = weight[node]; // selecting node

        for (int child : graph.get(node)) {
            if (child == parent) continue;

            dfs(child, node);

            dp[node][0] += Math.max(dp[child][0], dp[child][1]); // skip node
            dp[node][1] += dp[child][0]; // must skip child if taking node
        }
    }
}
```

### Example: Tree Diameter

**Problem**: Find the longest path between any two nodes.

```java
class Solution {
  private int[] maxDepth;
  private int diameter;
  private List<List<Integer>> graph;

  public int treeDiameter(int[][] edges) {
      int n = edges.length + 1;
      graph = new ArrayList<>();
      for (int i = 0; i < n; i++) graph.add(new ArrayList<>());

      // Build adjacency list
      for (int[] e : edges) {
          graph.get(e[0]).add(e[1]);
          graph.get(e[1]).add(e[0]);
      }

      maxDepth = new int[n];
      diameter = 0;

      dfs(0, -1);
      return diameter;
  }

  private void dfs(int node, int parent) {
      int first = 0, second = 0;

      for (int child : graph.get(node)) {
          if (child == parent) continue;

          dfs(child, node);
          int d = maxDepth[child] + 1;

          if (d > first) {
              second = first;
              first = d;
          } else if (d > second) {
              second = d;
          }
      }

      maxDepth[node] = first;
      diameter = Math.max(diameter, first + second);
  }
}
```

### Example: Counting Paths Through Each Node (Rerooting DP)

When you need dp for **every node as root**, not just one root. Reroot in O(N) instead of running DFS N times.

```
Phase 1: Root at node 0, compute dp_down[node] (standard tree DP)
Phase 2: For each node, compute dp_up[node] (contribution from parent's side)
         dp_up[child] = combine(dp_up[node], dp_down[siblings])
Phase 3: answer[node] = combine(dp_down[node], dp_up[node])
```

This is called **rerooting technique** and avoids O(N^2) recomputation.

---

## 11. Bitmask DP

### Pattern

When you have a **small set** (N <= 20) and need to track which elements are used. Represent the set as a bitmask.

```
State:  dp[mask] = answer when the elements in `mask` have been used/visited
        mask is an integer where bit i = 1 means element i is included

Transition:
  dp[mask | (1 << j)] = f(dp[mask], j)  for each unused j
```

### Example: Traveling Salesman Problem (TSP)

**Problem**: Visit all N cities exactly once and return to start. Minimize total distance.

```
State:  dp[mask][i] = min cost to visit all cities in `mask`,    ending at city i

Transition:
  dp[mask | (1<<j)][j] = min(dp[mask][i] + dist[i][j])        for each i in mask, j not in mask

Base: dp[1][0] = 0 (start at city 0, only city 0 visited)
Answer: min(dp[(1<<n)-1][i] + dist[i][0]) for all i
```

```java
public class TSPSolver {

    /**
     * Solves the Traveling Salesman Problem using DP with bitmasks.
     * Starts at city 0 and returns to city 0 at the end.
     *
     * @param dist distance matrix (square, dist[i][j] is cost from i to j)
     * @return minimal tour cost; Double.POSITIVE_INFINITY if input invalid
     */
    public static double tsp(double[][] dist) {
        int n = (dist == null) ? 0 : dist.length;
        if (n == 0) return Double.POSITIVE_INFINITY;
        for (double[] row : dist) {
            if (row == null || row.length != n) return Double.POSITIVE_INFINITY;
        }

        int N = 1 << n;
        double INF = Double.POSITIVE_INFINITY;

        double[][] dp = new double[N][n];
        for (int mask = 0; mask < N; mask++) {
            for (int i = 0; i < n; i++) {
                dp[mask][i] = INF;
            }
        }

        // Start at city 0 with only city 0 visited
        dp[1][0] = 0.0;

        for (int mask = 1; mask < N; mask++) {
            for (int i = 0; i < n; i++) {
                if (dp[mask][i] == INF) continue;
                if ((mask & (1 << i)) == 0) continue; // i must be in mask

                for (int j = 0; j < n; j++) {  if ((mask & (1 << j)) != 0) continue; // already visited j
                    int newMask = mask | (1 << j);  double cand = dp[mask][i] + dist[i][j];  if (cand < dp[newMask][j]) {      dp[newMask][j] = cand;  }
                }
            }
        }

        int full = (1 << n) - 1;
        double ans = INF;
        for (int i = 0; i < n; i++) {
            double tour = dp[full][i] + dist[i][0]; // return to start
            if (tour < ans) ans = tour;
        }
        return ans;
    }

    // Optional: simple test
    public static void main(String[] args) {
        double[][] dist = {
            {0, 10, 15, 20},
            {10, 0, 35, 25},
            {15, 35, 0, 30},
            {20, 25, 30, 0}
        };
        System.out.println(tsp(dist)); // expected minimal tour cost
    }
}

```

### Example: Assignment Problem

**Problem**: N workers, N tasks. Assign each worker exactly one task to minimize total cost.

```java
public class MinAssignmentDP {
  public int minAssignment(int[][] cost) {
      int n = cost.length;
      int INF = Integer.MAX_VALUE / 4;

      int size = 1 << n;
      int[] dp = new int[size];

      // initialize all to INF
      for (int i = 0; i < size; i++) dp[i] = INF;
      dp[0] = 0;

      for (int mask = 0; mask < size; mask++) {

          // count how many bits are ON → which worker to assign next
          int worker = Integer.bitCount(mask);
          if (worker >= n) continue;

          for (int task = 0; task < n; task++) {

              // if task already used in mask, skip
              if ((mask & (1 << task)) != 0) continue;

              public class MinAssignmentDP {

  public int minAssignment(int[][] cost) {
      int n = cost.length;
      int INF = Integer.MAX_VALUE / 4;

      int size = 1 << n;
      int[] dp = new int[size];

      // initialize all to INF
      for (int i = 0; i < size; i++) dp[i] = INF;
      dp[0] = 0;

      for (int mask = 0; mask < size; mask++) {

          // count how many bits are ON → which worker to assign next
          int worker = Integer.bitCount(mask);
          if (worker >= n) continue;

          for (int task = 0; task < n; task++) {

              // if task already used in mask, skip
              if ((mask & (1 << task)) != 0) continue;                
              int newMask = mask | (1 << task);
              dp[newMask] = Math.min(dp[newMask], dp[mask] + cost[worker][task]);
          }
      }
      return dp[size - 1];
  }
}

```

### Bitmask Tricks

```java
# Check if bit i is set
(mask & (1 << i)) != 0

# Set bit i
mask | (1 << i)

# Clear bit i
mask & ~(1 << i)

# Iterate over all subsets of mask
int sub = mask;
while (sub > 0) {
    // process sub
    sub = (sub - 1) & mask;
}

# Count set bits
Integer.bitCount(mask)
```

### Complexity

Time: O(2^N * N) or O(2^N * N^2), Space: O(2^N * N)

Only feasible for N <= ~20.

---

## 12. Digit DP

### Pattern

Count numbers in range [L, R] with some digit property. Use the trick: `count(R) - count(L-1)`.

```
State:  dp[pos][tight][...extra state...]

pos:    current digit position (left to right)
tight:  are we still constrained by the upper bound?
extra:  problem-specific (digit sum, last digit, etc.)
```
### Digit DP Template

```java
long digitDP(long N) {
    // Convert N into digit array
    char[] s = Long.toString(N).toCharArray();
    int n = s.length;
    int[] digits = new int[n];
    for (int i = 0; i < n; i++) digits[i] = s[i] - '0';

    // Memo: pos, tight, state → long
    // Here "state" is just an int. If you need more, pack it into an int.
    long[][][] memo = new long[n][2][MAX_STATE];
    boolean[][][] seen = new boolean[n][2][MAX_STATE];

    // DFS recursion
    return solve(0, 1, initialState());
}
```

### And the recursive function:

```java
long solve(int pos, int tight, int state) {
    if (pos == digits.length) {
        return baseCase(state);
    }

    if (tight == 0 && seen[pos][tight][state]) {
        return memo[pos][tight][state];
    }

    int limit = (tight == 1) ? digits[pos] : 9;
    long ans = 0;

    for (int d = 0; d <= limit; d++) {
        int newState = transition(state, d);
        int newTight = (tight == 1 && d == limit) ? 1 : 0;
        ans += solve(pos + 1, newTight, newState);
    }

    if (tight == 0) {
        seen[pos][tight][state] = true;
        memo[pos][tight][state] = ans;
    }

    return ans;
}
```

***

# 🧩 **You must implement three tiny functions:**

```java
int initialState() {
    return 0; // or whatever your DP state starts as
}

int transition(int state, int digit) {
    // compute new state from old + digit
    return state; // modify as needed
}

long baseCase(int state) {
    // return what you want when all digits are processed
    return 1; // or 0, or something else
}
```


### Common Digit DP Problems

| Problem | Extra state |
|---------|------------|
| Count numbers with digit sum S | remaining_sum |
| Count numbers with no repeated digits | used_digits (bitmask) |

---

## 13. Probability / Expected Value DP

### Pattern

```
State:  dp[state] = probability of reaching state, OR
        dp[state] = expected number of steps from state to goal

For expected value (working backwards from goal):
  dp[goal] = 0
  dp[state] = 1 + sum(p_transition * dp[next_state])
```

### Example: Expected Dice Rolls to Reach N

**Problem**: Roll a 6-sided die repeatedly. What's the expected number of rolls to reach sum >= N?

```java
public class ExpectedRolls {
    public double expectedRolls(int n) {
        // dp[i] = expected rolls to reach sum >= n starting from sum i
        double[] dp = new double[n + 7];  // padding for safe indexing

        // Fill dp backwards
        for (int i = n - 1; i >= 0; i--) {
            dp[i] = 1.0;  // one roll for sure

            double sum = 0.0;
            for (int face = 1; face <= 6; face++) {
                int next = i + face;
                if (next > n) next = n;    // same as Python: dp[min(...)]
                sum += dp[next];
            }

            dp[i] += sum / 6.0;
        }
        return dp[0];
    }
}
```

---

## 14. DP on DAGs

### Pattern

Any DP where dependencies form a Directed Acyclic Graph. Process nodes in **topological order**.

```
For each node u in topological order:
    for each edge u -> v:
        dp[v] = combine(dp[v], dp[u] + edge_weight)
```

### Example: Longest Path in DAG

```java
import java.util.*;

public class LongestPathDAG {

    // adj: adjacency list where each u maps to List<int[]> of {v, w}
    public int longestPathDAG(List<List<int[]>> adj, int n) {

        // Step 1: compute in-degree
        int[] inDeg = new int[n];
        for (int u = 0; u < n; u++) {
            for (int[] edge : adj.get(u)) {
                int v = edge[0];
                inDeg[v]++;
            }
        }

        // Step 2: Kahn's algorithm for topological ordering
        Queue<Integer> queue = new ArrayDeque<>();
        int[] dp = new int[n]; // dp[u] = longest path ending at u

        for (int i = 0; i < n; i++) {
            if (inDeg[i] == 0) {
                queue.add(i);
            }
        }

        // Step 3: Process nodes in topological order
        while (!queue.isEmpty()) {
            int u = queue.poll();

            for (int[] edge : adj.get(u)) {
                int v = edge[0];
                int w = edge[1];

                dp[v] = Math.max(dp[v], dp[u] + w);

                inDeg[v]--;
                if (inDeg[v] == 0) {  queue.add(v);
                }
            }
        }

        // Step 4: longest path over all vertices
        int best = 0;
        for (int val : dp) best = Math.max(best, val);
        return best;
    }
}
```

### Example: Number of Paths in DAG

```java
import java.util.*;

public class CountPathsDAG {

    public long countPathsDAG(List<List<Integer>> adj, int n, int src, int dst) {

        // Step 1: compute in-degree of each vertex
        int[] inDeg = new int[n];
        for (int u = 0; u < n; u++) {
            for (int v : adj.get(u)) {
                inDeg[v]++;
            }
        }

        // Step 2: initialize queue with all zero‑in‑degree nodes (Kahn’s algorithm)
        Queue<Integer> queue = new ArrayDeque<>();
        long[] dp = new long[n];
        dp[src] = 1;    // exactly 1 path from src to itself at start

        for (int i = 0; i < n; i++) {
            if (inDeg[i] == 0) {
                queue.add(i);
            }
        }

        // Step 3: Topological BFS
        while (!queue.isEmpty()) {
            int u = queue.poll();

            for (int v : adj.get(u)) {

                // accumulate number of paths reaching v
                dp[v] += dp[u];

                // update in-degree
                inDeg[v]--;
                if (inDeg[v] == 0) {  queue.add(v);
                }
            }
        }

        return dp[dst];
    }
}
```

---

## 15. DP Optimizations

When the basic DP is too slow, apply these optimizations.

### 15.0 Space Optimization Principles

The most common DP optimization — reducing memory without changing time complexity. This is a **frequent interview follow-up**: "Can you do it in less space?"

#### The Core Rule

> **If `dp[i]` only depends on a bounded window of previous states, you only need to keep that window in memory.**

#### Decision Framework

| Dependency pattern | Reduction | Technique |
|-------------------|-----------|-----------|
| `dp[i]` depends only on `dp[i-1]` | O(N) → O(1) | Two variables |
| `dp[i]` depends on `dp[i-1]` and `dp[i-2]` | O(N) → O(1) | Three variables |
| `dp[i][j]` depends on row `i-1` only | O(MN) → O(N) | Two rows or single row |
| `dp[i][j]` depends on `dp[i-1][j-1]`, `dp[i-1][j]`, `dp[i][j-1]` | O(MN) → O(N) | Single row + saved diagonal |
| `dp[i][j]` depends on any `dp[i][k]`, `dp[k][j]` | **Cannot reduce** | Need full table (interval DP) |
| `dp[mask]` over subsets | **Cannot reduce** | Need full 2^N table |

#### The Reverse-Iteration Trick (Critical for Knapsack)

When flattening 2D → 1D, the **iteration direction** determines whether old or new values are read:

```
Forward iteration (left to right):
  dp[w - weight[i]] reads the ALREADY-UPDATED value from THIS iteration
  → item i can be reused → UNBOUNDED knapsack

Reverse iteration (right to left):
  dp[w - weight[i]] reads the NOT-YET-UPDATED value from PREVIOUS iteration
  → item i used at most once → 0/1 knapsack

Mnemonic: "Reverse = Restrict (to one use)"
```

#### The Diagonal-Save Trick (for LCS / Edit Distance)

When a single-row DP depends on `dp[i-1][j-1]` (the diagonal), that value gets overwritten as you process column `j`. Save it before overwriting:

```java
prev_diag = 0
for j in range(1, n + 1):
    temp = dp[j]           # save dp[i-1][j] before overwrite
    dp[j] = f(dp[j],       # dp[i-1][j]  (old value, still intact)
              dp[j-1],      # dp[i][j-1]  (already updated this row)
              prev_diag)    # dp[i-1][j-1] (saved from last iteration)
    prev_diag = temp        # carry forward for next column
```

#### The Simultaneous-Update Rule (State Machine DP)

When multiple states depend on each other at step `i-1`, update them **simultaneously** — otherwise you'll accidentally read a partially-updated current-step value:

```java
# WRONG: hold uses the just-updated rest value
rest = max(rest, cool)
hold = max(hold, rest - prices[i])  # bug: rest is already step i!

# CORRECT: compute all new values, then assign
new_rest = max(rest, cool)
new_hold = max(hold, rest - prices[i])
new_cool = hold + prices[i]
rest, hold, cool = new_rest, new_hold, new_cool

# ALSO CORRECT: Python tuple unpacking (idiomatic)
rest, hold, cool = max(rest, cool), max(hold, rest - prices[i]), hold + prices[i]
```

#### When Space Optimization Isn't Possible

- **Interval DP**: `dp[i][j]` depends on arbitrary sub-intervals — need full O(N^2) table
- **Bitmask DP**: `dp[mask]` over all 2^N subsets — need full table
- **When you need to reconstruct the solution**: Space optimization preserves the final answer but discards the path. To reconstruct, either keep the full table or use Hirschberg's divide-and-conquer trick (works for LCS in O(N) space)
- **Tree DP with rerooting**: Needs full dp_down[] and dp_up[] arrays

#### Space Optimization Summary by Pattern

| Pattern | Original space | Optimized space | How |
|---------|---------------|----------------|-----|
| Fibonacci / Linear (window) | O(N) | O(1) | Rolling variables |
| Grid DP | O(MN) | O(N) | Process row by row |
| 0/1 Knapsack | O(NW) | O(W) | 1D array, **reverse** iteration |
| Unbounded Knapsack | O(NW) | O(W) | 1D array, **forward** iteration |
| LCS / Edit Distance | O(MN) | O(min(M,N)) | Single row + diagonal save |
| State Machine DP | O(N × S) | O(S) | S variables, simultaneous update |
| Interval DP | O(N^2) | O(N^2) | Cannot reduce |
| Bitmask DP | O(2^N) | O(2^N) | Cannot reduce |

---

## 16. Pattern Recognition Cheat Sheet

### By Problem Type

| You see... | Think... | Pattern |
|------------|----------|---------|
| "Count ways" with choices at each step | Linear DP or Knapsack | Sec 3, 5 |
| Grid traversal, paths | Grid DP | Sec 4 |
| "Take or skip" with weight/capacity | Knapsack | Sec 5 |
| "Longest increasing/decreasing" | LIS | Sec 6 |
| Two strings, matching | LCS / Edit Distance | Sec 7 |
| Merge/split intervals optimally | Interval DP | Sec 8 |
| Buy/sell, hold/not-hold states | State Machine DP | Sec 9 |
| Tree + subtree values | Tree DP | Sec 10 |
| Small N (<=20), subset tracking | Bitmask DP | Sec 11 |
| "How many numbers in [L,R] with property" | Digit DP | Sec 12 |
| Random events, "expected number of" | Probability DP | Sec 13 |
| Graph with dependencies | DP on DAG | Sec 14 |

### By Constraint Size

| N range | Likely approach |
|---------|----------------|
| N <= 20 | Bitmask DP O(2^N * N) |
| N <= 500 | Interval DP O(N^3) |
| N <= 5000 | O(N^2) DP (LCS, LIS naive) |
| N <= 10^5 | O(N log N) DP (LIS optimized, HLD) |
| N <= 10^6 | O(N) DP (linear, Kadane's) |

### Quick Complexity Reference

| Pattern | Time | Space |
|---------|------|-------|
| Linear DP | O(N) or O(NS) | O(N) or O(1) |
| Grid DP | O(MN) | O(MN) or O(N) |
| 0/1 Knapsack | O(NW) | O(W) |
| LIS | O(N log N) | O(N) |
| LCS | O(MN) | O(MN) or O(N) |
| Interval DP | O(N^3) or O(N^2) | O(N^2) |
| Tree DP | O(N) | O(N) |
| Bitmask DP | O(2^N * N) | O(2^N) |
| Digit DP | O(D * S * 10) | O(D * S) |
