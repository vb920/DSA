# Stack & Queue Patterns — Comprehensive Guide

Stacks and queues are deceptively powerful. Beyond basic LIFO/FIFO operations, they unlock efficient solutions to problems involving **nearest elements**, **sliding windows**, **expression parsing**, and **histogram areas** --- problems that would otherwise require O(N^2) brute force.

---

## Quick Navigation: "I need to..."

| I need to... | Technique | Section |
|--------------|-----------|---------|
| Find **next greater/smaller** element | Monotonic Stack | [2](#2-monotonic-stack) |
| Find **previous greater/smaller** element | Monotonic Stack (iterate forward) | [2](#2-monotonic-stack) |
| **Sliding window** min/max | Monotonic Deque | [5](#5-monotonic-deque-sliding-window-minmax) |
| **Validate** brackets/parentheses | Stack matching | [3](#3-parentheses-and-bracket-matching) |
| **Evaluate** mathematical expressions | Stack-based parser | [4](#4-expression-evaluation) |
| **Largest rectangle** in histogram | Monotonic Stack | [6](#6-histogram-problems) |
| **Max rectangle** in binary matrix | Histogram + Monotonic Stack | [6](#6-histogram-problems) |
| **Stock span** / days until warmer | Monotonic Stack | [7](#7-stock-span-and-daily-temperatures) |
| **Sliding window** with sum/average | Queue / prefix sums | [8](#8-queue-patterns) |
| Process in **level order** | BFS queue | [8](#8-queue-patterns) |
| **Min stack** / **Max queue** | Augmented structures | [9](#9-augmented-stacks-and-queues) |
| **Trapping rain water** | Monotonic Stack or two pointers | [10](#10-trapping-rain-water) |

---

## Table of Contents

1. [Stack & Queue Fundamentals](#1-stack--queue-fundamentals)
2. [Monotonic Stack](#2-monotonic-stack)
3. [Parentheses and Bracket Matching](#3-parentheses-and-bracket-matching)
4. [Expression Evaluation](#4-expression-evaluation)
5. [Monotonic Deque (Sliding Window Min/Max)](#5-monotonic-deque-sliding-window-minmax)
6. [Histogram Problems](#6-histogram-problems)
7. [Stock Span and Daily Temperatures](#7-stock-span-and-daily-temperatures)
8. [Queue Patterns](#8-queue-patterns)
9. [Augmented Stacks and Queues](#9-augmented-stacks-and-queues)
10. [Trapping Rain Water](#10-trapping-rain-water)
11. [Pattern Recognition Cheat Sheet](#11-pattern-recognition-cheat-sheet)

---

## 1. Stack & Queue Fundamentals

### Stack (LIFO --- Last In, First Out)

```
Push 1, Push 2, Push 3:

  |  3  |  <-- top
  |  2  |
  |  1  |
  +-----+

Pop -> 3, Pop -> 2, Pop -> 1
```

```java
import java.util.*;

List<Integer> stack = new ArrayList<>();
stack.add(1);           // push
stack.add(2);
int top = stack.get(stack.size() - 1); // peek
stack.remove(stack.size() - 1);        // pop

```

### Queue (FIFO --- First In, First Out)

```
Enqueue 1, 2, 3:

  Front -> [1, 2, 3] <- Back

Dequeue -> 1, Dequeue -> 2, Dequeue -> 3
```

```java
import java.util.*;

Queue<Integer> queue = new ArrayDeque<>();
queue.offer(1);
queue.offer(2);
int front = queue.peek(); // peek
queue.poll();             // dequeue

```

### Deque (Double-Ended Queue)

```
Can push/pop from BOTH ends in O(1):

  Front <-> [1, 2, 3] <-> Back

appendleft / popleft  |  append / pop
```

```java
Deque<Integer> dq = new ArrayDeque<>();
dq.addLast(3);
dq.addFirst(1);
dq.removeLast(); // 3
dq.removeFirst(); // 1

```

### Why Not Just Use Arrays?

| Operation | List | deque |
|-----------|------|-------|
| append (right) | O(1) | O(1) |
| pop (right) | O(1) | O(1) |
| insert (left) | **O(N)** | O(1) |
| pop (left) | **O(N)** | O(1) |

Use `deque` whenever you need O(1) operations at both ends.

---

## 2. Monotonic Stack

The single most important stack pattern. Solves a family of "nearest" problems in O(N).

### The Core Idea

A **monotonic stack** maintains elements in sorted order (either increasing or decreasing). When a new element violates the order, pop elements until the invariant is restored. The popped elements have found their "answer."

```
Monotonic DECREASING stack (for next greater element):

Array: [2, 1, 5, 6, 2, 3]

Process each element:
  2: stack empty, push             stack: [2]
  1: 1 < 2 (ok, maintain order)   stack: [2, 1]
  5: 5 > 1, pop 1 (next greater of 1 is 5)
     5 > 2, pop 2 (next greater of 2 is 5)
     push 5                        stack: [5]
  6: 6 > 5, pop 5 (next greater of 5 is 6)
     push 6                        stack: [6]
  2: 2 < 6, push                   stack: [6, 2]
  3: 3 > 2, pop 2 (next greater of 2 is 3)
     push 3                        stack: [6, 3]
  End: remaining in stack have no next greater -> -1

Result: [5, 5, 6, -1, 3, -1]
```

### 2.1 Next Greater Element

**Problem**: For each element, find the first element to its right that is larger.

```java
public static int[] nextGreater(int[] arr) {
    int n = arr.length;
    int[] result = new int[n];
    Arrays.fill(result, -1);
    Deque<Integer> stack = new ArrayDeque<>();

    for (int i = 0; i < n; i++) {
        while (!stack.isEmpty() && arr[stack.peek()] < arr[i]) {
            int idx = stack.pop();
            result[idx] = arr[i];
        }
        stack.push(i);
    }
    return result;
}

```

```
arr:    [2, 1, 5, 6, 2, 3]
result: [5, 5, 6,-1, 3,-1]
```

### 2.2 Next Smaller Element

Flip the comparison. Use a monotonic **increasing** stack.

```java
public static int[] nextSmaller(int[] arr) {
    int n = arr.length;
    int[] result = new int[n];
    Arrays.fill(result, -1);
    Deque<Integer> stack = new ArrayDeque<>();

    for (int i = 0; i < n; i++) {
        while (!stack.isEmpty() && arr[stack.peek()] > arr[i]) {
            int idx = stack.pop();
            result[idx] = arr[i];
        }
        stack.push(i);
    }
    return result;
}

```

```
arr:    [4, 8, 5, 2, 25]
result: [2, 5, 2,-1, -1]
```

### 2.3 Previous Greater Element

Iterate **forward** (same direction), but the answer is what's already on the stack when you push.

```java
public static int[] previousGreater(int[] arr) {
    int n = arr.length;
    int[] result = new int[n];
    Arrays.fill(result, -1);
    Deque<Integer> stack = new ArrayDeque<>();

    for (int i = 0; i < n; i++) {
        while (!stack.isEmpty() && arr[stack.peek()] <= arr[i]) stack.pop();
        if (!stack.isEmpty()) result[i] = arr[stack.peek()];
        stack.push(i);
    }
    return result;
}

```

```
arr:    [10, 4, 2, 20, 40, 12, 30]
result: [-1,10,4, -1, -1, 40, 40]
```

### 2.4 Previous Smaller Element

```java
public static int[] previousSmaller(int[] arr) {
    int n = arr.length;
    int[] result = new int[n];
    Arrays.fill(result, -1);
    Deque<Integer> stack = new ArrayDeque<>();

    for (int i = 0; i < n; i++) {
        while (!stack.isEmpty() && arr[stack.peek()] >= arr[i]) stack.pop();
        if (!stack.isEmpty()) result[i] = arr[stack.peek()];
        stack.push(i);
    }
    return result;
}

```

### The Complete Monotonic Stack Family

| Problem | Stack type | When to pop | Answer for popped | Answer from stack top |
|---------|-----------|-------------|-------------------|-----------------------|
| **Next greater** | Decreasing | `arr[stack[-1]] < arr[i]` | Popped element's next greater = arr[i] | --- |
| **Next smaller** | Increasing | `arr[stack[-1]] > arr[i]` | Popped element's next smaller = arr[i] | --- |
| **Previous greater** | Decreasing | `arr[stack[-1]] <= arr[i]` | --- | stack top after pops = prev greater of i |
| **Previous smaller** | Increasing | `arr[stack[-1]] >= arr[i]` | --- | stack top after pops = prev smaller of i |

### The Key Insight

```
When you pop element X because of element Y:
  - Y is the NEXT greater/smaller of X (depending on stack type)
  - The new stack top is the PREVIOUS greater/smaller of X

One pass gives you TWO pieces of information per element!
```

### Circular Array Variant

For circular arrays, iterate the array **twice** (indices 0 to 2N-1):

```java
public static int[] nextGreaterCircular(int[] arr) {
    int n = arr.length;
    int[] result = new int[n];
    Arrays.fill(result, -1);
    Deque<Integer> stack = new ArrayDeque<>();

    for (int i = 0; i < 2 * n; i++) {
        int value = arr[i % n];
        while (!stack.isEmpty() && arr[stack.peek()] < value) {
            int idx = stack.pop();
            result[idx] = value;
        }
        if (i < n) stack.push(i);
    }
    return result;
}

```

```
arr:    [1, 2, 1]
result: [2,-1, 2]  (circular: after arr[2]=1, next is arr[0]=1, then arr[1]=2)
```

---

## 3. Parentheses and Bracket Matching

### Valid Parentheses

```java
public static boolean isValid(String s) {
    Deque<Character> stack = new ArrayDeque<>();
    Map<Character, Character> pairs = Map.of(
        ')', '(', ']', '[', '}', '{'
    );

    for (char ch : s.toCharArray()) {
        if (pairs.containsValue(ch)) {
            stack.push(ch);
        } else if (pairs.containsKey(ch)) {
            if (stack.isEmpty() || stack.pop() != pairs.get(ch)) return false;
        }
    }
    return stack.isEmpty();
}

```

### Minimum Removals to Make Valid

```java
public static int minRemovals(String s) {
    Deque<Integer> stack = new ArrayDeque<>();

    for (int i = 0; i < s.length(); i++) {
        char ch = s.charAt(i);
        if (ch == '(') stack.push(i);
        else if (ch == ')') {
            if (!stack.isEmpty() && s.charAt(stack.peek()) == '(') stack.pop();
            else stack.push(i);
        }
    }
    return stack.size();
}

```

### Longest Valid Parentheses

```java
public static int longestValidParentheses(String s) {
    Deque<Integer> stack = new ArrayDeque<>();
    stack.push(-1);
    int maxLen = 0;

    for (int i = 0; i < s.length(); i++) {
        char ch = s.charAt(i);
        if (ch == '(') {
            stack.push(i);
        } else {
            stack.pop();
            if (stack.isEmpty()) stack.push(i);
            else maxLen = Math.max(maxLen, i - stack.peek());
        }
    }
    return maxLen;
}

```

```
s = ")()())"

i=0 ')': pop -1, stack empty -> push 0 as sentinel  stack: [0]
i=1 '(': push 1                                      stack: [0, 1]
i=2 ')': pop 1, length = 2-0 = 2                     stack: [0]
i=3 '(': push 3                                      stack: [0, 3]
i=4 ')': pop 3, length = 4-0 = 4                     stack: [0]
i=5 ')': pop 0, stack empty -> push 5                 stack: [5]

Answer: 4
```

### Score of Parentheses

```
() = 1
(()) = 2 * 1 = 2
()() = 1 + 1 = 2
(()(()))  = 2 * (1 + 2*1) = 6
```

```java
public static int scoreOfParentheses(String s) {
    Deque<Integer> stack = new ArrayDeque<>();
    stack.push(0);

    for (char ch : s.toCharArray()) {
        if (ch == '(') {
            stack.push(0);
        } else {
            int inner = stack.pop();
            int add = Math.max(1, 2 * inner);
            stack.push(stack.pop() + add);
        }
    }
    return stack.pop();
}

```

---

## 4. Expression Evaluation

### Infix Evaluation (with precedence)

```
Input: "3 + 2 * 4 - 1"
       = 3 + 8 - 1
       = 10
```

Use two stacks: one for numbers, one for operators.

```java
public static int evaluate(String expression) {
    Deque<Integer> vals = new ArrayDeque<>();
    Deque<Character> ops = new ArrayDeque<>();

    String tokens = expression.replace(" ", "");

    int i = 0;
    while (i < tokens.length()) {
        char c = tokens.charAt(i);

        if (Character.isDigit(c)) {
            int num = 0;
            while (i < tokens.length() && Character.isDigit(tokens.charAt(i))) {
                num = num * 10 + (tokens.charAt(i) - '0');
                i++;
            }
            vals.push(num);
            continue;
        }

        if (c == '(') ops.push(c);
        else if (c == ')') {
            while (ops.peek() != '(') applyOp(ops, vals);
            ops.pop(); // remove '('
        } else {
            while (!ops.isEmpty() && ops.peek() != '(' && precedence(ops.peek()) >= precedence(c))
                applyOp(ops, vals);
            ops.push(c);
        }
        i++;
    }

    while (!ops.isEmpty()) applyOp(ops, vals);
    return vals.pop();
}

private static int precedence(char op) {
    return (op == '+' || op == '-') ? 1 : (op == '*' || op == '/') ? 2 : 0;
}

private static void applyOp(Deque<Character> ops, Deque<Integer> vals) {
    char op = ops.pop();
    int b = vals.pop();
    int a = vals.pop();
    switch (op) {
        case '+': vals.push(a + b); break;
        case '-': vals.push(a - b); break;
        case '*': vals.push(a * b); break;
        case '/': vals.push(a / b); break;
    }
}

```

### Infix to Postfix (Shunting Yard)

```
Infix:    3 + 4 * 2 / (1 - 5)
Postfix:  3 4 2 * 1 5 - / +
```

```java
public static List<String> infixToPostfix(List<String> tokens) {
    List<String> output = new ArrayList<>();
    Deque<String> ops = new ArrayDeque<>();

    Map<String, Integer> prec = Map.of(
        "+", 1,
        "-", 1,
        "*", 2,
        "/", 2
    );

    for (String token : tokens) {
        if (token.matches("\\d+")) {
            output.add(token);
        } else if (token.equals("(")) {
            ops.push(token);
        } else if (token.equals(")")) {
            while (!ops.peek().equals("(")) output.add(ops.pop());
            ops.pop();
        } else {
            while (!ops.isEmpty() && !ops.peek().equals("(") && prec.get(ops.peek()) >= prec.get(token)) {
                output.add(ops.pop());
            }
            ops.push(token);
        }
    }

    while (!ops.isEmpty()) output.add(ops.pop());
    return output;
}

```

### Postfix Evaluation

```java
public static int evalPostfix(List<String> tokens) {
    Deque<Integer> stack = new ArrayDeque<>();

    for (String token : tokens) {
        if (token.matches("\\d+")) {
            stack.push(Integer.parseInt(token));
        } else {
            int b = stack.pop();
            int a = stack.pop();
            switch (token) {
                case "+": stack.push(a + b); break;
                case "-": stack.push(a - b); break;
                case "*": stack.push(a * b); break;
                case "/": stack.push(a / b); break;
            }
        }
    }
    return stack.pop();
}

```

---

## 5. Monotonic Deque (Sliding Window Min/Max)

The queue counterpart of monotonic stack. Maintains a window's min or max in **O(1) per element**.

### The Core Idea

Maintain a deque of indices. The front is always the current window's min (or max). Remove from the back when a new element makes old elements irrelevant. Remove from the front when the element leaves the window.

```
Sliding window max, window size k=3:

arr: [1, 3, -1, -3, 5, 3, 6, 7]

Window [1,3,-1]:
  deque maintains DECREASING order of values
  deque (indices): [1]  (index of 3 -- 1 and -1 are smaller, irrelevant)
  max = arr[deque[0]] = 3

Window [3,-1,-3]:
  deque: [1, 2]  wait... let me trace properly
```

### Sliding Window Maximum

```java
public static int[] maxSlidingWindow(int[] arr, int k) {
    Deque<Integer> dq = new ArrayDeque<>();
    List<Integer> result = new ArrayList<>();

    for (int i = 0; i < arr.length; i++) {
        while (!dq.isEmpty() && dq.peekFirst() < i - k + 1)
            dq.pollFirst();

        while (!dq.isEmpty() && arr[dq.peekLast()] <= arr[i])
            dq.pollLast();

        dq.offerLast(i);

        if (i >= k - 1) result.add(arr[dq.peekFirst()]);
    }

    return result.stream().mapToInt(x -> x).toArray();
}

```

### Trace

```
arr = [1, 3, -1, -3, 5, 3, 6, 7],  k = 3

i=0: arr[0]=1,  dq=[0]                          (not full yet)
i=1: arr[1]=3,  pop 0 (1<3), dq=[1]             (not full yet)
i=2: arr[2]=-1, dq=[1,2]                        result: [3]   (max=arr[1]=3)
i=3: arr[3]=-3, dq=[1,2,3]                      result: [3,3] (max=arr[1]=3)
i=4: arr[4]=5,  pop 3,2,1 (all<5), dq=[4]       result: [3,3,5]
i=5: arr[5]=3,  dq=[4,5]                        result: [3,3,5,5]
i=6: arr[6]=6,  pop 5,4 (all<6), dq=[6]         result: [3,3,5,5,6]
i=7: arr[7]=7,  pop 6 (6<7), dq=[7]             result: [3,3,5,5,6,7]
```

### Sliding Window Minimum

Flip the comparison: maintain **increasing** order in the deque.

```java
public static int[] minSlidingWindow(int[] arr, int k) {
    Deque<Integer> dq = new ArrayDeque<>();
    List<Integer> result = new ArrayList<>();

    for (int i = 0; i < arr.length; i++) {
        while (!dq.isEmpty() && dq.peekFirst() < i - k + 1)
            dq.pollFirst();

        while (!dq.isEmpty() && arr[dq.peekLast()] >= arr[i])
            dq.pollLast();

        dq.offerLast(i);

        if (i >= k - 1) result.add(arr[dq.peekFirst()]);
    }

    return result.stream().mapToInt(x -> x).toArray();
}

```

### Why It's O(N)

Each element is pushed into the deque **once** and popped **at most once**. Total operations: 2N. Even though there's a while loop inside the for loop, the total work across all iterations is O(N).

### Monotonic Deque vs Monotonic Stack

| | Monotonic Stack | Monotonic Deque |
|--|----------------|-----------------|
| Structure | Stack (one end) | Deque (both ends) |
| Window | Unbounded (all previous) | Fixed size k |
| Remove from | Back only | Front (expired) + Back (dominated) |
| Finds | Next/previous greater/smaller | Sliding window min/max |
| Time | O(N) total | O(N) total |

---

## 6. Histogram Problems

### Largest Rectangle in Histogram

**Problem**: Given bars of varying heights, find the largest rectangular area.

```
Heights: [2, 1, 5, 6, 2, 3]

     _
    | |
  _ | |
 | || |   _
 | || | _ | |
_| || || || |
|_||_||_||_||_|
 2  1  5  6  2  3

Largest rectangle: 5x2 = 10 (bars of height 5 and 6)
```

**Key insight**: For each bar, find how far it can extend left and right (i.e., the nearest shorter bar on each side). This is exactly **previous smaller** + **next smaller**.

```java
public static int largestRectangleHistogram(int[] heights) {
    int n = heights.length;
    Deque<Integer> stack = new ArrayDeque<>();
    int maxArea = 0;

    for (int i = 0; i <= n; i++) {
        int h = (i == n) ? 0 : heights[i];

        while (!stack.isEmpty() && heights[stack.peek()] > h) {
            int height = heights[stack.pop()];
            int width = stack.isEmpty() ? i : i - stack.peek() - 1;
            maxArea = Math.max(maxArea, height * width);
        }
        stack.push(i);
    }
    return maxArea;
}

```

### Trace

```
heights = [2, 1, 5, 6, 2, 3]

i=0: h=2, push          stack: [0]
i=1: h=1, pop 0 (h=2)   area = 2*1 = 2     stack: [1]
i=2: h=5, push           stack: [1, 2]
i=3: h=6, push           stack: [1, 2, 3]
i=4: h=2, pop 3 (h=6)    area = 6*1 = 6
          pop 2 (h=5)    area = 5*2 = 10    stack: [1, 4]
i=5: h=3, push           stack: [1, 4, 5]
i=6: h=0 (sentinel)
     pop 5 (h=3)    area = 3*1 = 3
     pop 4 (h=2)    area = 2*4 = 8
     pop 1 (h=1)    area = 1*6 = 6

Max area = 10
```

### Why Width Calculation Works

When we pop index `j` because of index `i`:
- `i` is the **next smaller** on the right
- `stack[-1]` (after pop) is the **previous smaller** on the left
- Width = `i - stack[-1] - 1` (everything between the two boundaries)

```
heights:   ... [3] [5] [6] [2] ...
indices:   ...  a   j        i  ...

Pop j (height 5) because of i (height 2):
  Left boundary: a (previous smaller)
  Right boundary: i (next smaller)
  Width = i - a - 1
```

### Maximal Rectangle in Binary Matrix

**Problem**: Find the largest rectangle of 1s in a binary matrix.

**Reduction**: Treat each row as the base of a histogram. Build up heights row by row, apply histogram algorithm.

```java
public static int maximalRectangle(int[][] matrix) {
    if (matrix.length == 0) return 0;
    int m = matrix.length, n = matrix[0].length;
    int[] heights = new int[n];
    int maxArea = 0;

    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            heights[j] = matrix[i][j] == 1 ? heights[j] + 1 : 0;
        }
        maxArea = Math.max(maxArea, largestRectangleHistogram(heights));
    }
    return maxArea;
}

```

```
Matrix:         Heights row by row:
1 0 1 0 0       [1, 0, 1, 0, 0]  -> max rect = 1
1 0 1 1 1       [2, 0, 2, 1, 1]  -> max rect = 3
1 1 1 1 1       [3, 1, 3, 2, 2]  -> max rect = 6
1 0 0 1 0       [4, 0, 0, 3, 0]  -> max rect = 3

Answer: 6 (3x2 block in row 3)
```

---

## 7. Stock Span and Daily Temperatures

### Stock Span

**Problem**: For each day, how many consecutive days before it had a price <= today's price?

```
Prices:  [100, 80, 60, 70, 60, 75, 85]
Spans:   [  1,  1,  1,  2,  1,  4,  6]
                          ^        ^
                        60,70    60,70,60,75,80,85? No...
```

This is **previous greater** in disguise: span = distance to the previous day with a strictly higher price.

```java
public static int[] stockSpan(int[] prices) {
    int n = prices.length;
    int[] span = new int[n];
    Deque<Integer> stack = new ArrayDeque<>();

    for (int i = 0; i < n; i++) {
        while (!stack.isEmpty() && prices[stack.peek()] <= prices[i])
            stack.pop();
        span[i] = stack.isEmpty() ? i + 1 : i - stack.peek();
        stack.push(i);
    }
    return span;
}

```

### Daily Temperatures

**Problem**: For each day, how many days until a warmer temperature?

This is **next greater element** returning the distance.

```java
public static int[] dailyTemperatures(int[] temps) {
    int n = temps.length;
    int[] result = new int[n];
    Deque<Integer> stack = new ArrayDeque<>();

    for (int i = 0; i < n; i++) {
        while (!stack.isEmpty() && temps[stack.peek()] < temps[i]) {
            int idx = stack.pop();
            result[idx] = i - idx;
        }
        stack.push(i);
    }
    return result;
}

```

```
temps:  [73, 74, 75, 71, 69, 72, 76, 73]
result: [ 1,  1,  4,  2,  1,  1,  0,  0]
```

---

## 8. Queue Patterns

### BFS (Breadth-First Search)

The most fundamental queue pattern. Process nodes level by level.

```java
public static void bfs(Map<Integer, List<Integer>> graph, int start) {
    Set<Integer> visited = new HashSet<>();
    Queue<Integer> queue = new ArrayDeque<>();
    visited.add(start);
    queue.offer(start);

    while (!queue.isEmpty()) {
        int node = queue.poll();
        for (int neigh : graph.get(node)) {
            if (!visited.contains(neigh)) {
                visited.add(neigh);
                queue.offer(neigh);
            }
        }
    }
}

```

### Level-Order Processing

When you need to process each level separately:

```java
public static void bfsByLevel(Map<Integer, List<Integer>> graph, int start) {
    Set<Integer> visited = new HashSet<>();
    Queue<Integer> queue = new ArrayDeque<>();
    visited.add(start);
    queue.offer(start);

    int level = 0;
    while (!queue.isEmpty()) {
        int size = queue.size();
        for (int i = 0; i < size; i++) {
            int node = queue.poll();
            for (int neigh : graph.get(node)) {
                if (!visited.contains(neigh)) {
                    visited.add(neigh);
                    queue.offer(neigh);
                }
            }
        }
        level++;
    }
}

```

### Task Scheduling / Process Queue

```java
public static List<String> roundRobin(List<String[]> tasks, int quantum) {
    Queue<String[]> queue = new ArrayDeque<>(tasks);
    List<String> order = new ArrayList<>();
    int time = 0;

    while (!queue.isEmpty()) {
        String[] task = queue.poll();
        String name = task[0];
        int remaining = Integer.parseInt(task[1]);

        int run = Math.min(quantum, remaining);
        time += run;
        remaining -= run;

        if (remaining > 0) queue.offer(new String[]{name, String.valueOf(remaining)});
        else order.add(name + " @ " + time);
    }
    return order;
}

```

### Recent Counter (Sliding Window with Queue)

```java
class RecentCounter {
    Deque<Integer> queue = new ArrayDeque<>();

    public int ping(int t) {
        queue.offer(t);
        while (queue.peek() < t - 3000)
            queue.poll();
        return queue.size();
    }
}

```

---

## 9. Augmented Stacks and Queues

### Min Stack (O(1) getMin)

```java
class MinStack {
    private Deque<int[]> stack = new ArrayDeque<>();

    public void push(int val) {
        int min = stack.isEmpty() ? val : Math.min(val, stack.peek()[1]);
        stack.push(new int[]{val, min});
    }

    public int pop() {
        return stack.pop()[0];
    }

    public int top() {
        return stack.peek()[0];
    }

    public int getMin() {
        return stack.peek()[1];
    }
}

```

### Max Stack (O(1) getMax)

Same idea: store `(value, current_max)` pairs.

### Min Queue (O(1) amortized getMin)

Use **two stacks** to simulate a queue, each stack tracking its min.

```java
class MinQueue {
    private Deque<int[]> pushStack = new ArrayDeque<>();
    private Deque<int[]> popStack = new ArrayDeque<>();

    public void enqueue(int val) {
        int min = pushStack.isEmpty() ? val : Math.min(val, pushStack.peek()[1]);
        pushStack.push(new int[]{val, min});
    }

    public int dequeue() {
        if (popStack.isEmpty()) {
            while (!pushStack.isEmpty()) {
                int[] top = pushStack.pop();
                int val = top[0];
                int min = popStack.isEmpty() ? val : Math.min(val, popStack.peek()[1]);
                popStack.push(new int[]{val, min});
            }
        }
        return popStack.pop()[0];
    }

    public int getMin() {
        if (pushStack.isEmpty()) return popStack.peek()[1];
        if (popStack.isEmpty()) return pushStack.peek()[1];
        return Math.min(pushStack.peek()[1], popStack.peek()[1]);
    }
}

```

### Two Stacks = One Queue

The classic trick: a push stack and a pop stack. When pop stack is empty, pour all elements from push stack (reversing the order).

```
Enqueue 1, 2, 3:     push_stack: [1, 2, 3]    pop_stack: []
Dequeue:              push_stack: []            pop_stack: [3, 2, 1]
                      pop from pop_stack -> 1 (correct FIFO order!)
```

Amortized O(1) per operation: each element is moved at most once from push to pop stack.

---

## 10. Trapping Rain Water

A classic that combines multiple stack/pointer techniques.

### Approach 1: Monotonic Stack

```java
public static int trapStack(int[] height) {
    Deque<Integer> stack = new ArrayDeque<>();
    int water = 0;

    for (int i = 0; i < height.length; i++) {
        while (!stack.isEmpty() && height[stack.peek()] < height[i]) {
            int bottom = stack.pop();
            if (stack.isEmpty()) break;
            int width = i - stack.peek() - 1;
            int bounded = Math.min(height[i], height[stack.peek()]) - height[bottom];
            water += width * bounded;
        }
        stack.push(i);
    }
    return water;
}

```

### How It Works

```
height: [0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1]

When we pop index 2 (h=0) because of index 3 (h=2):
  bottom = height[2] = 0
  left wall = height[stack[-1]] = height[1] = 1
  right wall = height[3] = 2
  water level = min(1, 2) - 0 = 1
  width = 3 - 1 - 1 = 1
  water += 1 * 1 = 1

We compute water LAYER BY LAYER, horizontally.
```

### Approach 2: Two Pointers (O(1) space)

```java
public static int trapTwoPointers(int[] height) {
    int left = 0, right = height.length - 1;
    int leftMax = 0, rightMax = 0, water = 0;

    while (left < right) {
        if (height[left] < height[right]) {
            if (height[left] >= leftMax) leftMax = height[left];
            else water += leftMax - height[left];
            left++;
        } else {
            if (height[right] >= rightMax) rightMax = height[right];
            else water += rightMax - height[right];
            right--;
        }
    }
    return water;
}

```

### Approach 3: Prefix Max Arrays

```java
public static int trapPrefix(int[] height) {
    int n = height.length;
    int[] leftMax = new int[n];
    int[] rightMax = new int[n];

    leftMax[0] = height[0];
    for (int i = 1; i < n; i++) leftMax[i] = Math.max(leftMax[i - 1], height[i]);

    rightMax[n - 1] = height[n - 1];
    for (int i = n - 2; i >= 0; i--) rightMax[i] = Math.max(rightMax[i + 1], height[i]);

    int water = 0;
    for (int i = 0; i < n; i++) water += Math.min(leftMax[i], rightMax[i]) - height[i];

    return water;
}

```

### Comparison

| Approach | Time | Space | Idea |
|----------|------|-------|------|
| Monotonic Stack | O(N) | O(N) | Horizontal layers between walls |
| Two Pointers | O(N) | O(1) | Process from both ends inward |
| Prefix Max | O(N) | O(N) | Water at each position = min(left_max, right_max) - height |

---

## 11. Pattern Recognition Cheat Sheet

### By Problem Type

| You see... | Think... | Section |
|------------|----------|---------|
| "Next greater/smaller element" | Monotonic Stack | 2 |
| "Previous greater/smaller element" | Monotonic Stack | 2 |
| "Sliding window min/max" | Monotonic Deque | 5 |
| "Valid parentheses" | Stack matching | 3 |
| "Evaluate expression" | Two stacks (values + ops) | 4 |
| "Largest rectangle in histogram" | Monotonic Stack (increasing) | 6 |
| "Maximal rectangle in matrix" | Row histograms + monotonic stack | 6 |
| "Stock span" / "days until warmer" | Monotonic Stack (decreasing) | 7 |
| "Trapping rain water" | Stack / Two Pointers / Prefix Max | 10 |
| "Process level by level" | BFS with queue | 8 |
| "Min/Max in O(1) with push/pop" | Augmented Stack | 9 |
| "Min/Max in O(1) with enqueue/dequeue" | Augmented Queue (2 stacks) | 9 |

### Monotonic Stack Decision Table

| Problem | Stack Order | Iterate Direction | Answer Location |
|---------|-------------|-------------------|-----------------|
| Next greater | Decreasing | Left to right | On pop: `arr[i]` is the answer |
| Next smaller | Increasing | Left to right | On pop: `arr[i]` is the answer |
| Previous greater | Decreasing | Left to right | Stack top is the answer |
| Previous smaller | Increasing | Left to right | Stack top is the answer |
| Largest rectangle | Increasing | Left to right | On pop: compute width x height |
| Trapping water | Decreasing | Left to right | On pop: compute trapped water |

### Complexity Summary

| Pattern | Time | Space |
|---------|------|-------|
| Monotonic Stack (any variant) | O(N) | O(N) |
| Monotonic Deque (sliding window) | O(N) | O(K) where K = window size |
| Bracket matching | O(N) | O(N) |
| Expression evaluation | O(N) | O(N) |
| Histogram largest rectangle | O(N) | O(N) |
| Maximal rectangle in matrix | O(MN) | O(N) |
| Min Stack / Max Stack | O(1) per op | O(N) |
| Min Queue (two stacks) | O(1) amortized | O(N) |
| Trapping rain water | O(N) | O(1) to O(N) |

### The Meta-Pattern

Almost every stack/queue problem follows this template:

```
for each element:
    while stack/deque is not empty AND current element violates the invariant:
        pop and COMPUTE ANSWER for popped element
    push current element
```

The "invariant" is either increasing or decreasing order. The "answer computation" varies by problem (next greater, rectangle area, trapped water, etc.), but the structure is always the same.
