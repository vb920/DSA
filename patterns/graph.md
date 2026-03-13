# Graph Problem Patterns — Comprehensive Guide

Graphs model relationships: cities connected by roads, users in a social network, tasks with dependencies. This guide covers **every major graph technique** for competitive programming and interviews.

---

## Quick Navigation: "I need to..."

| I need to... | Technique | Section |
|--------------|-----------|---------|
| Traverse / explore a graph | BFS / DFS | [1](#1-graph-traversals) |
| Find **shortest path** | Dijkstra / Bellman-Ford / Floyd / 0-1 BFS | [2](#2-shortest-paths) |
| Find **minimum spanning tree** | Kruskal / Prim | [3](#3-minimum-spanning-tree) |
| Process nodes in **dependency order** | Topological Sort | [4](#4-topological-sort) |
| Find **strongly connected components** | Tarjan / Kosaraju | [5](#5-strongly-connected-components) |
| Find **bridges / articulation points** | Tarjan's bridge-finding | [6](#6-bridges-and-articulation-points) |
| Check if graph is **bipartite** | BFS/DFS 2-coloring | [7](#7-bipartite-graphs) |
| Detect **cycles** | DFS coloring / Union-Find | [8](#8-cycle-detection) |
| Manage **connected components** dynamically | Union-Find (DSU) | [9](#9-union-find-dsu) |
| Handle **multi-source** shortest path | Multi-source BFS / virtual node | [10](#10-multi-source-and-virtual-nodes) |
| DP on a graph | DP on DAG / shortest path DP | [11](#11-dp-on-graphs) |

---

## Table of Contents

1. [Graph Traversals](#1-graph-traversals)
2. [Shortest Paths](#2-shortest-paths)
3. [Minimum Spanning Tree](#3-minimum-spanning-tree)
4. [Topological Sort](#4-topological-sort)
5. [Strongly Connected Components](#5-strongly-connected-components)
6. [Bridges and Articulation Points](#6-bridges-and-articulation-points)
7. [Bipartite Graphs](#7-bipartite-graphs)
8. [Cycle Detection](#8-cycle-detection)
9. [Union-Find (DSU)](#9-union-find-dsu)
10. [Multi-Source and Virtual Nodes](#10-multi-source-and-virtual-nodes)
11. [DP on Graphs](#11-dp-on-graphs)
12. [Pattern Recognition Cheat Sheet](#12-pattern-recognition-cheat-sheet)

---

## 0. Graph Representations

Before anything, know how to store a graph.

### Adjacency List (most common)

```java
int n = 5;
List<List<Integer>> adj = new ArrayList<>();
for (int i = 0; i < n; i++) adj.add(new ArrayList<>());
adj.get(0).add(1); // edge 0 -> 1
adj.get(1).add(0); // undirected

// Weighted graph adjacency list
tatic class Edge {
    int to;
    int w;
    Edge(int to, int w) { this.to = to; this.w = w; }
}
List<List<Edge>> wadj = new ArrayList<>();
for (int i = 0; i < n; i++) wadj.add(new ArrayList<>());
wadj.get(0).add(new Edge(1, 10));

```

### Adjacency Matrix

```java
int n = 5;
long INF = (long)1e18;
long[][] dist = new long[n][n];
for (int i = 0; i < n; i++) Arrays.fill(dist[i], INF);
dist[0][1] = 10;
for (int i = 0; i < n; i++) dist[i][i] = 0;

```

### Edge List

```java
class Edge3 {
    long w;
    int u, v;
    Edge3(long w, int u, int v) { this.w = w; this.u = u; this.v = v; }
}
List<Edge3> edges = new ArrayList<>();
edges.add(new Edge3(10, 0, 1));
edges.sort(Comparator.comparingLong(e -> e.w));

```

### When to Use Which

| Representation | Space | Check edge? | Iterate neighbors | Best for |
|---------------|-------|-------------|-------------------|----------|
| Adjacency List | O(V+E) | O(degree) | O(degree) | Most problems |
| Adjacency Matrix | O(V^2) | O(1) | O(V) | Dense, Floyd-Warshall |
| Edge List | O(E) | O(E) | O(E) | Kruskal's, edge sorting |

---

## 1. Graph Traversals

### BFS (Breadth-First Search)

Explores level by level. Finds **shortest path in unweighted graphs**.

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
                q.add(v);
            }
        }
    }
    return dist;
}

```

### DFS (Depth-First Search)

Explores as deep as possible. Used for cycle detection, topological sort, SCC, bridges.

```java
public static void dfs(int u, List<List<Integer>> adj, boolean[] vis) {
    vis[u] = true;
    for (int v : adj.get(u)) if (!vis[v]) dfs(v, adj, vis);
}

```

### Iterative DFS (for large graphs in Python)

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

### BFS vs DFS

| | BFS | DFS |
|--|-----|-----|
| Data structure | Queue | Stack / recursion |
| Finds shortest path? | Yes (unweighted) | No |
| Memory | O(width of graph) | O(depth of graph) |
| Use for | Shortest path, level-order | Cycle detection, topo sort, SCC |

---

## 2. Shortest Paths

The most important graph family. Five algorithms for different situations.

### Algorithm Selection Guide

```
What kind of graph?
    |
    +-- Unweighted? --> BFS  O(V + E)
    |
    +-- Non-negative weights? --> Dijkstra  O((V + E) log V)
    |
    +-- Negative weights, no negative cycle? --> Bellman-Ford  O(VE)
    |
    +-- All pairs? --> Floyd-Warshall  O(V^3)
    |
    +-- Weights are only 0 and 1? --> 0-1 BFS  O(V + E)
    |
    +-- DAG? --> Topological Sort + relaxation  O(V + E)
```

### 2.1 Dijkstra's Algorithm

**When**: Non-negative edge weights, single source.

```java
static class PEdge {
    int to, w;
    PEdge(int t, int w) { this.to = t; this.w = w; }
}

public static long[] dijkstra(int src, List<List<PEdge>> adj) {
    int n = adj.size();
    long[] dist = new long[n];
    Arrays.fill(dist, Long.MAX_VALUE);
    dist[src] = 0;
    PriorityQueue<long[]> pq = new PriorityQueue<>(Comparator.comparingLong(a -> a[0]));
    pq.add(new long[]{0, src});

    while (!pq.isEmpty()) {
        long[] cur = pq.poll();
        long d = cur[0];
        int u = (int)cur[1];
        if (d != dist[u]) continue;
        for (PEdge e : adj.get(u)) {
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

**Why it works**: Always processes the unvisited node with the smallest distance. Since all weights are non-negative, once a node is processed, its distance is final.

**Common mistake**: Using Dijkstra with negative weights. It fails because a "processed" node might get a shorter path later through a negative edge.

### 2.2 Bellman-Ford

**When**: Negative edge weights allowed. Detects negative cycles.

```java
static class BFEdge {
    int u, v, w;
    BFEdge(int u, int v, int w) { this.u = u; this.v = v; this.w = w; }
}

public static long[] bellmanFord(int src, int n, List<BFEdge> edges) {
    long[] dist = new long[n];
    Arrays.fill(dist, Long.MAX_VALUE);
    dist[src] = 0;

    for (int i = 0; i < n - 1; i++) {
        for (BFEdge e : edges) {
            if (dist[e.u] != Long.MAX_VALUE && dist[e.u] + e.w < dist[e.v])
                dist[e.v] = dist[e.u] + e.w;
        }
    }
    return dist;
}

```

**Why N-1 iterations?** The shortest path has at most N-1 edges. Each iteration relaxes paths of one more edge. If the Nth iteration still improves something, there's a negative cycle.

### 2.3 Floyd-Warshall

**When**: All-pairs shortest paths. Small graph (V <= 500).

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

**Why it works**: `dp[i][j][k]` = shortest path from i to j using only nodes 0..k as intermediates. The three nested loops consider each possible intermediate node.

**Bonus**: Detect negative cycles by checking if `dist[i][i] < 0` for any i.

### 2.4 0-1 BFS

**When**: Edge weights are only **0 or 1**. Like BFS but uses a deque.

```java
static class ZEdge {
    int to, w;
    ZEdge(int t, int w) { this.to = t; this.w = w; }
}

public static long[] zeroOneBFS(int src, List<List<ZEdge>> adj) {
    int n = adj.size();
    long[] dist = new long[n];
    Arrays.fill(dist, Long.MAX_VALUE);
    dist[src] = 0;
    Deque<Integer> dq = new ArrayDeque<>();
    dq.add(src);

    while (!dq.isEmpty()) {
        int u = dq.pollFirst();
        for (ZEdge e : adj.get(u)) {
            long nd = dist[u] + e.w;
            if (nd < dist[e.to]) {
                dist[e.to] = nd;
                if (e.w == 0) dq.addFirst(e.to);
                else dq.addLast(e.to);
            }
        }
    }
    return dist;
}

```

**Why it works**: Weight-0 edges don't increase distance, so those neighbors should be processed at the same "level" as the current node (front of deque). Weight-1 edges go to the next level (back of deque). This is exactly BFS with two levels of priority.

### 2.5 Shortest Path on DAG

**When**: Directed acyclic graph. Process in topological order.

```java
public static long[] dagShortestPath(int src, List<List<PEdge>> adj, int[] topo) {
    int n = adj.size();
    long[] dist = new long[n];
    Arrays.fill(dist, Long.MAX_VALUE);
    dist[src] = 0;

    for (int u : topo) {
        if (dist[u] == Long.MAX_VALUE) continue;
        for (PEdge e : adj.get(u))
            dist[e.to] = Math.min(dist[e.to], dist[u] + e.w);
    }
    return dist;
}

```

### Shortest Path Summary

| Algorithm | Time | Space | Weights | Negative cycle? |
|-----------|------|-------|---------|----------------|
| BFS | O(V+E) | O(V) | Unweighted | N/A |
| Dijkstra | O((V+E)log V) | O(V) | Non-negative | N/A |
| Bellman-Ford | O(VE) | O(V) | Any | Detects |
| Floyd-Warshall | O(V^3) | O(V^2) | Any | Detects |
| 0-1 BFS | O(V+E) | O(V) | 0 or 1 | N/A |
| DAG relaxation | O(V+E) | O(V) | Any (DAG) | N/A (no cycles) |

---

## 3. Minimum Spanning Tree

**Problem**: Connect all nodes with minimum total edge weight.

### 3.1 Kruskal's Algorithm

**Idea**: Sort edges by weight, greedily add the lightest edge that doesn't create a cycle. Uses Union-Find.

```java
class DSU {
    int[] p, r;
    DSU(int n) {
        p = new int[n]; r = new int[n];
        for (int i = 0; i < n; i++) p[i] = i;
    }
    int find(int x) {
        if (p[x] != x) p[x] = find(p[x]);
        return p[x];
    }
    boolean union(int a, int b) {
        a = find(a); b = find(b);
        if (a == b) return false;
        if (r[a] < r[b]) { int t = a; a = b; b = t; }
        p[b] = a;
        if (r[a] == r[b]) r[a]++;
        return true;
    }
}

class MEdge {
    int u, v, w;
    MEdge(int u, int v, int w) { this.u = u; this.v = v; this.w = w; }
}

public static long kruskal(int n, List<MEdge> edges) {
    edges.sort(Comparator.comparingInt(e -> e.w));
    DSU d = new DSU(n);
    long ans = 0;

    for (MEdge e : edges) if (d.union(e.u, e.v)) ans += e.w;
    return ans;
}

```

### 3.2 Prim's Algorithm

**Idea**: Grow the MST from a starting node. Always add the lightest edge connecting the MST to a non-MST node.

```java
public static long prim(int start, List<List<PEdge>> adj) {
    int n = adj.size();
    boolean[] vis = new boolean[n];
    PriorityQueue<long[]> pq = new PriorityQueue<>(Comparator.comparingLong(a -> a[0]));
    pq.add(new long[]{0, start});
    long sum = 0;

    while (!pq.isEmpty()) {
        long[] cur = pq.poll();
        int u = (int)cur[1];
        if (vis[u]) continue;
        vis[u] = true;
        sum += cur[0];
        for (PEdge e : adj.get(u)) if (!vis[e.to]) pq.add(new long[]{e.w, e.to});
    }
    return sum;
}

```

### Kruskal vs Prim

| | Kruskal | Prim |
|--|---------|------|
| Time | O(E log E) | O((V+E) log V) |
| Best for | Sparse graphs (E ~ V) | Dense graphs (E ~ V^2) |
| Data structure | Union-Find | Priority Queue |
| Edge list needed | Yes | No (adjacency list) |

### MST Properties

| Property | Explanation |
|----------|-------------|
| Cut Property | Lightest edge crossing any cut is in MST |
| Cycle Property | Heaviest edge in any cycle is NOT in MST |
| Uniqueness | MST is unique if all edge weights are distinct |
| N-1 edges | MST of N nodes always has exactly N-1 edges |

---

## 4. Topological Sort

**Problem**: Order nodes so that for every edge u -> v, u comes before v. Only works on **DAGs** (directed acyclic graphs).

### 4.1 Kahn's Algorithm (BFS-based)

```java
public static int[] topoSort(List<List<Integer>> adj) {
    int n = adj.size();
    int[] indeg = new int[n];
    for (int u = 0; u < n; u++) for (int v : adj.get(u)) indeg[v]++;

    Deque<Integer> q = new ArrayDeque<>();
    for (int i = 0; i < n; i++) if (indeg[i] == 0) q.add(i);

    int[] ord = new int[n]; int idx = 0;
    while (!q.isEmpty()) {
        int u = q.poll(); ord[idx++] = u;
        for (int v : adj.get(u)) if (--indeg[v] == 0) q.add(v);
    }
    return (idx == n) ? ord : null;
}

```

### 4.2 DFS-based

```java
public static void dfsTopo(int u, List<List<Integer>> adj, boolean[] vis, Deque<Integer> st) {
    vis[u] = true;
    for (int v : adj.get(u)) if (!vis[v]) dfsTopo(v, adj, vis, st);
    st.push(u);
}

```

### Applications

| Application | How topo sort helps |
|-------------|-------------------|
| Course scheduling | Prerequisites form a DAG |
| Build systems (Make) | Dependencies must be built first |
| Shortest/longest path in DAG | Relax edges in topo order |
| DP on DAG | Process states in topo order |
| Cycle detection (directed) | If topo sort fails, cycle exists |

---

## 5. Strongly Connected Components

**Problem**: Find maximal groups where every node can reach every other node in a **directed graph**.

```
    1 --> 2 --> 5 --> 6
    ^    /      ^    /
    |   v       |   v
    4 <-3       8 <-7

SCC 1: {1, 2, 3, 4}   (cycle: 1->2->3->4->1)
SCC 2: {5, 6, 7, 8}   (cycle: 5->6->7->8->5)
```

### 5.1 Kosaraju's Algorithm

**Idea**: Two DFS passes. First on original graph (get finish order), then on reversed graph (in reverse finish order).

```java
public static List<List<Integer>> kosaraju(List<List<Integer>> adj) {
    int n = adj.size();
    boolean[] vis = new boolean[n];
    Deque<Integer> st = new ArrayDeque<>();

    // 1st pass
    for (int i = 0; i < n; i++) if (!vis[i]) dfs1(i, adj, vis, st);

    // Build reverse
    List<List<Integer>> rev = new ArrayList<>();
    for (int i = 0; i < n; i++) rev.add(new ArrayList<>());
    for (int u = 0; u < n; u++) for (int v : adj.get(u)) rev.get(v).add(u);

    Arrays.fill(vis, false);
    List<List<Integer>> scc = new ArrayList<>();

    // 2nd pass
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

### 5.2 Tarjan's Algorithm

**Idea**: Single DFS. Track discovery time and the lowest reachable discovery time (low-link). When `low[u] == disc[u]`, node u is the root of an SCC.

```java
static int timeTarjan;

public static List<List<Integer>> tarjan(List<List<Integer>> adj) {
    int n = adj.size();
    int[] disc = new int[n], low = new int[n];
    boolean[] on = new boolean[n];
    Deque<Integer> st = new ArrayDeque<>();
    Arrays.fill(disc, -1);
    List<List<Integer>> res = new ArrayList<>();

    for (int i = 0; i < n; i++) if (disc[i] == -1) dfsT(i, adj, disc, low, on, st, res);
    return res;
}

private static void dfsT(int u, List<List<Integer>> adj, int[] disc, int[] low,
                         boolean[] on, Deque<Integer> st, List<List<Integer>> res) {
    disc[u] = low[u] = timeTarjan++;
    st.push(u); on[u] = true;

    for (int v : adj.get(u)) {
        if (disc[v] == -1) {
            dfsT(v, adj, disc, low, on, st, res);
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

---

## 6. Bridges and Articulation Points

### Bridge

An edge whose removal **disconnects** the graph.

### Articulation Point

A node whose removal disconnects the graph.

```
    1 --- 2 --- 5 --- 6
    |    /      |    /
    |   /       |   /
    3 -/        7 -/
         ^
    bridge: 2-5 (removing it disconnects the two halves)
    articulation points: 2, 5
```

### Finding Bridges

```java
public static List<int[]> bridges(List<List<Integer>> adj) {
    int n = adj.size();
    int[] disc = new int[n], low = new int[n];
    Arrays.fill(disc, -1);
    List<int[]> res = new ArrayList<>();
    int[] time = {0};

    for (int i = 0; i < n; i++) if (disc[i] == -1) dfsB(i, -1, adj, disc, low, time, res);
    return res;
}

private static void dfsB(int u, int p, List<List<Integer>> adj, int[] disc, int[] low,
                         int[] time, List<int[]> res) {
    disc[u] = low[u] = time[0]++;
    for (int v : adj.get(u)) {
        if (v == p) continue;
        if (disc[v] == -1) {
            dfsB(v, u, adj, disc, low, time, res);
            low[u] = Math.min(low[u], low[v]);
            if (low[v] > disc[u]) res.add(new int[]{u, v});
        } else low[u] = Math.min(low[u], disc[v]);
    }
}

```

### Finding Articulation Points

```java
public static List<Integer> articulation(List<List<Integer>> adj) {
    int n = adj.size();
    int[] disc = new int[n], low = new int[n];
    boolean[] ap = new boolean[n];
    Arrays.fill(disc, -1);
    int[] time = {0};

    for (int i = 0; i < n; i++) if (disc[i] == -1) dfsA(i, -1, adj, disc, low, ap, time);

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
    if (p == -1 && child > 1) ap[u] = true;
}

```

### Understanding `low[v]`

`low[v]` = the earliest discovery time reachable from v's subtree via back edges. If `low[v] > disc[u]`, no back edge from v's subtree reaches above u, so edge u-v is a bridge.

```
disc:     0    1    2    3
          u -- a -- b -- c
          |              |
          +--------------+  (back edge c -> u)

low[c] = 0 (can reach u via back edge)
low[b] = 0 (inherits from c)
low[a] = 0 (inherits from b)

Edge u-a: low[a]=0 not > disc[u]=0  -> NOT a bridge (correct: back edge saves it)
```

---

## 7. Bipartite Graphs

**Problem**: Can we 2-color the graph such that no adjacent nodes share a color?

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
        if (color[i] != -1) continue;
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
| Task assignment (workers to jobs) | Bipartite matching |
| Graph coloring (2 colors) | Bipartite check |
| Building teams (no conflicts) | 2-coloring |
| Maximum independent set on bipartite | Konig's theorem |

---

## 8. Cycle Detection

### Directed Graph: DFS Coloring

Three states: WHITE (unvisited), GRAY (in current DFS path), BLACK (finished).

```java
public static boolean hasCycleDirected(List<List<Integer>> adj) {
    int n = adj.size();
    int[] col = new int[n];

    for (int i = 0; i < n; i++) if (col[i] == 0)
        if (dfsC(i, adj, col)) return true;
    return false;
}

private static boolean dfsC(int u, List<List<Integer>> adj, int[] col) {
    col[u] = 1;
    for (int v : adj.get(u)) {
        if (col[v] == 1) return true;
        if (col[v] == 0 && dfsC(v, adj, col)) return true;
    }
    col[u] = 2;
    return false;
}

```

**Back edge** (GRAY -> GRAY) = cycle. Cross edge (GRAY -> BLACK) = no cycle.

### Undirected Graph: DFS with Parent

```java
public static boolean hasCycleUndirected(List<List<Integer>> adj) {
    int n = adj.size();
    boolean[] vis = new boolean[n];

    for (int i = 0; i < n; i++) if (!vis[i])
        if (dfsCU(i, -1, adj, vis)) return true;
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

### Undirected Graph: Union-Find

```java
public static boolean cycleUF(int n, List<int[]> edges) {
    DSU d = new DSU(n);
    for (int[] e : edges) {
        if (!d.union(e[0], e[1])) return true;
    }
    return false;
}

---

## 9. Union-Find (DSU)

**Problem**: Dynamically merge sets and check if two elements are in the same set.

### Implementation

```java
class DSU2 {
    int[] p, r;
    DSU2(int n) {
        p = new int[n]; r = new int[n];
        for (int i = 0; i < n; i++) p[i] = i;
    }
    int find(int x) {
        if (p[x] != x) p[x] = find(p[x]);
        return p[x];
    }
    boolean union(int a, int b) {
        a = find(a); b = find(b);
        if (a == b) return false;
        if (r[a] < r[b]) { int t = a; a = b; b = t; }
        p[b] = a;
        if (r[a] == r[b]) r[a]++;
        return true;
    }
}

```

### Complexity

| Operation | Time |
|-----------|------|
| find | O(alpha(N)) ~ O(1) amortized |
| union | O(alpha(N)) ~ O(1) amortized |

`alpha(N)` is the inverse Ackermann function --- grows so slowly it's effectively constant (alpha(10^80) = 4).

### Applications

| Problem | DSU usage |
|---------|----------|
| Kruskal's MST | Check if edge creates cycle |
| Dynamic connectivity | Are u and v connected? |
| Number of components | Track `components` counter |
| Cycle detection (undirected) | Union returns false = cycle |
| Offline LCA (Tarjan's) | Merge subtrees during DFS |

---

## 10. Multi-Source and Virtual Nodes

### Multi-Source BFS

**Problem**: Find the shortest distance from **any source** to each node.

Simply start BFS with all sources in the queue at distance 0.

```java
public static int[] multiSourceBFS(List<Integer> sources, List<List<Integer>> adj) {
    int n = adj.size();
    int[] dist = new int[n];
    Arrays.fill(dist, -1);
    Deque<Integer> q = new ArrayDeque<>();

    for (int s : sources) {
        dist[s] = 0;
        q.add(s);
    }

    while (!q.isEmpty()) {
        int u = q.poll();
        for (int v : adj.get(u)) if (dist[v] == -1) {
            dist[v] = dist[u] + 1;
            q.add(v);
        }
    }
    return dist;
}

```

### Virtual Source / Sink

**Problem**: Shortest path from any of multiple sources, or max flow with multiple sources/sinks.

**Trick**: Create a virtual node connected to all sources (weight 0). Run single-source algorithm from virtual node.

```
Real graph:            With virtual source:

  S1    S2    S3         V (virtual)
  |     |     |         /|\
  v     v     v        / | \
  A --- B --- C      S1  S2  S3   (0-weight edges)
                      |   |   |
                      A   B   C
```

```java
// Add an extra node as virtual source
int virtual = adj.size();
adj.add(new ArrayList<>());
for (int s : sources) adj.get(virtual).add(s);

long[] dist = dijkstra(virtual, adj);

```

---

## 11. DP on Graphs

### DP on DAG

Process nodes in topological order. Most DP on graphs requires no cycles.

```java
# Longest path in DAG
public static long longestPath(List<List<PEdge>> adj, int[] topo) {
    int n = adj.size();
    long[] dp = new long[n];

    for (int u : topo)
        for (PEdge e : adj.get(u))
            dp[e.to] = Math.max(dp[e.to], dp[u] + e.w);

    long ans = 0;
    for (long x : dp) ans = Math.max(ans, x);
    return ans;
}

```

### Counting Paths in DAG

```java
public static long countPaths(List<List<Integer>> adj, int src, int dst, int[] topo) {
    int n = adj.size();
    long[] dp = new long[n];
    dp[src] = 1;

    for (int u : topo)
        for (int v : adj.get(u)) dp[v] += dp[u];

    return dp[dst];
}

```

### Shortest Path as DP

Dijkstra is essentially DP with a priority queue:

```
dp[v] = min(dp[u] + weight(u, v)) for all edges (u, v)
```

Bellman-Ford is the brute-force DP:

```
dp[k][v] = min cost to reach v using at most k edges
dp[k][v] = min(dp[k-1][u] + weight(u, v)) for all edges
```


---

## 12. Pattern Recognition Cheat Sheet

### By Problem Type

| You see... | Think... | Section |
|------------|----------|---------|
| "Shortest path" (unweighted) | BFS | 1 |
| "Shortest path" (weighted, non-negative) | Dijkstra | 2 |
| "Shortest path" (negative weights) | Bellman-Ford | 2 |
| "All pairs shortest path" | Floyd-Warshall | 2 |
| "Minimum cost to connect all nodes" | MST (Kruskal/Prim) | 3 |
| "Order tasks with dependencies" | Topological Sort | 4 |
| "Find cycles in directed graph" | DFS coloring or Topo Sort | 8 |
| "Groups where everyone can reach everyone" | SCC (Tarjan/Kosaraju) | 5 |
| "Critical edges / nodes" | Bridges / Articulation Points | 6 |
| "Can we 2-color?" or "split into two groups" | Bipartite check | 7 |
| "Dynamic connectivity" | Union-Find (DSU) | 9 |
| "Multiple starting points" | Multi-source BFS / virtual node | 10 |
| "Longest path" or "count paths" | DP on DAG | 11 |

### By Constraint Size

| V, E range | Feasible algorithms |
|------------|-------------------|
| V <= 500 | Floyd-Warshall O(V^3), Brute force |
| V <= 5,000 | Bellman-Ford O(VE), O(V^2) matching |
| V <= 10^5, E <= 10^5 | Dijkstra, BFS, DFS, Topo Sort, SCC, DSU |
| V <= 10^5, E <= 10^6 | Same as above (watch constant factors) |
| V <= 10^6 | BFS/DFS only, simple DSU |

### Algorithm Complexity Reference

| Algorithm | Time | Space |
|-----------|------|-------|
| BFS / DFS | O(V + E) | O(V) |
| Dijkstra | O((V + E) log V) | O(V) |
| Bellman-Ford | O(VE) | O(V) |
| Floyd-Warshall | O(V^3) | O(V^2) |
| 0-1 BFS | O(V + E) | O(V) |
| Kruskal | O(E log E) | O(V) |
| Prim | O((V + E) log V) | O(V) |
| Topological Sort | O(V + E) | O(V) |
| SCC (Tarjan/Kosaraju) | O(V + E) | O(V) |
| Bridges / APs | O(V + E) | O(V) |
| Bipartite Check | O(V + E) | O(V) |
| DSU (per operation) | O(alpha(V)) | O(V) |

### Decision Flowchart

What is the problem about?
    |
    +-- Finding shortest distances?
    |       |
    |       +-- Unweighted? --> BFS
    |       +-- Non-negative weights? --> Dijkstra
    |       +-- Negative weights? --> Bellman-Ford
    |       +-- All pairs (V <= 500)? --> Floyd-Warshall
    |       +-- Weights 0 or 1? --> 0-1 BFS
    |       +-- DAG? --> Topo sort + relax
    |
    +-- Connecting components?
    |       |
    |       +-- Minimum cost? --> MST (Kruskal/Prim)
    |       +-- Dynamic union/check? --> DSU
    |
    +-- Ordering / dependencies?
    |       |
    |       +-- Linear order? --> Topological Sort
    |
    +-- Structural analysis?
    |       |
    |       +-- Strongly connected groups? --> SCC
    |       +-- Critical edges? --> Bridges
    |       +-- Critical nodes? --> Articulation Points
    |       +-- Two-colorable? --> Bipartite check
    |       +-- Has cycle? --> DFS coloring / DSU
    |
    +-- Counting / DP?
            |
            +-- Has cycles? --> Condense SCCs to DAG, then DP
            +-- DAG? --> DP in topological order
