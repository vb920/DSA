

# Tree Problem Patterns 


## Quick Navigation: "I need to..."

| I need to... | Technique | Section |
|--------------|-----------|---------|
| Traverse a tree | DFS / BFS | [1](#1-tree-traversals) |
| Query values in a **subtree** | Euler Tour + Segment Tree | [2](#2-euler-tour-subtree-queries) |
| Find **Lowest Common Ancestor** | Binary Lifting / Euler+RMQ | [3](#3-lowest-common-ancestor) |
| Compute DP for **every node as root** | Rerooting DP | [4](#4-rerooting-dp) |
| Find **diameter / center** of tree | Two-BFS or Tree DP | [5](#5-tree-diameter-and-center) |
| Compute DP on subtrees | Tree DP | [6](#6-tree-dp-patterns) |
| Tree Properties| Basic Techniques |[7](#7-basic-tree-properties) |

---

## Table of Contents

1. [Tree Traversals](#1-tree-traversals)
2. [Euler Tour (Subtree Queries)](#2-euler-tour-subtree-queries)
3. [Lowest Common Ancestor](#3-lowest-common-ancestor)
4. [Rerooting DP](#4-rerooting-dp)
5. [Tree Diameter and Center](#5-tree-diameter-and-center)
6. [Tree DP Patterns](#6-tree-dp-patterns)
7. [Tree Properties](#7-basic-tree-properties)
8. [Pattern Recognition Cheat Sheet](#8-pattern-recognition-cheat-sheet)
---

***

## 1) Tree Traversals

**Invariant.** In DFS, on *return* from `dfs(u,parent)`, all children’s work is complete (post‑order facts are ready). In BFS, distances grow by +1 level at a time.

```
Tree:       1
           / \
          2   3
         / \
        4   5

Pre-order:  1, 2, 4, 5, 3  (enter order — top down)
Post-order: 4, 5, 2, 3, 1  (leave order — bottom up)
```
1.  **Generic graph / tree via edges** (so you can paste into any graph/tree problem that gives `n` and `edges`)
2.  **Binary‑tree traversals** (so you can paste into standard `TreeNode` problems)
***

## ✅ Option A — Graph / (Undirected) Tree Traversal Templates

```java
import java.util.*;

class Solution {

    /* -------------------- Adjacency Builder -------------------- */
    // LeetCode often gives you: int n, int[][] edges
    // This builds an undirected adjacency list.
    private List<Integer>[] buildAdj(int n, int[][] edges) {
        List<Integer>[] adj = new ArrayList[n];
        for (int i = 0; i < n; i++) adj[i] = new ArrayList<>();
        for (int[] e : edges) {
            int u = e[0], v = e[1];
            adj[u].add(v);
            adj[v].add(u);
        }
        return adj;
    }

    /* -------------------- Recursive DFS (pre + post) -------------------- */
    // Returns both preorder and postorder (useful for narration/verification).
    private void dfsRec(int u, int p, List<Integer>[] adj,
                        List<Integer> preorder, List<Integer> postorder) {
        preorder.add(u);                         // PRE-ORDER work
        for (int v : adj[u]) {
            if (v == p) continue;
            dfsRec(v, u, adj, preorder, postorder);
        }
        postorder.add(u);                        // POST-ORDER work
    }

    // Example callable: returns preorder of a connected tree/graph from root
    public List<Integer> dfsPreorder(int n, int[][] edges, int root) {
        List<Integer>[] adj = buildAdj(n, edges);
        List<Integer> pre = new ArrayList<>();
        List<Integer> post = new ArrayList<>(); // if you also need post
        dfsRec(root, -1, adj, pre, post);
        return pre;
    }

    /* -------------------- BFS (single-source distances) -------------------- */
    // Returns dist[] with -1 for unreachable nodes (typical LeetCode BFS pattern).
    public int[] bfsDistances(int n, int[][] edges, int root) {
        List<Integer>[] adj = buildAdj(n, edges);
        int[] dist = new int[n];
        Arrays.fill(dist, -1);
        ArrayDeque<Integer> q = new ArrayDeque<>();
        dist[root] = 0;
        q.add(root);

        while (!q.isEmpty()) {
            int u = q.removeFirst();
            for (int v : adj[u]) {
                if (dist[v] == -1) {
                    dist[v] = dist[u] + 1;
                    q.addLast(v);
                }
            }
        }
        return dist;
    }

    /* -------------------- Iterative DFS (pre, optional post) -------------------- */
    // Preorder using a manual stack with a visited-flag frame.
    // If you also want postorder, collect it where indicated.
    public List<Integer> dfsIterativePre(int n, int[][] edges, int root) {
        List<Integer>[] adj = buildAdj(n, edges);
        List<Integer> pre = new ArrayList<>();
        // List<Integer> post = new ArrayList<>(); // uncomment if needed

        // frame: (node, parent, visitedFlag)
        ArrayDeque<int[]> st = new ArrayDeque<>();
        st.push(new int[]{root, -1, 0});

        while (!st.isEmpty()) {
            int[] f = st.pop();
            int u = f[0], p = f[1], visited = f[2];
            if (visited == 1) {
                // post.add(u); // collect postorder here if desired
                continue;
            }
            pre.add(u);
            st.push(new int[]{u, p, 1});  // schedule post-visit
            // Push neighbors (any order is fine; reverse for a specific order)
            for (int v : adj[u]) {
                if (v != p) st.push(new int[]{v, u, 0});
            }
        }
        return pre;
    }
}
```

### What changed vs your original

*   Added **`buildAdj`** so you can drop this into problems that give `n` and `edges`.
*   Kept your **pre/post placement** exactly, but exposed as re‑usable methods.
*   Removed global/static state and wrapped inside **`class Solution`**, which LeetCode expects.
*   Kept `ArrayDeque` and `-1` distance convention (LeetCode‑friendly).

***

## ✅ Option B — Binary Tree Traversal Templates (for `TreeNode`)

Use these when LeetCode provides the `TreeNode` definition.  
(**Do not** redefine `TreeNode`—LeetCode includes it.)

```java
import java.util.*;

class Solution {

    /* -------------------- Preorder (recursive) -------------------- */
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        preorder(root, res);
        return res;
    }
    private void preorder(TreeNode node, List<Integer> res) {
        if (node == null) return;
        res.add(node.val);
        preorder(node.left, res);
        preorder(node.right, res);
    }

    /* -------------------- Inorder (recursive) -------------------- */
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        inorder(root, res);
        return res;
    }
    private void inorder(TreeNode node, List<Integer> res) {
        if (node == null) return;
        inorder(node.left, res);
        res.add(node.val);
        inorder(node.right, res);
    }

    /* -------------------- Postorder (recursive) -------------------- */
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        postorder(root, res);
        return res;
    }
    private void postorder(TreeNode node, List<Integer> res) {
        if (node == null) return;
        postorder(node.left, res);
        postorder(node.right, res);
        res.add(node.val);
    }

    /* -------------------- Level Order (BFS) -------------------- */
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if (root == null) return res;
        ArrayDeque<TreeNode> q = new ArrayDeque<>();
        q.add(root);
        while (!q.isEmpty()) {
            int sz = q.size();
            List<Integer> level = new ArrayList<>(sz);
            for (int i = 0; i < sz; i++) {
                TreeNode cur = q.removeFirst();
                level.add(cur.val);
                if (cur.left != null) q.addLast(cur.left);
                if (cur.right != null) q.addLast(cur.right);
            }
            res.add(level);
        }
        return res;
    }

    /* -------------------- Preorder (iterative) -------------------- */
    public List<Integer> preorderTraversalIterative(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if (root == null) return res;
        ArrayDeque<TreeNode> st = new ArrayDeque<>();
        st.push(root);
        while (!st.isEmpty()) {
            TreeNode node = st.pop();
            res.add(node.val);
            // push right first so left is processed first
            if (node.right != null) st.push(node.right);
            if (node.left != null) st.push(node.left);
        }
        return res;
    }

    /* -------------------- Inorder (iterative) -------------------- */
    public List<Integer> inorderTraversalIterative(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        ArrayDeque<TreeNode> st = new ArrayDeque<>();
        TreeNode cur = root;
        while (cur != null || !st.isEmpty()) {
            while (cur != null) {
                st.push(cur);
                cur = cur.left;
            }
            cur = st.pop();
            res.add(cur.val);
            cur = cur.right;
        }
        return res;
    }

    /* -------------------- Postorder (iterative, one stack) -------------------- */
    public List<Integer> postorderTraversalIterative(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        ArrayDeque<TreeNode> st = new ArrayDeque<>();
        TreeNode cur = root, last = null;
        while (cur != null || !st.isEmpty()) {
            if (cur != null) {
                st.push(cur);
                cur = cur.left;
            } else {
                TreeNode peek = st.peek();
                if (peek.right != null && last != peek.right) {
                    cur = peek.right; // go right subtree
                } else {
                    res.add(peek.val); // visit
                    last = st.pop();
                }
            }
        }
        return res;
    }
}
```

> **Tip:** For problems like *Right Side View*, *Zigzag Level Order*, *Check Completeness*, you can reuse the `levelOrder` BFS skeleton and just change what you collect per level.

***

## Quick sanity notes

*   **Graph flavor**: stick to `int n, int[][] edges` + `buildAdj`.
*   **TreeNode flavor**: keep everything in `class Solution` and **don’t** redeclare `TreeNode`.
*   Your original DFS/BFS logic was sound—this refactor mainly wraps it into **function signatures** LeetCode expects and removes static/global state.

### When to Use Which

| DFS | BFS |
|-----|-----|
| Subtree computations | Level-order processing |
| Path problems | Shortest distance (unweighted) |
| Euler tour, LCA | Finding tree diameter |
| Most tree DP | Multi-source BFS on trees |


***

## 2) Euler Tour (Subtree Queries)

**Invariant.** In a DFS **preorder** numbering, the nodes of a subtree of `u` occupy the **contiguous range** `[tin[u], tout[u]]`.

```
Tree:        0
            / \
           1   2
          / \
         3   4

DFS order:  0 -> 1 -> 3 -> 4 -> 2

tin:   [0, 1, 4, 2, 3]
tout:  [4, 3, 4, 2, 3]

Flat array: [0] [1] [3] [4] [2]
             0   1   2   3   4

Subtree of 1: tin[1]=1, tout[1]=3 -> range [1..3] -> nodes 1,3,4  ✓
```

### Idea

*   Run DFS; set `tin[u]` when you **enter** `u`, and after finishing all children set `tout[u] = timer-1`.
*   Any **subtree aggregate/query** becomes a **range** query on the flattened array.

### Implementation (tin/tout, ancestor check, subtree range)

```java
import java.util.*;

public class EulerTour {
    public final int n;
    public final int[] tin, tout, parent;
    private int timer = 0;

    public EulerTour(List<Integer>[] adj, int root) {
        this.n = adj.length;
        this.tin = new int[n];
        this.tout = new int[n];
        this.parent = new int[n];
        Arrays.fill(parent, -1);
        dfs(root, -1, adj);
    }

    private void dfs(int u, int p, List<Integer>[] adj) {
        parent[u] = p;
        tin[u] = timer++;
        for (int v : adj[u]) {
            if (v == p) continue;
            dfs(v, u, adj);
        }
        tout[u] = timer - 1;
    }

    public boolean isAncestor(int u, int v) {
        // u is ancestor of v if v's entry is within u's subtree range
        return tin[u] <= tin[v] && tin[v] <= tout[u];
    }

    public int[] subtreeRange(int u) {
        return new int[]{tin[u], tout[u]};
    }
}
```

> **Use with a Segment Tree/Fenwick:** store node values in an array `flat[]` by position `tin[node]`.  
> Subtree sum = `seg.query(tin[u], tout[u])`; point update = `seg.update(tin[u], newVal)`; range updates need a lazy segtree. (Keep it conceptual for interviews.)

***

## 3) Lowest Common Ancestor


```
              0
             / \
            1   2
           / \   \
          3   4   5
         / \
        6   7

LCA(6, 4) = 1      (1 is the deepest node above both 6 and 4)
LCA(6, 7) = 3      (3 is parent of both)
LCA(6, 5) = 0      (have to go all the way to root)
LCA(3, 3) = 3      (a node is its own ancestor)
```

### Why Does LCA Matter?

LCA is a **building block** for many tree problems:

| Problem | How LCA helps |
|---------|---------------|
| Distance between u and v | `depth[u] + depth[v] - 2*depth[LCA(u,v)]` |
| Path sum/max/min on trees | Split path at LCA: `u->LCA` + `LCA->v` |


```
Tree:
         0 (depth 0)
         |
         1 (depth 1)
         |
         2 (depth 2)
         |
         3 (depth 3)
         |
         4 (depth 4)

up table:
         k=0(1)  k=1(2)  k=2(4)
node 0:   -1      -1      -1
node 1:    0      -1      -1
node 2:    1       0      -1
node 3:    2       1      -1
node 4:    3       2       0

LCA(4, 2):
  depth[4]=4, depth[2]=2, diff=2
  Climb 4 by 2 steps: up[4][1] = 2
  Now both at node 2 -> LCA = 2
```

**Invariant.** `up[k][v]` stores the **2^k‑th ancestor** of node `v` (or `-1` if none).

### Why it matters

*   Distance: `dist(u,v) = depth[u] + depth[v] - 2*depth[lca(u,v)]`
*   Path queries often split at the LCA.

### Implementation (data‑driven LOG, O(N log N) build, O(log N) query)

```java
import java.util.*;

public class LCA {
    private final int n, LOG;
    private final int[][] up;   // up[k][v] = 2^k-th ancestor of v
    private final int[] depth;

    public LCA(List<Integer>[] adj, int root) {
        this.n = adj.length;
        this.LOG = 32 - Integer.numberOfLeadingZeros(Math.max(1, n));
        this.up = new int[LOG][n];
        this.depth = new int[n];
        for (int k = 0; k < LOG; k++) Arrays.fill(up[k], -1);
        dfs(root, -1, 0, adj);
        build();
    }

    private void dfs(int u, int p, int d, List<Integer>[] adj) {
        up[0][u] = p;
        depth[u] = d;
        for (int v : adj[u]) {
            if (v == p) continue;
            dfs(v, u, d + 1, adj);
        }
    }

    private void build() {
        for (int k = 1; k < LOG; k++) {
            for (int v = 0; v < n; v++) {
                int mid = up[k - 1][v];
                up[k][v] = (mid == -1) ? -1 : up[k - 1][mid];
            }
        }
    }

    public int lca(int u, int v) {
        if (depth[u] < depth[v]) { int tmp = u; u = v; v = tmp; }
        int diff = depth[u] - depth[v];
        for (int k = 0; k < LOG; k++) {
            if (((diff >> k) & 1) == 1) u = up[k][u];
        }
        if (u == v) return u;
        for (int k = LOG - 1; k >= 0; k--) {
            if (up[k][u] != up[k][v]) {
                u = up[k][u];
                v = up[k][v];
            }
        }
        return up[0][u];
    }

    public int dist(int u, int v) {
        int w = lca(u, v);
        return depth[u] + depth[v] - 2 * depth[w];
    }

    /** kth ancestor of u (k=0 returns u). Returns -1 if no such ancestor. */
    public int kthAncestor(int u, int k) {
        for (int bit = 0; bit < LOG && u != -1; bit++) {
            if (((k >> bit) & 1) == 1) u = up[bit][u];
        }
        return u;
    }

    /** kth node on path u→v (k=0 gives u). */
    public int kthOnPath(int u, int v, int k) {
        int w = lca(u, v);
        int du = depth[u] - depth[w];
        int dv = depth[v] - depth[w];
        if (k <= du) {
            return kthAncestor(u, k);
        } else {
            int k2 = du + dv - k; // steps from v upward
            return kthAncestor(v, k2);
        }
    }
}
```

### B) Add a **Binary‑Tree‑only LCA** shortcut

For classic LeetCode “LCA of BT,” include the standard recursive solution that doesn’t require preprocessing (works when parent pointers/indices aren’t given):

```java
// Returns LCA in a binary tree (not BST), O(n)
private TreeNode lcaBT(TreeNode root, TreeNode p, TreeNode q) {
    if (root == null || root == p || root == q) return root;
    TreeNode L = lcaBT(root.left, p, q);
    TreeNode R = lcaBT(root.right, p, q);
    if (L != null && R != null) return root;
    return L != null ? L : R;
}
```

This pairs nicely with your lifting‑based LCA for indexed trees. 
### C) Add a **BST‑specific LCA** one‑liner

Since you have a BST focus elsewhere, include:

```java
// LCA in BST exploiting ordering, O(h)
private TreeNode lcaBST(TreeNode root, TreeNode p, TreeNode q) {
    int lo = Math.min(p.val, q.val), hi = Math.max(p.val, q.val);
    while (root != null) {
        if (root.val > hi) root = root.left;
        else if (root.val < lo) root = root.right;
        else return root;
    }
    return null;
}
```

***

## 4) Rerooting DP

**Invariant.** For each node `u`,

*   `down[u]` (or `dpDown[u]`) summarizes info from **u’s subtree**,
*   `up[u]` (`dpUp[u]`) summarizes info from **outside u’s subtree**,
*   **Answer** at `u` = combine(`down[u]`, `up[u]`).

### Example A — Sum of distances from each node to all nodes (eccentricity sum)

Standard 2‑pass solution:

1.  Post‑order: compute `subtreeSize[u]` and `down[u]` (sum of distances to nodes in u’s subtree).
2.  Pre‑order: propagate `answer[child] = answer[u] - subtreeSize[child] + (n - subtreeSize[child])`.

```java
import java.util.*;

public class SumOfDistances {
    private final int n;
    private final int[] size;
    private final int[] down;     // sum of distances within subtree
    private final int[] ans;      // final answer for each node

    public SumOfDistances(List<Integer>[] adj) {
        this.n = adj.length;
        this.size = new int[n];
        this.down = new int[n];
        this.ans = new int[n];
        Arrays.fill(size, 1);
        dfsDown(0, -1, adj);      // fill size[] and down[]
        ans[0] = down[0];
        dfsUp(0, -1, adj);        // fill ans[] for all nodes
    }

    private void dfsDown(int u, int p, List<Integer>[] adj) {
        for (int v : adj[u]) {
            if (v == p) continue;
            dfsDown(v, u, adj);
            size[u] += size[v];
            down[u] += down[v] + size[v]; // all nodes in v-subtree are +1 further
        }
    }

    private void dfsUp(int u, int p, List<Integer>[] adj) {
        for (int v : adj[u]) {
            if (v == p) continue;
            // Move root from u to v:
            // nodes in v-subtree get 1 nearer; outside (n - size[v]) get 1 farther
            ans[v] = ans[u] - size[v] + (n - size[v]);
            dfsUp(v, u, adj);
        }
    }

    public int[] answers() { return ans; }
}
```

### Example B — Farthest distance from every node (eccentricity)

Track **two best downward arms** per node; then a top‑down pass provides an **upward** arm.

```java
import java.util.*;

public class FarthestFromEach {
    private final int n;
    private final int[][] bestDown; // [u][0]=longest, [u][1]=2nd longest
    private final int[] bestChild;  // which child gave the longest arm
    private final int[] up;         // best upward arm length

    public FarthestFromEach(List<Integer>[] adj) {
        this.n = adj.length;
        this.bestDown = new int[n][2];
        this.bestChild = new int[n];
        Arrays.fill(bestChild, -1);
        this.up = new int[n];
        dfsDown(0, -1, adj);
        dfsUp(0, -1, adj);
    }

    private void dfsDown(int u, int p, List<Integer>[] adj) {
        for (int v : adj[u]) {
            if (v == p) continue;
            dfsDown(v, u, adj);
            int d = 1 + bestDown[v][0];
            if (d > bestDown[u][0]) {
                bestDown[u][1] = bestDown[u][0];
                bestDown[u][0] = d;
                bestChild[u] = v;
            } else if (d > bestDown[u][1]) {
                bestDown[u][1] = d;
            }
        }
    }

    private void dfsUp(int u, int p, List<Integer>[] adj) {
        for (int v : adj[u]) {
            if (v == p) continue;
            int use = (bestChild[u] == v) ? bestDown[u][1] : bestDown[u][0];
            up[v] = Math.max(up[u], use) + 1;
            dfsUp(v, u, adj);
        }
    }

    /** Eccentricity (farthest distance) for each node. */
    public int[] eccentricities() {
        int[] ans = new int[n];
        for (int i = 0; i < n; i++) ans[i] = Math.max(bestDown[i][0], up[i]);
        return ans;
    }
}
```

***

## 5) Tree Diameter and Center

**Invariant.** The **diameter endpoints** are mutually farthest. The **center(s)** lie at the middle of a diameter (1 or 2 nodes).

### Two‑BFS/DFS diameter (simplest)

```java
import java.util.*;

public class DiameterBFS {
    static int[] bfs(int src, List<Integer>[] adj) {
        int n = adj.length;
        int[] dist = new int[n];
        Arrays.fill(dist, -1);
        ArrayDeque<Integer> q = new ArrayDeque<>();
        dist[src] = 0; q.add(src);
        while (!q.isEmpty()) {
            int u = q.removeFirst();
            for (int v : adj[u]) {
                if (dist[v] == -1) {
                    dist[v] = dist[u] + 1;
                    q.addLast(v);
                }
            }
        }
        return dist;
    }

    /** Returns diameter length (in edges). */
    public static int diameter(List<Integer>[] adj) {
        int n = adj.length;
        int[] d0 = bfs(0, adj);
        int u = 0;
        for (int i = 0; i < n; i++) if (d0[i] > d0[u]) u = i;
        int[] du = bfs(u, adj);
        int v = u;
        for (int i = 0; i < n; i++) if (du[i] > du[v]) v = i;
        return du[v];
    }
}
```

### DP diameter (two best downward paths per node)

```java
import java.util.*;

public class DiameterDP {
    private int best = 0;

    public int diameter(List<Integer>[] adj) {
        dfs(0, -1, adj);
        return best;
    }

    private int dfs(int u, int p, List<Integer>[] adj) {
        int first = 0, second = 0;
        for (int v : adj[u]) {
            if (v == p) continue;
            int d = dfs(v, u, adj) + 1;
            if (d > first) { second = first; first = d; }
            else if (d > second) { second = d; }
        }
        best = Math.max(best, first + second);
        return first;
    }
}
```

### Tree center(s) via leaf peeling

```java
import java.util.*;

public class TreeCenter {
    public static int[] centers(List<Integer>[] adj) {
        int n = adj.length;
        if (n <= 2) return java.util.stream.IntStream.range(0, n).toArray();

        int[] deg = new int[n];
        for (int i = 0; i < n; i++) deg[i] = adj[i].size();

        ArrayDeque<Integer> leaves = new ArrayDeque<>();
        for (int i = 0; i < n; i++) if (deg[i] <= 1) leaves.add(i);

        int remaining = n;
        while (remaining > 2) {
            int batch = leaves.size();
            remaining -= batch;
            for (int i = 0; i < batch; i++) {
                int leaf = leaves.removeFirst();
                for (int nb : adj[leaf]) {
                    if (--deg[nb] == 1) leaves.addLast(nb);
                }
            }
        }
        // 1 or 2 centers left in the queue
        int[] ans = new int[leaves.size()];
        int idx = 0;
        for (int x : leaves) ans[idx++] = x;
        return ans;
    }
}
```

***

## 6) Tree DP Patterns

### Pattern A — Subtree Aggregation

**Invariant.** When we return from `dfs(u)`, the aggregate over each child’s subtree is already computed.

```java
import java.util.*;

public class SubtreeSum {
    public static int dfsSum(int u, int p, List<Integer>[] adj, int[] val) {
        int total = val[u];
        for (int v : adj[u]) {
            if (v == p) continue;
            total += dfsSum(v, u, adj, val);
        }
        return total;
    }
}
```

### Pattern B — Select / Skip (Maximum Independent Set on Tree)

**State.** `dp[u][0]`: best if **u NOT selected**; `dp[u][1]`: best if **u selected**.  
**Transitions.**

*   `dp[u][0] = Σ max(dp[v][0], dp[v][1])`
*   `dp[u][1] = val[u] + Σ dp[v][0]`

```java
import java.util.*;

public class TreeMIS {
    private final int[][] dp;

    public TreeMIS(int n) { dp = new int[n][2]; }

    public int solve(List<Integer>[] adj, int[] val, int root) {
        dfs(root, -1, adj, val);
        return Math.max(dp[root][0], dp[root][1]);
    }

    private void dfs(int u, int p, List<Integer>[] adj, int[] val) {
        dp[u][1] = val[u];
        for (int v : adj[u]) {
            if (v == p) continue;
            dfs(v, u, adj, val);
            dp[u][0] += Math.max(dp[v][0], dp[v][1]);
            dp[u][1] += dp[v][0];
        }
    }
}
```

### Pattern C — Path Through Node (per‑node “two‑arms” trick)

**Goal.** For each node, longest path length **passing through** it.

```java
import java.util.*;

public class PathThroughNode {
    public static int[] longestThroughEach(List<Integer>[] adj, int root) {
        int n = adj.length;
        int[] best = new int[n];

        dfs(root, -1, adj, best);
        return best;
    }

    private static int dfs(int u, int p, List<Integer>[] adj, int[] best) {
        int first = 0, second = 0;
        for (int v : adj[u]) {
            if (v == p) continue;
            int d = dfs(v, u, adj, best) + 1;
            if (d > first) { second = first; first = d; }
            else if (d > second) { second = d; }
        }
        best[u] = first + second; // longest path through u
        return first;             // longest downward arm from u
    }
}
```

***
## 7) Basic Tree Properties 


### 2.1) **Maximum Depth of Binary Tree**

**Invariant.** Height of a node `u` is `1 + max(height(u.left), height(u.right))`; height of `null` is `0`. The tree’s maximum depth is the height of the root.

**Idea**  
Compute heights **post‑order** (children first, then node). BFS level‑count also works (number of layers).

**Implementation (post‑order DFS)**

```java
// Definition for a binary tree node.
// class TreeNode { int val; TreeNode left, right; TreeNode(int x){val=x;} }

class SolutionMaxDepth {
    public int maxDepth(TreeNode root) {
        if (root == null) return 0;
        int L = maxDepth(root.left);
        int R = maxDepth(root.right);
        return 1 + Math.max(L, R);
    }
}
```

**Alternative (BFS level count)**

```java
class SolutionMaxDepthBFS {
    public int maxDepth(TreeNode root) {
        if (root == null) return 0;
        java.util.ArrayDeque<TreeNode> q = new java.util.ArrayDeque<>();
        q.add(root);
        int depth = 0;
        while (!q.isEmpty()) {
            int sz = q.size();
            while (sz-- > 0) {
                TreeNode cur = q.removeFirst();
                if (cur.left  != null) q.addLast(cur.left);
                if (cur.right != null) q.addLast(cur.right);
            }
            depth++;
        }
        return depth;
    }
}
```

**Notes**

*   Time `O(n)`, space `O(h)` recursion (worst `O(n)`), or `O(w)` for BFS.
*   DFS is shorter; BFS is sometimes clearer when asked “levels.”

***

### 2.2) **Minimum Depth of Binary Tree**

**Invariant.** Minimum depth = nodes on the **shortest root‑to‑leaf** path. A **leaf** is a node with **no** children.

**Common trap**  
You **cannot** do `1 + min(minDepth(left), minDepth(right))` when one child is `null`—you’d “short‑circuit” through a non‑existent subtree.

**Idea**

*   **BFS**: the first leaf you pop gives the min depth (stop early).
*   **DFS**: handle the **single‑child** case explicitly.

**Implementation (safe DFS)**

```java
class SolutionMinDepth {
    public int minDepth(TreeNode root) {
        if (root == null) return 0;
        int L = minDepth(root.left);
        int R = minDepth(root.right);
        if (root.left == null)  return 1 + R; // must go right
        if (root.right == null) return 1 + L; // must go left
        return 1 + Math.min(L, R);
    }
}
```

**Alternative (BFS early exit)**

```java
class SolutionMinDepthBFS {
    public int minDepth(TreeNode root) {
        if (root == null) return 0;
        java.util.ArrayDeque<TreeNode> q = new java.util.ArrayDeque<>();
        q.add(root);
        int depth = 1;
        while (!q.isEmpty()) {
            int sz = q.size();
            while (sz-- > 0) {
                TreeNode cur = q.removeFirst();
                if (cur.left == null && cur.right == null) return depth; // first leaf
                if (cur.left  != null) q.addLast(cur.left);
                if (cur.right != null) q.addLast(cur.right);
            }
            depth++;
        }
        return depth;
    }
}
```

**Notes**

*   Time `O(n)`. DFS space `O(h)`; BFS space `O(w)`.
*   Prefer BFS if you want the shortest level quickly.

***

### 2.3) **Balanced Binary Tree** (height‑balanced)

**Invariant.** A tree is balanced iff **every** node satisfies `|height(left) − height(right)| ≤ 1`.

**Idea**  
Bottom‑up **post‑order**: return subtree height; if any child is unbalanced, bubble up a **sentinel** (e.g., `-1`) to short‑circuit.

**Implementation (post‑order with sentinel)**

```java
class SolutionBalanced {
    public boolean isBalanced(TreeNode root) {
        return height(root) != -1;
    }
    private int height(TreeNode node) {
        if (node == null) return 0;
        int LH = height(node.left);  if (LH == -1) return -1;
        int RH = height(node.right); if (RH == -1) return -1;
        if (Math.abs(LH - RH) > 1) return -1;
        return 1 + Math.max(LH, RH);
    }
}
```

**Notes**

*   Time `O(n)` (each node once), space `O(h)`.
*   Avoid top‑down “recompute heights” (`O(n^2)` worst‑case).

***

### 2.4) **Symmetric Tree** (mirror check)

**Invariant.** A tree is symmetric iff `left` is a **mirror** of `right`:  
`isMirror(a, b) = (a == null && b == null) || (a != null && b != null && a.val == b.val && isMirror(a.left, b.right) && isMirror(a.right, b.left))`.

**Idea**  
Compare **cross children**: `a.left` ↔ `b.right` and `a.right` ↔ `b.left`.

**Implementation (paired recursion)**

```java
class SolutionSymmetric {
    public boolean isSymmetric(TreeNode root) {
        return root == null || isMirror(root.left, root.right);
    }
    private boolean isMirror(TreeNode a, TreeNode b) {
        if (a == null || b == null) return a == b;
        if (a.val != b.val) return false;
        return isMirror(a.left, b.right) && isMirror(a.right, b.left);
    }
}
```

**Iterative (queue of pairs)**

```java
class SolutionSymmetricIter {
    public boolean isSymmetric(TreeNode root) {
        if (root == null) return true;
        java.util.ArrayDeque<TreeNode> q = new java.util.ArrayDeque<>();
        q.add(root.left); q.add(root.right);
        while (!q.isEmpty()) {
            TreeNode a = q.removeFirst(), b = q.removeFirst();
            if (a == null && b == null) continue;
            if (a == null || b == null || a.val != b.val) return false;
            q.addLast(a.left);  q.addLast(b.right);
            q.addLast(a.right); q.addLast(b.left);
        }
        return true;
    }
}
```

**Notes**

*   Time `O(n)`, space `O(h)` (DFS) or `O(w)` (BFS).
*   **Common bug**: comparing `left.left` with `right.left` instead of cross.

***

### 2.5) **Same Tree** (structural & value equality)

**Invariant.** Two trees are the same iff **both structure and values** match at every corresponding node.

**Idea**  
Traverse both trees **in lockstep**; compare nullness and values; recurse on `(left, left)` and `(right, right)`.

### **2.5) Same Tree (structural & value equality)**

**Invariant.** Two binary trees `p` and `q` are the *same* iff for every corresponding position:

*   both nodes are `null` **or** both are non‑`null` with equal `val`, **and**
*   their left subtrees are the same **and** their right subtrees are the same.

**Idea**  
Traverse both trees **in lockstep**. At each step, short‑circuit on any mismatch (nullness or value). Either use a tiny **recursive** check, or an **iterative** BFS that enqueues node **pairs**.

**Implementation (recursive, 4 lines of logic)**

```java
// class TreeNode { int val; TreeNode left, right; TreeNode(int x){ val = x; } }

class SolutionSameTree {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if (p == null || q == null) return p == q;       // both null -> true; one null -> false
        if (p.val != q.val) return false;                // value mismatch
        return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
    }
}
```

**Implementation (iterative, queue of pairs)**

```java
class SolutionSameTreeIter {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        java.util.ArrayDeque<TreeNode> dq = new java.util.ArrayDeque<>();
        dq.add(p); dq.add(q);
        while (!dq.isEmpty()) {
            TreeNode a = dq.removeFirst(), b = dq.removeFirst();
            if (a == null || b == null) {
                if (a != b) return false;        // exactly one is null
                continue;                         // both null -> skip
            }
            if (a.val != b.val) return false;
            dq.addLast(a.left);  dq.addLast(b.left);
            dq.addLast(a.right); dq.addLast(b.right);
        }
        return true;
    }
}
```

#### Micro‑recall (one‑liners)

*   **Max Depth**: `1 + max(L, R)` (post‑order).
*   **Min Depth**: first leaf via BFS, or DFS with **single‑child rule**.
*   **Balanced**: post‑order height with **-1 sentinel**.
*   **Symmetric**: `isMirror(left, right)` with **cross** children.
*   **Same Tree**: lockstep equality (structure + value).

## 8) Pattern Recognition Cheat Sheet 

**By query type**

*   **Subtree sum/min/max** → **Euler Tour + Segment Tree** (range `[tin[u], tout[u]]`)
*   **Subtree update** → **Euler Tour + Lazy Segment Tree**
*   **LCA query** → **Binary Lifting** (or Euler+RMQ idea)
*   **Distance(u,v)** → `depth[u] + depth[v] − 2*depth[lca(u,v)]`
*   **Answer for every root** → **Rerooting DP** (two passes)
*   **Is u ancestor of v?** → check `tin[u] ≤ tin[v] ≤ tout[u]`
*   **Tree diameter** → **Two‑BFS** or **DP (two‑arms)**

**Decision flow**

    Need subtree queries?   → Euler Tour (+ segment tree)
    Need LCA / distance?    → Binary Lifting (O(log N))
    Need per-root answers?  → Rerooting DP
    Need subtree DP value?  → Post-order DP (aggregate/select-skip)
    Need diameter/center?   → Two-BFS or two-arms DP; peel for center(s)

***

## Build Notes / Edge Cases

*   **Dynamic LOG**: `LOG = 32 - Integer.numberOfLeadingZeros(max(1, n))` — keeps lifting table minimal and correct.
*   **Recursion depth**: Java’s default stack is generally fine for trees up to typical interview sizes; for very deep trees, switch to iterative or increase stack if needed.
*   **Indexing**: All examples assume nodes are `0..n-1`, adjacency list `List<Integer>[] adj`.
*   **Weighted paths**: For max/min along a path with lifting, store an extra table `agg[k][v]` built alongside `up[k][v]`.

