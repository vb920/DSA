# FAANG SDE-2 Matrix Traversal & Grid Graphs Guide

This guide structures the most frequent 2D grid and matrix problems into distinct patterns. In an SDE-2 interview, the expectation is not just solving the problem, but recognizing *why* a specific traversal method (DFS, BFS, or Union-Find) is optimal, strictly managing exact time and space trade-offs.

---

## 1. Connected Components & Islands
**Problems:** Number of Islands, Max Area of Island, Count Sub Islands

### 💡 Approaches & Complexities

**Approach A: Depth-First Search (DFS)**
*   **Idea:** The standard, fastest-to-write approach. Iterate through the grid, and when unvisited land is found, sink it recursively in all 4 directions (`grid[i][j] = '0'`) to prevent cycle revisits.
*   **Time Complexity:** $\mathcal{O}(M \times N)$ where $M$ is rows and $N$ is cols. We evaluate every cell conditionally independent of depth.
*   **Space Complexity:** $\mathcal{O}(M \times N)$ worst-case for the implicit recursion stack (e.g., if the entire grid is one giant zig-zagging island). Modifying the grid in-place gives $\mathcal{O}(1)$ *auxiliary/explicit* memory overhead.

**Approach B: Breadth-First Search (BFS)**
*   **Idea:** Use a Queue to radiate level-by-level instead of diving deeply. Mandatory fallback in tight memory constraint environments where deep recursion causes a Stack Overflow.
*   **Time Complexity:** $\mathcal{O}(M \times N)$.
*   **Space Complexity:** $\mathcal{O}(\min(M, N))$ auxiliary space for the Queue. The maximum perimeter of an expanding BFS boundary inside an $M \times N$ matrix dictates peak memory.

**Approach C: Union-Find (Disjoint Set)**
*   **Idea:** Map the 2D grid into a flattened 1D array of size $M \times N$. When a `1` is spotted, union it mathematically with its active adjacent `1`s. Excellent scaling for continuous or dynamically spawned grids.
*   **Time Complexity:** $\mathcal{O}(M \times N \times \alpha(M \times N))$, where $\alpha$ is the Inverse Ackermann function (essentially $\mathcal{O}(1)$).
*   **Space Complexity:** $\mathcal{O}(M \times N)$ strictly, mandated to store the 1D `parent` and `rank` tracking arrays.

<details>
<summary><b>💻 Canonical Code Implementations</b> (Click to expand)</summary>

### Number of Islands (DFS In-Place)
```java
class Solution {
    public int numIslands(char[][] grid) {
        int islands = 0;
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (grid[i][j] == '1') {
                    islands++;
                    dfs(grid, i, j);
                }
            }
        }
        return islands;
    }

    private void dfs(char[][] grid, int i, int j) {
        if (i < 0 || i >= grid.length || j < 0 || j >= grid[0].length || grid[i][j] == '0') return;
        grid[i][j] = '0'; // mark visited to prevent cycles
        dfs(grid, i - 1, j); dfs(grid, i + 1, j); dfs(grid, i, j - 1); dfs(grid, i, j + 1);
    }
}
```

### Max Area of Island (DFS)
```java
class Solution {
    public int maxAreaOfIsland(int[][] grid) {
        int maxArea = 0;
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (grid[i][j] == 1) maxArea = Math.max(maxArea, dfs(grid, i, j));
            }
        }
        return maxArea;
    }

    private int dfs(int[][] grid, int i, int j) {
        if (i < 0 || i >= grid.length || j < 0 || j >= grid[0].length || grid[i][j] == 0) return 0;
        grid[i][j] = 0; // sink the island
        return 1 + dfs(grid, i-1, j) + dfs(grid, i+1, j) + dfs(grid, i, j-1) + dfs(grid, i, j+1);
    }
}
```

### Count Sub Islands (DFS Validation)
```java
class Solution {
    public int countSubIslands(int[][] grid1, int[][] grid2) {
        int count = 0;
        for (int i = 0; i < grid1.length; i++) {
            for (int j = 0; j < grid1[0].length; j++) {
                // Start DFS only if we find land in grid2
                if (grid2[i][j] == 1 && dfs(grid1, grid2, i, j)) count++;
            }
        }
        return count;
    }
    
    private boolean dfs(int[][] g1, int[][] g2, int i, int j) {
        if (i < 0 || i >= g1.length || j < 0 || j >= g1[0].length || g2[i][j] == 0) return true;
        g2[i][j] = 0; // mark visited immediately
        
        boolean isSub = (g1[i][j] == 1); 
        
        // Evaluate ALL directions unconditionally to clear the whole island from grid2!
        boolean up = dfs(g1, g2, i - 1, j);
        boolean down = dfs(g1, g2, i + 1, j);
        boolean left = dfs(g1, g2, i, j - 1);
        boolean right = dfs(g1, g2, i, j + 1);
        
        return isSub && up && down && left && right;
    }
}
```
</details>

---

## 2. Multi-Source Spread & State Matrix
**Problems:** Flood Fill, Rotting Oranges, Walls And Gates / Shortest Distance from All Buildings

### 💡 Approaches & Complexities

**Problem: Flood Fill (DFS/BFS)**
*   **Idea:** Standard interconnected origin expansion. Paint the coordinate network. Key interview trap: explicitly ensure you short-circuit recursion if `oldColor == newColor`.
*   **Time Complexity:** $\mathcal{O}(M \times N)$.
*   **Space Complexity:** $\mathcal{O}(M \times N)$ max stack/queue overhead tracking recursive depth.

**Problem: Rotting Oranges / Walls and Gates (Multi-Source BFS)**
*   **Idea:** A huge SDE-2 check. You *cannot* evaluate single-source BFS chains from every target ($O(M^2 \times N^2)$ execution). You **must** pre-load the common Queue with *all origins* at $Time = 0$, radiating outwards symmetrically per tick layer.
*   **Time Complexity:** $\mathcal{O}(M \times N)$. Every coordinate processes exactly once.
*   **Space Complexity:** $\mathcal{O}(M \times N)$ queuing constraint.

**Problem: Shortest Distance from All Buildings (Aggressive Pruned BFS)**
*   **Idea:** Pathfinding with aggressive invalidation logic. Track a global `distances` matrix. For every building, run a BFS that increments travel distance on empty plots. Important optimization: limit traversals purely to empty plots that successfully connected to the *previous* building mapped.
*   **Time Complexity:** $\mathcal{O}(B \times M \times N)$ mapped by processing the entire grid iteratively per building $B$. 
*   **Space Complexity:** $\mathcal{O}(M \times N)$ maintaining aggregated shortest-distance storage grids.

<details>
<summary><b>💻 Canonical Code Implementations</b> (Click to expand)</summary>

### Flood Fill (DFS)
```java
class Solution {
    public int[][] floodFill(int[][] image, int sr, int sc, int color) {
        int oldColor = image[sr][sc];
        // Trap check: prevent infinite loop
        if (oldColor != color) dfs(image, sr, sc, oldColor, color);
        return image;
    }
    
    private void dfs(int[][] image, int i, int j, int oldColor, int color) {
        if (i < 0 || i >= image.length || j < 0 || j >= image[0].length || image[i][j] != oldColor) return;
        image[i][j] = color;
        dfs(image, i-1, j, oldColor, color); dfs(image, i+1, j, oldColor, color);
        dfs(image, i, j-1, oldColor, color); dfs(image, i, j+1, oldColor, color);
    }
}
```

### Rotting Oranges (Multi-Source BFS)
```java
class Solution {
    public int orangesRotting(int[][] grid) {
        Queue<int[]> q = new LinkedList<>();
        int fresh = 0, minutes = 0;
        
        // Pre-process ALL rotten origins together simultaneously 
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (grid[i][j] == 2) q.add(new int[]{i, j});
                else if (grid[i][j] == 1) fresh++;
            }
        }
        
        if (fresh == 0) return 0;
        int[][] dirs = {{1,0}, {-1,0}, {0,1}, {0,-1}};
        
        while (!q.isEmpty()) {
            int size = q.size();
            boolean rotted = false;
            for (int i = 0; i < size; i++) {
                int[] curr = q.poll();
                for (int[] d : dirs) {
                    int nx = curr[0] + d[0], ny = curr[1] + d[1];
                    if (nx >= 0 && ny >= 0 && nx < grid.length && ny < grid[0].length && grid[nx][ny] == 1) {
                        grid[nx][ny] = 2; // Infect adjacent
                        q.add(new int[]{nx, ny});
                        fresh--;
                        rotted = true;
                    }
                }
            }
            if (rotted) minutes++; 
        }
        return fresh == 0 ? minutes : -1;
    }
}
```

### Walls and Gates (Multi-Source BFS)
```java
class Solution {
    public void wallsAndGates(int[][] rooms) {
        int m = rooms.length;
        if (m == 0) return;
        int n = rooms[0].length;
        Queue<int[]> q = new LinkedList<>();
        
        // Pre-process all gates (value 0) into the queue
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (rooms[i][j] == 0) q.add(new int[]{i, j});
            }
        }
        
        int[][] dirs = {{1,0},{-1,0},{0,1},{0,-1}};
        
        // BFS outward layer by layer
        while (!q.isEmpty()) {
            int[] curr = q.poll();
            int r = curr[0], c = curr[1];
            
            for (int[] d : dirs) {
                int nr = r + d[0], nc = c + d[1];
                // Only step onto unvisited empty rooms
                if (nr >= 0 && nr < m && nc >= 0 && nc < n && rooms[nr][nc] == Integer.MAX_VALUE) {
                    rooms[nr][nc] = rooms[r][c] + 1; // distance
                    q.add(new int[]{nr, nc});
                }
            }
        }
    }
}
```

### Shortest Distance from All Buildings (Aggressive Pruned BFS)
```java
class Solution {
    public int shortestDistance(int[][] grid) {
        int m = grid.length, n = grid[0].length;
        int[][] dist = new int[m][n];
        int[][] reach = new int[m][n];
        int buildings = 0;
        
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 1) {
                    buildings++;
                    bfs(grid, dist, reach, i, j);
                }
            }
        }
        
        int minDist = Integer.MAX_VALUE;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 0 && reach[i][j] == buildings) {
                    minDist = Math.min(minDist, dist[i][j]);
                }
            }
        }
        return minDist == Integer.MAX_VALUE ? -1 : minDist;
    }
    
    private void bfs(int[][] grid, int[][] dist, int[][] reach, int r, int c) {
        int m = grid.length, n = grid[0].length;
        Queue<int[]> q = new LinkedList<>();
        q.add(new int[]{r, c});
        boolean[][] visited = new boolean[m][n];
        visited[r][c] = true;
        
        int[][] dirs = {{1,0},{-1,0},{0,1},{0,-1}};
        int steps = 0;
        
        while (!q.isEmpty()) {
            int size = q.size();
            steps++;
            for (int k = 0; k < size; k++) {
                int[] curr = q.poll();
                for (int[] d : dirs) {
                    int nr = curr[0] + d[0], nc = curr[1] + d[1];
                    if (nr >= 0 && nr < m && nc >= 0 && nc < n && !visited[nr][nc] && grid[nr][nc] == 0) {
                        visited[nr][nc] = true;
                        dist[nr][nc] += steps;     // accumulate distance
                        reach[nr][nc]++;           // count successfully reached buildings
                        q.add(new int[]{nr, nc});
                    }
                }
            }
        }
    }
}
```
</details>

