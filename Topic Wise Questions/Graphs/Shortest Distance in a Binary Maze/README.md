## Shortest Distance in a Binary Maze


https://www.geeksforgeeks.org/problems/shortest-path-in-a-binary-maze-1655453161/1

Given a `n * m` matrix `grid` where each element can either be `0` or `1`. You need to find the shortest distance between a given source cell to a destination cell. The path can only be created out of a cell if its value is `1`. 

If the path is not possible between source cell and destination cell, then return `-1`.

`Note :` You can move into an adjacent cell if that adjacent cell is filled with element `1`. Two cells are adjacent if they share a side. In other words, you can move in one of the four directions, Up, Down, Left and Right. The source and destination cell are based on the zero based indexing. The destination cell should be 1.


#### Example 1:

```
Input:
grid[][] = {{1, 1, 1, 1},
            {1, 1, 0, 1},
            {1, 1, 1, 1},
            {1, 1, 0, 0},
            {1, 0, 0, 1}}
source = {0, 1}
destination = {2, 2}
Output:
3
Explanation:
1 1 1 1
1 1 0 1
1 1 1 1
1 1 0 0
1 0 0 1
The highlighted part in the matrix denotes the 
shortest path from source to destination cell.

```

#### Example 2:
```
Input:
grid[][] = {{1, 1, 1, 1, 1},
            {1, 1, 1, 1, 1},
            {1, 1, 1, 1, 0},
            {1, 0, 1, 0, 1}}
source = {0, 0}
destination = {3, 4}
Output:
-1
Explanation:
The path is not possible between source and 
destination, hence return -1.
```
### Your Task:

```
You don't need to read or print anything. Your task is to complete the function shortestPath() which takes the a 2D integer array grid, source cell and destination cell as an input parameters and returns the shortest distance between source and destination cell.
```

#### Expected Time Complexity: ```O(n * m)```
#### Expected Auxiliary Space: ```O(n * m)```

#### Constraints:
```
1 ≤ n, m ≤ 500
grid[i][j] == 0 or grid[i][j] == 1
The source and destination cells are always inside the given matrix.
```

## Solutions

#### Key Points:
```


```

Here’s a complete solution using **Breadth-First Search (BFS)** to find the **shortest path** from `source` to `destination` in a matrix where only `1` represents valid paths.

### ✅ **Why BFS?**
- This is an **unweighted grid**, where each move costs the same.
- BFS guarantees the **shortest path** in such grids because it explores level-by-level.

---

### ✅ **Approach / Algorithm**

1. **Check edge case**:
   - If source or destination is `0` (blocked), return `-1`.
2. Use **queue** for BFS traversal.
3. Track visited cells to avoid cycles.
4. For each cell, move in **4 directions** (up, down, left, right).
5. If you reach the destination during BFS, return the number of steps taken.
6. If queue is exhausted and destination not reached → return `-1`.

---

### ✅ **Code with Comments (Java)**

```java
import java.util.*;

class Solution {

    // Inner class to represent a cell in the grid along with distance from the source
    static class Cell {
        int row, col, dist;  // Coordinates and distance
        Cell(int row, int col, int dist) {
            this.row = row;
            this.col = col;
            this.dist = dist;
        }
    }

    public int shortestPath(int[][] grid, int[] source, int[] destination) {
        int n = grid.length;         // Total number of rows
        int m = grid[0].length;      // Total number of columns

        // Step 1: Edge case - If either source or destination is blocked (0), return -1
        if (grid[source[0]][source[1]] == 0 || grid[destination[0]][destination[1]] == 0)
            return -1;

        // Step 2: If source and destination are the same, no need to move
        if (source[0] == destination[0] && source[1] == destination[1])
            return 0;

        // Step 3: Initialize a queue for BFS traversal
        Queue<Cell> queue = new LinkedList<>();

        // Step 4: Visited matrix to avoid revisiting the same cell
        boolean[][] visited = new boolean[n][m];

        // Step 5: Direction vectors for 4 adjacent movements (up, down, left, right)
        int[] dx = {-1, 1, 0, 0};  // Row change
        int[] dy = {0, 0, -1, 1};  // Column change

        // Step 6: Start BFS from the source cell
        queue.offer(new Cell(source[0], source[1], 0));  // Add source to queue with distance 0
        visited[source[0]][source[1]] = true;            // Mark source as visited

        // Step 7: Perform BFS loop
        while (!queue.isEmpty()) {
            Cell current = queue.poll();  // Dequeue the front cell
            int row = current.row;
            int col = current.col;
            int dist = current.dist;

            // Step 8: Explore all 4 directions from the current cell
            for (int i = 0; i < 4; i++) {
                int newRow = row + dx[i];
                int newCol = col + dy[i];

                // Step 9: Check if the new cell is within grid bounds
                if (newRow >= 0 && newCol >= 0 && newRow < n && newCol < m) {

                    // Step 10: Proceed only if the new cell is traversable and not visited
                    if (grid[newRow][newCol] == 1 && !visited[newRow][newCol]) {

                        // Step 11: If we've reached the destination cell, return the distance + 1
                        if (newRow == destination[0] && newCol == destination[1]) {
                            return dist + 1;
                        }

                        // Step 12: Mark the cell visited and add it to queue for further traversal
                        visited[newRow][newCol] = true;
                        queue.offer(new Cell(newRow, newCol, dist + 1));
                    }
                }
            }
        }

        // Step 13: If destination is unreachable after BFS completes
        return -1;
    }
}

```

---

### 🔁 **Dry Run Example**

```text
Input:
grid = {
  {1, 1, 1, 1},
  {1, 1, 0, 1},
  {1, 1, 1, 1},
  {1, 1, 0, 0},
  {1, 0, 0, 1}
}
source = {0, 1}
destination = {2, 2}
```

**BFS Traversal Path**:
- Start at (0,1)
- → (1,1) → (2,1) → (2,2) ✅

**Distance:** 3

---

### ✅ Time & Space Complexity

- **Time Complexity:** `O(n * m)` – We visit each cell at most once.
- **Space Complexity:** `O(n * m)` – For the visited matrix and queue.

---



























