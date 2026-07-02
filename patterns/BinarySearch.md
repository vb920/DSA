# Binary Search Patterns — Comprehensive Guide

Binary search is not just "find a number in a sorted array." It's a general technique for narrowing down a search space by half at each step. Once you see it as **searching for a boundary** rather than searching for a value, an enormous class of problems opens up.

---

## Quick Navigation: "I need to..."

| I need to... | Technique | Section |
|--------------|-----------|---------|
| Find exact value in sorted array | Classic binary search | [1](#1-classic-binary-search) |
| Find **first** occurrence / insertion point | Lower bound | [2](#2-lower-bound-and-upper-bound) |
| Find **last** occurrence | Upper bound | [2](#2-lower-bound-and-upper-bound) |
| Find min/max value satisfying a condition | Binary search on answer | [3](#3-binary-search-on-answer) |
| Search on **real numbers** | Floating-point binary search | [4](#4-binary-search-on-real-numbers) |
| Find **peak** in mountain array | Binary search on bitonic | [5](#5-peak-finding) |
| Search in **rotated** sorted array | Modified binary search | [6](#6-rotated-sorted-array) |
| Find Kth smallest / **median** | Binary search on value | [7](#7-kth-smallest-and-median) |
| Minimize **maximum** or maximize **minimum** | Binary search on answer | [3](#3-binary-search-on-answer) |
| Optimize on **unimodal** function | Ternary search | [8](#8-ternary-search) |
| Search in **2D sorted** matrix | Row/column binary search | [9](#9-binary-search-on-2d) |

---

## Table of Contents

1. [Classic Binary Search](#1-classic-binary-search)
2. [Lower Bound and Upper Bound](#2-lower-bound-and-upper-bound)
3. [Binary Search on Answer](#3-binary-search-on-answer)
4. [Binary Search on Real Numbers](#4-binary-search-on-real-numbers)
5. [Peak Finding](#5-peak-finding)
6. [Rotated Sorted Array](#6-rotated-sorted-array)
7. [Kth Smallest and Median](#7-kth-smallest-and-median)
8. [Ternary Search](#8-ternary-search)
9. [Binary Search on 2D](#9-binary-search-on-2d)
11. [Common Patterns Collection](#11-common-patterns-collection)
12. [Pattern Recognition Cheat Sheet](#12-pattern-recognition-cheat-sheet)

---

## 1. Classic Binary Search

### The Idea

Repeatedly cut the search space in half. Requires a **sorted** or **monotonic** property.

```
Find 7 in [1, 3, 5, 7, 9, 11, 13]

Step 1: lo=0, hi=6, mid=3, arr[3]=7  -> found!

Find 6:
Step 1: lo=0, hi=6, mid=3, arr[3]=7  -> 6 < 7, search left
Step 2: lo=0, hi=2, mid=1, arr[1]=3  -> 6 > 3, search right
Step 3: lo=2, hi=2, mid=2, arr[2]=5  -> 6 > 5, search right
Step 4: lo=3, hi=2  -> lo > hi, not found
```

### Implementation

```java
int binary_search(int[] arr, int target) {
    int lo = 0, hi = arr.length - 1;

    while (lo <= hi) {
        int mid = lo + (hi - lo) / 2;  // avoids overflow (matters in C++/Java)

        if (arr[mid] == target) {
            return mid;
        } else if (arr[mid] < target) {
            lo = mid + 1;
        } else {
            hi = mid - 1;
        }
    }

    return -1;  // not found
}
```

### The #1 Source of Bugs

Off-by-one errors. The key rules:

| Choice | When |
|--------|------|
| `lo <= hi` | Searching for exact match; search space can be a single element |
| `lo < hi` | Searching for a boundary; loop ends with `lo == hi` = answer |
| `mid = lo + (hi - lo) // 2` | Always use this instead of `(lo + hi) // 2` to prevent overflow |
| `lo = mid + 1` | Exclude mid from left search (mid is too small) |
| `hi = mid - 1` | Exclude mid from right search (mid is too large) |
| `hi = mid` | Include mid (it might be the answer) --- used with `lo < hi` |

---

## 2. Lower Bound and Upper Bound

The **most useful** binary search variants. Instead of finding an exact match, find a **boundary**.

### Mental Model

Think of the array as having a property that flips from False to True (or vice versa). Binary search finds where the flip happens.

```
arr:    [1, 3, 5, 5, 5, 7, 9]
target: 5

"Is arr[i] >= 5?"
         F  F  T  T  T  T  T
              ^
              lower_bound = 2 (first True)

"Is arr[i] > 5?"
         F  F  F  F  F  T  T
                       ^
                       upper_bound = 5 (first True)
```

### Lower Bound (First >= target)

Returns the **leftmost** position where target could be inserted to maintain sorted order. Also: first occurrence of target.

```java
int lower_bound(int[] arr, int target) {
    int lo = 0, hi = arr.length;  // note: hi = len(arr), not len(arr)-1

    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;
        if (arr[mid] < target) {
            lo = mid + 1;    // mid is too small, exclude it
        } else {
            hi = mid;        // mid might be the answer, keep it
        }
    }

    return lo;  // first index where arr[index] >= target
}
```

### Upper Bound (First > target)

Returns the position **after** the last occurrence of target.

```java
int upper_bound(int[] arr, int target) {
    int lo = 0, hi = arr.length;

    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;
        if (arr[mid] <= target) {
            lo = mid + 1;    // mid is <= target, exclude it
        } else {
            hi = mid;        // mid is > target, might be the answer
        }
    }

    return lo;  // first index where arr[index] > target
}
```

### Derived Queries

| Query | Implementation |
|-------|---------------|
| First occurrence of x | `lb = lower_bound(arr, x)` then check `arr[lb] == x` |
| Last occurrence of x | `upper_bound(arr, x) - 1` then check value |
| Count of x | `upper_bound(arr, x) - lower_bound(arr, x)` |
| First element > x | `upper_bound(arr, x)` |
| Last element < x | `lower_bound(arr, x) - 1` |
| First element >= x | `lower_bound(arr, x)` |
| Last element <= x | `upper_bound(arr, x) - 1` |
| Element closest to x | Compare `arr[lb]` and `arr[lb-1]` |

### Trace: First and Last Occurrence

```
arr = [1, 2, 2, 2, 3, 4], target = 2

lower_bound(arr, 2):
  lo=0, hi=6
  mid=3, arr[3]=2 >= 2 -> hi=3
  mid=1, arr[1]=2 >= 2 -> hi=1
  mid=0, arr[0]=1 < 2  -> lo=1
  lo=hi=1 -> return 1  (first occurrence)

upper_bound(arr, 2):
  lo=0, hi=6
  mid=3, arr[3]=2 <= 2 -> lo=4
  mid=5, arr[5]=4 > 2  -> hi=5
  mid=4, arr[4]=3 > 2  -> hi=4
  lo=hi=4 -> return 4  (first position AFTER last 2)

Last occurrence: upper_bound - 1 = 3
Count of 2s: 4 - 1 = 3
```

---

## 3. Binary Search on Answer

The most powerful pattern. When you can't search in an array but can **check if an answer is feasible**.

### The Framework

```
"Find the minimum X such that condition(X) is True"

condition(X):
  ... too small ...  F F F F F T T T T T  ... large enough ...
                                ^
                          answer is here (first True)

Binary search finds this boundary.
```

```java
int binary_search_on_answer(int lo, int hi, int [] condition) {
    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;
        if (condition.test(mid)) {
            hi = mid;        // mid works, try smaller
        } else {
            lo = mid + 1;    // mid doesn't work, need bigger
        }
    }

    return lo;  // minimum value where condition is True
}
```

### Example 1: Minimum Days to Make M Bouquets

**Problem**: N flowers bloom on given days. Need M bouquets of K adjacent flowers. What's the minimum day?

```java
public class Solution {
    public int min_days_bouquets(int[] bloom_day, int m, int k) {
        int n = bloom_day.length;
        if (m * k > n) {
            return -1;
        }

        int lo = Integer.MAX_VALUE, hi = Integer.MIN_VALUE;
        for (int x : bloom_day) {
            lo = Math.min(lo, x);
            hi = Math.max(hi, x);
        }

        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;

            if (can_make(bloom_day, n, m, k, mid)) {
                hi = mid;      // mid works
            } else {
                lo = mid + 1;  // mid doesn't work
            }
        }

        return lo;
    }

    // direct equivalent of Python's inner function can_make()
    private boolean can_make(int[] bloom_day, int n, int m, int k, int day) {
        int bouquets = 0;
        int consecutive = 0;

        for (int i = 0; i < n; i++) {
            if (bloom_day[i] <= day) {
                consecutive++;
                if (consecutive == k) {
                    bouquets++;
                    consecutive = 0;
                }
            } else {
                consecutive = 0;
            }
        }

        return bouquets >= m;
    }
}
```

### Example 2: Minimize Maximum (Split Array)

**Problem**: Split array into K subarrays to minimize the maximum subarray sum.

```
arr = [7, 2, 5, 10, 8], k = 2

If max_sum = 18: [7,2,5] and [10,8] -> sums 14, 18 -> works (2 splits)
If max_sum = 17: can't split into <= 2 parts with each <= 17?
  [7,2,5] and [10,8=18] > 17 -> need 3 parts -> doesn't work
  Actually [7,2,5,10=24] > 17 too... let's trace properly
  [7,2,5]=14 ok, [10]=10 ok, [8]=8 ok -> 3 parts > 2 -> doesn't work

If max_sum = 18: [7,2,5]=14, [10,8]=18 -> 2 parts -> works!
```

```java
public class Solution {
    public int split_array(int[] nums, int k) {
        int lo = Integer.MIN_VALUE;
        int hi = 0;

        // lo = max(nums), hi = sum(nums)
        for (int x : nums) {
            lo = Math.max(lo, x);
            hi += x;
        }

        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (can_split(nums, k, mid)) {
                hi = mid;        // this works, try smaller
            } else {
                lo = mid + 1;    // need larger max_sum
            }
        }
        return lo;
    }

    // Can we split into <= k parts, each with sum <= max_sum?
    private boolean can_split(int[] nums, int k, int max_sum) {
        int parts = 1;
        int current = 0;

        for (int num : nums) {
            if (current + num > max_sum) {
                parts += 1;
                current = num;
                if (parts > k) {
                    return false;
                }
            } else {
                current += num;
            }
        }
        return true;
    }
}
```

### Example 3: Maximize Minimum (Aggressive Cows)

**Problem**: Place K cows in N stalls to maximize the minimum distance between any two cows.

```java
public class Solution {
    public int aggressive_cows(int[] stalls, int k) {
        Arrays.sort(stalls);

        int lo = 1, hi = stalls[stalls.length - 1] - stalls[0];
        while (lo < hi) {
            int mid = lo + (hi - lo + 1) / 2;  // round UP to avoid infinite loop
            if (can_place(stalls, k, mid)) {
                lo = mid;         // this works, try bigger (maximize!)
            } else {
                hi = mid - 1;     // too big, need smaller
            }
        }
        return lo;
    }

    // Can we place k cows with at least min_dist between each?
    private boolean can_place(int[] stalls, int k, int min_dist) {
        int count = 1;
        int last = stalls[0];

        for (int i = 1; i < stalls.length; i++) {
            if (stalls[i] - last >= min_dist) {
                count += 1;
                last = stalls[i];
                if (count >= k) {
                    return true;
                }
            }
        }
        return false;
    }
}
```

**Note the difference**: When **maximizing**, we set `lo = mid` (keep current if it works). To avoid infinite loops, use `mid = lo + (hi - lo + 1) // 2` (round up).

### Minimize vs Maximize Template

```java
# MINIMIZE: find smallest X where condition is True
# F F F F T T T T -> find first T
while (lo < hi) {
    int mid = lo + (hi - lo) / 2;
    if (condition(mid)) {
        hi = mid;
    } else {
        lo = mid + 1;
    }
}
# MAXIMIZE: find largest X where condition is True
# T T T T F F F F -> find last T
while (lo < hi) {
    int mid = lo + (hi - lo + 1) / 2;  // round UP!
    if (condition(mid)) {
        lo = mid;
    } else {
        hi = mid - 1;
    }
}
```

### Common "Binary Search on Answer" Problems

| Problem | What to binary search | Condition |
|---------|----------------------|-----------|
| Split array, minimize max sum | max subarray sum | Can split into <= K parts? |
| Koko eating bananas | eating speed | Can finish in H hours? |
| Ship packages in D days | ship capacity | Can ship all in D days? |
| Aggressive cows | min distance | Can place K cows? |
| Painter's partition | max section length | Can paint with K painters? |
| Find median of two sorted arrays | partition point | Left half <= right half? |
| Minimum time to complete tasks | time | Can all tasks finish? |
| Allocate books to students | max pages | Can distribute to K students? |

---

## 4. Binary Search on Real Numbers

When the answer is a real number, use a fixed number of iterations instead of `lo < hi` (which may not converge for floats).

### Template

```java
double binary_search_float(double lo, double hi, int iterations) {
    for (int i = 0; i < iterations; i++) {
        double mid = (lo + hi) / 2;
        if (condition(mid)) {
            hi = mid;
        } else {
            lo = mid;
        }
    }
    return lo;   // or hi, or (lo + hi) / 2
}
```

100 iterations give precision of about `(hi - lo) / 2^100`, which is far beyond `float64` precision.

### Example: Square Root

```java
double sqrt(double x, double eps) {
    double lo = 0.0, hi = Math.max(1.0, x);

    for (int i = 0; i < 100; i++) {
        double mid = (lo + hi) / 2.0;

        if (mid * mid > x) {
            hi = mid;
        } else {
            lo = mid;
        }
    }

    return lo;
}
```

### Example: Rope Cutting

**Problem**: Given N ropes of various lengths, cut exactly K pieces of equal length. Maximize the length of each piece.

```java
public class Solution {
    public double max_rope_length(int[] ropes, int k) {
        // edge case: if all ropes are zero, answer is zero
        int max = 0;
        for (int r : ropes){
          max = Math.max(max, r);
        }
        if (max == 0) return 0.0;

        double lo = 0.0, hi = max;

        for (int i = 0; i < 100; i++) {
            double mid = (lo + hi) / 2.0;

            // how many pieces of length mid can we cut?
            int pieces = 0;
            if (mid > 0) {
                for (int r : ropes) {
                    pieces += (int) (r / mid);
                    // small micro-guard: avoid overflow in extreme cases
                    if (pieces >= k && i < 99) break;
                }
            }

            if (pieces >= k) {
                lo = mid;   // can cut k pieces, try longer
            } else {
                hi = mid;   // too few pieces, try shorter
            }
        }

        return lo;
    }
}
```

### Why Fixed Iterations?

Floating-point `lo < hi` may never terminate due to precision issues. With 100 iterations, the interval shrinks by a factor of 2^100 --- more than enough for any practical precision requirement.

---

## 5. Peak Finding

### Peak Element in Array

**Problem**: Find any local maximum (element greater than both neighbors).

```
arr: [1, 3, 5, 4, 2]
          ^  ^
         rising  falling -> peak at index 2 (value 5)
```

```java
int find_peak(int[] arr) {
    int lo = 0, hi = arr.length - 1;

    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;
        if (arr[mid] < arr[mid + 1]) {
            lo = mid + 1;    // peak is to the right (still rising)
        } else {
            hi = mid;        // peak is here or to the left (falling)
        }
    }

    return lo;  // lo == hi == peak index
}
```

**Why it works**: If `arr[mid] < arr[mid+1]`, the slope is going up, so there must be a peak to the right (even if the array goes up then wraps around, the right boundary or the end of the array guarantees a peak). If `arr[mid] >= arr[mid+1]`, the slope is going down, so there's a peak at mid or to the left.

### Mountain Array (Bitonic)

Find peak in a strictly increasing then strictly decreasing array. Same algorithm.

```java
int peak_of_mountain(int[] arr) {
    int lo = 0, hi = arr.length - 1;

    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;
        if (arr[mid] < arr[mid + 1]) {
            lo = mid + 1;
        } else {
            hi = mid;
        }
    }

    return lo;
}
```

### Search in Mountain Array

First find the peak. Then binary search both halves.

```java
public class Solution {
    public int search_mountain(int[] arr, int target) {
        // find peak
        int lo = 0, hi = arr.length - 1;
        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (arr[mid] < arr[mid + 1]) {
                lo = mid + 1;
            } else {
                hi = mid;
            }
        }
        int peak = lo;

        // search ascending half [0, peak]
        int result = binary_search(arr, target, 0, peak, true);
        if (result != -1) {
            return result;
        }

        // search descending half [peak+1, n-1]
        return binary_search(arr, target, peak + 1, arr.length - 1, false);
    }

    int binary_search(int[] arr, int target, int lo, int hi, boolean ascending) {
        while (lo <= hi) {
            int mid = lo + (hi - lo) / 2;
            if (arr[mid] == target) {
                return mid;
            }
            if (ascending) {
                if (arr[mid] < target) {
                    lo = mid + 1;
                } else {
                    hi = mid - 1;
                }
            } else {
                if (arr[mid] > target) {
                    lo = mid + 1;
                } else {
                    hi = mid - 1;
                }
            }
        }
        return -1;
    }
}
```

---

## 6. Rotated Sorted Array

### The Structure

```
Original:  [1, 2, 3, 4, 5, 6, 7]
Rotated:   [4, 5, 6, 7, 1, 2, 3]
                      ^
                   rotation point (minimum)
```

### Find Minimum (Rotation Point)

```java
int find_min_rotated(int[] arr) {
    int lo = 0, hi = arr.length - 1;
    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;
        if (arr[mid] > arr[hi]) {
            lo = mid + 1;    // min is to the right
        } else {
            hi = mid;        // min is here or to the left
        }
    }

    return lo;  // index of minimum element
}
```

**Why compare with `arr[hi]`?**
- If `arr[mid] > arr[hi]`: the rotation point is between mid+1 and hi
- If `arr[mid] <= arr[hi]`: the right half is sorted, rotation point is at mid or left

### Search in Rotated Array (No Duplicates)

```java
int search_rotated(int[] arr, int target) {
    int lo = 0, hi = arr.length - 1;
    while (lo <= hi) {
        int mid = lo + (hi - lo) / 2;
        if (arr[mid] == target) {
            return mid;
        }

        // determine which half is sorted
        if (arr[lo] <= arr[mid]) {
            // left half is sorted
            if (arr[lo] <= target && target < arr[mid]) {
                hi = mid - 1;
            } else {
                lo = mid + 1;
            }
        } else {
            // right half is sorted
            if (arr[mid] < target && target <= arr[hi]) {
                lo = mid + 1;
            } else {
                hi = mid - 1;
            }
        }
    }

    return -1;
}
``
```

### Search in Rotated Array (With Duplicates)

Duplicates break the `arr[lo] <= arr[mid]` check. When `arr[lo] == arr[mid] == arr[hi]`, we can't tell which side is sorted. Shrink both sides.

```java
boolean search_rotated_dups(int[] arr, int target) {
    int lo = 0, hi = arr.length - 1;
    while (lo <= hi) {
        int mid = lo + (hi - lo) / 2;
        if (arr[mid] == target) {
            return true;
        }

        // can't determine sorted side
        if (arr[lo] == arr[mid] && arr[mid] == arr[hi]) {
            lo += 1;
            hi -= 1;
        } else if (arr[lo] <= arr[mid]) {  // left half is sorted
            if (arr[lo] <= target && target < arr[mid]) {
                hi = mid - 1;
            } else {
                lo = mid + 1;
            }
        } else {  // right half is sorted
            if (arr[mid] < target && target <= arr[hi]) {
                lo = mid + 1;
            } else {
                hi = mid - 1;
            }
        }
    }

    return false;
}
```

Worst case with duplicates: O(N) (e.g., `[1,1,1,1,1,1,2,1,1]`).

---

## 7. Kth Smallest and Median

### Kth Smallest in Sorted Matrix

**Problem**: N x N matrix where each row and column is sorted. Find the Kth smallest element.

```java
public class Solution {
    public int kth_smallest_matrix(int[][] matrix, int k) {
        int n = matrix.length;

        int lo = matrix[0][0], hi = matrix[n - 1][n - 1];
        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (count_less_equal(matrix, n, mid) >= k) {
                hi = mid;
            } else {
                lo = mid + 1;
            }
        }
        return lo;
    }

    // Count elements <= target using the sorted structure (start from bottom-left)
    private int count_less_equal(int[][] matrix, int n, int target) {
        int count = 0;
        int row = n - 1, col = 0;  // start bottom-left
        while (row >= 0 && col < n) {
            if (matrix[row][col] <= target) {
                count += row + 1;   // all elements above in this column
                col += 1;
            } else {
                row -= 1;
            }
        }
        return count;
    }
}
```

### Median of Two Sorted Arrays

**Problem**: Find the median of two sorted arrays in O(log(min(m,n))).

```java
public class Solution {

    public double find_median(int[] nums1, int[] nums2) {
        // ensure nums1 is shorter
        if (nums1.length > nums2.length) {
            int[] tmp = nums1;
            nums1 = nums2;
            nums2 = tmp;
        }

        int m = nums1.length, n = nums2.length;
        int half = (m + n + 1) / 2;

        int lo = 0, hi = m;
        while (lo <= hi) {
            int i = lo + (hi - lo) / 2;  // partition point in nums1
            int j = half - i;            // partition point in nums2

            // values at partition boundaries
            int left1  = (i > 0) ? nums1[i - 1] : Integer.MIN_VALUE;
            int left2  = (j > 0) ? nums2[j - 1] : Integer.MIN_VALUE;
            int right1 = (i < m) ? nums1[i]     : Integer.MAX_VALUE;
            int right2 = (j < n) ? nums2[j]     : Integer.MAX_VALUE;

            if (left1 <= right2 && left2 <= right1) {
                // correct partition
                if (((m + n) % 2) == 1) {
                    return Math.max(left1, left2);
                }
                return (Math.max(left1, left2) + Math.min(right1, right2)) / 2.0;
            } else if (left1 > right2) {
                hi = i - 1;  // too many from nums1
            } else {
                lo = i + 1;  // too few from nums
            }
        }
        return 0;
    }
```

### How It Works

```
nums1: [1, 3, | 8, 9]      i = 2 (take 2 from nums1)
nums2: [2, | 5, 6, 7, 10]   j = 3 (take 3 from nums2)

Left half:  {1, 3, 2, 5, 6}   max = 6
Right half: {8, 9, 7, 10}     min = 7

Check: left1=3 <= right2=7 ✓  and  left2=6 <= right1=8 ✓
       -> correct partition!

Wait, we need half = (4+5+1)//2 = 5 elements in left half.
i=2 from nums1, j=3 from nums2 -> 5 total ✓

Median (odd total) = max(left1, left2) = max(3, 6) = 6...
Actually let me recalculate. Sorted: [1,2,3,5,6,7,8,9,10], median = 6. ✓
```

---

## 8. Ternary Search

### When to Use

Binary search works for monotonic functions. **Ternary search** works for **unimodal** functions (one peak or one valley).

```
Unimodal (one peak):          Unimodal (one valley):
     *                              *         *
    * *                              *       *
   *   *                              *     *
  *     *                              *   *
 *       *                              * *
*         *                              *
```

### Finding Maximum of Unimodal Function

```java
// Ternary search to maximize a unimodal function f on [lo, hi]
public double ternary_search_max(double lo, double hi, int iterations) {
    for (int i = 0; i < iterations; i++) {
        double m1 = lo + (hi - lo) / 3.0;
        double m2 = hi - (hi - lo) / 3.0;

        if (f(m1) < f(m2)) {
            lo = m1;   // max is in [m1, hi]
        } else {
            hi = m2;   // max is in [lo, m2]
        }
    }
    return (lo + hi) / 2.0;
}

// Default iterations = 200 (like your Python default)
public double ternary_search_max(double lo, double hi) {
    return ternary_search_max(lo, hi, 200);
}

// Replace/override this with your target function
protected double f(double x) {
    // Example placeholder: override in subclass or edit directly
    return - (x - 3.0) * (x - 3.0); // peaked at x = 3
}

```

### Finding Minimum of Unimodal Function

```java

// Ternary search to minimize a unimodal function f on [lo, hi]
public double ternary_search_min(double lo, double hi, int iterations) {
    for (int i = 0; i < iterations; i++) {
        double m1 = lo + (hi - lo) / 3.0;
        double m2 = hi - (hi - lo) / 3.0;

        if (f(m1) < f(m2)) {
            hi = m2;    // min is in [lo, m2]
        } else {
            lo = m1;    // min is in [m1, hi]
        }
    }
    return (lo + hi) / 2.0;
}

// Default iterations = 200 (like your Python default)
public double ternary_search_min(double lo, double hi) {
    return ternary_search_min(lo, hi, 200);
}

// Replace/override this with your target function
protected double f(double x) {
    // Example placeholder: override in subclass or edit directly
    return - (x - 3.0) * (x - 3.0); // peaked at x = 3
}

```

### Integer Ternary Search

```java
public int ternary_search_int(int lo, int hi) {
    while (hi - lo > 2) {
        int m1 = lo + (hi - lo) / 3;
        int m2 = hi - (hi - lo) / 3;
        if (f(m1) < f(m2)) {
            lo = m1 + 1;
        } else {
            hi = m2 - 1;
        }
    }
    // check remaining candidates
    int best = lo;
    for (int x = lo; x <= hi; x++) {
        if (f(x) > f(best)) {
            best = x;
        }
    }
    return best;
}

```

### Ternary vs Binary Search

| | Binary Search | Ternary Search |
|--|--------------|----------------|
| Function shape | Monotonic (always increasing or decreasing) | Unimodal (one peak or valley) |
| Queries per iteration | 1 | 2 |
| Reduction per iteration | 1/2 | 1/3 |
| Convergence | ~log2(N) steps | ~log(3/2)(N) steps |
| Prefer | When you can reframe as boundary search | When function is truly unimodal |

**Tip**: Many ternary search problems can be converted to binary search by searching for the "derivative = 0" point (where the function changes from increasing to decreasing).

---

## 9. Binary Search on 2D

### Search in Row-Sorted and Column-Sorted Matrix

**Problem**: Each row is sorted left to right, each column sorted top to bottom. Find target.

```java
boolean search_2d_staircase(int[][] matrix, int target) {
    if (matrix == null || matrix.length == 0) {
        return false;
    }

    int m = matrix.length;
    int n = matrix[0].length;

    int row = 0, col = n - 1;  // top-right corner

    while (row < m && col >= 0) {
        if (matrix[row][col] == target) {
            return true;
        } else if (matrix[row][col] < target) {
            row += 1;   // need bigger, go down
        } else {
            col -= 1;   // need smaller, go left
        }
    }

    return false;
}
```

### Search in Fully Sorted Matrix

**Problem**: Rows are sorted, and first element of each row > last element of previous row. Treat as a flat sorted array.

```java
boolean search_2d_flat(int[][] matrix, int target) {
    int m = matrix.length;
    int n = matrix[0].length;

    int lo = 0, hi = m * n - 1;

    while (lo <= hi) {
        int mid = lo + (hi - lo) / 2;
        int val = matrix[mid / n][mid % n];

        if (val == target) {
            return true;
        } else if (val < target) {
            lo = mid + 1;
        } else {
            hi = mid - 1;
        }
    }

    return false;
}
```

### Count Elements Less Than X in Sorted Matrix

Used as a building block for Kth smallest (Section 7).

```java
int count_less_equal(int[][] matrix, int target) {
    int count = 0;
    int row = matrix.length - 1;
    int col = 0;

    while (row >= 0 && col < matrix[0].length) {
        if (matrix[row][col] <= target) {
            count += row + 1;
            col += 1;
        } else {
            row -= 1;
        }
    }

    return count;
}
```

---

### Mapping to Our Functions
| Our function             | Java equivalent                                                        |
| ------------------------|---------------------------------------------------------------------------------------------------- |
| `lower_bound(arr, x)`    | `lower_bound(arr, x)` (custom binary search)                                                                         |
| `upper_bound(arr, x)`    | `upper_bound(arr, x)` (custom binary search)                                                                         |
| First occurrence of x    | `int i = lower_bound(arr, x); if (i < n && arr[i] == x) i;`                                                          |
| Last occurrence of x     | `int i = upper_bound(arr, x) - 1; if (i >= 0 && arr[i] == x) i;`                                                     |
| Count of x               | `upper_bound(arr, x) - lower_bound(arr, x)`                                                                          |
| Insert maintaining order | `int pos = Collections.binarySearch(list, x); if (pos < 0) pos = -pos - 1; list.add(pos, x);` (O(N) due to shifting) |

***


## 11. Common Patterns Collection

### Find First Bad Version

```java
int first_bad_version(int n) {
    int lo = 1, hi = n;
    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;
        if (is_bad(mid)) {
            hi = mid;
        } else {
            lo = mid + 1;
        }
    }

    return lo;
}

// This simulates the is_bad API from LeetCode.
// Replace this with your actual logic.
boolean is_bad(int version) {
    return false;
}
```

### Capacity to Ship Packages

```java
public class Solution {
    public int ship_within_days(int[] weights, int days) {
        int lo = 0, hi = 0;  // lo = max(weights), hi = sum(weights)
        for (int w : weights) {
            lo = Math.max(lo, w);
            hi += w;
        }

        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (can_ship(weights, days, mid)) {
                hi = mid;
            } else {
                lo = mid + 1;
            }
        }
        return lo;
    }

    // Can we ship all weights within 'days' using capacity 'capacity' per day?
    private boolean can_ship(int[] weights, int days, int capacity) {
        int d = 1, current = 0;
        for (int w : weights) {
            if (current + w > capacity) {
                d += 1;
                current = w;
            } else {
                current += w;
            }
        }
        return d <= days;
    }
}
```

### Koko Eating Bananas

```java
public class Solution {
    public int min_eating_speed(int[] piles, int h) {
        int lo = 1, hi = 0;              // hi = max(piles)
        for (int p : piles) {
            if (p > hi) hi = p;
        }

        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (can_finish(piles, h, mid)) {
                hi = mid;
            } else {
                lo = mid + 1;
            }
        }
        return lo;
    }

    // sum(ceil(p / speed) for p in piles) <= h ?
    private boolean can_finish(int[] piles, int h, int speed) {
        long hours = 0; // use long to be safe on large inputs
        for (int p : piles) {
            hours += (p + speed - 1) / speed;  // integer ceiling
            if (hours > h) return false;       // early exit
        }
        return hours <= h;
    }
}
```

### Find Smallest Divisor Given a Threshold

```java
public class Solution {
    public int smallest_divisor(int[] nums, int threshold) {
        int lo = 1, hi = 0;
        for (int n : nums) {
            if (n > hi) hi = n;  // hi = max(nums)
        }

        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (total_sum(nums, mid) <= threshold) {
                hi = mid;
            } else {
                lo = mid + 1;
            }
        }
        return lo;
    }

    // sum(ceil(n / divisor) for n in nums)
    private int total_sum(int[] nums, int divisor) {
        int sum = 0;
        for (int n : nums) {
            sum += (n + divisor - 1) / divisor; // integer ceil
        }
        return sum;
    }
}
```

---

## 12. Pattern Recognition Cheat Sheet

### By Problem Type

| You see... | Pattern | Template |
|------------|---------|----------|
| "Find in sorted array" | Classic BS | `lo <= hi`, exact match |
| "First/last occurrence" | Lower/upper bound | `lo < hi`, boundary search |
| "Minimize the maximum" | BS on answer (minimize) | `condition(mid) -> hi=mid` |
| "Maximize the minimum" | BS on answer (maximize) | `condition(mid) -> lo=mid` (round up!) |
| "Minimum speed/capacity/size" | BS on answer (minimize) | Check feasibility |
| "Sorted + rotated" | Modified BS | Determine sorted half first |
| "Peak / mountain" | BS on slope | Compare `mid` with `mid+1` |
| "Real-valued answer" | Float BS | Fixed 100 iterations |
| "Kth smallest" | BS on value | Count elements <= mid |
| "Optimize unimodal function" | Ternary search | Two midpoints per iteration |

### The Universal Template

Almost every binary search problem fits one of these two templates:

```java
# Template 1: MINIMIZE (find first True)
# F F F F T T T T
int minimize(int lo, int hi) {
    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;
        if (condition(mid)) {
            hi = mid;
        } else {
            lo = mid + 1;
        }
    }
    return lo;
}

# Template 2: MAXIMIZE (find last True)
# T T T T F F F F
int maximize(int lo, int hi) {
    while (lo < hi) {
        int mid = lo + (hi - lo + 1) / 2;   // round UP
        if (condition(mid)) {
            lo = mid;
        } else {
            hi = mid - 1;
        }
    }
    return lo;
}
```

### Common Pitfalls

| Pitfall | Fix |
|---------|-----|
| Infinite loop (lo never advances) | Use `mid = lo + (hi - lo + 1) // 2` when `lo = mid` |
| Off-by-one on boundaries | Decide: is `hi` inclusive or exclusive? Be consistent |
| Wrong comparison direction | Draw the F/T boundary and check which side you're shrinking |
| Integer overflow in `(lo+hi)/2` | Always use `lo + (hi - lo) // 2` |
| Float BS doesn't converge | Use fixed iterations (100) instead of `while lo < hi` |
| Forgetting edge cases | Check: empty array, single element, all same, target not present |

### Complexity Summary

| Pattern | Time | Space |
|---------|------|-------|
| Classic binary search | O(log N) | O(1) |
| Lower/upper bound | O(log N) | O(1) |
| BS on answer | O(log(range) * check) | O(1) |
| Float BS | O(iterations * check) | O(1) |
| Rotated array search | O(log N) | O(1) |
| 2D matrix search | O(M + N) or O(log(MN)) | O(1) |
| Ternary search | O(log(range) * 2 evals) | O(1) |