---

## 3. Boundary & Perimeter Traversal
**Problems:** Surrounded Regions, Number of Enclaves, Number of Closed Islands

### 💡 Approaches & Complexities

**Approach: Reverse Elimination Boundary Sweeping (DFS/BFS)**
*   **Idea:** A quintessential FAANG structural trick. Attempting to traverse from the inside-out introduces complex boundary exception logic. **Inverting the traversal** simplifies everything natively.
    1. Iterate purely across the perimeter edge columns and rows. When hitting a valid object, run DFS/BFS to designate those specific connected blocks topologically as "Safe".
    2. Any nodes within the matrix remaining untouched by the border elimination check are mathematically enveloped/closed. Toggle them linearly.
*   **Time Complexity:** $\mathcal{O}(M \times N)$. The interior array parsing and initial linear border checks perfectly bind.
*   **Space Complexity:** $\mathcal{O}(M \times N)$ max bounding call stack if borders snake inwards heavily natively without cycle shortcuts.

<details>
<summary><b>💻 Canonical Code Implementations</b> (Click to expand)</summary>

### Surrounded Regions
```java
class Solution {
    public void solve(char[][] board) {
        int rows = board.length, cols = board[0].length;
        
        // Mark borders as Safe Space ('S')
        for (int r = 0; r < rows; r++) { dfs(board, r, 0); dfs(board, r, cols - 1); }
        for (int c = 0; c < cols; c++) { dfs(board, 0, c); dfs(board, rows - 1, c); }

        // Iterate inner matrix: Flip trapped 'O' to 'X', restore Safe 'S' back to 'O'
        for (int r = 0; r < rows; r++) {
            for (int c = 0; c < cols; c++) {
                if (board[r][c] == 'O') board[r][c] = 'X';
                else if (board[r][c] == 'S') board[r][c] = 'O';
            }
        }
    }
    private void dfs(char[][] board, int r, int c) {
        if (r < 0 || r >= board.length || c < 0 || c >= board[0].length || board[r][c] != 'O') return;
        board[r][c] = 'S'; 
        dfs(board, r-1, c); dfs(board, r+1, c); dfs(board, r, c-1); dfs(board, r, c+1);
    }
}
```

### Number of Closed Islands
```java
class Solution {
    public int closedIsland(int[][] board) {
        int rows = board.length, cols = board[0].length, count = 0;
        
        // Eliminate borders tracking
        for (int r = 0; r < rows; r++) { dfs(board, r, 0); dfs(board, r, cols - 1); }
        for (int c = 0; c < cols; c++) { dfs(board, 0, c); dfs(board, rows - 1, c); }

        // Count internally enveloped pockets
        for (int r = 1; r < rows - 1; r++) {
            for (int c = 1; c < cols - 1; c++) {
                if (board[r][c] == 0) { 
                    dfs(board, r, c);
                    count++;
                }
            }
        }
        return count;
    }
    private void dfs(int[][] board, int r, int c) {
        if (r < 0 || r >= board.length || c < 0 || c >= board[0].length || board[r][c] != 0) return;
        board[r][c] = 1; // Sink
        dfs(board, r-1, c); dfs(board, r+1, c); dfs(board, r, c-1); dfs(board, r, c+1);
    }
}
```
</details>

---

## 4. Intersection Flow 
**Problems:** Pacific Atlantic Water Flow

### 💡 Approaches & Complexities

**Approach: Dual Reverse Topologies (DFS/BFS)**
*   **Idea:** Mapping outward flows analytically per pixel towards $O(1)$ targets is extremely slow explicitly. Invert logic: compute water flowing **upwards** starting natively from the physical oceans to index reachability internally.
    1. Search from the Pacific top/left edges tracking into a `boolean[][] pacific`. Water logic is logically inverted (`heights[next] >= heights[curr]`).
    2. Search from the Atlantic bottom/right tracking `atlantic[][]`.
    3. Return any $X,Y$ matrix cell verifying intersection $intersect = pacific[x] \cap atlantic[x]$.
*   **Time Complexity:** $\mathcal{O}(M \times N)$ optimal bound handling two perfectly parallel sweeps across coordinate limits.
*   **Space Complexity:** $\mathcal{O}(M \times N)$ required allocation tracking the individual intersection bool matrices explicit layout mappings.

<details>
<summary><b>💻 Canonical Code Implementations</b> (Click to expand)</summary>

### Pacific Atlantic Water Flow (DFS)
```java
public class Solution {
    public List<List<Integer>> pacificAtlantic(int[][] matrix) {
        List<List<Integer>> res = new ArrayList<>();
        if (matrix.length == 0) return res;
        int m = matrix.length, n = matrix[0].length;
        
        boolean[][] pacific = new boolean[m][n];
        boolean[][] atlantic = new boolean[m][n];
        
        // Traverse upwards from borders independently
        for (int i = 0; i < m; i++) {
            dfs(matrix, pacific, i, 0, Integer.MIN_VALUE);     // Left Border
            dfs(matrix, atlantic, i, n-1, Integer.MIN_VALUE);  // Right Border
        }
        for (int j = 0; j < n; j++) {
            dfs(matrix, pacific, 0, j, Integer.MIN_VALUE);     // Top Border
            dfs(matrix, atlantic, m-1, j, Integer.MIN_VALUE);  // Bottom Border
        }
        
        // Filter intersections mapping
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (pacific[i][j] && atlantic[i][j]) res.add(Arrays.asList(i, j));
            }
        }
        return res;
    }
    
    private void dfs(int[][] matrix, boolean[][] visited, int i, int j, int prevHeight) {
        if (i < 0 || i >= matrix.length || j < 0 || j >= matrix[0].length) return;
        if (visited[i][j] || matrix[i][j] < prevHeight) return; // Note reversed constraints handling UPWARD pathing
        
        visited[i][j] = true;
        dfs(matrix, visited, i-1, j, matrix[i][j]);
        dfs(matrix, visited, i+1, j, matrix[i][j]);
        dfs(matrix, visited, i, j-1, matrix[i][j]);
        dfs(matrix, visited, i, j+1, matrix[i][j]);
    }
}
```
</details>

---

## 5. Shortest Paths in Grids & State Space Compressions
**Problems:** Minimum Knight Moves, Shortest Path in Binary Matrix, Sliding Puzzle

### 💡 Approaches & Complexities

**Approach A: Unweighted Distance BFS**
*   **Idea:** Exclusively BFS limits depths efficiently testing bounds to derive exactly minimum path constraints spanning out from $0$. DFS mathematically fails constraint verification natively unweighted.
*   **Time Complexity:** $\mathcal{O}(M \times N)$ tracking queue steps.
*   **Space Complexity:** $\mathcal{O}(\min(M, N))$ bounding the max width layer active Queue.

**Approach B: State Space Encoded BFS (Sliding Puzzle)**
*   **Idea:** Graph matrices are rarely strictly evaluated evaluating indexes physically transitioning. Evaluate configurations serializing the matrix layout structurally into Strings mapping `123456`. Permutate valid char array swaps pushing new structural shapes into a target String mapped iteration structure validated with `HashSets`.
*   **Time Complexity:** $\mathcal{O}((M \times N)!)$ effectively spanning configuration permutations ($e.g. 6!$ states).
*   **Space Complexity:** $\mathcal{O}((M \times N)!)$ maintaining exhaustive visited combinations logically bounding limit repeats.

**Approach C: Bidirectional BFS Exploration**
*   **Idea:** Enqueuing structurally simultaneous expansions stemming specifically identically from explicitly known Source constraints mapping simultaneously against Target Origins.
*   **Time Complexity:** Mitigates recursive compounding dropping expansion depth testing strictly down from $\mathcal{O}(b^d)$ deeply mathematically optimized to tightly bound $\mathcal{O}(b^{d/2})$.
*   **Space Complexity:** $\mathcal{O}(b^{d/2})$ scaling logic tracking isolated overlapping Set intersections limits instead of Queue logic.

<details>
<summary><b>💻 Canonical Code Implementations</b> (Click to expand)</summary>

### Shortest Path in Binary Matrix
```java
class Solution {
    public int shortestPathBinaryMatrix(int[][] grid) {
        if (grid[0][0] == 1) return -1;
        int n = grid.length;
        if (n == 1) return 1;
        
        Queue<int[]> q = new LinkedList<>();
        q.add(new int[]{0, 0});
        grid[0][0] = 1; // Mark visited natively mapped
        
        int[][] dirs = {{1,0},{-1,0},{0,1},{0,-1},{1,1},{-1,-1},{1,-1},{-1,1}};
        int steps = 1;
        
        while (!q.isEmpty()) {
            int size = q.size();
            for (int i = 0; i < size; i++) {
                int[] curr = q.poll();
                if (curr[0] == n - 1 && curr[1] == n - 1) return steps;
                
                for (int[] d : dirs) {
                    int nx = curr[0] + d[0], ny = curr[1] + d[1];
                    // Pruned safely bounded tracking optimal limit maps
                    if (nx >= 0 && nx < n && ny >= 0 && ny < n && grid[nx][ny] == 0) {
                        grid[nx][ny] = 1;
                        q.add(new int[]{nx, ny});
                    }
                }
            }
            steps++;
        }
        return -1;
    }
}
```

### Minimum Knight Moves (Standard BFS)
```java
class Solution {
    public int minKnightMoves(int x, int y) {
        x = Math.abs(x); y = Math.abs(y); // Symmetrical property folding map quadrant natively
        Queue<int[]> q = new LinkedList<>();
        q.add(new int[]{0, 0});
        Set<String> visited = new HashSet<>();
        visited.add("0,0");
        
        int[][] dirs = {{1,2},{2,1},{2,-1},{1,-2},{-1,-2},{-2,-1},{-2,1},{-1,2}};
        int steps = 0;
        
        while (!q.isEmpty()) {
            int size = q.size();
            for (int i = 0; i < size; i++) {
                int[] curr = q.poll();
                if (curr[0] == x && curr[1] == y) return steps;
                
                for (int[] d : dirs) {
                    int nx = curr[0] + d[0];
                    int ny = curr[1] + d[1];
                    // Prune bounds effectively maintaining logical spans validating coordinate
                    if (nx >= -2 && ny >= -2 && visited.add(nx + "," + ny)) {
                        q.add(new int[]{nx, ny});
                    }
                }
            }
            steps++;
        }
        return -1;
    }
}
```

