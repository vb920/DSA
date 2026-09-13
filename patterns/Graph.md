# Graph Problem Patterns — Comprehensive Guide

Graphs model relationships: cities connected by roads, users in a social network, tasks with dependencies, game positions. This guide covers **all 17 syllabus patterns**, ordered from foundations to advanced, plus reference appendices and a full pattern-recognition cheat sheet.

---

## Quick Navigation: "I need to..."

| I need to... | Technique | Section |
|--------------|-----------|---------|
| Store & traverse a graph | BFS / DFS | [1](#1-graph-representation--basic-traversal) |
| 2-color / split into two groups | Bipartite check | [2](#2-bipartite-graphs--coloring) |
| Work with 2D grids | Grid flood fill | [3](#3-grid-traversal-foundations) |
| Nearest source to every cell | Multi-source BFS | [4](#4-multi-source-bfs--virtual-nodes) |
| Shortest path (unweighted) + path itself | BFS + parent tracking | [5](#5-unweighted-shortest-path) |
| Transform words/states | Implicit graph BFS | [6](#6-word-transformation-bfs-implicit-graphs) |
| "Same node, different circumstances" | State-space BFS | [7](#7-bfs-with-expanded-states) |
| Merge sets / dynamic connectivity | DSU | [8](#8-disjoint-set-union-dsu-foundations) |
| Sizes, relations, deletions | Advanced DSU | [9](#9-advanced-disjoint-set-union) |
| Order tasks by dependencies | Topological Sort | [10](#10-topological-sort-foundations) |
| DP over a DAG | Topological DP | [11](#11-topological-dynamic-programming) |
| Min rounds / min completion time | Dependency variants | [12](#12-multi-dependency-ordering) |
| Shortest path (weighted) | Dijkstra / Bellman-Ford / Floyd / 0-1 BFS | [13](#13-weighted-graph-foundations) |
| Shortest path with ≤ K stops / budget | Layered shortest paths | [14](#14-restricted--layered-shortest-paths) |
| Min cost to connect all nodes | MST (Kruskal / Prim) | [15](#15-minimum-spanning-tree) |
| "After K steps" / critical edges | Functional graphs, Bridges/APs | [16](#16-functional-graph-cycles--bridges--articulation-points) |
| "Can player force a win?" | Game-state propagation | [17](#17-advanced-graph-state--game-problems) |
| Strongly connected groups | SCC | [Appendix A](#appendix-a-strongly-connected-components) |
| Detect cycles | DFS coloring / DSU | [Appendix B](#appendix-b-cycle-detection) |

---

## Table of Contents

1. Graph Representation & Basic Traversal
2. Bipartite Graphs & Coloring
3. Grid Traversal Foundations
4. Multi-Source BFS & Virtual Nodes
5. Unweighted Shortest Path
6. Word Transformation BFS (Implicit Graphs)
7. BFS with Expanded States
8. Disjoint Set Union (DSU) Foundations
9. Advanced Disjoint Set Union
10. Topological Sort Foundations
11. Topological Dynamic Programming
12. Multi-Dependency Ordering
13. Weighted Graph Foundations
14. Restricted & Layered Shortest Paths
15. Minimum Spanning Tree
16. Functional Graph Cycles + Bridges & Articulation Points
17. Advanced Graph State & Game Problems
- Appendix A: Strongly Connected Components
- Appendix B: Cycle Detection
18. Pattern Recognition Cheat Sheet

---

## 1. Graph Representation & Basic Traversal

Before anything, know how to store a graph. Two shared edge classes are used throughout this document:

```java
// Weighted adjacency-list edge: u -> to with weight w
static class Edge {
    int to, w;
    Edge(int to, int w) { this.to = to; this.w = w; }
}

// Full edge with both endpoints: for edge lists (Bellman-Ford, Kruskal)
static class FullEdge {
    int u, v, w;
    FullEdge(int u, int v, int w) { this.u = u; this.v = v; this.w = w; }
}
```

### 1.1 Adjacency List (most common)

```java
int n = 5;
List<List<Integer>> adj = new ArrayList<>();
for (int i = 0; i < n; i++) adj.add(new ArrayList<>());
adj.get(0).add(1); // edge 0 -> 1
adj.get(1).add(0); // undirected: add both directions

// Weighted
List<List<Edge>> wadj = new ArrayList<>();
for (int i = 0; i < n; i++) wadj.add(new ArrayList<>());
wadj.get(0).add(new Edge(1, 10));
```

### 1.2 Adjacency Matrix

```java
int n = 5;
long INF = (long)1e18;
long[][] dist = new long[n][n];
for (int i = 0; i < n; i++) {
    Arrays.fill(dist[i], INF);
    dist[i][i] = 0;
}
dist[0][1] = 10;
```

### 1.3 Edge List

```java
List<FullEdge> edges = new ArrayList<>();
edges.add(new FullEdge(0, 1, 10));
edges.sort(Comparator.comparingInt(e -> e.w));
```

### 1.4 When to Use Which

| Representation | Space | Check edge? | Iterate neighbors | Best for |
|---------------|-------|-------------|-------------------|----------|
| Adjacency List | O(V+E) | O(degree) | O(degree) | Most problems |
| Adjacency Matrix | O(V^2) | O(1) | O(V) | Dense graphs, Floyd-Warshall |
| Edge List | O(E) | O(E) | O(E) | Kruskal's, edge sorting |

### 1.5 BFS (Breadth-First Search)

Explores level by level. Finds **shortest path in unweighted graphs** (full treatment in Section 5).

```java
public static int[] bfs(int start, List<List<Integer>> adj) {
    int n = adj.size();
    int[] dist = new int[n];
    Arrays.fill(dist, -1);
    Deque<Integer> q = new ArrayDeque<>();
    dist[start] = 0;
    q.add(start);
    while (!q.isEmpty()) {
        int u = q.poll();
        for (int v : adj.get(u)) {
            if (dist[v] == -1) {
                dist[v] = dist[u] + 1;
                q.add(v);              // mark when PUSHING, not popping
            }
        }
    }
    return dist;
}
```

### 1.6 DFS (Depth-First Search)

Explores as deep as possible. Foundation for cycle detection, topological sort, SCC, bridges.

```java
public static void dfs(int u, List<List<Integer>> adj, boolean[] vis) {
    vis[u] = true;
    for (int v : adj.get(u)) if (!vis[v]) dfs(v, adj, vis);
}
```

### 1.7 Iterative DFS (for deep graphs — avoids stack overflow)

```java
public static void dfsIter(int start, List<List<Integer>> adj) {
    boolean[] vis = new boolean[adj.size()];
    Deque<Integer> st = new ArrayDeque<>();
    st.push(start);
    while (!st.isEmpty()) {
        int u = st.pop();
        if (vis[u]) continue;
        vis[u] = true;
        for (int v : adj.get(u)) if (!vis[v]) st.push(v);
    }
}
```

### 1.8 BFS vs DFS

| | BFS | DFS |
|--|-----|-----|
| Data structure | Queue | Stack / recursion |
| Finds shortest path? | Yes (unweighted) | No |
| Memory | O(width) | O(depth) |
| Use for | Shortest path, level-order | Cycle detection, topo sort, SCC |

---

## 2. Bipartite Graphs & Coloring

**Problem**: Can we 2-color the graph so no adjacent nodes share a color?

```
Bipartite:           Not bipartite:
  1 --- 2              1 --- 2
  |     |              |   / |
  3 --- 4              3 --- 4
                       (odd cycle 1-2-3)
```

### Check + Color

```java
public static boolean isBipartite(List<List<Integer>> adj) {
    int n = adj.size();
    int[] color = new int[n];
    Arrays.fill(color, -1);

    for (int i = 0; i < n; i++) {
        if (color[i] != -1) continue;          // new component
        Deque<Integer> q = new ArrayDeque<>();
        q.add(i); color[i] = 0;
        while (!q.isEmpty()) {
            int u = q.poll();
            for (int v : adj.get(u)) {
                if (color[v] == -1) {
                    color[v] = 1 - color[u];
                    q.add(v);
                } else if (color[v] == color[u]) return false;
            }
        }
    }
    return true;
}
```

### Key Property

A graph is bipartite **if and only if** it contains no odd-length cycle.

### Applications

| Application | Connection |
|-------------|-----------|
| Task assignment (workers ↔ jobs) | Bipartite matching |
| Team building with conflicts | 2-coloring |
| Offline bipartite checks with DSU | Parity DSU (Section 9.2) |
| Maximum independent set (bipartite) | König's theorem |

---

## 3. Grid Traversal Foundations

**When**: The "graph" is a 2D grid. Each cell is a node; neighbors are up/down/left/right (sometimes 8 directions). No adjacency list needed — neighbors are computed on the fly.

### The Direction Array Pattern

```java
static int[] dr = {-1, 1, 0, 0};   // up, down, -, -
static int[] dc = {0, 0, -1, 1};   // -, -, left, right

// 8-direction variant (includes diagonals)
static int[] dr8 = {-1, -1, -1, 0, 0, 1, 1, 1};
static int[] dc8 = {-1, 0, 1, -1, 1, -1, 0, 1};
```

### Flood Fill / Connected Components (BFS-based) — Number of Islands

```java
public static int numIslands(char[][] grid) {
    int rows = grid.length, cols = grid[0].length;
    boolean[][] vis = new boolean[rows][cols];
    int count = 0;

    for (int r = 0; r < rows; r++)
        for (int c = 0; c < cols; c++)
            if (grid[r][c] == '1' && !vis[r][c]) {
                count++;
                bfsGrid(grid, vis, r, c);
            }
    return count;
}

static void bfsGrid(char[][] grid, boolean[][] vis, int sr, int sc) {
    Deque<int[]> q = new ArrayDeque<>();
    q.add(new int[]{sr, sc});
    vis[sr][sc] = true;                        // mark when PUSHING
    while (!q.isEmpty()) {
        int[] cur = q.poll();
        for (int d = 0; d < 4; d++) {
            int nr = cur[0] + dr[d], nc = cur[1] + dc[d];
            if (nr < 0 || nr >= grid.length || nc < 0 || nc >= grid[0].length) continue;
            if (vis[nr][nc] || grid[nr][nc] == '0') continue;
            vis[nr][nc] = true;
            q.add(new int[]{nr, nc});
        }
    }
}
```

**Why BFS over recursive DFS**: A 1000×1000 grid can contain a path of depth 10⁶ — recursive DFS blows the call stack in Java. Use BFS or an explicit stack.

### Converting Grid ↔ Node ID (reuses every graph algorithm)

```java
int id = r * cols + c;
int r = id / cols, c = id % cols;
```

With this, Dijkstra, DSU, and topo sort all work on grids unchanged.

### Common Mistakes

| Mistake | Consequence |
|---------|-------------|
| Marking visited on **pop** instead of **push** | Same cell enqueued many times → TLE/MLE |
| Missing bounds check | `ArrayIndexOutOfBounds` |
| Recursive DFS on big grids | Stack overflow |

| Complexity | Cost |
|-----------|------|
| Time | O(rows × cols) — each cell visited once |
| Space | O(rows × cols) visited + queue |

---

## 4. Multi-Source BFS & Virtual Nodes

**When**: Find, for every node/cell, the distance to the **nearest** source. Start BFS with **all sources in the queue at distance 0** — never run one BFS per source (that's O(V·(V+E))).

### 4.1 Multi-Source BFS (general graph)

```java
public static int[] multiSourceBFS(List<Integer> sources, List<List<Integer>> adj) {
    int n = adj.size();
    int[] dist = new int[n];
    Arrays.fill(dist, -1);
    Deque<Integer> q = new ArrayDeque<>();
    for (int s : sources) { dist[s] = 0; q.add(s); }

    while (!q.isEmpty()) {
        int u = q.poll();
        for (int v : adj.get(u))
            if (dist[v] == -1) { dist[v] = dist[u] + 1; q.add(v); }
    }
    return dist;
}
```

### 4.2 Multi-Source Grid BFS

```java
public static int[][] multiSourceGridBFS(int rows, int cols, List<int[]> sources) {
    int[][] dist = new int[rows][cols];
    for (int[] row : dist) Arrays.fill(row, -1);
    Deque<int[]> q = new ArrayDeque<>();
    for (int[] s : sources) { dist[s[0]][s[1]] = 0; q.add(s); }

    while (!q.isEmpty()) {
        int[] cur = q.poll();
        for (int d = 0; d < 4; d++) {
            int nr = cur[0] + dr[d], nc = cur[1] + dc[d];
            if (nr < 0 || nr >= rows || nc < 0 || nc >= cols) continue;
            if (dist[nr][nc] != -1) continue;
            dist[nr][nc] = dist[cur[0]][cur[1]] + 1;
            q.add(new int[]{nr, nc});
        }
    }
    return dist;
}
```

### 4.3 Rotting Oranges (levels = minutes)

Track time inside the queue entry; the answer is the max timestamp. A fresh-orange counter detects "impossible."

```java
public static int orangesRotting(int[][] grid) {
    int rows = grid.length, cols = grid[0].length;
    Deque<int[]> q = new ArrayDeque<>();
    int fresh = 0, minutes = 0;

    for (int r = 0; r < rows; r++)
        for (int c = 0; c < cols; c++) {
            if (grid[r][c] == 2) q.add(new int[]{r, c, 0});
            else if (grid[r][c] == 1) fresh++;
        }

    while (!q.isEmpty()) {
        int[] cur = q.poll();
        minutes = Math.max(minutes, cur[2]);
        for (int d = 0; d < 4; d++) {
            int nr = cur[0] + dr[d], nc = cur[1] + dc[d];
            if (nr < 0 || nr >= rows || nc < 0 || nc >= cols || grid[nr][nc] != 1) continue;
            grid[nr][nc] = 2;
            fresh--;
            q.add(new int[]{nr, nc, cur[2] + 1});
        }
    }
    return fresh == 0 ? minutes : -1;
}
```

### 4.4 Which Cells Are the Sources?

| Pattern | Sources | Output |
|---------|---------|--------|
| 01-Matrix | all 0-cells | distance to nearest 0 |
| Walls & Gates | all gates | distance to nearest gate |
| Rotting Oranges | all rotten oranges | minutes until all rotten |

### 4.5 Virtual Source Node

**Trick**: One algorithm run instead of many — create a virtual node with 0-weight edges to all sources.

```
Real graph:            With virtual source:
  S1    S2    S3           V (virtual)
  |     |     |           /|\
  v     v     v          / | \
  A --- B --- C        S1  S2  S3   (0-weight edges)
```

```java
int virtual = adj.size();
adj.add(new ArrayList<>());
for (int s : sources) adj.get(virtual).add(s);

long[] dist = dijkstra(virtual, adjAsWeighted);
```

---

## 5. Unweighted Shortest Path

BFS gives distances (§1.5). Here is the full toolkit: distances **and** the actual path.

### 5.1 BFS with Parent Tracking

```java
// Returns {dist[], par[]}. par[v] = predecessor of v on a shortest path.
public static int[][] bfsWithPaths(int start, List<List<Integer>> adj) {
    int n = adj.size();
    int[] dist = new int[n], par = new int[n];
    Arrays.fill(dist, -1);
    Arrays.fill(par, -1);

    Deque<Integer> q = new ArrayDeque<>();
    dist[start] = 0;
    par[start] = start;
    q.add(start);

    while (!q.isEmpty()) {
        int u = q.poll();
        for (int v : adj.get(u)) {
            if (dist[v] != -1) continue;
            dist[v] = dist[u] + 1;
            par[v] = u;                    // remember how we got here
            q.add(v);
        }
    }
    return new int[][]{dist, par};
}

// Rebuild shortest path start -> dst. Empty list = unreachable.
public static List<Integer> reconstructPath(int start, int dst, int[] par) {
    List<Integer> path = new ArrayList<>();
    if (par[dst] == -1) return path;
    for (int v = dst; ; v = par[v]) {
        path.add(v);
        if (v == start) break;
    }
    Collections.reverse(path);
    return path;
}
```

### 5.2 Early Exit

If only one target matters, stop as soon as it is **dequeued** — BFS layers are exact, so first arrival is optimal:

```java
if (u == dst) return dist[u];   // provably shortest
```

### 5.3 Level-by-Level BFS (counting rounds)

For "minimum number of *moves/rounds*", process the queue one whole layer at a time:

```java
int steps = 0;
while (!q.isEmpty()) {
    int sz = q.size();                 // current layer
    while (sz-- > 0) {
        int u = q.poll();
        for (int v : adj.get(u))
            if (dist[v] == -1) { dist[v] = dist[u] + 1; q.add(v); }
    }
    steps++;                           // one full "move" completed
}
```

This is the skeleton behind Word Ladder (§6), Rotting Oranges (§4.3), and Parallel Courses (§12.3).

### 5.4 Why BFS Gives Shortest Paths

Invariant: nodes are dequeued in **nondecreasing distance** order. Every distance-`d` node is discovered from a distance-`(d−1)` node, and by the time any distance-`d` node is dequeued, all shorter distances are final. So the **first** time `v` is seen, `dist[v]` is optimal. DFS has no layer guarantee — its distances can be arbitrarily bad.

### 5.5 Worked Micro-Example

```
Graph:  0 - 1 - 2
        |       |
        3 ----- 4        BFS from 0:

dist = [0, 1, 2, 1, 2]
par  = [0, 0, 1, 0, 3]

Path 0→4: walk par back: 4 → 3 → 0, reverse → [0, 3, 4]   (length 2)
```

### 5.6 Common Mistakes

| Mistake | Consequence |
|---------|-------------|
| Marking visited on pop instead of push | Duplicates flood the queue → TLE/MLE |
| Leaving `par[start] = -1` | Reconstruction loops forever |
| Forgetting `Collections.reverse` | Path printed destination-first |
| Using DFS order as shortest path | Wrong answers |

---

## 6. Word Transformation BFS (Implicit Graphs)

**When**: Nodes are strings/configurations and edges are defined by a *rule* (one-letter change, one-wheel turn). The graph is never built explicitly — **neighbors are generated on the fly**. Ask *"how do I generate neighbors?"* instead of *"what are the edges?"*

### 6.1 Word Ladder

Neighbor = any word differing by exactly one letter. Naive pairwise comparison is O(N²·L); instead generate all L×26 mutations and test the dictionary.

```java
public static int ladderLength(String begin, String end, List<String> wordList) {
    Set<String> dict = new HashSet<>(wordList);
    if (!dict.contains(end)) return 0;

    Deque<String> q = new ArrayDeque<>();
    Set<String> vis = new HashSet<>();
    q.add(begin); vis.add(begin);
    int steps = 1;

    while (!q.isEmpty()) {
        int sz = q.size();                          // level-by-level (§5.3)
        for (int i = 0; i < sz; i++) {
            String cur = q.poll();
            if (cur.equals(end)) return steps;
            char[] arr = cur.toCharArray();
            for (int p = 0; p < arr.length; p++) {
                char orig = arr[p];
                for (char ch = 'a'; ch <= 'z'; ch++) {
                    if (ch == orig) continue;
                    arr[p] = ch;
                    String next = new String(arr);
                    if (dict.contains(next) && vis.add(next)) q.add(next);
                }
                arr[p] = orig;                       // restore position
            }
        }
        steps++;
    }
    return 0;
}
```

### 6.2 Wildcard Bucket Preprocessing (huge dictionaries / repeated queries)

Group words by patterns with one position wildcarded: `hot` → `*ot`, `h*t`, `ho*`. Words sharing a bucket are adjacent.

```java
Map<String, List<String>> buckets = new HashMap<>();
for (String w : dict) {
    char[] a = w.toCharArray();
    for (int p = 0; p < a.length; p++) {
        char orig = a[p];
        a[p] = '*';
        buckets.computeIfAbsent(new String(a), k -> new ArrayList<>()).add(w);
        a[p] = orig;
    }
}
```

### 6.3 Open the Lock (string states, ±1 moves with wraparound)

```java
// neighbors of state "0123":
for (int i = 0; i < 4; i++) {
    char[] up = cur.toCharArray();
    up[i] = up[i] == '9' ? '0' : (char)(up[i] + 1);       // +1 turn
    char[] down = cur.toCharArray();
    down[i] = down[i] == '0' ? '9' : (char)(down[i] - 1); // -1 turn
    // skip deadends/visited, else enqueue
}
```

### 6.4 Optimization: Bidirectional BFS

Search from `begin` and `end` simultaneously, always expanding the smaller frontier; stop when frontiers touch. Cuts explored space from O(b^d) to O(b^(d/2)).

---

## 7. BFS with Expanded States

**When**: Reaching a node with different "extras" (keys held, last edge color) leads to different futures. **The state is `(node, extra)`, not just the node.** Mental model: a **layered graph** where each node is duplicated once per state — then run plain BFS.

### 7.1 Bitmask States: Shortest Path with Keys (LC 864)

A cell is passable only if you hold the lock's key — so the same cell *is different* depending on your keys.

```java
public static int shortestPathAllKeys(String[] grid) {
    int rows = grid.length, cols = grid[0].length();
    int sr = 0, sc = 0, keyCount = 0;
    for (int r = 0; r < rows; r++)
        for (int c = 0; c < cols; c++) {
            char ch = grid[r].charAt(c);
            if (ch == '@') { sr = r; sc = c; }
            if (ch >= 'a' && ch <= 'f') keyCount = Math.max(keyCount, ch - 'a' + 1);
        }

    int full = (1 << keyCount) - 1;
    boolean[][][] vis = new boolean[rows][cols][1 << keyCount];   // (r, c, keys)
    Deque<int[]> q = new ArrayDeque<>();
    q.add(new int[]{sr, sc, 0});
    vis[sr][sc][0] = true;
    int steps = 0;

    while (!q.isEmpty()) {
        int sz = q.size();
        for (int i = 0; i < sz; i++) {
            int[] cur = q.poll();
            int r = cur[0], c = cur[1], mask = cur[2];
            if (mask == full) return steps;
            for (int d = 0; d < 4; d++) {
                int nr = r + dr[d], nc = c + dc[d];
                if (nr < 0 || nr >= rows || nc < 0 || nc >= cols) continue;
                char ch = grid[nr].charAt(nc);
                if (ch == '#') continue;
                if (ch >= 'A' && ch <= 'F' && (mask & (1 << (ch - 'A'))) == 0)
                    continue;                                     // locked, no key
                int nmask = mask;
                if (ch >= 'a' && ch <= 'f') nmask |= (1 << (ch - 'a'));
                if (!vis[nr][nc][nmask]) {
                    vis[nr][nc][nmask] = true;
                    q.add(new int[]{nr, nc, nmask});
                }
            }
        }
        steps++;
    }
    return -1;
}
```

**Bitmask idioms**: have item k? `mask & (1 << k)` · pick up k: `mask | (1 << k)` · full set: `(1 << n) - 1`.

### 7.2 Color States: Shortest Alternating Paths (LC 1129)

State = `(node, color of incoming edge)`; the next edge must differ.

```java
public static int[] shortestAlternating(int n, int[][] red, int[][] blue) {
    List<List<int[]>> adj = new ArrayList<>();
    for (int i = 0; i < n; i++) adj.add(new ArrayList<>());
    for (int[] e : red)  adj.get(e[0]).add(new int[]{e[1], 0});
    for (int[] e : blue) adj.get(e[0]).add(new int[]{e[1], 1});

    int[][] dist = new int[n][2];
    for (int[] row : dist) Arrays.fill(row, Integer.MAX_VALUE);
    Deque<int[]> q = new ArrayDeque<>();
    q.add(new int[]{0, 0}); q.add(new int[]{0, 1});
    dist[0][0] = dist[0][1] = 0;

    while (!q.isEmpty()) {
        int[] cur = q.poll();
        for (int[] e : adj.get(cur[0])) {
            if (e[1] == cur[1]) continue;                  // must alternate
            if (dist[cur[0]][cur[1]] + 1 < dist[e[0]][e[1]]) {
                dist[e[0]][e[1]] = dist[cur[0]][cur[1]] + 1;
                q.add(new int[]{e[0], e[1]});
            }
        }
    }
    int[] ans = new int[n];
    for (int i = 0; i < n; i++) {
        int best = Math.min(dist[i][0], dist[i][1]);
        ans[i] = best == Integer.MAX_VALUE ? -1 : best;
    }
    return ans;
}
```

### 7.3 Common "Extra State" Choices

| Extra state | Example |
|-------------|---------|
| Bitmask of collected items | Keys and Rooms (LC 864) |
| Last edge color | Alternating Paths (LC 1129) |
| Remainder mod k | Walks divisible by k |
| Moves/stops used | → Section 14 |
| (cell, direction) | Robots with orientation |

### 7.4 Complexity & The Critical Mistake

Complexity: **O(V × S)** states (S = states per node: 2^keys, 2, ...). A 50-cell grid with 6 keys = 50 × 64 = 3200 states — tiny.

> **Critical mistake**: Visiting by node only. The first visit to a cell may carry a different key set than the optimal one — `visited` **must** be dimensioned by the full state.

---

## 8. Disjoint Set Union (DSU) Foundations

**Problem**: Dynamically merge sets; check if two elements are in the same set.

```java
class DSU {
    int[] p, sz;
    DSU(int n) {
        p = new int[n]; sz = new int[n];
        for (int i = 0; i < n; i++) { p[i] = i; sz[i] = 1; }
    }
    int find(int x) {                     // iterative path halving — no stack overflow
        while (p[x] != x) { p[x] = p[p[x]]; x = p[x]; }
        return x;
    }
    boolean union(int a, int b) {         // false = already connected (= cycle!)
        a = find(a); b = find(b);
        if (a == b) return false;
        if (sz[a] < sz[b]) { int t = a; a = b; b = t; }
        p[b] = a; sz[a] += sz[b];
        return true;
    }
}
```

### Complexity

| Operation | Time |
|-----------|------|
| find | O(α(N)) ≈ O(1) amortized |
| union | O(α(N)) ≈ O(1) amortized |

`α(N)` is the inverse Ackermann function — effectively constant (α(10⁸⁰) = 4).

### Applications

| Problem | DSU usage |
|---------|----------|
| Kruskal's MST | Reject edges that create cycles |
| Dynamic connectivity | "Are u and v connected?" |
| Component counting | Track a counter, decrement per successful union |
| Cycle detection (undirected) | `union` returns false ⇒ cycle |
| Offline LCA (Tarjan's) | Merge subtrees during DFS |

---

## 9. Advanced Disjoint Set Union

### 9.1 DSU with Component Count

Expose the number of components; decrement on each successful union — answers "how many components remain" after every edge addition.

```java
class DSUComponents extends DSU {
    int components;
    DSUComponents(int n) { super(n); components = n; }
    boolean union(int a, int b) {
        boolean merged = super.union(a, b);
        if (merged) components--;
        return merged;
    }
}
```

### 9.2 Weighted / Parity DSU (relations between elements)

Each node stores `rel[x]` = parity of the relation from x to its parent. Answers *"same or different class?"* and detects contradictions — **offline bipartite checking**, food-chain problems.

```java
class DSUParity {
    int[] p, rel;
    DSUParity(int n) {
        p = new int[n]; rel = new int[n];
        for (int i = 0; i < n; i++) p[i] = i;
    }
    int find(int x) {
        if (p[x] == x) return x;
        int root = find(p[x]);
        rel[x] ^= rel[p[x]];              // compose parities up to root
        p[x] = root;
        return root;
    }
    // relAB: 0 = a,b same class; 1 = different classes
    boolean union(int a, int b, int relAB) {
        int ra = find(a), rb = find(b);
        if (ra == rb) return (rel[a] ^ rel[b]) == relAB;   // consistent?
        p[rb] = ra;
        rel[rb] = rel[a] ^ rel[b] ^ relAB;
        return true;
    }
    int parity(int a, int b) { return rel[a] ^ rel[b]; }   // valid if find(a)==find(b)
}
```

**Why it works**: `parity(a,b) = rel[a] ^ rel[b]` (through the shared root). When merging, solve for the new root edge so every stored equation stays true.

### 9.3 Rollback DSU (for deletions / offline dynamic connectivity)

Union by size, **no path compression** (compression destroys the undo history). Each union pushes the attached root; rollback undoes exactly one union in O(1).

```java
class DSURollback {
    int[] p, sz;
    int components;
    Deque<Integer> st = new ArrayDeque<>();

    DSURollback(int n) {
        p = new int[n]; sz = new int[n];
        for (int i = 0; i < n; i++) { p[i] = i; sz[i] = 1; }
        components = n;
    }
    int find(int x) { while (p[x] != x) x = p[x]; return x; }   // NO compression

    boolean union(int a, int b) {
        a = find(a); b = find(b);
        if (a == b) { st.push(-1); return false; }   // no-op marker keeps counts aligned
        if (sz[a] < sz[b]) { int t = a; a = b; b = t; }
        p[b] = a; sz[a] += sz[b]; components--;
        st.push(b);
        return true;
    }
    void rollback() {
        int b = st.pop();
        if (b == -1) return;
        p[b] = b; sz[find(b)] -= sz[b]; components++;
    }
}
```

### 9.4 The Reverse-Time Trick

DSU can't delete edges — so **process operations in reverse**: deletions become insertions. "Components after removing edges e_k..e_m?" becomes a forward sweep of unions over the remaining edges.

| Advanced DSU | Use when |
|--------------|----------|
| Size/count-tracked | Component size / count / max-component queries |
| Parity/weighted | Relations between elements, offline bipartite |
| Rollback | Offline dynamic connectivity, segment tree on time |
| Reverse processing | Edge/vertex **deletions** |

---

## 10. Topological Sort Foundations

**Problem**: Order nodes so every edge u → v has u before v. Only exists for **DAGs** — if it fails, a cycle exists (that's your directed-cycle detector).

### 10.1 Kahn's Algorithm (BFS-based)

```java
// Returns order, or null if a cycle exists.
public static int[] topoSort(List<List<Integer>> adj) {
    int n = adj.size();
    int[] indeg = new int[n];
    for (int u = 0; u < n; u++)
        for (int v : adj.get(u)) indeg[v]++;

    Deque<Integer> q = new ArrayDeque<>();
    for (int i = 0; i < n; i++) if (indeg[i] == 0) q.add(i);

    int[] ord = new int[n]; int idx = 0;
    while (!q.isEmpty()) {
        int u = q.poll(); ord[idx++] = u;
        for (int v : adj.get(u)) if (--indeg[v] == 0) q.add(v);
    }
    return (idx == n) ? ord : null;    // null  <=>  cycle
}
```

### 10.2 DFS-based

```java
public static void dfsTopo(int u, List<List<Integer>> adj, boolean[] vis, Deque<Integer> st) {
    vis[u] = true;
    for (int v : adj.get(u)) if (!vis[v]) dfsTopo(v, adj, vis, st);
    st.push(u);          // pushed after all descendants → popping yields topo order
}
```

### 10.3 Applications

| Application | How topo sort helps |
|-------------|-------------------|
| Course scheduling | Prerequisites form a DAG |
| Build systems (Make) | Dependencies built first |
| Shortest/longest path in DAG | Relax edges in topo order (§13.5) |
| DP on DAG | Process states in topo order (§11) |
| Directed cycle detection | `null` result ⇔ cycle |

---

## 11. Topological Dynamic Programming

### 11.0 The Universal Recipe

```
1. Build the graph. If a cycle is possible → topo sort; null ⇒ cycle ⇒ handle it
   (return -1 / false). Kahn's null-check IS the cycle detector — no separate DFS.
2. Define dp[v] = answer for the subproblem ENDING at v.
3. Process u in topological order — every predecessor of v is finalized
   before v, so one pass suffices.
4. Relax every edge u -> v using either form:
      PUSH: for each u, push updates to successors.
      PULL: for each v, combine values from all predecessors (needs reverse adj).
```

### The Four Canonical Forms

| dp[v] means | Recurrence | Example |
|-------------|-----------|---------|
| Longest path ending at v | `max(dp[u] + w)` over preds | Longest path in DAG |
| # paths from s to v | `Σ dp[u]` over preds | Count routes |
| Earliest finish time | `max(finish[p]) + dur[v]` | Critical path (§12.4) |
| Aggregate merged from all preds | merge f(pred) into v | Largest color value (LC 1857) |

### 11.1 Longest Path in a DAG (with reconstruction)

```java
public static long[] dagLongest(List<List<Edge>> adj, int[] topo, int[] par) {
    int n = adj.size();
    long[] dp = new long[n];
    Arrays.fill(par, -1);
    for (int u : topo)
        for (Edge e : adj.get(u))
            if (dp[u] + e.w > dp[e.to]) {
                dp[e.to] = dp[u] + e.w;
                par[e.to] = u;              // best predecessor
            }
    return dp;
}

// Reconstruct best path:
int best = 0;
for (int v = 0; v < n; v++) if (dp[v] > dp[best]) best = v;
List<Integer> path = new ArrayList<>();
for (int v = best; v != -1; v = par[v]) path.add(v);
Collections.reverse(path);
```

### 11.2 Counting Paths (with modulo — counts grow exponentially)

```java
public static long countPaths(List<List<Integer>> adj, int[] topo, int src, int dst, long MOD) {
    int n = adj.size();
    long[] dp = new long[n];
    dp[src] = 1;
    for (int u : topo)
        for (int v : adj.get(u))
            dp[v] = (dp[v] + dp[u]) % MOD;
    return dp[dst];
}
```

### 11.3 Aggregate DP — Largest Color Value (LC 1857)

`dp[v][c]` = max count of color `c` on any path ending at `v`. Each node counts its own color **once**, then pushes all 26 counters forward.

```java
public static int largestPathValue(String colors, List<List<Integer>> adj) {
    int n = adj.size();
    int[] topo = topoSort(adj);
    if (topo == null) return -1;                    // cycle

    int[][] dp = new int[n][26];
    int ans = 0;
    for (int u : topo) {
        int c = colors.charAt(u) - 'a';
        dp[u][c]++;                                 // count u's own color once
        ans = Math.max(ans, dp[u][c]);
        for (int v : adj.get(u))
            for (int k = 0; k < 26; k++)
                dp[v][k] = Math.max(dp[v][k], dp[u][k]);
    }
    return ans;
}
```

### 11.4 Shortest Path as DP (the unifying view)

All shortest-path algorithms are the **same recurrence** with different processing orders:

```
dp[v] = min over preds u of (dp[u] + w(u, v))

DAG:            topo order        → O(V+E), any weights
Unweighted:     BFS order         → O(V+E)
Weights ≥ 0:    Dijkstra order    → O((V+E) log V)
No order known: iterate n−1 times → Bellman-Ford, O(VE)
```

**Key insight**: whenever you can prove a valid processing order (topo order, BFS layers, Dijkstra's finalized order), one clean pass replaces Bellman-Ford's brute-force repetition.

### 11.5 Common Mistakes

| Mistake | Consequence |
|---------|-------------|
| Iterating `0..n-1` instead of topo order | Only valid if all edges go low→high index |
| Not skipping `dp[u] == INF` nodes | INF + w overflow corrupts results |
| Counting paths without modulo | Overflow — counts are exponential |
| Treating `topo == null` as an error | Null **means cycle** — that's the answer (−1) |
| Using `int` for weighted path sums | Overflow on long positive paths |

---

## 12. Multi-Dependency Ordering

Kahn's mechanics (§10) solve a family of scheduling problems.

### 12.1 Course Schedule I — "Can all tasks be completed?" (LC 207)

Completion is possible **iff** Kahn's pops all n nodes (⇔ no cycle):

```java
public static boolean canFinish(int n, int[][] prereq) {
    // prereq[i] = [a, b]: take b before a  →  edge b -> a
    List<List<Integer>> adj = new ArrayList<>();
    for (int i = 0; i < n; i++) adj.add(new ArrayList<>());
    int[] indeg = new int[n];
    for (int[] p : prereq) { adj.get(p[1]).add(p[0]); indeg[p[0]]++; }

    Deque<Integer> q = new ArrayDeque<>();
    for (int i = 0; i < n; i++) if (indeg[i] == 0) q.add(i);

    int done = 0;
    while (!q.isEmpty()) {
        int u = q.poll(); done++;
        for (int v : adj.get(u)) if (--indeg[v] == 0) q.add(v);
    }
    return done == n;
}
```

### 12.2 Course Schedule II — "Return a valid order" (LC 210)

Same skeleton; collect popped nodes; empty array on cycle:

```java
public static int[] findOrder(int n, int[][] prereq) {
    List<List<Integer>> adj = new ArrayList<>();
    for (int i = 0; i < n; i++) adj.add(new ArrayList<>());
    int[] indeg = new int[n];
    for (int[] p : prereq) { adj.get(p[1]).add(p[0]); indeg[p[0]]++; }

    Deque<Integer> q = new ArrayDeque<>();
    for (int i = 0; i < n; i++) if (indeg[i] == 0) q.add(i);

    int[] ord = new int[n]; int idx = 0;
    while (!q.isEmpty()) {
        int u = q.poll(); ord[idx++] = u;
        for (int v : adj.get(u)) if (--indeg[v] == 0) q.add(v);
    }
    return (idx == n) ? ord : new int[0];
}
```

- **Lexicographically smallest order**: swap `ArrayDeque` for a `PriorityQueue` — always pop the smallest available task. O(E + V log V).
- **Unique order?** The order is unique ⇔ the queue holds **exactly one** node at every step.

### 12.3 Parallel Courses — minimum semesters (LC 1136)

Unblocked courses run **in parallel** → each Kahn "wave" is one semester. This equals **longest path with unit weights**:

```java
public static int minimumSemesters(int n, int[][] relations) {
    List<List<Integer>> adj = new ArrayList<>();
    for (int i = 0; i < n; i++) adj.add(new ArrayList<>());
    int[] indeg = new int[n];
    for (int[] r : relations) { adj.get(r[0]).add(r[1]); indeg[r[1]]++; }

    Deque<Integer> q = new ArrayDeque<>();
    for (int i = 0; i < n; i++) if (indeg[i] == 0) q.add(i);

    int semesters = 0, done = 0;
    while (!q.isEmpty()) {
        int sz = q.size();               // everything currently queued runs together
        semesters++;
        while (sz-- > 0) {
            int u = q.poll(); done++;
            for (int v : adj.get(u)) if (--indeg[v] == 0) q.add(v);
        }
    }
    return done == n ? semesters : -1;   // -1 = cycle
}
```

### 12.4 Weighted Dependencies — Critical Path (minimum completion time)

Task `u` takes `dur[u]`, starts only after **all** prerequisites finish:
`finish[u] = max(finish[p]) + dur[u]` — the **pull** form of topo DP over the reverse graph. The answer is the longest weighted path in the DAG.

```java
public static long minCompletionTime(List<List<Integer>> adj, int[] topo, int[] dur) {
    int n = adj.size();
    List<List<Integer>> radj = new ArrayList<>();
    for (int i = 0; i < n; i++) radj.add(new ArrayList<>());
    for (int u = 0; u < n; u++)
        for (int v : adj.get(u)) radj.get(v).add(u);

    long[] finish = new long[n];
    long ans = 0;
    for (int u : topo) {
        long start = 0;
        for (int p : radj.get(u)) start = Math.max(start, finish[p]);  // wait for all
        finish[u] = start + dur[u];
        ans = Math.max(ans, finish[u]);
    }
    return ans;
}
```

### 12.5 Which Tasks Can *Never* Be Done?

Any node with leftover `indeg[v] > 0` after Kahn sits in, or behind, a cycle:

```java
List<Integer> stuck = new ArrayList<>();
for (int v = 0; v < n; v++) if (indeg[v] > 0) stuck.add(v);
```

### 12.6 Counting Valid Orders (n ≤ 20 — bitmask DP)

```java
public static long countOrders(int n, int[][] prereq) {
    int[] pre = new int[n];                       // pre[v] = mask of v's prerequisites
    for (int[] p : prereq) pre[p[0]] |= (1 << p[1]);

    long[] dp = new long[1 << n];
    dp[0] = 1;
    for (int mask = 0; mask < (1 << n); mask++)
        for (int v = 0; v < n; v++)
            if ((mask & (1 << v)) == 0 && (pre[v] & mask) == pre[v])  // prereqs met
                dp[mask | (1 << v)] += dp[mask];
    return dp[(1 << n) - 1];
}
```

### Variants Summary

| Variant | Technique | Complexity |
|---------|-----------|------------|
| Possible at all? | Kahn, `done == n` | O(V+E) |
| Return one order | Kahn + order array | O(V+E) |
| Lexicographically smallest | Kahn + PriorityQueue | O(E + V log V) |
| Minimum rounds (parallel) | Level-by-level Kahn | O(V+E) |
| Minimum time (durations) | Pull DP / critical path | O(V+E) |
| Tasks stuck in cycles | Leftover `indeg > 0` | O(V) |
| Count all orders (n ≤ 20) | Bitmask DP | O(2ⁿ · n) |

---

## 13. Weighted Graph Foundations

The most important algorithm family. Selection guide first:

```
What kind of graph?
    |
    +-- Unweighted? ----------------------------> BFS (§5)  O(V+E)
    +-- Non-negative weights? ------------------> Dijkstra   O((V+E) log V)
    +-- Negative weights, no neg. cycle? -------> Bellman-Ford  O(VE)
    +-- All pairs? ------------------------------> Floyd-Warshall  O(V^3)
    +-- Weights only 0 and 1? ------------------> 0-1 BFS  O(V+E)
    +-- DAG? ------------------------------------> Topo sort + relaxation  O(V+E)
```

### 13.1 Dijkstra's Algorithm

**When**: non-negative weights, single source.

```java
public static long[] dijkstra(int src, List<List<Edge>> adj) {
    int n = adj.size();
    long[] dist = new long[n];
    Arrays.fill(dist, Long.MAX_VALUE);
    dist[src] = 0;
    PriorityQueue<long[]> pq = new PriorityQueue<>(Comparator.comparingLong(a -> a[0]));
    pq.add(new long[]{0, src});

    while (!pq.isEmpty()) {
        long[] cur = pq.poll();
        long d = cur[0];
        int u = (int) cur[1];
        if (d != dist[u]) continue;          // stale entry — skip
        for (Edge e : adj.get(u)) {
            long nd = d + e.w;
            if (nd < dist[e.to]) {
                dist[e.to] = nd;
                pq.add(new long[]{nd, e.to});
            }
        }
    }
    return dist;
}
```

**Why it works**: always settles the unvisited node with smallest distance; with non-negative weights, a settled node's distance is final.

> **Common mistake**: Dijkstra with negative weights — a "settled" node may later be improved through a negative edge, and the algorithm never revisits it.

### 13.2 Bellman-Ford

**When**: negative weights allowed; detects negative cycles.

```java
public static long[] bellmanFord(int src, int n, List<FullEdge> edges) {
    long[] dist = new long[n];
    Arrays.fill(dist, Long.MAX_VALUE);
    dist[src] = 0;

    for (int i = 0; i < n - 1; i++) {
        for (FullEdge e : edges) {
            if (dist[e.u] != Long.MAX_VALUE && dist[e.u] + e.w < dist[e.v])
                dist[e.v] = dist[e.u] + e.w;
        }
    }
    // Negative cycle check: if an Nth round still relaxes anything → cycle exists
    return dist;
}
```

**Why N−1 iterations?** A shortest path has at most N−1 edges; each round extends relaxed paths by one more edge. Improvement on round N ⇒ negative cycle.

### 13.3 Floyd-Warshall

**When**: all-pairs, small graph (V ≤ 500).

```java
public static void floydWarshall(long[][] d) {
    int n = d.length;
    for (int k = 0; k < n; k++)
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                if (d[i][k] + d[k][j] < d[i][j])
                    d[i][j] = d[i][k] + d[k][j];
}
```

**Meaning**: `dp[i][j][k]` = shortest i→j path using only intermediates 0..k. **Bonus**: negative cycle exists iff any `d[i][i] < 0`.

### 13.4 0-1 BFS

**When**: weights are only **0 or 1**. BFS with a deque — 0-edges push front (same level), 1-edges push back (next level).

```java
public static long[] zeroOneBFS(int src, List<List<Edge>> adj) {
    int n = adj.size();
    long[] dist = new long[n];
    Arrays.fill(dist, Long.MAX_VALUE);
    dist[src] = 0;
    Deque<Integer> dq = new ArrayDeque<>();
    dq.add(src);

    while (!dq.isEmpty()) {
        int u = dq.pollFirst();
        for (Edge e : adj.get(u)) {
            long nd = dist[u] + e.w;
            if (nd < dist[e.to]) {
                dist[e.to] = nd;
                if (e.w == 0) dq.addFirst(e.to);
                else          dq.addLast(e.to);
            }
        }
    }
    return dist;
}
```

### 13.5 Shortest Path on a DAG

Process in topo order — works even with negative weights (§11.4):

```java
public static long[] dagShortestPath(int src, List<List<Edge>> adj, int[] topo) {
    int n = adj.size();
    long[] dist = new long[n];
    Arrays.fill(dist, Long.MAX_VALUE);
    dist[src] = 0;
    for (int u : topo) {
        if (dist[u] == Long.MAX_VALUE) continue;
        for (Edge e : adj.get(u))
            dist[e.to] = Math.min(dist[e.to], dist[u] + e.w);
    }
    return dist;
}
```

### Shortest Path Summary

| Algorithm | Time | Space | Weights | Negative cycle? |
|-----------|------|-------|---------|----------------|
| BFS | O(V+E) | O(V) | Unweighted | N/A |
| Dijkstra | O((V+E) log V) | O(V) | Non-negative | N/A |
| Bellman-Ford | O(VE) | O(V) | Any | Detects |
| Floyd-Warshall | O(V³) | O(V²) | Any | Detects |
| 0-1 BFS | O(V+E) | O(V) | 0 or 1 | N/A |
| DAG relaxation | O(V+E) | O(V) | Any (DAG) | N/A |

---

## 14. Restricted & Layered Shortest Paths

**When**: shortest path under a constraint — "at most K stops," "within fuel budget." This is Section 7's state-space idea on **weighted** graphs: state = `(node, resource used)`.

### 14.1 Cheapest Flights Within K Stops (LC 787)

#### Approach 1: Bellman-Ford limited to K+1 rounds

Each round extends paths by **exactly one edge** — the snapshot freezes the previous layer.

```java
public static int findCheapestPrice(int n, int[][] flights, int src, int dst, int k) {
    long[] dist = new long[n];
    Arrays.fill(dist, Long.MAX_VALUE);
    dist[src] = 0;

    for (int round = 0; round <= k; round++) {       // k stops = k+1 edges
        long[] next = Arrays.copyOf(dist, n);        // freeze previous layer!
        for (int[] f : flights) {
            if (dist[f[0]] == Long.MAX_VALUE) continue;
            if (dist[f[0]] + f[2] < next[f[1]])
                next[f[1]] = dist[f[0]] + f[2];
        }
        dist = next;
    }
    return dist[dst] == Long.MAX_VALUE ? -1 : (int) dist[dst];
}
```

**Why the snapshot matters**: relaxing in-place lets one round chain several edges, destroying the edge-count guarantee.

#### Approach 2: Dijkstra on state `(node, stops)`

```java
public static int findCheapestPricePQ(int n, List<List<int[]>> adj, int src, int dst, int k) {
    PriorityQueue<long[]> pq = new PriorityQueue<>(Comparator.comparingLong(a -> a[0]));
    pq.add(new long[]{0, src, 0});                   // {cost, node, edges used}

    while (!pq.isEmpty()) {
        long[] cur = pq.poll();
        long cost = cur[0];
        int u = (int) cur[1], edges = (int) cur[2];
        if (u == dst) return (int) cost;
        if (edges == k + 1) continue;                // constraint exhausted
        for (int[] e : adj.get(u))
            pq.add(new long[]{cost + e[1], e[0], edges + 1});
    }
    return -1;
}
```

**Why plain Dijkstra fails**: it permanently keeps only the *cheapest* way to reach `u`, discarding a slightly costlier path that used **fewer stops** — which might be the only one satisfying the constraint. Expanding the state to `(node, stops)` restores correctness. State space = V × (K+1); add a `dist[node][stops]` pruning table when K is large.

### 14.2 Fuel / Budget Constraints (LC 1928 pattern)

State = `(node, fuel remaining)`; transitions consume fuel; minimize cost. Dijkstra over V × fuelMax states.

### Constraint Summary

| Constraint type | State | Algorithm |
|-----------------|-------|-----------|
| ≤ K edges/stops | (node, stops) | Layered Bellman-Ford or state Dijkstra |
| ≤ F fuel / budget | (node, fuel) | Dijkstra on states |
| Edge-color rules | (node, color) | BFS on states (§7.2) |

---

## 15. Minimum Spanning Tree

**Problem**: connect all nodes with minimum total edge weight.

### 15.1 Kruskal's Algorithm

Sort edges by weight; greedily add the lightest edge that doesn't create a cycle (DSU, §8):

```java
public static long kruskal(int n, List<FullEdge> edges) {
    edges.sort(Comparator.comparingInt(e -> e.w));
    DSU d = new DSU(n);
    long ans = 0;
    int used = 0;
    for (FullEdge e : edges)
        if (d.union(e.u, e.v)) { ans += e.w; used++; }
    // used == n-1  <=>  graph was connected
    return ans;
}
```

### 15.2 Prim's Algorithm

Grow the tree from a start node; always add the lightest edge leaving the tree:

```java
public static long prim(int start, List<List<Edge>> adj) {
    int n = adj.size();
    boolean[] vis = new boolean[n];
    PriorityQueue<long[]> pq = new PriorityQueue<>(Comparator.comparingLong(a -> a[0]));
    pq.add(new long[]{0, start});
    long sum = 0;

    while (!pq.isEmpty()) {
        long[] cur = pq.poll();
        int u = (int) cur[1];
        if (vis[u]) continue;
        vis[u] = true;
        sum += cur[0];
        for (Edge e : adj.get(u))
            if (!vis[e.to]) pq.add(new long[]{e.w, e.to});
    }
    return sum;
}
```

### Kruskal vs Prim

| | Kruskal | Prim |
|--|---------|------|
| Time | O(E log E) | O((V+E) log V) |
| Best for | Sparse graphs (E ~ V) | Dense graphs (E ~ V²) |
| Data structure | Union-Find | Priority Queue |
| Input | Edge list | Adjacency list |

### MST Properties

| Property | Explanation |
|----------|-------------|
| Cut Property | Lightest edge crossing any cut is in the MST |
| Cycle Property | Heaviest edge in any cycle is NOT in the MST |
| Uniqueness | MST is unique if all edge weights are distinct |
| N−1 edges | MST of N connected nodes has exactly N−1 edges |

---

## 16. Functional Graph Cycles + Bridges & Articulation Points

### 16.1 Functional Graphs (Successor Graphs)

**When**: every node has **exactly one outgoing edge** (`succ[v]`). Structure is always a "rho" (ρ): disjoint tails feeding simple cycles.

```
0 → 1 → 2 → 3 → 4
        ↑       |
        +-------+     cycle: 2 → 3 → 4 → 2   tail: 0 → 1 → 2
```

#### Find the Cycle (walk N steps)

After N steps from any start, you are **guaranteed to be inside** the cycle:

```java
int v = 0;
for (int i = 0; i < n; i++) v = succ[v];     // v is on the cycle
int len = 1, u = succ[v];
while (u != v) { u = succ[u]; len++; }       // cycle length
```

#### Floyd's Tortoise and Hare — O(1) extra space

```java
int slow = start, fast = succ[start];
while (slow != fast) { slow = succ[slow]; fast = succ[succ[fast]]; }
slow = start;                                 // find cycle entry:
while (slow != fast) { slow = succ[slow]; fast = succ[fast]; }
// slow == fast == cycle entry
```

#### Binary Lifting — k-th successor in O(log k)

`up[k][v]` = node reached from v after 2^k steps:

```java
int LOG = 60;                                  // covers k up to ~1e18
int[][] up = new int[LOG][n];
up[0] = succ;
for (int k = 1; k < LOG; k++)
    for (int v = 0; v < n; v++)
        up[k][v] = up[k - 1][up[k - 1][v]];

int kthSucc(int v, long k) {
    for (int b = 0; k > 0; b++, k >>= 1)
        if ((k & 1) == 1) v = up[b][v];
    return v;
}
```

Store min/max alongside in the same table for aggregate k-step queries.

| Problem | Mapping |
|---------|---------|
| Find the Duplicate Number (LC 287) | `i → nums[i]`; duplicate = cycle entry |
| Circular Array Loop (LC 457) | `i → (i + nums[i]) mod n` |
| "Position after 10^18 moves" | k-th successor via lifting |
| k-th ancestor on trees | Same lifting table on parent pointers |

**Complexity**: build O(N log N), query O(log k).

### 16.2 Bridges and Articulation Points

**Bridge**: edge whose removal disconnects the graph.
**Articulation point**: node whose removal disconnects the graph.

```
    1 --- 2 --- 5 --- 6
    |    /      |    /
    |   /       |   /
    3 -/        7 -/

bridge: 2-5        articulation points: 2, 5
```

#### Finding Bridges

```java
public static List<int[]> bridges(List<List<Integer>> adj) {
    int n = adj.size();
    int[] disc = new int[n], low = new int[n];
    Arrays.fill(disc, -1);
    List<int[]> res = new ArrayList<>();
    int[] time = {0};
    for (int i = 0; i < n; i++)
        if (disc[i] == -1) dfsB(i, -1, adj, disc, low, time, res);
    return res;
}

private static void dfsB(int u, int p, List<List<Integer>> adj, int[] disc, int[] low,
                         int[] time, List<int[]> res) {
    disc[u] = low[u] = time[0]++;
    for (int v : adj.get(u)) {
        if (v == p) continue;                  // skip the edge we came from
        if (disc[v] == -1) {
            dfsB(v, u, adj, disc, low, time, res);
            low[u] = Math.min(low[u], low[v]);
            if (low[v] > disc[u]) res.add(new int[]{u, v});   // bridge
        } else low[u] = Math.min(low[u], disc[v]);
    }
}
```

#### Finding Articulation Points

```java
public static List<Integer> articulation(List<List<Integer>> adj) {
    int n = adj.size();
    int[] disc = new int[n], low = new int[n];
    boolean[] ap = new boolean[n];
    Arrays.fill(disc, -1);
    int[] time = {0};
    for (int i = 0; i < n; i++)
        if (disc[i] == -1) dfsA(i, -1, adj, disc, low, ap, time);

    List<Integer> res = new ArrayList<>();
    for (int i = 0; i < n; i++) if (ap[i]) res.add(i);
    return res;
}

private static void dfsA(int u, int p, List<List<Integer>> adj, int[] disc, int[] low,
                         boolean[] ap, int[] time) {
    disc[u] = low[u] = time[0]++;
    int child = 0;
    for (int v : adj.get(u)) {
        if (v == p) continue;
        if (disc[v] == -1) {
            child++;
            dfsA(v, u, adj, disc, low, ap, time);
            low[u] = Math.min(low[u], low[v]);
            if (p != -1 && low[v] >= disc[u]) ap[u] = true;
        } else low[u] = Math.min(low[u], disc[v]);
    }
    if (p == -1 && child > 1) ap[u] = true;    // root with 2+ DFS children
}
```

#### Understanding `low[v]`

`low[v]` = earliest discovery time reachable from v's subtree via back edges. If `low[v] > disc[u]`, no back edge from v's subtree climbs above u → edge (u, v) is a **bridge**.

```
disc:     0    1    2    3
          u -- a -- b -- c
          |              |
          +--------------+   (back edge c -> u)

low[c] = 0, low[b] = 0, low[a] = 0   (all inherit the back edge)
Edge u-a: low[a]=0 is NOT > disc[u]=0  →  NOT a bridge  ✓ (back edge saves it)
```

---

## 17. Advanced Graph State & Game Problems

**When**: positions are nodes, moves are edges, and you must decide **WIN/LOSE** per position. Solve by **backward propagation** from terminal states.

### 17.1 The Three Rules (Backward Induction)

A position (with the player to move) is:

1. **WINNING** if **at least one** move leads to a LOSING position.
2. **LOSING** if **all** moves lead to WINNING positions.
3. **DRAW/UNKNOWN** if the rules can't decide — only possible when cycles exist.

### 17.2 Reverse BFS with Outdegree Counting

```java
// state[u]: 0 = unknown, 1 = WIN, 2 = LOSE
// terminals: positions with no moves (LOSE for the player to move)
public static int[] whoWins(int n, List<List<Integer>> adj, List<Integer> terminals) {
    List<List<Integer>> radj = new ArrayList<>();
    for (int i = 0; i < n; i++) radj.add(new ArrayList<>());
    int[] out = new int[n];
    for (int u = 0; u < n; u++) {
        out[u] = adj.get(u).size();
        for (int v : adj.get(u)) radj.get(v).add(u);
    }

    int[] state = new int[n];
    Deque<Integer> q = new ArrayDeque<>();
    for (int t : terminals) { state[t] = 2; q.add(t); }

    while (!q.isEmpty()) {
        int u = q.poll();
        for (int p : radj.get(u)) {          // p can move to u
            if (state[p] != 0) continue;
            if (state[u] == 2) {             // p can move to a LOSER → p WINS
                state[p] = 1;
                q.add(p);
            } else if (--out[p] == 0) {      // all of p's moves are WINNERS → p LOSES
                state[p] = 2;
                q.add(p);
            }
        }
    }
    return state;                            // leftover 0s = draws / cycle-locked
}
```

**Why outdegree counting**: p is LOSING only when *every* successor is confirmed WINNING — the counter tracks undecided successors. Nodes on cycles whose fate depends on themselves never resolve → DRAW.

### 17.3 Richer State: Cat and Mouse (LC 913)

Same propagation, but the state is `(mousePos, catPos, whoseTurn)` with three outcomes (mouse wins / cat wins / draw). General lesson: **expand the state until the game rules are fully encoded in it** — then plain backward BFS works.

### 17.4 Sprague–Grundy (Nim-style impartial games, brief)

`grundy(u) = mex{ grundy(v) : u → v }`; a position is LOSING iff `grundy == 0`. Independent subgames combine by **XOR** of Grundy values.

| Game pattern | Technique |
|--------------|-----------|
| Win/lose, no cycles | Reverse topo/BFS from terminals |
| Win/lose with cycles (draws) | Outdegree counting; leftovers = draw |
| Two movers, conflicting goals | State = (pos₁, pos₂, turn) |
| Independent subgames | Grundy numbers + XOR |

---

## Appendix A: Strongly Connected Components

**Problem**: find maximal groups where every node reaches every other (directed graph).

```
    1 --> 2 --> 5 --> 6
    ^    /      ^    /
    |   v       |   v
    4 <-3       8 <-7

SCC 1: {1,2,3,4}   SCC 2: {5,6,7,8}
```

### A.1 Kosaraju's Algorithm (two DFS passes)

DFS on original graph for finish order; DFS on reversed graph in reverse finish order.

```java
public static List<List<Integer>> kosaraju(List<List<Integer>> adj) {
    int n = adj.size();
    boolean[] vis = new boolean[n];
    Deque<Integer> st = new ArrayDeque<>();

    for (int i = 0; i < n; i++) if (!vis[i]) dfs1(i, adj, vis, st);

    List<List<Integer>> rev = new ArrayList<>();
    for (int i = 0; i < n; i++) rev.add(new ArrayList<>());
    for (int u = 0; u < n; u++)
        for (int v : adj.get(u)) rev.get(v).add(u);

    Arrays.fill(vis, false);
    List<List<Integer>> scc = new ArrayList<>();
    while (!st.isEmpty()) {
        int u = st.pop();
        if (!vis[u]) {
            List<Integer> comp = new ArrayList<>();
            dfs2(u, rev, vis, comp);
            scc.add(comp);
        }
    }
    return scc;
}

private static void dfs1(int u, List<List<Integer>> adj, boolean[] vis, Deque<Integer> st) {
    vis[u] = true;
    for (int v : adj.get(u)) if (!vis[v]) dfs1(v, adj, vis, st);
    st.push(u);
}

private static void dfs2(int u, List<List<Integer>> rev, boolean[] vis, List<Integer> comp) {
    vis[u] = true; comp.add(u);
    for (int v : rev.get(u)) if (!vis[v]) dfs2(v, rev, vis, comp);
}
```

### A.2 Tarjan's Algorithm (single DFS)

Track discovery time and low-link; `low[u] == disc[u]` ⇒ u roots an SCC.

```java
public static List<List<Integer>> tarjan(List<List<Integer>> adj) {
    int n = adj.size();
    int[] disc = new int[n], low = new int[n];
    boolean[] on = new boolean[n];
    Deque<Integer> st = new ArrayDeque<>();
    Arrays.fill(disc, -1);
    List<List<Integer>> res = new ArrayList<>();
    int[] time = {0};                              // per-call counter (not static!)
    for (int i = 0; i < n; i++)
        if (disc[i] == -1) dfsT(i, adj, disc, low, on, st, res, time);
    return res;
}

private static void dfsT(int u, List<List<Integer>> adj, int[] disc, int[] low,
                         boolean[] on, Deque<Integer> st, List<List<Integer>> res, int[] time) {
    disc[u] = low[u] = time[0]++;
    st.push(u); on[u] = true;

    for (int v : adj.get(u)) {
        if (disc[v] == -1) {
            dfsT(v, adj, disc, low, on, st, res, time);
            low[u] = Math.min(low[u], low[v]);
        } else if (on[v]) low[u] = Math.min(low[u], disc[v]);
    }

    if (low[u] == disc[u]) {
        List<Integer> comp = new ArrayList<>();
        while (true) {
            int v = st.pop(); on[v] = false;
            comp.add(v);
            if (v == u) break;
        }
        res.add(comp);
    }
}
```

**Bonus application**: condense SCCs into a DAG, then run topo DP (§11) on it — the standard way to do DP on graphs *with* cycles.

---

## Appendix B: Cycle Detection

### B.1 Directed: DFS 3-Coloring

WHITE = unvisited, GRAY = in current path, BLACK = finished. A back edge GRAY→GRAY = cycle.

```java
public static boolean hasCycleDirected(List<List<Integer>> adj) {
    int[] col = new int[adj.size()];
    for (int i = 0; i < adj.size(); i++)
        if (col[i] == 0 && dfsC(i, adj, col)) return true;
    return false;
}

private static boolean dfsC(int u, List<List<Integer>> adj, int[] col) {
    col[u] = 1;
    for (int v : adj.get(u)) {
        if (col[v] == 1) return true;                    // back edge → cycle
        if (col[v] == 0 && dfsC(v, adj, col)) return true;
    }
    col[u] = 2;
    return false;
}
```

(Equivalent: Kahn's returning `null` in §10.1.)

### B.2 Undirected: DFS with Parent

```java
public static boolean hasCycleUndirected(List<List<Integer>> adj) {
    boolean[] vis = new boolean[adj.size()];
    for (int i = 0; i < adj.size(); i++)
        if (!vis[i] && dfsCU(i, -1, adj, vis)) return true;
    return false;
}

private static boolean dfsCU(int u, int p, List<List<Integer>> adj, boolean[] vis) {
    vis[u] = true;
    for (int v : adj.get(u)) {
        if (v == p) continue;
        if (vis[v] || dfsCU(v, u, adj, vis)) return true;
    }
    return false;
}
```

### B.3 Undirected: Union-Find

```java
public static boolean cycleUF(int n, List<int[]> edges) {
    DSU d = new DSU(n);
    for (int[] e : edges)
        if (!d.union(e[0], e[1])) return true;   // union failed = already connected
    return false;
}
```

---

## 18. Pattern Recognition Cheat Sheet

### By Problem Type

| You see... | Think... | Section |
|------------|----------|---------|
| 2D grid, "connected regions" | Grid flood fill | 3 |
| "Nearest X to every cell" | Multi-source BFS | 4 |
| "Shortest path" + the path itself | BFS + parent array | 5 |
| "Shortest path" (weighted, non-negative) | Dijkstra | 13 |
| "Shortest path" (negative weights) | Bellman-Ford | 13 |
| "All pairs shortest path" | Floyd-Warshall | 13 |
| Weights only 0/1, or "flip at most one" | 0-1 BFS | 13 |
| States are words/strings/configurations | Implicit graph — generate neighbors | 6 |
| "Same node, different circumstances" (keys, colors) | State-space BFS (node, extra) | 7 |
| "At most K stops / with budget" | Layered shortest path | 14 |
| "Minimum cost to connect all nodes" | MST (Kruskal/Prim) | 15 |
| "Order tasks with dependencies" | Topological Sort | 10 |
| "Min semesters / min completion time" | Level-Kahn / critical path | 12 |
| DP values on a DAG (longest path, counts) | Topological DP | 11 |
| "After exactly K steps" on out-degree-1 graph | Functional graph + binary lifting | 16 |
| "Critical edges / nodes" | Bridges / Articulation Points | 16 |
| "Groups where everyone reaches everyone" | SCC | App. A |
| "Can we 2-color?" / "split into two groups" | Bipartite check | 2 |
| "Dynamic connectivity" / merging groups | DSU | 8 |
| Sizes, relations, or deletions with DSU | Advanced DSU / reverse time | 9 |
| "Has a cycle?" | DFS coloring (directed), DFS/DSU (undirected) | App. B |
| "Can player force a win?" | Backward win/lose propagation | 17 |

### By Constraint Size

| V, E range | Feasible algorithms |
|------------|---------------------|
| V ≤ 500 | Floyd-Warshall O(V³), brute force |
| V ≤ 5,000 | Bellman-Ford O(VE), O(V²) algorithms |
| V, E ≤ 10⁵ | Dijkstra, BFS, DFS, topo sort, SCC, DSU, game propagation |
| V ≤ 10⁵, E ≤ 10⁶ | Same — watch constant factors |
| V ≤ 10⁶ | BFS/DFS only, simple DSU |
| State-space search | states = V × S must fit (S = 2^keys, K+1 stops, fuel...) |
| n ≤ 20 | Bitmask DP over subsets (e.g., counting topo orders) |

### Algorithm Complexity Reference

| Algorithm | Time | Space |
|-----------|------|-------|
| BFS / DFS / flood fill | O(V + E) | O(V) |
| BFS + path reconstruction | O(V + E) | O(V) |
| Implicit/state BFS | O(V·S + E·S) | O(V·S) |
| Dijkstra | O((V + E) log V) | O(V) |
| Bellman-Ford | O(VE) | O(V) |
| Layered Bellman-Ford (K rounds) | O(K·E) | O(V) |
| Floyd-Warshall | O(V³) | O(V²) |
| 0-1 BFS | O(V + E) | O(V) |
| Kruskal | O(E log E) | O(V) |
| Prim | O((V + E) log V) | O(V) |
| Topological Sort | O(V + E) | O(V) |
| Topo DP | O(V + E · state) | O(V · state) |
| SCC (Tarjan/Kosaraju) | O(V + E) | O(V) |
| Bridges / Articulation Points | O(V + E) | O(V) |
| Bipartite Check | O(V + E) | O(V) |
| DSU (per operation) | O(α(V)) | O(V) |
| Binary lifting (build / query) | O(N log N) / O(log k) | O(N log N) |
| Game win/lose propagation | O(V + E) | O(V) |

### Decision Flowchart

```
What is the problem about?
    |
    +-- Is the input a grid?
    |       +-- Connected regions? -------------------> Flood fill (§3)
    |       +-- Nearest source per cell? --------------> Multi-source BFS (§4)
    |
    +-- Finding shortest distances?
    |       +-- Unweighted? ---------------------------> BFS (+ parents, §5)
    |       +-- Non-negative weights? -----------------> Dijkstra (§13)
    |       +-- Negative weights? ---------------------> Bellman-Ford (§13)
    |       +-- All pairs, V <= 500? ------------------> Floyd-Warshall (§13)
    |       +-- Weights 0 or 1? -----------------------> 0-1 BFS (§13)
    |       +-- DAG? ----------------------------------> Topo sort + relax (§13)
    |       +-- At most K stops / budget? -------------> Layered states (§14)
    |       +-- Node + extra circumstance? ------------> State-space BFS (§7)
    |
    +-- Nodes are strings / configurations? -----------> Implicit graph (§6)
    |
    +-- Connecting components?
    |       +-- Minimum cost? -------------------------> MST (§15)
    |       +-- Dynamic union/check? ------------------> DSU (§8); advanced (§9)
    |
    +-- Ordering / dependencies?
    |       +-- One valid order? ----------------------> Topological sort (§10)
    |       +-- Min rounds / min time? ----------------> §12
    |       +-- DP values on the DAG? -----------------> Topo DP (§11)
    |
    +-- "After K steps" / exactly one out-edge? -------> Functional graph (§16.1)
    |
    +-- Structural analysis?
    |       +-- Strongly connected groups? ------------> SCC (App. A)
    |       +-- Critical edges? -----------------------> Bridges (§16.2)
    |       +-- Critical nodes? -----------------------> Articulation points (§16.2)
    |       +-- Two-colorable? ------------------------> Bipartite check (§2)
    |       +-- Has a cycle? --------------------------> App. B (or Kahn = null)
    |
    +-- Game / adversarial movement? ------------------> Backward propagation (§17)
    |
    +-- Counting paths / structures on a DAG? ---------> Topo DP with mod (§11)
```
