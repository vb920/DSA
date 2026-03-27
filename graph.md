# Graph: FAANG SDE-2 Mastery List (Top 2-3%)

This list is heavily curated for top-tier FAANG interviews (L4/L5 / SDE-2 levels). It categorizes standard graph problems into explicit structural patterns with the expectations of an SDE-2 engineer in a systems or algorithms interview setting. Like the DP patterns, this strips away purely competitive programming tricks to focus entirely on robust state management, graph theory fundamentals, and advanced traversal techniques.

## 1. Matrix & Grid Traversal (DFS/BFS)
* **SDE-2 Expectation:** Flawless 2D boundary checks without repetitive code (`directions` array), modifying grids in-place to save memory when permitted, and recognizing multi-source BFS vs single-source DFS immediately.
* Number of Islands / Max Area of Island / Count Sub Islands
* Flood Fill / Rotting Oranges
* Walls And Gates / Shortest Distance from All Buildings
* Pacific Atlantic Water Flow
* Surrounded Regions / Number of Enclaves / Number of Closed Islands
* Minimum Knight Moves / Shortest Path in Binary Matrix / Sliding Puzzle
* Trapping Rain Water II (Grid + Min-Heap BFS boundary shrinking)

## 2. Standard Traversal & Connected Components
* **SDE-2 Expectation:** Knowing when to pass state naturally downwards (DFS) versus exploring radially level-by-level (BFS). Clean management of `visited` states and cycle-detection mapping for object references.
* Clone Graph (Object reference depth mapping)
* Reorder Routes to Make All Paths Lead to The City Zero
* Find Eventual Safe States (Tri-color state cycle detection)
* Evaluate Division (String-weighted edges, queries DFS)
* Detonate the Maximum Bombs (Directed overlaps)
* Number of Connected Components In An Undirected Graph / Number of Provinces

## 3. Topological Sort (Dependencies & DAGs)
* **SDE-2 Expectation:** Using Kahn’s indegree counting algorithm seamlessly with a queue, or equivalently identifying cycles via DFS path tracing. Recognizing implicit dependencies like string characters or task sequences.
* Course Schedule I, II, IV
* Parallel Courses I, III
* Alien Dictionary / Verifying An Alien Dictionary (Implicit order tracing)
* Find All Possible Recipes from Given Supplies
* Build a Matrix With Conditions
* Largest Color Value in a Directed Graph

## 4. Union-Find (Disjoint Set)
* **SDE-2 Expectation:** Implementing Path Compression and Union by Rank perfectly from memory. Recognizing when Union-Find dynamically tracks connected components much cleaner than full recalculations via BFS/DFS.
* Redundant Connection
* Accounts Merge (Complex multi-entity grouping)
* Graph Valid Tree
* Regions Cut By Slashes (Geometric mapping)
* Remove Max Number of Edges to Keep Graph Fully Traversable
* Greatest Common Divisor Traversal
* Number of Good Paths

## 5. Shortest Path (Dijkstra / Edge Weights)
* **SDE-2 Expectation:** Implementing a clean Dijkstra with a Priority Queue explicitly saving running state distance pairs, and knowing how to prevent useless execution by pruning worse paths early within the queue loop itself.
* Network Delay Time (Dijkstra Baseline)
* Cheapest Flights Within K Stops (Constrained Dijkstra / Bellman-Ford)
* Path with Minimum Effort
* Path with Maximum Probability (Max-Heap Dijkstra variant)
* Minimum Cost to Make at Least One Valid Path in a Grid (0-1 BFS)
* Find the City With the Smallest Number of Neighbors at a Threshold Distance (Floyd-Warshall)
* Minimum Fuel Cost to Report to the Capital (DFS Tree accumulations)

## 6. Minimum Spanning Tree (Prim's / Kruskal's)
* **SDE-2 Expectation:** Mostly recognizing that sorting edges + executing Union-Find perfectly represents Kruskal's for cheap uniform connectivity.
* Min Cost to Connect All Points
* Find Critical and Pseudo Critical Edges in Minimum Spanning Tree

## 7. Advanced Configurations & Specialized Views
* **SDE-2 Expectation:** Operating cleanly on odd-length cycle findings and modifying a traversal to handle complex path requirements, including word ladders or explicit tracking equations.
* Is Graph Bipartite? / Divide Nodes Into the Maximum Number of Groups
* Reconstruct Itinerary (Hierholzer's Algorithm for Eulerian Paths)
* Word Ladder (Transition building + Bidirectional BFS optimization)
* Snakes And Ladders / Open The Lock
* Shortest Path with Alternating Colors