### Sliding Puzzle (State Space Mapping BFS)
```java
class Solution {
    public int slidingPuzzle(int[][] board) {
        String target = "123450";
        StringBuilder sb = new StringBuilder();
        for (int[] row : board) for (int val : row) sb.append(val);
        String start = sb.toString();
        
        if (start.equals(target)) return 0;
        
        // Maps adjacencies limits explicitly bounded matching string offsets
        int[][] dirs = {{1, 3}, {0, 2, 4}, {1, 5}, {0, 4}, {1, 3, 5}, {2, 4}};
        Queue<String> q = new LinkedList<>();
        Set<String> visited = new HashSet<>();
        
        q.add(start);
        visited.add(start);
        int moves = 0;
        
        while (!q.isEmpty()) {
            int size = q.size();
            for (int i = 0; i < size; i++) {
                String curr = q.poll();
                if (curr.equals(target)) return moves;
                
                int zeroIdx = curr.indexOf('0');
                for (int swapIdx : dirs[zeroIdx]) {
                    StringBuilder nextSb = new StringBuilder(curr);
                    nextSb.setCharAt(zeroIdx, curr.charAt(swapIdx));
                    nextSb.setCharAt(swapIdx, '0');
                    String next = nextSb.toString(); // Config space mutated naturally
                    
                    if (visited.add(next)) q.add(next);
                }
            }
            moves++;
        }
        return -1;
    }
}
```
</details>

---

## 6. Grid + Min-Heap (Advanced Boundary Reduction Traversal)
**Problems:** Trapping Rain Water II

### 💡 Approaches & Complexities

**Approach: Dijkstra Priority Queue Validation (Boundary Shrinking)**
*   **Idea:** Basic standard iteration depth bounds systematically fail identifying complex multi-axis matrix valley basins structurally mapped relying purely on absolute minimum enclosed boundary walls dictating limits mapping pooling logic analytically.
*   **Implementation:** Expand logic caching completely tracking matrix border configurations inherently mapping standard bounds caching values directly into a strict `Min-Heap` constraint Queue evaluating physically polling minimum bounding values evaluating matrix structures. Shrink walls progressively analyzing relative internal limits pooling depths calculating positive variance mappings natively.
*   **Time Complexity:** $\mathcal{O}(M \times N \times \log(M \times N))$ constrained handling sorting parameters pushing arrays per iteration constraints into heap maps cleanly.
*   **Space Complexity:** $\mathcal{O}(M \times N)$ explicit indexing limits configuring visited constraints verifying redundant paths limits naturally.

<details>
<summary><b>💻 Canonical Code Implementations</b> (Click to expand)</summary>

### Trapping Rain Water II (Min-Heap BFS Bounds Reduction)
```java
class Solution {
    public int trapRainWater(int[][] heightMap) {
        if (heightMap == null || heightMap.length == 0) return 0;
        int m = heightMap.length, n = heightMap[0].length;
        
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> Integer.compare(a[2], b[2]));
        boolean[][] visited = new boolean[m][n];
        
        // Init 1: Push all outer perimeter walls mapping limits inwards securely
        for (int i = 0; i < m; i++) {
            visited[i][0] = true; pq.add(new int[]{i, 0, heightMap[i][0]});
            visited[i][n-1] = true; pq.add(new int[]{i, n-1, heightMap[i][n-1]});
        }
        for (int j = 0; j < n; j++) {
            visited[0][j] = true; pq.add(new int[]{0, j, heightMap[0][j]});
            visited[m-1][j] = true; pq.add(new int[]{m-1, j, heightMap[m-1][j]});
        }
        
        int[][] dirs = {{1,0},{-1,0},{0,1},{0,-1}};
        int water = 0;
        int maxBoundaryHeight = 0; // Represents tracking absolute bounding perimeter limit securely
        
        while (!pq.isEmpty()) {
            int[] curr = pq.poll(); // Guaranteed strictly minimum bound extracted securely
            int r = curr[0], c = curr[1], h = curr[2];
            maxBoundaryHeight = Math.max(maxBoundaryHeight, h);
            
            for (int[] d : dirs) {
                int nr = r + d[0], nc = c + d[1];
                if (nr >= 0 && nr < m && nc >= 0 && nc < n && !visited[nr][nc]) {
                    visited[nr][nc] = true;
                    // Pool accumulates explicitly tracking boundary difference mapping bounds effectively
                    if (heightMap[nr][nc] < maxBoundaryHeight) {
                        water += maxBoundaryHeight - heightMap[nr][nc];
                    }
                    pq.add(new int[]{nr, nc, heightMap[nr][nc]});
                }
            }
        }
        return water;
    }
}
```
</details>
# Clone Graph

**Idea:** Deep copy an undirected graph using a map from original to cloned nodes.
**Complexity:** Time O(V+E), Space O(V).

```java
/* Definition for a Node. */
class Node {
    public int val;
    public List<Node> neighbors;
    public Node() { val = 0; neighbors = new ArrayList<>(); }
    public Node(int _val) { val = _val; neighbors = new ArrayList<>(); }
    public Node(int _val, ArrayList<Node> _neighbors) { val = _val; neighbors = _neighbors; }
}
```

## DFS Clone

**Idea:** Recursively copy nodes, storing clones in a hashmap.
**Complexity:** Time O(V+E), Space O(V) recursion stack.

```java
class Solution {
    public Node cloneGraph(Node node) {
        if (node == null) return null;
        Map<Node, Node> map = new HashMap<>();
        dfs(node, map);
        return map.get(node);
    }
    private void dfs(Node node, Map<Node, Node> map) {
        map.put(node, new Node(node.val));
        for (Node nb : node.neighbors) {
            if (!map.containsKey(nb)) dfs(nb, map);
            map.get(node).neighbors.add(map.get(nb));
        }
    }
}
```

## BFS Clone

**Idea:** Iteratively copy nodes using a queue.
**Complexity:** Time O(V+E), Space O(V).

```java
class Solution {
    public Node cloneGraph(Node node) {
        if (node == null) return null;
        Map<Node, Node> map = new HashMap<>();
        Queue<Node> q = new LinkedList<>();
        q.add(node);
        map.put(node, new Node(node.val));
        while (!q.isEmpty()) {
            Node cur = q.remove();
            for (Node nb : cur.neighbors) {
                if (!map.containsKey(nb)) {
                    map.put(nb, new Node(nb.val));
                    q.add(nb);
                }
                map.get(cur).neighbors.add(map.get(nb));
            }
        }
        return map.get(node);
    }
}
```

# Reorder Routes to Make All Paths Lead to City Zero

## DFS

**Idea:** Build directed graph with reversal flag and DFS from city 0, counting needed reversals.
**Complexity:** Time O(N+E), Space O(N) recursion.

```java
class Solution {
    public int minReorder(int n, int[][] connections) {
        List<int[]>[] g = new ArrayList[n];
        for (int i = 0; i < n; i++) g[i] = new ArrayList<>();
        for (int[] c : connections) {
            g[c[0]].add(new int[]{c[1], 1}); // original direction needs reversal
            g[c[1]].add(new int[]{c[0], 0}); // reverse direction is fine
        }
        boolean[] vis = new boolean[n];
        return dfs(g, vis, 0);
    }
    private int dfs(List<int[]>[] g, boolean[] vis, int u) {
        vis[u] = true;
        int res = 0;
        for (int[] e : g[u]) {
            int v = e[0], rev = e[1];
            if (!vis[v]) {
                res += rev + dfs(g, vis, v);
            }
        }
        return res;
    }
}
```

## BFS

**Idea:** Same graph, BFS from 0 counting reversal edges.
**Complexity:** Time O(N+E), Space O(N).

```java
class Solution {
    public int minReorder(int n, int[][] connections) {
        List<int[]>[] g = new ArrayList[n];
        for (int i = 0; i < n; i++) g[i] = new ArrayList<>();
        for (int[] c : connections) {
            g[c[0]].add(new int[]{c[1], 1});
            g[c[1]].add(new int[]{c[0], 0});
        }
        boolean[] vis = new boolean[n];
        Queue<Integer> q = new LinkedList<>();
        q.offer(0); vis[0] = true;
        int ans = 0;
        while (!q.isEmpty()) {
            int u = q.poll();
            for (int[] e : g[u]) {
                int v = e[0], rev = e[1];
                if (!vis[v]) {
                    ans += rev;
                    vis[v] = true;
                    q.offer(v);
                }
            }
        }
        return ans;
    }
}
```

# Eventual Safe States

## DFS

**Idea:** Color‑coding (0 = unvisited, 1 = visiting, 2 = safe) to detect cycles; safe nodes are those that finish without hitting a cycle.
**Complexity:** Time O(V+E), Space O(V) recursion.

```java
class Solution {
    public List<Integer> eventualSafeNodes(int[][] graph) {
        int n = graph.length;
        int[] color = new int[n];
        List<Integer> safe = new ArrayList<>();
        for (int i = 0; i < n; i++) if (dfs(graph, i, color)) safe.add(i);
        return safe;
    }
    private boolean dfs(int[][] g, int v, int[] c) {
        if (c[v] != 0) return c[v] == 2;
        c[v] = 1;
        for (int nb : g[v]) if (!dfs(g, nb, c)) return false;
        c[v] = 2;
        return true;
    }
}
```

## BFS (Topological)

**Idea:** Reverse graph, start from nodes with indegree 0, propagate safety.
**Complexity:** Time O(V+E), Space O(V).

```java
class Solution {
    public List<Integer> eventualSafeNodes(int[][] graph) {
        int n = graph.length;
        int[] indeg = new int[n];
        List<List<Integer>> rev = new ArrayList<>();
        for (int i = 0; i < n; i++) rev.add(new ArrayList<>());
        for (int i = 0; i < n; i++)
            for (int nb : graph[i]) { rev.get(nb).add(i); indeg[i]++; }
        Queue<Integer> q = new LinkedList<>();
        for (int i = 0; i < n; i++) if (indeg[i] == 0) q.offer(i);
        boolean[] safe = new boolean[n];
        while (!q.isEmpty()) {
            int v = q.poll();
            safe[v] = true;
            for (int pre : rev.get(v)) if (--indeg[pre] == 0) q.offer(pre);
        }
        List<Integer> res = new ArrayList<>();
        for (int i = 0; i < n; i++) if (safe[i]) res.add(i);
        return res;
    }
}
```

