# Backtracking Patterns — Comprehensive Guide

Backtracking is **brute force with early termination**. You explore a decision tree, and whenever a partial solution can't possibly lead to a valid complete solution, you **prune** that branch and backtrack. The power of backtracking comes not from what it explores, but from what it **doesn't** explore.

---

## Quick Navigation: "I need to..."

| I need to... | Technique | Section |
|--------------|-----------|---------|
| Generate all **permutations** | Swap-based / used-array backtracking | [2](#2-permutations) |
| Generate all **combinations** (choose k from n) | Index-based backtracking | [3](#3-combinations) |
| Generate all **subsets** (power set) | Include/exclude at each step | [4](#4-subsets) |
| Handle **duplicates** in generation | Sort + skip adjacent duplicates | [5](#5-handling-duplicates) |
| Solve **N-Queens** / board placement | Row-by-row with column/diagonal tracking | [6](#6-grid-and-board-problems) |
| Solve **Sudoku** | Cell-by-cell with constraint checking | [6](#6-grid-and-board-problems) |
| **Partition** array into k equal subsets | Bucket-filling backtracking | [7](#7-partitioning-problems) |
| Generate **parentheses** / valid sequences | Count-based constraints | [8](#8-string-backtracking) |
| Search for **word in grid** | DFS with visited tracking | [6](#6-grid-and-board-problems) |
| Optimize with **pruning** | Feasibility + bound + symmetry pruning | [9](#9-pruning-techniques) |


---

## Table of Contents

1. [The Backtracking Framework](#1-the-backtracking-framework)
2. [Permutations](#2-permutations)
3. [Combinations](#3-combinations)
4. [Subsets](#4-subsets)
5. [Handling Duplicates](#5-handling-duplicates)
6. [Grid and Board Problems](#6-grid-and-board-problems)
7. [Partitioning Problems](#7-partitioning-problems)
8. [String Backtracking](#8-string-backtracking)
9. [Pruning Techniques](#9-pruning-techniques)
10. [Common Patterns Collection](#10-common-patterns-collection)
11. [Pattern Recognition Cheat Sheet](#11-pattern-recognition-cheat-sheet)

---

## 1. The Backtracking Framework

### The Idea

Every backtracking problem follows the same skeleton:

```
1. Choose   — pick a candidate for the current position
2. Explore  — recurse with that choice
3. Unchoose — undo the choice (backtrack)
```

### The Universal Template

```java
void backtrack(State state, List<Candidate> choices) {
    // Base case
    if (isComplete(state)) {
        processSolution(state);
        return;
    }
    for (Candidate candidate : choices) {
        if (isValid(state, candidate)) {

            // 1. Choose
            apply(state, candidate);

            // 2. Explore (pass next choices as needed)
            backtrack(state, getNextChoices(state, choices));

            // 3. Unchoose
            undo(state, candidate);
        }
    }
}
```

### The Decision Tree

Every backtracking algorithm implicitly explores a **tree**. Each node is a partial solution, each edge is a decision, and leaves are complete (or pruned) solutions.

Actually for 3-bit, leaves ARE the 3-bit strings.
Pruning "11" prefix means we skip "110" and "111".
Result: 000, 001, 010, 100, 101 — 5 valid strings.
```
Constraint: “no two consecutive 1s”, n=3
Tree explores 8 leaves without pruning. With pruning, we skip any path that already has “11”.
Valid: 000, 001, 010, 100, 101  (5 strings)
### Recursion vs State Space
```
Think of each recursive call as **one level** of the decision tree:

| Level | Decision | State changes |
|-------|----------|---------------|
| 0 | Which element goes first? | Add to `path[0]` |
| 1 | Which element goes second? | Add to `path[1]` |
| ... | ... | ... |
| n-1 | Which element goes last? | Add to `path[n-1]` |

### Implementation — Basic Template

```java
public List<List<Integer>> solve(int n) {
    List<List<Integer>> result = new ArrayList<>();
    backtrack(new ArrayList<>(), n, result);
    return result;
}

private void backtrack(List<Integer> path, int n, List<List<Integer>> result) {
    // Base case: solution is complete
    if (path.size() == n) {
        result.add(new ArrayList<>(path));  // copy!
        return;
    }

    for (int candidate : getCandidates(path)) {
        // choose
        path.add(candidate);

        // explore
        backtrack(path, n, result);

        // unchoose
        path.remove(path.size() - 1);
    }
}

// Placeholder: must be implemented by you
private List<Integer> getCandidates(List<Integer> path) {
    // return next valid candidates based on 'path'
    return new ArrayList<>();
}
```

### ⚠️ Critical: Copy the Path!

```java
# WRONG — all entries point to the same list
result.append(path)

# CORRECT — snapshot the current state
result.add(new ArrayList<>(path));                          // snapshot
result.add(Collections.unmodifiableList(new ArrayList<>(path))); // immutable snapshot
```

Since `path` is mutated during backtracking, you must copy it when recording a solution.

---

## 2. Permutations

### Problem: Generate All Permutations of [1..n]

Each position chooses from the remaining unused elements.

### Approach A: Used-Array

Track which elements are used with a boolean array.

```
Tree for [1, 2, 3]:

Level 0 (pick 1st):     1           2           3
Level 1 (pick 2nd):   2   3       1   3       1   2
Level 2 (pick 3rd):  3     2     3     1     2     1

Permutations: [1,2,3] [1,3,2] [2,1,3] [2,3,1] [3,1,2] [3,2,1]
```

```java
public List<List<Integer>> permutationsUsedArray(int[] nums) {
    int n = nums.length;
    List<List<Integer>> result = new ArrayList<>();
    boolean[] used = new boolean[n];
    backtrack(new ArrayList<>(), nums, used, result);
    return result;
}

private void backtrack(List<Integer> path, int[] nums, boolean[] used, List<List<Integer>> result) {
    // base case: full permutation
    if (path.size() == nums.length) {
        result.add(new ArrayList<>(path));  // snapshot!
        return;
    }

    for (int i = 0; i < nums.length; i++) {
        if (!used[i]) {
            used[i] = true;                 // choose
            path.add(nums[i]);

            backtrack(path, nums, used, result);  // explore

            path.remove(path.size() - 1);   // unchoose
            used[i] = false;
        }
    }
}

```

### Approach B: Swap-Based

Instead of a separate `used` array, swap elements into position. More memory efficient.

```
[1, 2, 3]
 ^  fix position 0: swap with 0, 1, 2

pos=0: [1, 2, 3]  →  recurse on [_, 2, 3]
       [2, 1, 3]  →  recurse on [_, 1, 3]
       [3, 2, 1]  →  recurse on [_, 2, 1]
```

```java
public List<List<Integer>> permutationsSwap(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    backtrack(nums, 0, result);
    return result;
}

private void backtrack(int[] nums, int start, List<List<Integer>> result) {
    // base case: full permutation
    if (start == nums.length) {
        result.add(toList(nums));   // snapshot!
        return;
    }

    for (int i = start; i < nums.length; i++) {
        swap(nums, start, i);       // choose
        backtrack(nums, start + 1, result);  // explore
        swap(nums, start, i);       // unchoose
    }
}
```

### Complexity

- **Number of permutations**: n!
- **Time**: O(n × n!) — n! permutations, each takes O(n) to copy
- **Space**: O(n) recursion depth (excluding output)

---

## 3. Combinations

### Problem: Choose k Elements from [1..n]

The key difference from permutations: **order doesn't matter**, so we enforce an ordering (e.g., always pick in increasing order) to avoid duplicates.

### The Trick: Start Index

```
C(4, 2) — choose 2 from [1, 2, 3, 4]:

          start=1
        /    |    \    \
       1     2     3    4
      /|\   /\     |
     2 3 4  3  4   4

Combinations: [1,2] [1,3] [1,4] [2,3] [2,4] [3,4]

Notice: we never go backward (e.g., no [2,1]).
```

```java
public List<List<Integer>> combinations(int n, int k) {
    List<List<Integer>> result = new ArrayList<>();
    backtrack(1, n, k, new ArrayList<>(), result);
    return result;
}
private void backtrack(int start, int n, int k,List<Integer> path,List<List<Integer>> result) {
    // base case: exact size
    if (path.size() == k) {
        result.add(new ArrayList<>(path));   // snapshot!
        return;
    }

    int needed = k - path.size();

    for (int i = start; i <= n; i++) {
        int remaining = n - i + 1;
        // pruning: if not enough numbers remain to fill path -> stop
        if (remaining < needed) break;
        path.add(i);                       // choose
        backtrack(i + 1, n, k, path, result); // explore
        path.remove(path.size() - 1);      // unchoose
    }
}
```

### Why `i + 1` and Not `i`?

- `backtrack(i + 1, ...)` → each element used **at most once** (combinations)
- `backtrack(i, ...)` → elements can repeat (combinations with repetition)
- `backtrack(start, ...)` → ERROR: would repeat same combinations

### Combination with Repetition

```java
public List<List<Integer>> combinationsWithRepetition(int[] candidates, int k) {
    List<List<Integer>> result = new ArrayList<>();
    backtrack(0, candidates, k, new ArrayList<>(), result);
    return result;
}

private void backtrack(int start, int[] candidates, int k, List<Integer> path, List<List<Integer>> result) {
    // base case
    if (path.size() == k) {
        result.add(new ArrayList<>(path));   // snapshot!
        return;
    }

    for (int i = start; i < candidates.length; i++) {
        path.add(candidates[i]);            // choose

        backtrack(i, candidates, k, path, result);
        // ^ keep i same to allow reuse (same as Python)

        path.remove(path.size() - 1);       // unchoose
    }
}

```

### Complexity

- **Number of combinations**: C(n, k) = n! / (k!(n-k)!)
- **Time**: O(k × C(n, k))
- **Space**: O(k) recursion depth

---

## 4. Subsets

### Problem: Generate All Subsets (Power Set)

Two classic approaches:

### Approach A: Include/Exclude (Binary Decision)

At each element, make a binary choice: include it or skip it.

```
Array: [1, 2, 3]
                      {}
                   /      \
               {1}         {}           ← include/exclude 1
              /    \      /    \
          {1,2}   {1}  {2}    {}        ← include/exclude 2
          / \     / \   / \   / \
      {1,2,3}{1,2}{1,3}{1}{2,3}{2}{3}{} ← include/exclude 3
```

```java

public List<List<Integer>> subsetsIncludeExclude(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    backtrack(0, nums, new ArrayList<>(), result);
    return result;
}

private void backtrack(int index,int[] nums,List<Integer> path,List<List<Integer>> result) {

    // Base case: reached end
    if (index == nums.length) {
        result.add(new ArrayList<>(path));  // snapshot!
        return;
    }

    // ---- Include nums[index] ----
    path.add(nums[index]);
    backtrack(index + 1, nums, path, result);
    path.remove(path.size() - 1);

    // ---- Exclude nums[index] ----
    backtrack(index + 1, nums, path, result);
}

```

### Approach B: Iterative Growth

At each level, choose any element with index ≥ start.

```java
public List<List<Integer>> subsetsIterativeGrowth(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    backtrack(0, nums, new ArrayList<>(), result);
    return result;
}

private void backtrack(int start,    int[] nums,    List<Integer> path,    List<List<Integer>> result) {

    // Every partial path is a valid subset → snapshot it
    result.add(new ArrayList<>(path));

    for (int i = start; i < nums.length; i++) {
        path.add(nums[i]);                       // choose
        backtrack(i + 1, nums, path, result);    // explore
        path.remove(path.size() - 1);            // unchoose
    }
}

```

### Approach C: Bitmask (Non-Recursive)

```java
public List<List<Integer>> subsetsBitmask(int[] nums) {
    int n = nums.length;
    List<List<Integer>> result = new ArrayList<>();

    int totalMasks = 1 << n;  // same as Python: 1 << n

    for (int mask = 0; mask < totalMasks; mask++) {
        List<Integer> subset = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            if ((mask & (1 << i)) != 0) {    // check bit
                subset.add(nums[i]);
            }
        }

        result.add(subset);
    }
    return result;
}

```

### Complexity

- **Number of subsets**: 2^n
- **Time**: O(n × 2^n)
- **Space**: O(n) recursion depth

---

## 5. Handling Duplicates

### The Problem

If the input has duplicates, naive backtracking generates duplicate solutions:

```
Input: [1, 1, 2]
Naive subsets: {}, {1}, {1}, {2}, {1,1}, {1,2}, {1,2}, {1,1,2} ^                        ^ duplicate!               duplicate!
```

### The Fix: Sort + Skip Adjacent

**Sort** the array first. Then at each decision level, **skip a candidate if it equals the previous candidate at the same level**.

```
Sorted: [1, 1, 2]

Level decision for "which element next?":
  candidates at start=0: [1, 1, 2]
    - pick 1 (index 0) ✓
    - pick 1 (index 1) ✗ SKIP (same as previous candidate at this level)
    - pick 2 (index 2) ✓
```

### Subsets with Duplicates

```java

public List<List<Integer>> subsetsWithDup(int[] nums) {
    Arrays.sort(nums);  // critical!
    List<List<Integer>> result = new ArrayList<>();
    backtrack(0, nums, new ArrayList<>(), result);
    return result;
}

private void backtrack(int start,    int[] nums,    List<Integer> path,    List<List<Integer>> result) {

    result.add(new ArrayList<>(path));   // snapshot

    for (int i = start; i < nums.length; i++) {

        // Skip duplicates at the same decision level
        if (i > start && nums[i] == nums[i - 1]) {
            continue;
        }

        path.add(nums[i]);                       // choose
        backtrack(i + 1, nums, path, result);    // explore
        path.remove(path.size() - 1);            // unchoose
    }
}

```

### Permutations with Duplicates

```java
public List<List<Integer>> permutationsWithDup(int[] nums) {
    Arrays.sort(nums); // critical!
    List<List<Integer>> result = new ArrayList<>();
    boolean[] used = new boolean[nums.length];

    backtrack(nums, used, new ArrayList<>(), result);
    return result;
}

private void backtrack(int[] nums,    boolean[] used,    List<Integer> path,    List<List<Integer>> result) {

    if (path.size() == nums.length) {
        result.add(new ArrayList<>(path));  // snapshot
        return;
    }

    for (int i = 0; i < nums.length; i++) {

        if (used[i]) continue;

        // Skip duplicate permutations:
        // If nums[i] == nums[i-1] and nums[i-1] was NOT used,
        // then choosing nums[i] here would create a duplicate subtree.
        if (i > 0 && nums[i] == nums[i - 1] && !used[i - 1]) {
            continue;
        }

        used[i] = true;
        path.add(nums[i]);

        backtrack(nums, used, path, result);

        path.remove(path.size() - 1);
        used[i] = false;
    }
}

```

### Why `not used[i-1]`?

This is the tricky part. Consider `[1a, 1b, 2]`:

```
Without the check, both subtrees are identical:
  1a → 1b → 2   and   1b → 1a → 2

Rule: among equal elements, only pick them in the original order.
  - 1a before 1b: OK (original order)
  - 1b before 1a: SKIP

"not used[i-1]" means: the previous equal element was already returned
(not currently in the path), so we're trying to start a new branch with
this duplicate — skip it.
```

### Combination Sum with Duplicates

```java

public List<List<Integer>> combinationSumWithDup(int[] candidates, int target) {
    Arrays.sort(candidates);  // critical for pruning & duplicate skip
    List<List<Integer>> result = new ArrayList<>();
    backtrack(0, candidates, target, new ArrayList<>(), result);
    return result;
}

private void backtrack(int start,    int[] candidates,    int remaining,    List<Integer> path,    List<List<Integer>> result) {

    if (remaining == 0) {
        result.add(new ArrayList<>(path));   // snapshot!
        return;
    }

    for (int i = start; i < candidates.length; i++) {

        // Pruning: if number exceeds remaining, all later ones will too
        if (candidates[i] > remaining) break;

        // Skip duplicates at the same level
        if (i > start && candidates[i] == candidates[i - 1]) continue;

        path.add(candidates[i]);  // choose

        // i+1 ensures each element used at most once
        backtrack(i + 1, candidates, remaining - candidates[i], path, result);

        path.remove(path.size() - 1);  // unchoose
    }
}

```

### The Duplicate-Handling Rules

| Problem Type | Sort? | Skip Condition |
|-------------|-------|----------------|
| Subsets with dups | Yes | `i > start and nums[i] == nums[i-1]` |
| Permutations with dups | Yes | `i > 0 and nums[i] == nums[i-1] and not used[i-1]` |
| Combinations with dups | Yes | `i > start and nums[i] == nums[i-1]` |

---

## 6. Grid and Board Problems

### N-Queens

Place N queens on an N×N board so no two attack each other.

```
N = 4 solution:

. Q . .
. . . Q
Q . . .
. . Q .
```

**Key insight**: Place one queen per row. Track which columns and diagonals are occupied.

```
Diagonals encoding:
  - Main diagonal (↘): row - col is constant
  - Anti-diagonal (↙): row + col is constant

Board for N=4, showing (row-col) values:
   0   -1   -2   -3       ← main diagonal IDs
   1    0   -1   -2
   2    1    0   -1
   3    2    1    0

Board showing (row+col) values:
   0    1    2    3       ← anti-diagonal IDs
   1    2    3    4
   2    3    4    5
   3    4    5    6
```

```java

public List<List<String>> solveNQueens(int n) {
        List<List<String>> result = new ArrayList<>();

        Set<Integer> cols = new HashSet<>();
        Set<Integer> diag1 = new HashSet<>(); // row - col
        Set<Integer> diag2 = new HashSet<>(); // row + col

        List<int[]> queens = new ArrayList<>(); // store (row, col)

        backtrack(0, n, cols, diag1, diag2, queens, result);
        return result;
    }

    private void backtrack(int row,int n,Set<Integer> cols,Set<Integer> diag1,Set<Integer> diag2,List<int[]> queens,List<List<String>> result) {

        if (row == n) {
            // Build board representation
            List<String> board = new ArrayList<>();
            // queens list already has ordered rows because we append row by row
            for (int[] q : queens) {
                int col = q[1];
                String line =".".repeat(col) +"Q" +".".repeat(n - col - 1);
                board.add(line);
            }
            result.add(board);
            return;
        }

        for (int col = 0; col < n; col++) {

            if (cols.contains(col) ||
                diag1.contains(row - col) ||
                diag2.contains(row + col)) {
                continue;
            }

            // choose
            cols.add(col);
            diag1.add(row - col);
            diag2.add(row + col);
            queens.add(new int[]{row, col});

            // explore
            backtrack(row + 1, n, cols, diag1, diag2, queens, result);

            // unchoose
            queens.remove(queens.size() - 1);
            cols.remove(col);
            diag1.remove(row - col);
            diag2.remove(row + col);
        }
    }
```

### Sudoku Solver

Fill empty cells so every row, column, and 3×3 box contains 1–9.

```java

public boolean solveSudoku(int[][] board) {
  // Constraint sets
  List<Set<Integer>> rows = new ArrayList<>();
  List<Set<Integer>> cols = new ArrayList<>();
  List<Set<Integer>> boxes = new ArrayList<>();

  for (int i = 0; i < 9; i++) {
      rows.add(new HashSet<>());
      cols.add(new HashSet<>());
      boxes.add(new HashSet<>());
  }

  // Track empty cells
  List<int[]> empty = new ArrayList<>();

  // Initialize state
  for (int r = 0; r < 9; r++) {
      for (int c = 0; c < 9; c++) {
          int val = board[r][c];

          if (val != 0) {
              rows.get(r).add(val);
              cols.get(c).add(val);
              boxes.get(boxId(r, c)).add(val);
          } else {
              empty.add(new int[]{r, c});
          }
      }
  }

  return backtrack(0, empty, board, rows, cols, boxes);
}

private boolean backtrack(int idx,    List<int[]> empty,    int[][] board,    List<Set<Integer>> rows,    List<Set<Integer>> cols,    List<Set<Integer>> boxes) {

  if (idx == empty.size()) {
      return true;  // all cells filled
  }

  int[] cell = empty.get(idx);
  int r = cell[0];
  int c = cell[1];
  int box = boxId(r, c);

  for (int val = 1; val <= 9; val++) {

      if (rows.get(r).contains(val) ||
          cols.get(c).contains(val) ||
          boxes.get(box).contains(val)) {
          continue;
      }

      // Choose
      board[r][c] = val;
      rows.get(r).add(val);
      cols.get(c).add(val);
      boxes.get(box).add(val);

      // Explore
      if (backtrack(idx + 1, empty, board, rows, cols, boxes)) {
          return true;
      }

      // Unchoose
      board[r][c] = 0;
      rows.get(r).remove(val);
      cols.get(c).remove(val);
      boxes.get(box).remove(val);
  }

  return false; // no valid number fits here
}

private int boxId(int r, int c) {
  return (r / 3) * 3 + (c / 3);
}

```

### Word Search in Grid

Find if a word exists in a grid by moving to adjacent cells (no revisiting).

```java
public class WordSearch {
    public boolean wordSearch(char[][] board, String word) {
        int R = board.length;
        int C = board[0].length;

        for (int r = 0; r < R; r++) {
            for (int c = 0; c < C; c++) {
                if (backtrack(board, word, r, c, 0)) {return true;
                }
            }
        }
        return false;
    }

    private boolean backtrack(char[][] board,   String word,   int r,   int c,   int k) {

        int R = board.length;
        int C = board[0].length;

        if (k == word.length()) {
            return true;
        }

        if (r < 0 || r >= R || c < 0 || c >= C) {
            return false;
        }

        if (board[r][c] != word.charAt(k)) {
            return false;
        }

        // Mark visited (in‑place trick)
        char temp = board[r][c];
        board[r][c] = '#';

        // Directions: right, left, down, up
        int[][] dirs = {{0,1}, {0,-1}, {1,0}, {-1,0}};
        for (int[] d : dirs) {
            int nr = r + d[0];
            int nc = c + d[1];

            if (backtrack(board, word, nr, nc, k + 1)) {
                return true;
            }
        }

        // Unchoose — restore original char
        board[r][c] = temp;
        return false;
    }
}
```

**In-place visited trick**: Temporarily replace `board[r][c]` with a sentinel character (`'#'`), then restore it when backtracking. Saves allocating a separate `visited` array.

---

## 7. Partitioning Problems

### Partition into k Equal-Sum Subsets

Given an array and integer k, can you partition the array into k subsets with equal sum?

```
Input: [4, 3, 2, 3, 5, 2, 1], k = 4
Total = 20, target per bucket = 5

Solution: {5}, {4,1}, {3,2}, {3,2}  ✓
```

```java
import java.util.*;

public class PartitionK {

    public boolean canPartitionK(int[] nums, int k) {
        int total = 0;
        for (int x : nums) total += x;
        if (total % k != 0) return false;

        int target = total / k;

        // Sort descending → important for pruning
        Arrays.sort(nums);
        reverse(nums);

        if (nums[0] > target) return false;

        int[] buckets = new int[k];

        return backtrack(0, nums, k, target, buckets);
    }

    private boolean backtrack(int index,   int[] nums,   int k,   int target,   int[] buckets) {

        if (index == nums.length) {
            for (int b : buckets)
                if (b != target) return false;
            return true;
        }

        Set<Integer> seen = new HashSet<>();  // symmetry pruning

        for (int i = 0; i < k; i++) {
            // Pruning: overflow
            if (buckets[i] + nums[index] > target) continue;

            // Avoid placing same value in identical buckets
            if (seen.contains(buckets[i])) continue;
            seen.add(buckets[i]);

            // Choose
            buckets[i] += nums[index];

            // Explore
            if (backtrack(index + 1, nums, k, target, buckets)) {
                return true;
            }

            // Unchoose
            buckets[i] -= nums[index];
        }

        return false;
    }

    // Helper: reverse sorted ascending → descending
    private void reverse(int[] nums) {
        int i = 0, j = nums.length - 1;
        while (i < j) {
            int tmp = nums[i];
            nums[i] = nums[j];
            nums[j] = tmp;
            i++; j--;
        }
    }
}
```

### Palindrome Partitioning

Split a string so every part is a palindrome.

```
Input: "aab"
Output: [["a","a","b"], ["aa","b"]]
```

```java
import java.util.*;

public class PalindromePartition {

    public List<List<String>> palindromePartition(String s) {
        List<List<String>> result = new ArrayList<>();
        backtrack(0, s, new ArrayList<>(), result);
        return result;
    }

    private void backtrack(int start,String s,List<String> path,List<List<String>> result) {

        if (start == s.length()) {
            result.add(new ArrayList<>(path));   // snapshot
            return;
        }

        for (int end = start; end < s.length(); end++) {
            if (isPalindrome(s, start, end)) {
                // choose
                path.add(s.substring(start, end + 1));

                // explore
                backtrack(end + 1, s, path, result);

                // unchoose
                path.remove(path.size() - 1);
            }
        }
    }

    private boolean isPalindrome(String s, int left, int right) {
        while (left < right) {
            if (s.charAt(left) != s.charAt(right)) {
                return false;
            }
            left++;
            right--;
        }
        return true;
    }
}
```

### Optimization: Precompute Palindromes with DP

```java
import java.util.*;

public class PalindromePartition {

    public List<List<String>> palindromePartitionOptimized(String s) {
        int n = s.length();

        // Precompute palindrome table
        boolean[][] isPal = new boolean[n][n];

        // 1-length substrings
        for (int i = 0; i < n; i++) {
            isPal[i][i] = true;
        }

        // 2-length substrings
        for (int i = 0; i < n - 1; i++) {
            isPal[i][i + 1] = (s.charAt(i) == s.charAt(i + 1));
        }

        // lengths >= 3
        for (int length = 3; length <= n; length++) {
            for (int i = 0; i <= n - length; i++) {
                int j = i + length - 1;
                isPal[i][j] = (s.charAt(i) == s.charAt(j)) && isPal[i + 1][j - 1];
            }
        }

        List<List<String>> result = new ArrayList<>();
        backtrack(0, s, isPal, new ArrayList<>(), result);
        return result;
    }

    private void backtrack(int start,String s,boolean[][] isPal,List<String> path,List<List<String>> result) {

        int n = s.length();

        if (start == n) {
            result.add(new ArrayList<>(path));  // snapshot
            return;
        }

        for (int end = start; end < n; end++) {
            if (isPal[start][end]) {
                // choose
                path.add(s.substring(start, end + 1));

                // explore
                backtrack(end + 1, s, isPal, path, result);

                // unchoose
                path.remove(path.size() - 1);
            }
        }
    }
}
```

---

## 8. String Backtracking

### Generate Parentheses

Generate all combinations of n pairs of well-formed parentheses.

```
n = 3:
((()))  (()())  (())()  ()(())  ()()()

Key constraint: at every prefix, #open ≥ #close
```

```java
import java.util.*;

public class GenerateParentheses {

    public List<String> generateParentheses(int n) {
        List<String> result = new ArrayList<>();
        backtrack(new StringBuilder(), 0, 0, n, result);
        return result;
    }

    private void backtrack(StringBuilder path,int openCount,int closeCount,int n,List<String> result) {

        // Complete string of length 2n
        if (path.length() == 2 * n) {
            result.add(path.toString());  // snapshot
            return;
        }

        // Try adding '('
        if (openCount < n) {
            path.append('(');                              // choose
            backtrack(path, openCount + 1, closeCount, n, result);  // explore
            path.deleteCharAt(path.length() - 1);          // unchoose
        }

        // Try adding ')'
        if (closeCount < openCount) {
            path.append(')');                              // choose
            backtrack(path, openCount, closeCount + 1, n, result);  // explore
            path.deleteCharAt(path.length() - 1);          // unchoose
        }
    }
}
```

### Letter Combinations of Phone Number

```
2 → "abc", 3 → "def", ..., 9 → "wxyz"
Input: "23"
Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]
```

```java
import java.util.*;

public class LetterCombinations {

    public List<String> letterCombinations(String digits) {
        if (digits == null || digits.length() == 0) {
            return new ArrayList<>();
        }

        Map<Character, String> mapping = new HashMap<>();
        mapping.put('2', "abc");
        mapping.put('3', "def");
        mapping.put('4', "ghi");
        mapping.put('5', "jkl");
        mapping.put('6', "mno");
        mapping.put('7', "pqrs");
        mapping.put('8', "tuv");
        mapping.put('9', "wxyz");

        List<String> result = new ArrayList<>();
        backtrack(0, digits, mapping, new StringBuilder(), result);
        return result;
    }

    private void backtrack(int index,String digits,Map<Character, String> mapping,StringBuilder path,List<String> result) {

        if (index == digits.length()) {
            result.add(path.toString());  // snapshot
            return;
        }

        String letters = mapping.get(digits.charAt(index));

        for (char ch : letters.toCharArray()) {
            path.append(ch);                                  // choose
            backtrack(index + 1, digits, mapping, path, result); // explore
            path.deleteCharAt(path.length() - 1);             // unchoose
        }
    }
}
```

### Restore IP Addresses

```
Input: "25525511135"
Output: ["255.255.11.135", "255.255.111.35"]
```

```java
import java.util.*;

public class RestoreIP {

    public List<String> restoreIpAddresses(String s) {
        List<String> result = new ArrayList<>();
        backtrack(0, s, new ArrayList<>(), result);
        return result;
    }

    private void backtrack(int start,String s,List<String> parts,List<String> result) {

        // If we have 4 parts, check if we've consumed all characters
        if (parts.size() == 4) {
            if (start == s.length()) {
                result.add(String.join(".", parts));
            }
            return;
        }

        int remainingDigits = s.length() - start;
        int remainingParts = 4 - parts.size();

        // Pruning: remaining digits must fit into remaining parts (1–3 digits each)
        if (remainingDigits < remainingParts ||
            remainingDigits > remainingParts * 3) {
            return;
        }

        // Try lengths 1, 2, 3
        for (int length = 1; length <= 3; length++) {
            if (start + length > s.length()) break;

            String segment = s.substring(start, start + length);

            // No leading zeros unless segment == "0"
            if (segment.length() > 1 && segment.charAt(0) == '0') break;

            // Segment must be <= 255
            int value = Integer.parseInt(segment);
            if (value > 255) break;

            // Choose
            parts.add(segment);

            // Explore
            backtrack(start + length, s, parts, result);

            // Unchoose
            parts.remove(parts.size() - 1);
        }
    }
}
```

### Expression: Add Operators

Insert `+`, `-`, `*` between digits to reach a target.

```java
import java.util.*;

public class AddOperators {

    public List<String> addOperators(String num, int target) {
        List<String> result = new ArrayList<>();
        backtrack(0, "", 0, 0, num, target, result);
        return result;
    }

    private void backtrack(int index,String path,long value,long prevOperand,String num,int target,List<String> result) {

        // Base case: reached end of string
        if (index == num.length()) {
            if (value == target) {
                result.add(path);
            }
            return;
        }

        // Try all substring splits num[index : i]
        for (int i = index; i < num.length(); i++) {

            // Leading-zero rule: skip numbers like "05"
            if (i > index && num.charAt(index) == '0') break;

            String substr = num.substring(index, i + 1);
            long curr = Long.parseLong(substr);

            // First number: no operator allowed in front
            if (index == 0) {
                backtrack(i + 1, substr, curr, curr, num, target, result);
            } else {
                // Addition
                backtrack(i + 1, path + "+" + substr, value + curr, curr, num, target, result);

                // Subtraction
                backtrack(i + 1, path + "-" + substr, value - curr, -curr, num, target, result);

                // Multiplication:
                // Undo previous op: remove prevOperand and add (prevOperand * curr)
                backtrack(i + 1,path + "*" + substr,value - prevOperand + prevOperand * curr,prevOperand * curr,num,target,result
                );
            }
        }
    }
}
```

**Why track `prev_operand`?** Multiplication has higher precedence. If the expression so far evaluates to `2 + 3` and we multiply by `4`, the result should be `2 + 3*4 = 14`, not `(2+3)*4 = 20`. So we undo `+3` and redo `+3*4`.

---

## 9. Pruning Techniques

Pruning is what makes backtracking practical. Without it, you're just doing brute force.

### Type 1: Feasibility Pruning

**Stop early when the current path can't possibly lead to a solution.**

```java
# Combination Sum: if remaining < 0, stop
private void backtrack(int start,   List<Integer> path,   int remaining,   List<List<Integer>> result) {

    // PRUNE — overshot the target
    if (remaining < 0) {
        return;
    }

    // Found a valid combination
    if (remaining == 0) {
        result.add(new ArrayList<>(path));   // snapshot
        return;
    }

    // ...
}
```

### Type 4: Ordering Pruning

**Process elements in a smart order to trigger other pruning earlier.**

```java
# Sort in decreasing order: large elements fail faster, pruning more branches
Collections.sort(nums, Collections.reverseOrder());
# Sudoku: pick the cell with fewest candidates (MRV heuristic)
private int[] findBestCell(int[][] board) {
    int minOptions = 10;     // more than max options (1–9)
    int[] best = null;

    for (int r = 0; r < 9; r++) {
        for (int c = 0; c < 9; c++) {
            if (board[r][c] == 0) {

                int options = countValidDigits(board, r, c);

                if (options < minOptions) {minOptions = options;best = new int[]{r, c};
                }
            }
        }
    }

    return best;   // may be null if board is full
}
```

### Type 5: Memoization (When Subproblems Repeat)

If the same state can be reached via different paths, cache the result. This turns backtracking into **dynamic programming**.

```java
# Word Break: can we segment string into dictionary words?
import java.util.*;

public class WordBreakMemo {

    public boolean canBreak(String s, Set<String> wordSet) {
        Map<Integer, Boolean> memo = new HashMap<>();
        return dfs(0, s, wordSet, memo);
    }

    private boolean dfs(int start,    String s,    Set<String> wordSet,    Map<Integer, Boolean> memo) {

        // Memoized result?
        if (memo.containsKey(start)) {
            return memo.get(start);
        }

        // Reached end → valid break
        if (start == s.length()) {
            memo.put(start, true);
            return true;
        }

        // Try all possible end positions
        for (int end = start + 1; end <= s.length(); end++) {
            String substr = s.substring(start, end);

            if (wordSet.contains(substr) && dfs(end, s, wordSet, memo)) {
                memo.put(start, true);
                return true;
            }
        }

        // No valid break from here
        memo.put(start, false);
        return false;
    }
}
```

### Pruning Impact Summary

```
Without pruning:     O(n!)   or  O(2^n)   or  O(k^n)
With pruning:        Often orders of magnitude faster

Example — N-Queens:
  n=8:  Without pruning: 8^8 = 16M states
        With col/diag pruning: ~15K states
        Speedup: ~1000x
```

---
## 10. Common Patterns Collection

### Pattern A: "Generate All X" → Backtracking

Whenever a problem asks to **generate all** valid configurations:

```
Generate all:
  - Permutations       → Section 2
  - Combinations       → Section 3
  - Subsets            → Section 4
  - Palindrome splits  → Section 7
  - Valid parentheses  → Section 8
  - IP addresses       → Section 8
```

### Pattern B: "Can We Achieve X?" → Backtracking with Early Return

When the answer is True/False, return as soon as you find one solution:

```java
boolean canAchieve(State state, List<Choice> candidates) {

    // Base case: valid solution found
    if (isSolution(state)) {
        return true;
    }

    for (Choice choice : candidates) {

        if (isValid(state, choice)) {

            // Choose
            apply(state, choice);

            // Explore — propagate success immediately
            if (canAchieve(state, candidates)) {
                return true;
            }

            // Unchoose
            undo(state, choice);
        }
    }

    // Exhausted all options
    return false;
}
```

### Pattern C: "Find Optimal X" → Backtracking with Bound

Track the best solution found so far and prune branches that can't improve it:

```java
public class BranchAndBound {

    // Global best (initialized to +∞)
    private int best = Integer.MAX_VALUE;

    public void findOptimal(State state, int cost, List<Choice> candidates) {

        // Base case: complete solution
        if (isComplete(state)) {
            best = Math.min(best, cost);
            return;
        }

        // Branch & Bound pruning
        if (cost + lowerBound(state) >= best) {
            return;
        }

        for (Choice choice : candidates) {

            // Choose
            apply(state, choice);

            // Explore
            findOptimal(state, cost + choiceCost(choice), candidates);

            // Unchoose
            undo(state, choice);
        }
    }

    public int getBest() {
        return best;
    }

```

### Pattern D: Counting Solutions → Backtracking with Counter

```java
int countSolutions(State state, List<Choice> candidates) {

    // Base case: one complete solution found
    if (isComplete(state)) {
        return 1;
    }

    int total = 0;

    for (Choice choice : candidates) {
        if (isValid(state, choice)) {

            // Choose
            apply(state, choice);

            // Explore
            total += countSolutions(state, candidates);

            // Unchoose
            undo(state, choice);
        }
    }

    return total;
}
```

### Pattern E: Incremental Constraint Checking

Don't re-validate the entire state from scratch. Instead, maintain constraint data structures and update them incrementally:

```
N-Queens:
  BAD:  for each new queen, scan entire board for conflicts → O(n) per check
  GOOD: maintain sets for cols, diag1, diag2 → O(1) per check

Sudoku:
  BAD:  for each digit, scan row + col + box → O(n) per check
  GOOD: maintain sets for each row, col, box → O(1) per check
```

---

## 11. Pattern Recognition Cheat Sheet

### Decision Flowchart

```
Problem asks to...
   │
   ├── "Generate ALL valid ___"
   │     │
   │     ├── Order matters? → Permutations (Section 2)
   │     ├── Order doesn't matter, fixed size? → Combinations (Section 3)
   │     ├── Order doesn't matter, any size? → Subsets (Section 4)
   │     ├── Split/partition something? → Partitioning (Section 7)
   │     └── Build a string char by char? → String backtracking (Section 8)
   │
   ├── "Can we ___?" (yes/no)
   │     → Backtracking with early return (Pattern B)
   │
   ├── "Find the best ___"
   │     → Branch and bound (Pattern C)
   │
   ├── "Count how many ___"
   │     │
   │     ├── State space small? → Backtracking with counter
   │     └── Overlapping subproblems? → DP (memoized backtracking)
   │
   └── "Place items on grid with constraints"
         → Grid backtracking (Section 6)
```

### Complexity Summary

| Problem | # Solutions | Time |
|---------|-------------|------|
| Permutations of n | n! | O(n × n!) |
| Permutations with dups | n! / (k₁! × k₂! × ...) | O(n × result) |
| Combinations C(n,k) | C(n,k) | O(k × C(n,k)) |
| Subsets of n | 2^n | O(n × 2^n) |
| N-Queens | varies (~n!/nᵏ) | O(n!) worst |
| Sudoku (9×9) | 1 | O(9^empty) worst |


### When Backtracking vs DP

| Use Backtracking | Use DP |
|-----------------|--------|
| Need **all** solutions | Need **count** or **optimal** |
| State space has **no overlap** | Subproblems **overlap** |
| Constraints are **complex** (hard to encode as DP state) | State can be encoded as **tuple/mask** |
| Small input (n ≤ ~20) | Larger input (n ≤ ~1000+) |

### When Backtracking vs Greedy

| Use Backtracking | Use Greedy |
|-----------------|------------|
| Need to explore **multiple paths** | Locally optimal = globally optimal |
| No greedy property exists | Matroid / exchange argument works |
| Need **exact** answer | Need **approximate** or provably optimal |

### Common Mistakes to Avoid

| Mistake | Fix |
|---------|-----|
| Forgetting to copy `path` when saving | Use `path[:]` or `list(path)` |
| Not undoing the choice (backtrack step) | Always pair `choose` with `unchoose` |
| Generating duplicate solutions | Sort + skip (Section 5) |
| Not pruning → TLE | Add feasibility / bound / symmetry pruning |
| Infinite recursion | Ensure state progresses (index increases, mask grows) |
| Modifying iteration variable | Use index-based loop, not iterator over mutable collection |

### Template Quick Reference

```java
# Permutations
def perms(nums):
    backtrack with used[] or swap

# Combinations
def combs(n, k):
    backtrack(start, path)  # start ensures no duplicates

# Subsets
def subs(nums):
    backtrack(start, path)  # record at every node, not just leaves

# With duplicates
nums.sort()
if i > start and nums[i] == nums[i-1]: continue

# Grid placement
for col in range(n):
    if valid(row, col): place and recurse on row+1

# String building
for candidate_char in options:
    if constraints_met: append and recurse on index+1
```

---

**Backtracking is systematic trial-and-error.** The "trial" part is choosing a candidate; the "error" part is recognizing dead ends and undoing the choice. Master the template, learn the pruning tricks, and know when to switch to DP — that covers 90% of backtracking problems.
