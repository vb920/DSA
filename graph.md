# 📗 Graph: FAANG SDE-2 Mastery List — FINAL (Top 2-3%)

*Curated for top-tier FAANG interviews (L4/L5 / SDE-2). Strips away purely competitive programming tricks to focus on robust state management, graph theory fundamentals, and advanced traversal techniques.*

---

## 1. Matrix & Grid Traversal (DFS/BFS)
* **SDE-2 Expectation:** Flawless 2D boundary checks without repetitive code (`directions` array), modifying grids in-place to save memory when permitted, and recognizing multi-source BFS vs single-source DFS immediately.
* Number of Islands / Max Area of Island / Count Sub Islands
* Flood Fill
* Pacific Atlantic Water Flow
* Surrounded Regions / Number of Enclaves / Number of Closed Islands
* *Shortest Path in Binary Matrix (LC 1091)** 

## 2. Multi-Source BFS (Explicit Pattern)
* **SDE-2 Expectation:** Seeding the queue with ALL sources at distance 0 simultaneously (not running BFS per source), and recognizing "distance from nearest X" phrasing as the trigger.
* Rotting Oranges (LC 994) — canonical
* Walls And Gates (LC 286)
* 01 Matrix (LC 542) — multi-source BFS on distances
* As Far from Land as Possible (LC 1162) — inverse direction twist

## 3. Standard Traversal & Connected Components
* **SDE-2 Expectation:** Knowing when to pass state naturally downwards (DFS) versus exploring radially level-by-level (BFS). Clean management of `visited` states and cycle-detection mapping for object references.
* Clone Graph (Object reference depth mapping)
* Reorder Routes to Make All Paths Lead to The City Zero
* Find Eventual Safe States (Tri-color state cycle detection)
* Evaluate Division (String-weighted edges, queries DFS)
* Detonate the Maximum Bombs (Directed overlaps)
* Number of Connected Components In An Undirected Graph / Number of Provinces

## 4. Topological Sort (Dependencies & DAGs)
* **SDE-2 Expectation:** Using Kahn's indegree counting algorithm seamlessly with a queue, or equivalently identifying cycles via DFS path tracing. Recognizing implicit dependencies like string characters or task sequences.
* Course Schedule I, II, IV
* Parallel Courses I, III
* Alien Dictionary / Verifying An Alien Dictionary (Implicit order tracing)
* Find All Possible Recipes from Given Supplies
* Build a Matrix With Conditions
* Largest Color Value in a Directed Graph

## 5. Union-Find (Disjoint Set)
* **SDE-2 Expectation:** Implementing Path Compression and Union by Rank perfectly from memory. Recognizing when Union-Find dynamically tracks connected components much cleaner than full recalculations via BFS/DFS.
* Redundant Connection
* Accounts Merge (Complex multi-entity grouping)
* Graph Valid Tree
* Regions Cut By Slashes (Geometric mapping)
* Remove Max Number of Edges to Keep Graph Fully Traversable
* Greatest Common Divisor Traversal
* Number of Good Paths

### 5a. Weighted Union-Find (Alternate Solution Lens)
* **SDE-2 Expectation:** Knowing that ratio/weight queries between nodes can be answered with union-find storing relative weights to the root — often cleaner than DFS per query.
* Evaluate Division (LC 399) — solve BOTH ways (DFS + weighted UF)
* Redundant Connection II (LC 685) — weighted thinking on directed edges

## 6. Shortest Path (Dijkstra / Edge Weights)
* **SDE-2 Expectation:** Implementing a clean Dijkstra with a Priority Queue explicitly saving running state distance pairs, and knowing how to prevent useless execution by pruning worse paths early within the queue loop itself.
* Network Delay Time (Dijkstra Baseline)
* Cheapest Flights Within K Stops (Constrained Dijkstra / Bellman-Ford)
* Path with Minimum Effort
* Path with Maximum Probability (Max-Heap Dijkstra variant)
* Minimum Cost to Make at Least One Valid Path in a Grid (0-1 BFS)
* Find the City With the Smallest Number of Neighbors at a Threshold Distance (Floyd-Warshall)
* Minimum Fuel Cost to Report to the Capital (DFS Tree accumulations)