# Evaluate Division

**Idea:** Build weighted bidirectional graph of equations; for each query perform DFS to compute product of edge weights.
**Complexity:** Build O(E), each query O(V+E) worst case; overall O(Q·(V+E)). Space O(V+E).

```java
class Solution {
    public double[] calcEquation(List<List<String>> eq, double[] val, List<List<String>> qs) {
        Map<String, Map<String, Double>> g = build(eq, val);
        double[] ans = new double[qs.size()];
        for (int i = 0; i < qs.size(); i++)
            ans[i] = dfs(g, qs.get(i).get(0), qs.get(i).get(1), new HashSet<>());
        return ans;
    }
    private double dfs(Map<String, Map<String, Double>> g, String s, String t, Set<String> seen) {
        if (!g.containsKey(s)) return -1.0;
        if (g.get(s).containsKey(t)) return g.get(s).get(t);
        seen.add(s);
        for (var e : g.get(s).entrySet()) {
            if (!seen.contains(e.getKey())) {
                double r = dfs(g, e.getKey(), t, seen);
                if (r != -1.0) return r * e.getValue();
            }
        }
        return -1.0;
    }
    private Map<String, Map<String, Double>> build(List<List<String>> eq, double[] val) {
        Map<String, Map<String, Double>> g = new HashMap<>();
        for (int i = 0; i < eq.size(); i++) {
            String a = eq.get(i).get(0), b = eq.get(i).get(1);
            g.computeIfAbsent(a, k -> new HashMap<>()).put(b, val[i]);
            g.computeIfAbsent(b, k -> new HashMap<>()).put(a, 1.0/val[i]);
        }
        return g;
    }
}
```

# Detonate Maximum Bombs

**Idea:** Build directed graph where an edge i→j exists if bomb j is within radius of i; then for each bomb run DFS to count reachable bombs, taking maximum.
**Complexity:** Build O(N²), each DFS O(N+E); overall O(N²). Space O(N²) for adjacency list.

```java
class Solution {
    public int maximumDetonation(int[][] bombs) {
        int n = bombs.length;
        List<Integer>[] g = new ArrayList[n];
        for (int i = 0; i < n; i++) g[i] = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            long x1 = bombs[i][0], y1 = bombs[i][1], r = bombs[i][2];
            for (int j = 0; j < n; j++) if (i != j) {
                long dx = x1 - bombs[j][0];
                long dy = y1 - bombs[j][1];
                if (dx*dx + dy*dy <= r*r) g[i].add(j);
            }
        }
        int best = 0;
        for (int i = 0; i < n; i++) {
            boolean[] vis = new boolean[n];
            best = Math.max(best, dfs(g, i, vis));
        }
        return best;
    }
    private int dfs(List<Integer>[] g, int v, boolean[] vis) {
        vis[v] = true;
        int cnt = 1;
        for (int nb : g[v]) if (!vis[nb]) cnt += dfs(g, nb, vis);
        return cnt;
    }
}
```

# Number of Provinces (Connected Components in Undirected Graph)

**Idea:** Treat adjacency matrix as graph; run DFS/BFS to count connected components.
**Complexity:** Time O(N²) for matrix traversal, Space O(N) recursion/stack.

```java
class Solution {
    public int findCircleNum(int[][] isConnected) {
        int n = isConnected.length;
        boolean[] vis = new boolean[n];
        int provinces = 0;
        for (int i = 0; i < n; i++) if (!vis[i]) {
            dfs(isConnected, vis, i);
            provinces++;
        }
        return provinces;
    }
    private void dfs(int[][] g, boolean[] vis, int u) {
        vis[u] = true;
        for (int v = 0; v < g.length; v++)
            if (g[u][v] == 1 && !vis[v]) dfs(g, vis, v);
    }
}
```
# Course Schedule

## 1️⃣ Course Schedule (Can Finish) – BFS (Kahn's Algorithm)

**Idea:** Detect a cycle in the prerequisite graph via topological sorting; if all courses are processed, the schedule is feasible.
**Complexity:** `O(V + E)` time, `O(V)` space.

```java
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        // Build adjacency list
        List<List<Integer>> adj = new ArrayList<>();
        for (int i = 0; i < numCourses; i++) adj.add(new ArrayList<>());
        for (int[] pre : prerequisites) adj.get(pre[1]).add(pre[0]); // prereq -> course
        // Compute indegrees
        int[] indegree = new int[numCourses];
        for (int i = 0; i < numCourses; i++)
            for (int nxt : adj.get(i)) indegree[nxt]++;
        // Kahn's BFS
        Queue<Integer> q = new LinkedList<>();
        for (int i = 0; i < numCourses; i++) if (indegree[i] == 0) q.offer(i);
        int visited = 0;
        while (!q.isEmpty()) {
            int cur = q.poll();
            visited++;
            for (int nxt : adj.get(cur)) {
                if (--indegree[nxt] == 0) q.offer(nxt);
            }
        }
        return visited == numCourses;
    }
}
```

## 2️⃣ Course Schedule II (Find Order) – BFS (Kahn's Algorithm)

**Idea:** Perform a topological sort and return the order; an empty array signals a cycle.
**Complexity:** `O(V + E)` time, `O(V)` space.

```java
class Solution {
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        List<List<Integer>> adj = new ArrayList<>();
        for (int i = 0; i < numCourses; i++) adj.add(new ArrayList<>());
        for (int[] pre : prerequisites) adj.get(pre[1]).add(pre[0]);
        int[] indegree = new int[numCourses];
        for (int i = 0; i < numCourses; i++)
            for (int nxt : adj.get(i)) indegree[nxt]++;
        Queue<Integer> q = new LinkedList<>();
        for (int i = 0; i < numCourses; i++) if (indegree[i] == 0) q.offer(i);
        List<Integer> order = new ArrayList<>();
        while (!q.isEmpty()) {
            int cur = q.poll();
            order.add(cur);
            for (int nxt : adj.get(cur)) {
                if (--indegree[nxt] == 0) q.offer(nxt);
            }
        }
        if (order.size() != numCourses) return new int[0]; // cycle
        int[] res = new int[numCourses];
        for (int i = 0; i < numCourses; i++) res[i] = order.get(i);
        return res;
    }
}
```

## 3️⃣ Course Schedule IV – BFS + Hashing (Transitive Prerequisite Sets)

**Idea:** While processing nodes in topological order, propagate a `Set<Integer>` of all prerequisites for each course; queries are answered by membership checks.
**Complexity:** Building sets `O(V·(V+E))` worst‑case, query `O(1)`; space `O(V²)` for the prerequisite maps.

```java
class Solution {
    public List<Boolean> checkIfPrerequisite(int n, int[][] prerequisites, int[][] queries) {
        int[] indegree = new int[n];
        Map<Integer, Set<Integer>> adj = new HashMap<>();
        Map<Integer, Set<Integer>> preMap = new HashMap<>();
        for (int i = 0; i < n; i++) {
            adj.put(i, new HashSet<>());
            preMap.put(i, new HashSet<>());
        }
        for (int[] p : prerequisites) {
            indegree[p[1]]++;
            adj.get(p[0]).add(p[1]);
        }
        Queue<Integer> q = new LinkedList<>();
        for (int i = 0; i < n; i++) if (indegree[i] == 0) q.offer(i);
        while (!q.isEmpty()) {
            int cur = q.poll();
            for (int nxt : adj.get(cur)) {
                preMap.get(nxt).add(cur);
                preMap.get(nxt).addAll(preMap.get(cur));
                if (--indegree[nxt] == 0) q.offer(nxt);
            }
        }
        List<Boolean> ans = new ArrayList<>();
        for (int[] qy : queries) {
            ans.add(preMap.get(qy[1]).contains(qy[0]));
        }
        return ans;
    }
}
```

## 4️⃣ Course Schedule IV – Floyd‑Warshall (All‑Pairs Reachability)

**Idea:** Compute the transitive closure of the prerequisite graph using dynamic programming on a boolean matrix.
**Complexity:** `O(V³)` time, `O(V²)` space.

```java
class Solution {
    public List<Boolean> checkIfPrerequisite(int n, int[][] prerequisites, int[][] queries) {
        boolean[][] reach = new boolean[n][n];
        for (int[] p : prerequisites) reach[p[0]][p[1]] = true;
        for (int k = 0; k < n; k++)
            for (int i = 0; i < n; i++)
                if (reach[i][k])
                    for (int j = 0; j < n; j++)
                        reach[i][j] = reach[i][j] || reach[k][j];
        List<Boolean> ans = new ArrayList<>();
        for (int[] q : queries) ans.add(reach[q[0]][q[1]]);
        return ans;
    }
}

## 5️⃣ Parallel Courses (Minimum Semesters) – BFS Level Tracking

**Idea:** Minimum semesters = maximum depth of the graph. 
Use Kahn BFS and track the number of "levels" (semesters) needed to process all nodes.
**Complexity:** `O(V + E)` time, `O(V)` space.

```java
class Solution {
    public int minimumSemesters(int n, int[][] relations) {
        List<List<Integer>> adj = new ArrayList<>();
        for (int i = 0; i <= n; i++) adj.add(new ArrayList<>());
        int[] indegree = new int[n + 1];
        for (int[] r : relations) {
            adj.get(r[0]).add(r[1]);
            indegree[r[1]]++;
        }
        Queue<Integer> q = new LinkedList<>();
        for (int i = 1; i <= n; i++) if (indegree[i] == 0) q.offer(i);
        int semesters = 0, count = 0;
        while (!q.isEmpty()) {
            int size = q.size();
            for (int i = 0; i < size; i++) {
                int cur = q.poll();
                count++;
                for (int nxt : adj.get(cur)) {
                    if (--indegree[nxt] == 0) q.offer(nxt);
                }
            }
            semesters++;
        }
        return count == n ? semesters : -1;
    }
}
```

## 6️⃣ Parallel Courses III (Minimum Time) – Kahn's BFS + DP

**Idea:** Track the earliest possible finish time for each course (`maxTime[v] = max(maxTime[v], maxTime[u] + duration[v])`). The answer is the maximum value in the `maxTime` array.
**Complexity:** `O(V + E)` time, `O(V)` space.

```java
class Solution {
    public int minimumTime(int n, int[][] relations, int[] time) {
        List<List<Integer>> adj = new ArrayList<>();
        for (int i = 0; i <= n; i++) adj.add(new ArrayList<>());
        int[] indegree = new int[n + 1];
        for (int[] r : relations) {
            adj.get(r[0]).add(r[1]);
            indegree[r[1]]++;
        }
        int[] maxTime = new int[n + 1];
        Queue<Integer> q = new LinkedList<>();
        for (int i = 1; i <= n; i++) {
            if (indegree[i] == 0) {
                q.offer(i);
                maxTime[i] = time[i - 1];
            }
        }
        while (!q.isEmpty()) {
            int u = q.poll();
            for (int v : adj.get(u)) {
                maxTime[v] = Math.max(maxTime[v], maxTime[u] + time[v - 1]);
                if (--indegree[v] == 0) q.offer(v);
            }
        }
        int ans = 0;
        for (int t : maxTime) ans = Math.max(ans, t);
        return ans;
    }
}

## 7️⃣ Alien Dictionary – DAG Construction + Kahn's BFS

**Idea:** Build a directed graph where an edge `u -> v` exists if character `u` comes before `v` in the alien language (found by comparing adjacent words). Use Kahn's BFS for topological sort; check for prefix errors (e.g., "abc" before "ab" is invalid) and cycles.
**Complexity:** `O(C)` time where `C` is the total length of all words, `O(1)` space (limited by 26 characters).

```java
class Solution {
    public String alienOrder(String[] words) {
        Map<Character, List<Character>> adj = new HashMap<>();
        Map<Character, Integer> counts = new HashMap<>();
        for (String word : words) {
            for (char c : word.toCharArray()) {
                counts.put(c, 0);
                adj.put(c, new ArrayList<>());
            }
        }
        for (int i = 0; i < words.length - 1; i++) {
            String w1 = words[i], w2 = words[i + 1];
            if (w1.length() > w2.length() && w1.startsWith(w2)) return "";
            for (int j = 0; j < Math.min(w1.length(), w2.length()); j++) {
                char c1 = w1.charAt(j), c2 = w2.charAt(j);
                if (c1 != c2) {
                    adj.get(c1).add(c2);
                    counts.put(c2, counts.get(c2) + 1);
                    break;
                }
            }
        }
        StringBuilder sb = new StringBuilder();
        Queue<Character> q = new LinkedList<>();
        for (char c : counts.keySet()) if (counts.get(c) == 0) q.add(c);
        while (!q.isEmpty()) {
            char c = q.poll();
            sb.append(c);
            for (char next : adj.get(c)) {
                counts.put(next, counts.get(next) - 1);
                if (counts.get(next) == 0) q.add(next);
            }
        }
        return sb.length() < counts.size() ? "" : sb.toString();
    }
}
```

## 8️⃣ Verifying An Alien Dictionary – Linear Scan + Custom Order Map

**Idea:** Map the custom alphabet to its rank (0-25). Compare adjacent words character-by-character; if any pair violates the order, or if a longer word is a prefix of a shorter following word, return false.
**Complexity:** `O(C)` time where `C` is total length of all words, `O(1)` space.

```java
class Solution {
    public boolean isAlienSorted(String[] words, String order) {
        int[] rank = new int[26];
        for (int i = 0; i < 26; i++) rank[order.charAt(i) - 'a'] = i;
        
        for (int i = 0; i < words.length - 1; i++) {
            String w1 = words[i], w2 = words[i+1];
            boolean diffFound = false;
            for (int j = 0; j < Math.min(w1.length(), w2.length()); j++) {
                if (w1.charAt(j) != w2.charAt(j)) {
                    if (rank[w1.charAt(j)-'a'] > rank[w2.charAt(j)-'a']) return false;
                    diffFound = true;
                    break;
                }
            }
            if (!diffFound && w1.length() > w2.length()) return false;
        }
        return true;
    }
}

## 9️⃣ Find All Possible Recipes from Given Supplies – Multi-Source BFS (Kahns)

**Idea Build an dependency graph where an edge ingredient -> recipe exists. Initialize indegree[recipe] as the number of its required ingredients. Start Kahn BFS with the initial `supplies`. If a recipes indegree hits 0, it is "crafted" and added to the queue to potentially satisfy other recipes.
**Complexity:** `O(R + V + E)` where `R` is number of recipes, `V` is total unique ingredients, and `E` is total dependency relationships.

```java
class Solution {
    public List<String> findAllRecipes(String[] recipes, List<List<String>> ingredients, String[] supplies) {
        Map<String, List<String>> adj = new HashMap<>();
        Map<String, Integer> indegree = new HashMap<>();
        for (int i = 0; i < recipes.length; i++) {
            indegree.put(recipes[i], ingredients.get(i).size());
            for (String ing : ingredients.get(i)) {
                adj.computeIfAbsent(ing, k -> new ArrayList<>()).add(recipes[i]);
            }
        }
        
        List<String> result = new ArrayList<>();
        Queue<String> q = new LinkedList<>();
        for (String s : supplies) q.add(s);
        
        while (!q.isEmpty()) {
            String cur = q.poll();
            if (adj.containsKey(cur)) {
                for (String recipe : adj.get(cur)) {
                    indegree.put(recipe, indegree.get(recipe) - 1);
                    if (indegree.get(recipe) == 0) {
                        q.add(recipe);
                        result.add(recipe);
                    }
                }
            }
        }
        return result;
    }
}
```

## 🔟 Build a Matrix With Conditions – Dual Topological Sort

**Idea:** Treat row and column conditions as two separate dependency graphs. Perform topological sort on both to find a valid row-ordering and column-ordering for numbers `1` to `k`. If a cycle exists in either, the matrix cannot be built. Map each number to its `(row, col)` coordinate in the final result.
**Complexity:** `O(k + RowCond + ColCond)` time and space.

```java
class Solution {
    public int[][] buildMatrix(int k, int[][] rowConditions, int[][] colConditions) {
        int[] rowOrder = topoSort(k, rowConditions);
        int[] colOrder = topoSort(k, colConditions);
        if (rowOrder == null || colOrder == null) return new int[0][0];
        
        int[][] result = new int[k][k];
        int[] rowPos = new int[k + 1];
        int[] colPos = new int[k + 1];
        for (int i = 0; i < k; i++) {
            rowPos[rowOrder[i]] = i;
            colPos[colOrder[i]] = i;
        }
        for (int i = 1; i <= k; i++) {
            result[rowPos[i]][colPos[i]] = i;
        }
        return result;
    }
    
    private int[] topoSort(int k, int[][] conditions) {
        List<Integer>[] adj = new ArrayList[k + 1];
        int[] indegree = new int[k + 1];
        for (int i = 1; i <= k; i++) adj[i] = new ArrayList<>();
        for (int[] c : conditions) {
            adj[c[0]].add(c[1]);
            indegree[c[1]]++;
        }
        Queue<Integer> q = new LinkedList<>();
        for (int i = 1; i <= k; i++) if (indegree[i] == 0) q.offer(i);
        int[] res = new int[k];
        int idx = 0;
        while (!q.isEmpty()) {
            int cur = q.poll();
            res[idx++] = cur;
            for (int next : adj[cur]) {
                if (--indegree[next] == 0) q.offer(next);
            }
        }
        return idx == k ? res : null;
    }
}

## 1️⃣1️⃣ Largest Color Value in a Directed Graph – Kahn's BFS + DP