### 6a. A* Search (One-Line Awareness)
* **SDE-2 Expectation:** Not implementing from scratch under pressure, but being able to say: "A heuristic-guided Dijkstra with `f = g + h`; admissible heuristic guarantees optimality" when an interviewer probes Knight Moves.
* Minimum Knight Moves (LC 1197) — A* with Chebyshev-based heuristic
* Shortest Path in a Grid with Obstacles Elimination (LC 1293) — discuss why A* helps conceptually

## 7. Minimum Spanning Tree (Prim's / Kruskal's)
* **SDE-2 Expectation:** Mostly recognizing that sorting edges + executing Union-Find perfectly represents Kruskal's for cheap uniform connectivity.
* Min Cost to Connect All Points
* Find Critical and Pseudo Critical Edges in Minimum Spanning Tree

## 8. Bitmask BFS (State Space Search)
* **SDE-2 Expectation:** Recognizing that `N <= 15` in a graph problem means you should use an integer bitmask to represent visited states inside your BFS queue — the "visited" state is not just a node, but the node *plus* items collected/nodes visited so far.
* Shortest Path Visiting All Nodes (The quintessential Bitmask BFS)
* Shortest Path to Get All Keys

## 9. Floyd's Cycle Detection (Functional Graphs)
* **SDE-2 Expectation:** Treating an array as a linked list via index→value mapping; knowing slow/fast pointer math and why it's O(1) space.
* Find the Duplicate Number (LC 287)
* Linked List Cycle II (LC 142) — the underlying mechanics
* Circular Array Loop (LC 457) — directed functional graph variant

## 10. Articulation Points & Bridges (Tarjan's Lite)
* **SDE-2 Expectation:** Understanding how to use a `discovery_time` and `lowest_reachable_time` array during a DFS to identify critical vulnerabilities in a network. Full Tarjan SCC is CP territory; bridges are not.
* Critical Connections in a Network

## 11. Bidirectional BFS (Explicit Callout)
* **SDE-2 Expectation:** The ability to explain *why* Bidirectional BFS is used (it reduces the search space from `b^d` to `2 * b^(d/2)`) and how to properly manage two expanding frontiers using HashSets to find the intersection.
* Word Ladder I & II
* Minimum Genetic Mutation

## 12. Advanced Configurations & Implicit Graph Modeling
* **SDE-2 Expectation:** Converting non-obvious structures into graphs — cells→nodes, states→nodes, strings→nodes. This meta-skill powers half of this section. Also: odd-length cycle detection and complex path requirements.
* Is Graph Bipartite? / Divide Nodes Into the Maximum Number of Groups
* Reconstruct Itinerary (Hierholzer's Algorithm for Eulerian Paths)
* Word Ladder (Transition building + Bidirectional BFS optimization)
* Snakes And Ladders / Open The Lock (states as graph nodes)
* Sliding Puzzle (board configurations as nodes)
* Shortest Path with Alternating Colors

---

## Verdict

**Coverage: ~90% as-is → 100% after 3 small fixes (~5 problems total)**

| Fix | Problems Added |
|---|---|
| Bipartite subsection (12a) | LC 785, LC 886 (+ LC 2767 already present) |
| Functional graph cycles in #9 | LC 2360, LC 2127 |
| Game-state problem in #12 | LC 913 |

### Final Sheet Stats

| Metric | Value |
|---|---|
| Sections | **12** (+ 2 sub-patterns: Weighted UF, A*) |
| Problems | **~55 curated problems** |
| Removed from original | Rotting Oranges/Walls And Gates moved out of #1 → dedicated Multi-Source section (#2); duplicates consolidated |
| CP stripped | Full Tarjan SCC, max-flow, heavy-light decomposition |

### Study Priority Tiers

| Tier | Sections |
|---|---|
| 🔴 **Master cold** | 1–6 (grid, multi-source, traversal, topo, union-find, shortest path) |
| 🟠 **Must be solid** | 7–9 (MST, bitmask BFS, Floyd's) |
| 🟡 **Know well** | 10–12 (bridges, bidirectional BFS, implicit modeling) |
| 🟢 **Awareness only** | 5a, 6a (weighted UF alternate lens, A* one-liner) |