**Idea:** Combine topological sort (Kahn's BFS) with dynamic programming. Maintain a 2D array `dp[n][26]` where `dp[u][c]` represents the maximum frequency of color `c` on any path ending at node `u`. When moving from `u` to `v`, update `dp[v][c] = max(dp[v][c], dp[u][c])`. After processing all predecessors of `v`, add its own color to the count.
**Complexity:** `O(V + E)` time (technically `O(26 * (V + E))`), `O(26 * V)` space.

```java
class Solution {
    public int largestPathValue(String colors, int[][] edges) {
        int n = colors.length();
        List<Integer>[] adj = new ArrayList[n];
        int[] indegree = new int[n];
        for (int i = 0; i < n; i++) adj[i] = new ArrayList<>();
        for (int[] e : edges) {
            adj[e[0]].add(e[1]);
            indegree[e[1]]++;
        }
        
        int[][] dp = new int[n][26];
        Queue<Integer> q = new LinkedList<>();
        for (int i = 0; i < n; i++) {
            if (indegree[i] == 0) {
                q.offer(i);
            }
        }
        
        int visited = 0, maxVal = 0;
        while (!q.isEmpty()) {
            int u = q.poll();
            visited++;
            int colorU = colors.charAt(u) - 'a';
            maxVal = Math.max(maxVal, ++dp[u][colorU]);
            
            for (int v : adj[u]) {
                for (int c = 0; c < 26; c++) {
                    dp[v][c] = Math.max(dp[v][c], dp[u][c]);
                }
                if (--indegree[v] == 0) q.offer(v);
            }
        }
        
        return visited == n ? maxVal : -1;
    }
}
```
# Phase 4: Union-Find (Disjoint Set Union)

Union-Find is the gold standard for **dynamic connectivity** problems. While BFS/DFS can find connected components in static graphs, Union-Find excels when edges are added incrementally, or when you need to group entities efficiently.

---

## 🏆 Optimized Union-Find Template (Path Compression + Union by Rank/Size)

**SDE-2 Expectation:** You must be able to implement this perfectly from memory. Path compression flattens the structure, while Union by Rank/Size keeps the tree balanced.

**Complexity:** `O(α(N))` per operation, where `α` is the inverse Ackermann function (effectively constant `O(1)` for all practical values of `N`).

```java
class UnionFind {
    private int[] parent;
    private int[] rank; // Or size[]
    private int count;  // Number of connected components

    public UnionFind(int n) {
        parent = new int[n];
        rank = new int[n];
        count = n;
        for (int i = 0; i < n; i++) parent[i] = i;
    }

    // Path Compression: Flattens the tree during find
    public int find(int i) {
        if (parent[i] == i) return i;
        return parent[i] = find(parent[i]); 
    }

    // Union by Rank: Attaches shorter tree under taller tree
    public boolean union(int i, int j) {
        int rootI = find(i);
        int rootJ = find(j);
        if (rootI != rootJ) {
            if (rank[rootI] < rank[rootJ]) parent[rootI] = rootJ;
            else if (rank[rootI] > rank[rootJ]) parent[rootJ] = rootI;
            else {
                parent[rootI] = rootJ;
                rank[rootJ]++;
            }
            count--;
            return true;
        }
        return false;
    }
    
    // Alternative: Union by Size
    // if (size[rootI] < size[rootJ]) { parent[rootI] = rootJ; size[rootJ] += size[rootI]; }
    
    public int getCount() { return count; }
}
```

---

## 1️⃣ Redundant Connection – Cycle Detection in Undirected Graphs

**Idea:** Iterate through edges and perform `union(u, v)`. If `union` returns `false`, it means `u` and `v` are already connected, and this edge forms a cycle. In a tree-like graph, this is the "redundant" edge.
**Complexity:** `O(N·α(N))` time, `O(N)` space.

```java
class Solution {
    public int[] findRedundantConnection(int[][] edges) {
        int n = edges.length;
        UnionFind uf = new UnionFind(n + 1);
        for (int[] edge : edges) {
            if (!uf.union(edge[0], edge[1])) return edge;
        }
        return new int[0];
    }
}
```

---

## 2️⃣ Accounts Merge – Complex Multi-Entity Grouping

**Idea:** Map each email to a unique ID and use Union-Find to group IDs that appear in the same account. Then, aggregate all emails by their component's root and sort them for the final output.
**Complexity:** `O(N·K·α(N·K) + N·K·log(N·K))` where `N` is the number of accounts and `K` is the average number of emails per account.

```java
class Solution {
    public List<List<String>> accountsMerge(List<List<String>> accounts) {
        int n = accounts.size();
        UnionFind uf = new UnionFind(n);
        Map<String, Integer> emailToIndex = new HashMap<>();

        for (int i = 0; i < n; i++) {
            for (int j = 1; j < accounts.get(i).size(); j++) {
                String email = accounts.get(i).get(j);
                if (emailToIndex.containsKey(email)) uf.union(i, emailToIndex.get(email));
                else emailToIndex.put(email, i);
            }
        }

        Map<Integer, List<String>> components = new HashMap<>();
        for (String email : emailToIndex.keySet()) {
            int root = uf.find(emailToIndex.get(email));
            components.computeIfAbsent(root, k -> new ArrayList<>()).add(email);
        }

        List<List<String>> merged = new ArrayList<>();
        for (int root : components.keySet()) {
            List<String> emails = components.get(root);
            Collections.sort(emails);
            List<String> ans = new ArrayList<>();
            ans.add(accounts.get(root).get(0));
            ans.addAll(emails);
            merged.add(ans);
        }
        return merged;
    }
}
```

---

## 3️⃣ Graph Valid Tree – Component Count + Cycle Detection

**Idea:** A valid tree must have exactly `n-1` edges and be fully connected. Use DSU to detect cycles (a `union` returning false) and then check if only `1` component remains.
**Complexity:** `O(N·α(N))` time.

```java
class Solution {
    public boolean validTree(int n, int[][] edges) {
        if (edges.length != n - 1) return false;
        UnionFind uf = new UnionFind(n);
        for (int[] e : edges) {
            if (!uf.union(e[0], e[1])) return false;
        }
        return uf.getCount() == 1;
    }
}
```

---

## 4️⃣ Regions Cut By Slashes – Grid Triangulation Mapping

**Idea:** Split each `1x1` grid cell into 4 triangles (0: Top, 1: Right, 2: Bottom, 3: Left). Use DSU to merge triangles within a cell based on the slash (`/` or `\`) and merge adjacent triangles across cell boundaries. The number of components is the number of regions.
**Complexity:** `O(N²·α(N²))` time.

```java
class Solution {
    public int regionsBySlashes(String[] grid) {
        int n = grid.length;
        UnionFind uf = new UnionFind(4 * n * n);
        for (int r = 0; r < n; r++) {
            for (int c = 0; c < n; c++) {
                int base = 4 * (r * n + c);
                char val = grid[r].charAt(c);
                if (val != '/') { uf.union(base + 0, base + 1); uf.union(base + 2, base + 3); }
                if (val != '\\') { uf.union(base + 0, base + 3); uf.union(base + 1, base + 2); }
                if (r < n - 1) uf.union(base + 2, base + 4 * ((r + 1) * n + c) + 0);
                if (c < n - 1) uf.union(base + 1, base + 4 * (r * n + (c + 1)) + 3);
            }
        }
        return uf.getCount();
    }
}
```

---

## 5️⃣ Remove Max Number of Edges... – Dual-Pass Parallel DSU

**Idea:** Maintain two DSUs, one for Alice and one for Bob. First, process "both-access" edges (Type 3) to maximize their use. Then process Type 1 (Alice) and Type 2 (Bob). Count successful unions; any edge that doesn't merge components is redundant.
**Complexity:** `O(E·α(N))` time.

```java
class Solution {
    public int maxNumEdgesToRemove(int n, int[][] edges) {
        UnionFind alice = new UnionFind(n + 1), bob = new UnionFind(n + 1);
        int usedEdges = 0;
        for (int[] e : edges) { if (e[0] == 3) { if (alice.union(e[1], e[2])) { bob.union(e[1], e[2]); usedEdges++; } } }
        for (int[] e : edges) {
            if (e[0] == 1) { if (alice.union(e[1], e[2])) usedEdges++; }
            else if (e[0] == 2) { if (bob.union(e[1], e[2])) usedEdges++; }
        }
        if (alice.getCount() != 2 || bob.getCount() != 2) return -1; // count=2 because index 0 is unused
        return edges.length - usedEdges;
    }
}
```

---

## 6️⃣ Greatest Common Divisor Traversal – Prime Factor Bridge DSU

**Idea:** Numbers form a path if they share a common prime factor. Use DSU to link each number to its prime factors. If all numbers belong to the same component, traversal is possible.
**Complexity:** `O(N·√M + N·α(N))` where `M` is the max value in `nums`.

```java
class Solution {
    public boolean canTraverseAllPairs(int[] nums) {
        if (nums.length == 1) return true;
        int max = 0; for (int x : nums) { if (x == 1) return false; max = Math.max(max, x); }
        UnionFind uf = new UnionFind(max + 1);
        for (int x : nums) {
            int d = 2, temp = x;
            while (d * d <= temp) {
                if (temp % d == 0) {
                    uf.union(x, d);
                    while (temp % d == 0) temp /= d;
                }
                d++;
            }
            if (temp > 1) uf.union(x, temp);
        }
        int root = uf.find(nums[0]);
        for (int i = 1; i < nums.length; i++) if (uf.find(nums[i]) != root) return false;
        return true;
    }
}
```

---

## 7️⃣ Number of Good Paths – Value-Ordered DSU + Combinatorics

**Idea:** A "good path" starts and ends at nodes with the same value where all intermediate nodes are $\le$ that value. Sort nodes by value, process them in order, and use DSU to merge components. For each component being merged, count nodes that share the current maximum value and add `nC2` pairs to the result.
**Complexity:** `O(N log N + N·α(N))` time.

```java
class Solution {
    public int numberOfGoodPaths(int[] vals, int[][] edges) {
        int n = vals.length;
        List<Integer>[] adj = new ArrayList[n];
        TreeMap<Integer, List<Integer>> valToNodes = new TreeMap<>();
        for (int i = 0; i < n; i++) {
            adj[i] = new ArrayList<>();
            valToNodes.computeIfAbsent(vals[i], k -> new ArrayList<>()).add(i);
        }
        for (int[] e : edges) {
            if (vals[e[0]] >= vals[e[1]]) adj[e[0]].add(e[1]); else adj[e[1]].add(e[0]);
        }
        UnionFind uf = new UnionFind(n);
        int[] count = new int[n]; 
        int goodPaths = n; // Each single node is a good path
        for (int val : valToNodes.keySet()) {
            for (int u : valToNodes.get(val)) {
                for (int v : adj[u]) uf.union(u, v);
            }
            Map<Integer, Integer> groupFreq = new HashMap<>(); // root -> count of max-val nodes
            for (int u : valToNodes.get(val)) {
                int root = uf.find(u);
                groupFreq.put(root, groupFreq.getOrDefault(root, 0) + 1);
            }
            for (int f : groupFreq.values()) goodPaths += (f * (f - 1)) / 2;
        }
        return goodPaths;
    }
}
```
# Phase 5: Shortest Path Algorithms & Global Optimization

Shortest path problems range from simple unweighted BFS to complex constrained scenarios. At the SDE-2 level, the expectation is not just knowing Dijkstra, but implementing it with optimal pruning and recognizing when to pivot to alternate algorithms like 0-1 BFS or Floyd-Warshall.

---

## 🏆 Optimized Dijkstra Template (PriorityQueue + Pruning)

**SDE-2 Expectation:** You must explicitly prune redundant paths within the queue loop. If a popped distance is already greater than the currently known shortest distance for that node, discard it immediately.

**Complexity:** `O(E log V)` time, `O(V + E)` space.

```java
class Dijkstra {
    public int[] shortestPath(int n, List<int[]>[] adj, int start) {
        int[] dist = new int[n];
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[start] = 0;

        // PriorityQueue stores [node, current_distance]
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[1] - b[1]);
        pq.offer(new int[]{start, 0});

        while (!pq.isEmpty()) {
            int[] cur = pq.poll();
            int u = cur[0], d = cur[1];

            // CRITICAL SDE-2 PRUNING:
            // Prevents re-processing nodes if a shorter path was already found
            if (d > dist[u]) continue;

            for (int[] edge : adj[u]) {
                int v = edge[0], weight = edge[1];
                if (dist[u] + weight < dist[v]) {
                    dist[v] = dist[u] + weight;
                    pq.offer(new int[]{v, dist[v]});
                }
            }
        }
        return dist;
    }
}
```

---

## 1️⃣ Network Delay Time – Baseline Dijkstra

**Idea:** Standard application of Dijkstra's algorithm. The total time for the signal to reach all nodes is the maximum of the shortest paths from the source to every other node.
**Complexity:** `O(E log V)`.

```java
class Solution {
    public int networkDelayTime(int[][] times, int n, int k) {
        List<int[]>[] adj = new ArrayList[n + 1];
        for (int i = 1; i <= n; i++) adj[i] = new ArrayList<>();
        for (int[] t : times) adj[t[0]].add(new int[]{t[1], t[2]});
        
        int[] dist = new int[n + 1];
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[k] = 0;
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[1] - b[1]);
        pq.add(new int[]{k, 0});
        
        while (!pq.isEmpty()) {
            int[] cur = pq.poll();
            int u = cur[0], d = cur[1];
            if (d > dist[u]) continue;
            for (int[] edge : adj[u]) {
                if (dist[u] + edge[1] < dist[edge[0]]) {
                    dist[edge[0]] = dist[u] + edge[1];
                    pq.add(new int[]{edge[0], dist[edge[0]]});
                }
            }
        }
        int max = 0;
        for (int i = 1; i <= n; i++) {
            if (dist[i] == Integer.MAX_VALUE) return -1;
            max = Math.max(max, dist[i]);
        }
        return max;
    }
}
```

---

## 2️⃣ Cheapest Flights Within K Stops – Constrained Shortest Path

**Idea:** Dijkstra with an added constraint (stops). We use `stops[node]` to track the minimum stops taken to reach a node so far. If we reach a node with more stops and a higher price, we prune. Alternatively, use **Bellman-Ford** (or BFS) for `K+1` iterations.
**Complexity:** `O(K·E)` for Bellman-Ford/BFS.

```java
class Solution {
    public int findCheapestPrice(int n, int[][] flights, int src, int dst, int k) {
        int[] prices = new int[n];
        Arrays.fill(prices, Integer.MAX_VALUE);
        prices[src] = 0;
        
        for (int i = 0; i <= k; i++) {
            int[] temp = Arrays.copyOf(prices, n);
            for (int[] f : flights) {
                int u = f[0], v = f[1], p = f[2];
                if (prices[u] != Integer.MAX_VALUE) {
                    temp[v] = Math.min(temp[v], prices[u] + p);
                }
            }
            prices = temp;
        }
        return prices[dst] == Integer.MAX_VALUE ? -1 : prices[dst];
    }
}
```

---

## 3️⃣ Path with Minimum Effort – Bottleneck Dijkstra

**Idea:** Find a path where the maximum absolute difference between adjacent cells (effort) is minimized. Use Dijkstra, but the "distance" to a neighbor is `max(current_effort, abs(height_diff))`.
**Complexity:** `O(N·M log(NM))`.

```java
class Solution {
    public int minimumEffortPath(int[][] heights) {
        int r = heights.length, c = heights[0].length;
        int[][] dist = new int[r][c];
        for (int[] row : dist) Arrays.fill(row, Integer.MAX_VALUE);
        dist[0][0] = 0;
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[2] - b[2]);
        pq.add(new int[]{0, 0, 0});
        int[][] dirs = {{0,1}, {0,-1}, {1,0}, {-1,0}};
        
        while (!pq.isEmpty()) {
            int[] cur = pq.poll();
            int x = cur[0], y = cur[1], d = cur[2];
            if (x == r - 1 && y == c - 1) return d;
            if (d > dist[x][y]) continue;
            for (int[] dir : dirs) {
                int nx = x + dir[0], ny = y + dir[1];
                if (nx >= 0 && nx < r && ny >= 0 && ny < c) {
                    int nextEffort = Math.max(d, Math.abs(heights[nx][ny] - heights[x][y]));
                    if (nextEffort < dist[nx][ny]) {
                        dist[nx][ny] = nextEffort;
                        pq.add(new int[]{nx, ny, nextEffort});
                    }
                }
            }
        }
        return 0;
    }
}
```

---

## 4️⃣ Path with Maximum Probability – Max-Heap Dijkstra

**Idea:** Standard Dijkstra variant. Instead of minimizing sum, maximize the product of edge probabilities. Use a `Max-Heap` (Priority Queue with reversed logic) and initialize weights to `0.0` (except source at `1.0`).
**Complexity:** `O(E log V)`.

```java
class Solution {
    public double maxProbability(int n, int[][] edges, double[] succProb, int start, int end) {
        List<double[]>[] adj = new ArrayList[n];
        for (int i = 0; i < n; i++) adj[i] = new ArrayList<>();
        for (int i = 0; i < edges.length; i++) {
            adj[edges[i][0]].add(new double[]{edges[i][1], succProb[i]});
            adj[edges[i][1]].add(new double[]{edges[i][0], succProb[i]});
        }
        double[] probs = new double[n];
        probs[start] = 1.0;
        PriorityQueue<double[]> pq = new PriorityQueue<>((a, b) -> Double.compare(b[1], a[1]));
        pq.add(new double[]{start, 1.0});
        
        while (!pq.isEmpty()) {
            double[] cur = pq.poll();
            int u = (int)cur[0];
            double p = cur[1];
            if (p < probs[u]) continue;
            for (double[] next : adj[u]) {
                if (probs[u] * next[1] > probs[(int)next[0]]) {
                    probs[(int)next[0]] = probs[u] * next[1];
                    pq.add(new double[]{next[0], probs[(int)next[0]]});
                }
            }
        }
        return probs[end];
    }
}
```

---

## 5️⃣ Minimum Cost to Make at Least One Valid Path – 0-1 BFS

**Idea:** If an edge matches the grid direction, its cost is `0`; otherwise, it's `1`. In a graph with only weights `0` and `1`, a standard `Deque` (0-1 BFS) is more efficient than Dijkstra. Add `0`-weight edges to the `front` and `1`-weight edges to the `back`.
**Complexity:** `O(N·M)` time.

```java
class Solution {
    public int minCost(int[][] grid) {
        int m = grid.length, n = grid[0].length;
        int[][] dist = new int[m][n];
        for (int[] row : dist) Arrays.fill(row, Integer.MAX_VALUE);
        dist[0][0] = 0;
        Deque<int[]> dq = new LinkedList<>();
        dq.addFirst(new int[]{0, 0});
        int[][] dirs = {{0,1}, {0,-1}, {1,0}, {-1,0}};
        
        while (!dq.isEmpty()) {
            int[] cur = dq.pollFirst();
            int r = cur[0], c = cur[1];
            if (r == m - 1 && c == n - 1) return dist[r][c];
            for (int i = 0; i < 4; i++) {
                int nr = r + dirs[i][0], nc = c + dirs[i][1];
                int cost = (grid[r][c] == i + 1) ? 0 : 1;
                if (nr >= 0 && nr < m && nc >= 0 && nc < n && dist[r][c] + cost < dist[nr][nc]) {
                    dist[nr][nc] = dist[r][c] + cost;
                    if (cost == 0) dq.addFirst(new int[]{nr, nc});
                    else dq.addLast(new int[]{nr, nc});
                }
            }
        }
        return -1;
    }
}
```

---

## 6️⃣ City With Smallest Number of Neighbors – Floyd-Warshall

**Idea:** When you need **all-pairs shortest paths**, Floyd-Warshall is the cleanest implementation. Use a triple loop to update shortest distances between all pairs of nodes $(i, j)$ via intermediate node $k$. Count how many cities are within `distanceThreshold` for each city.
**Complexity:** `O(V³)` time, `O(V²)` space.

```java
class Solution {
    public int findTheCity(int n, int[][] edges, int distanceThreshold) {
        int[][] dist = new int[n][n];
        for (int i = 0; i < n; i++) {
            Arrays.fill(dist[i], 10001); // Threshold is 10^4
            dist[i][i] = 0;
        }
        for (int[] e : edges) dist[e[0]][e[1]] = dist[e[1]][e[0]] = e[2];
        
        // Floyd-Warshall Core
        for (int k = 0; k < n; k++)
            for (int i = 0; i < n; i++)
                for (int j = 0; j < n; j++)
                    dist[i][j] = Math.min(dist[i][j], dist[i][k] + dist[k][j]);
        
        int minCities = n, res = -1;
        for (int i = 0; i < n; i++) {
            int count = 0;
            for (int j = 0; j < n; j++) if (dist[i][j] <= distanceThreshold) count++;
            if (count <= minCities) {
                minCities = count;
                res = i;
            }
        }
        return res;
    }
}
```

---

## 7️⃣ Minimum Fuel Cost to Report to the Capital – Tree DFS Accumulation

**Idea:** Everyone moves toward node 0. At each node, count how many people are in the subtree rooted there. Every group of `seats` size requires `1` car to move one edge up toward the capital.
**Complexity:** `O(V)` time.

```java
class Solution {
    long fuel = 0;
    public long minimumFuelCost(int[][] roads, int seats) {
        List<Integer>[] adj = new ArrayList[roads.length + 1];
        for (int i = 0; i <= roads.length; i++) adj[i] = new ArrayList<>();
        for (int[] r : roads) { adj[r[0]].add(r[1]); adj[r[1]].add(r[0]); }
        dfs(0, -1, adj, seats);
        return fuel;
    }
    
    private long dfs(int u, int p, List<Integer>[] adj, int seats) {
        long people = 1;
        for (int v : adj[u]) {
            if (v != p) {
                long subtreePeople = dfs(v, u, adj, seats);
                fuel += (subtreePeople + seats - 1) / seats; // ceil(people / seats)
                people += subtreePeople;
            }
        }
        return people;
    }
}
```
# Phase 6: Minimum Spanning Tree (MST)

Minimum Spanning Tree (MST) problems focus on connecting all nodes in a graph with the minimum total edge weight. At the SDE-2 level, the core expectation is a proficient implementation of **Kruskal's Algorithm** due to its intuitive use of sorting and Union-Find.

---

## 🏆 Kruskal's Algorithm Template (Sort + Union-Find)

**SDE-2 Expectation:** Recognize that Kruskal's is generally easier to implement than Prim's in an interview. The strategy is simple: sort all edges by weight and pick the cheapest ones that don't form a cycle.

**Complexity:** `O(E log E)` for sorting, then `O(E α(N))` for Union-Find operations.

```java
class Kruskal {
    public int minSpanningTree(int n, int[][] edges) {
        // edges format: [u, v, weight]
        Arrays.sort(edges, (a, b) -> Integer.compare(a[2], b[2]));
        
        UnionFind uf = new UnionFind(n);
        int mstWeight = 0;
        int edgesUsed = 0;

        for (int[] edge : edges) {
            if (uf.union(edge[0], edge[1])) {
                mstWeight += edge[2];
                if (++edgesUsed == n - 1) break;
            }
        }
        return edgesUsed == n - 1 ? mstWeight : -1;
    }
}
```

---

## 1️⃣ Min Cost to Connect All Points – Manhattan Distance MST

**Idea:** Every point can connect to every other point. Treat each point as a node and the Manhattan distance between them as the edge weight. Since the graph is complete ($N^2$ edges), apply Kruskal's to find the MST.
**Complexity:** `O(N² log N)` due to the $N^2$ possible edges.

```java
class Solution {
    public int minCostConnectPoints(int[][] points) {
        int n = points.size();
        List<int[]> edges = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                int dist = Math.abs(points[i][0] - points[j][0]) + 
                           Math.abs(points[i][1] - points[j][1]);
                edges.add(new int[]{i, j, dist});
            }
        }
        Collections.sort(edges, (a, b) -> a[2] - b[2]);
        UnionFind uf = new UnionFind(n);
        int cost = 0, count = 0;
        for (int[] e : edges) {
            if (uf.union(e[0], e[1])) {
                cost += e[2];
                if (++count == n - 1) break;
            }
        }
        return cost;
    }
}
```

---

## 2️⃣ Critical and Pseudo-Critical Edges – Edge Classification

**Idea:** An edge is **critical** if its removal increases the MST weight. An edge is **pseudo-critical** if it can be part of some MST but isn't in all of them (forcing its inclusion results in the same MST weight, provided it's not already critical).
**Complexity:** `O(E² α(N))` because we re-run Kruskal's for every edge to test exclusion/inclusion.

```java
class Solution {
    public List<List<Integer>> findCriticalAndPseudoCriticalEdges(int n, int[][] edges) {
        int m = edges.length;
        int[][] newEdges = new int[m][4]; // [u, v, w, originalIndex]
        for (int i = 0; i < m; i++) {
            newEdges[i][0] = edges[i][0];
            newEdges[i][1] = edges[i][1];
            newEdges[i][2] = edges[i][2];
            newEdges[i][3] = i;
        }
        Arrays.sort(newEdges, (a, b) -> a[2] - b[2]);

        int minWeight = getMST(n, newEdges, -1, -1);
        List<Integer> critical = new ArrayList<>();
        List<Integer> pseudo = new ArrayList<>();

        for (int i = 0; i < m; i++) {
            // Test Critical: If excluding edge i increases weight/breaks graph
            if (getMST(n, newEdges, -1, i) > minWeight) {
                critical.add(newEdges[i][3]);
            } else if (getMST(n, newEdges, i, -1) == minWeight) {
                // Test Pseudo: If forcing edge i maintains min weight
                pseudo.add(newEdges[i][3]);
            }
        }
        return Arrays.asList(critical, pseudo);
    }

    private int getMST(int n, int[][] edges, int forceIdx, int excludeIdx) {
        UnionFind uf = new UnionFind(n);
        int weight = 0, count = 0;
        if (forceIdx != -1) {
            uf.union(edges[forceIdx][0], edges[forceIdx][1]);
            weight += edges[forceIdx][2];
            count++;
        }
        for (int i = 0; i < edges.length; i++) {
            if (i == excludeIdx || i == forceIdx) continue;
            if (uf.union(edges[i][0], edges[i][1])) {
                weight += edges[i][2];
                count++;
            }
        }
        return count == n - 1 ? weight : Integer.MAX_VALUE;
    }
}
```# Phase 7: Advanced Configurations & Specialized Views (Eulerian/Bipartite/State-Space)

Advanced graph problems often require more than just a traversal. They might involve finding Eulerian paths, verifying bipartite properties, or augmenting the BFS state to handle complex constraints.

---

## 🏆 State-Space BFS Paradigm

**SDE-2 Expectation:** Beyond simple node traversal, you must be comfortable with "State-Space" BFS, where a node in the queue is defined by a tuple: `(current_node, state_variables)`. This is essential for handling path constraints like alternating colors or multi-step transitions.

---

## 1️⃣ Is Graph Bipartite? / Divide Nodes into Max Groups

**Idea:** A graph is bipartite if it contains no odd-length cycles (can be 2-colored). To divide nodes into maximum groups, first verify bipartition, then for each connected component, the max groups is the maximum distance between any two nodes (diameter) plus one.
**Complexity:** `O(V·(V+E))` to find diameters for all components.

```java
class Solution {
    public int magnificentSets(int n, List<List<Integer>> adj) {
        int[] color = new int[n + 1];
        List<List<Integer>> components = new ArrayList<>();
        for (int i = 1; i <= n; i++) {
            if (color[i] == 0) {
                List<Integer> component = new ArrayList<>();
                if (!isBipartite(i, 1, color, adj, component)) return -1;
                components.add(component);
            }
        }
        int totalGroups = 0;
        for (List<Integer> comp : components) {
            int maxDepth = 0;
            for (int node : comp) maxDepth = Math.max(maxDepth, bfsMaxDepth(node, n, adj));
            totalGroups += maxDepth;
        }
        return totalGroups;
    }

    private boolean isBipartite(int u, int c, int[] color, List<List<Integer>> adj, List<Integer> comp) {
        color[u] = c; comp.add(u);
        for (int v : adj.get(u)) {
            if (color[v] == c) return false;
            if (color[v] == 0 && !isBipartite(v, -c, color, adj, comp)) return false;
        }
        return true;
    }

    private int bfsMaxDepth(int start, int n, List<List<Integer>> adj) {
        Queue<Integer> q = new LinkedList<>();
        q.add(start);
        int[] dist = new int[n + 1]; Arrays.fill(dist, -1);
        dist[start] = 1;
        int max = 1;
        while (!q.isEmpty()) {
            int u = q.poll();
            for (int v : adj.get(u)) {
                if (dist[v] == -1) {
                    dist[v] = dist[u] + 1;
                    max = Math.max(max, dist[v]);
                    q.add(v);
                }
            }
        }
        return max;
    }
}
```

---

## 2️⃣ Reconstruct Itinerary – Hierholzer's Algorithm (Eulerian Path)

**Idea:** An Eulerian path visits every edge exactly once. Use Hierholzer's: perform a post-order DFS where you choose the lexicographically smallest neighbor via a PriorityQueue. The path is the reverse of the post-order list.
**Complexity:** `O(E log E)` for sorting neighbors.

```java
class Solution {
    Map<String, PriorityQueue<String>> adj = new HashMap<>();
    List<String> path = new LinkedList<>();

    public List<String> findItinerary(List<List<String>> tickets) {
        for (List<String> t : tickets) {
            adj.computeIfAbsent(t.get(0), k -> new PriorityQueue<>()).add(t.get(1));
        }
        dfs("JFK");
        return path;
    }

    private void dfs(String u) {
        PriorityQueue<String> pq = adj.get(u);
        while (pq != null && !pq.isEmpty()) {
            dfs(pq.poll());
        }
        path.add(0, u); // Reverse post-order
    }
}
```

---

## 3️⃣ Word Ladder – State-Space BFS

**Idea:** Shortest transformation path is a BFS problem. To find adjacent words efficiently, iterate through each character in the current word and try all `a-z` replacements. Checking against a `HashSet` is $O(1)$.
**Complexity:** `O(N · L²)` where `N` is word count and `L` is word length.

```java
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        Set<String> dict = new HashSet<>(wordList);
        if (!dict.contains(endWord)) return 0;
        Queue<String> q = new LinkedList<>();
        q.add(beginWord);
        int level = 1;
        while (!q.isEmpty()) {
            int size = q.size();
            for (int i = 0; i < size; i++) {
                String cur = q.poll();
                if (cur.equals(endWord)) return level;
                char[] chars = cur.toCharArray();
                for (int j = 0; j < chars.length; j++) {
                    char original = chars[j];
                    for (char c = 'a'; c <= 'z'; c++) {
                        chars[j] = c;
                        String next = String.valueOf(chars);
                        if (dict.contains(next)) {
                            q.add(next);
                            dict.remove(next);
                        }
                    }
                    chars[j] = original;
                }
            }
            level++;
        }
        return 0;
    }
}
```

---

## 4️⃣ Shortest Path with Alternating Colors – Multi-State BFS

**Idea:** BFS where the state is `(node, weight_of_incoming_edge)`. A node can be visited twice: once via a Red edge and once via a Blue edge. Maintain `dist[2][n]` to track these two separate paths.
**Complexity:** `O(V + E)`.

```java
class Solution {
    public int[] shortestAlternatingPaths(int n, int[][] redEdges, int[][] blueEdges) {
        List<Integer>[][] adj = new ArrayList[2][n];
        for (int i = 0; i < n; i++) { adj[0][i] = new ArrayList<>(); adj[1][i] = new ArrayList<>(); }
        for (int[] e : redEdges) adj[0][e[0]].add(e[1]);
        for (int[] e : blueEdges) adj[1][e[0]].add(e[1]);

        int[][] dist = new int[2][n];
        for (int[] d : dist) Arrays.fill(d, -1);
        dist[0][0] = 0; dist[1][0] = 0;

        Queue<int[]> q = new LinkedList<>();
        q.add(new int[]{0, 0}); // node, color (0: Red, 1: Blue)
        q.add(new int[]{0, 1});

        while (!q.isEmpty()) {
            int[] cur = q.poll();
            int u = cur[0], color = cur[1];
            int nextColor = 1 - color;
            for (int v : adj[nextColor][u]) {
                if (dist[nextColor][v] == -1) {
                    dist[nextColor][v] = dist[color][u] + 1;
                    q.add(new int[]{v, nextColor});
                }
            }
        }
        int[] res = new int[n];
        for (int i = 0; i < n; i++) {
            int d0 = dist[0][i], d1 = dist[1][i];
            if (d0 == -1 || d1 == -1) res[i] = Math.max(d0, d1);
            else res[i] = Math.min(d0, d1);
        }
        return res;
    }
}
```

---

## 5️⃣ Snakes And Ladders / Open The Lock – Implicit State BFS

**Idea:** Standard BFS on a 1D grid or multi-digit lock. The "graph" is formed by transitions (rolling a die or turning a wheel). Use a `visited` set to avoid infinite loops and find the shortest path.
**Complexity:** `O(V + E)` where $V$ is the total number of states.

```java
class SnakesAndLadders {
    public int snakesAndLadders(int[][] board) {
        int n = board.length, target = n * n;
        int[] flat = new int[target + 1];
        boolean leftToRight = true;
        int idx = 1;
        for (int r = n - 1; r >= 0; r--) {
            if (leftToRight) for (int c = 0; c < n; c++) flat[idx++] = board[r][c];
            else for (int c = n - 1; c >= 0; c--) flat[idx++] = board[r][c];
            leftToRight = !leftToRight;
        }
        Queue<Integer> q = new LinkedList<>();
        int[] dist = new int[target + 1];
        Arrays.fill(dist, -1);
        q.add(1); dist[1] = 0;
        while (!q.isEmpty()) {
            int curr = q.poll();
            if (curr == target) return dist[curr];
            for (int i = 1; i <= 6 && curr + i <= target; i++) {
                int next = curr + i;
                int destination = flat[next] == -1 ? next : flat[next];
                if (dist[destination] == -1) {
                    dist[destination] = dist[curr] + 1;
                    q.offer(destination);
                }
            }
        }
        return -1;
    }
}

class OpenTheLock {
    public int openLock(String[] deadends, String target) {
        Set<String> dead = new HashSet<>(Arrays.asList(deadends));
        if (dead.contains("0000")) return -1;
        Queue<String> q = new LinkedList<>();
        Set<String> visited = new HashSet<>();
        q.add("0000"); visited.add("0000");
        int step = 0;
        while (!q.isEmpty()) {
            int size = q.size();
            while (size-- > 0) {
                String cur = q.poll();
                if (cur.equals(target)) return step;
                for (int i = 0; i < 4; i++) {
                    for (int d : new int[]{-1, 1}) {
                        char[] chars = cur.toCharArray();
                        chars[i] = (char)((chars[i] - '0' + d + 10) % 10 + '0');
                        String next = new String(chars);
                        if (!visited.contains(next) && !dead.contains(next)) {
                            visited.add(next); q.offer(next);
                        }
                    }
                }
            }
            step++;
        }
        return -1;
    }
}
```


