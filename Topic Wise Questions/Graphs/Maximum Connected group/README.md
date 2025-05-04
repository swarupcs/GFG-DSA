## Maximum Connected group


https://www.geeksforgeeks.org/problems/maximum-connected-group/1


You are given a square binary grid. A grid is considered binary if every value in the grid is either `1 or 0`. You can change `at most one` cell in the grid from `0 to 1`. You need to find the largest group of connected  `1's`. Two cells are said to be connected if both are `adjacent(top, bottom, left, right)` to each other and both have the same value.


#### Example 1:

```
Input: grid = [1, 1]
             [0, 1]
Output: 4
Explanation: By changing cell (2,1), we can obtain a connected group of 4 1's
[1, 1]
[1, 1]

```

#### Example 2:
```
Input: grid = [1, 0, 1]
             [1, 0, 1]
             [1, 0, 1]
Output: 7
Explanation: By changing cell (3,2), we can obtain a connected group of 7 1's
[1, 0, 1]
[1, 0, 1]
[1, 1, 1]
```
### Your Task:

```

```

#### Expected Time Complexity: ```O(n^2)```
#### Expected Auxiliary Space: ```O(n^2)```

#### Constraints:
```
1 <= size of the grid<= 500
0 <= grid[i][j] <= 1
```

## Solutions

#### Key Points:
```


```


---

## ✅ **Intuition**

We are given a binary grid, where a group of `1`s is considered connected if they're adjacent (up/down/left/right). We are allowed to flip at most **one** `0` to `1` to try and **maximize** the size of such a group.

To solve this efficiently, we use **Disjoint Set Union (DSU)** or **Union Find**, which helps track connected components and their sizes.

---

## ✅ **Approach**

1. Use a DSU to group all initially connected 1's.
2. Traverse every `0` cell in the grid, and consider flipping it to `1`.
3. For each `0` cell, check its adjacent 1's, and **merge the sizes of their components** (using DSU) to compute the total group size if we flipped that cell.
4. Keep track of the **maximum size** seen after each hypothetical flip.
5. Also consider the case where the grid has no `0`s (i.e., already fully connected), and simply return the size of the largest group.

---

## ✅ **Algorithm**

1. Initialize the Disjoint Set for `n*n` elements.
2. For each cell that contains a `1`, union it with its adjacent `1`s.
3. For each cell containing a `0`:
   - Check its 4 neighbors.
   - If a neighbor is `1`, store its parent in a `Set` to avoid counting duplicates.
   - Sum the sizes of these unique neighboring components and add 1 for the flipped cell.
   - Update `maxIsland` with this size.
4. After processing all `0`s, iterate over all cells to find the largest component (in case grid has all 1s).
5. Return the maximum size found.

---

## ✅ **Code with Dry Run and Comments**

```java
class DisjointSet {
    int[] parent, size; // Arrays to store parent and size of each set

    // Constructor to initialize the Disjoint Set (Union-Find)
    DisjointSet(int n) {
        parent = new int[n]; // Parent array: stores the parent of each node
        size = new int[n];   // Size array: stores the size of each component
        for (int i = 0; i < n; i++) {
            parent[i] = i; // Initially, each node is its own parent (self-loop)
            size[i] = 1;    // Each node is a component of size 1 initially
        }
    }

    // Find function with path compression to optimize lookup
    int find(int node) {
        if (parent[node] == node) return node; // Base case: if node is its own parent
        return parent[node] = find(parent[node]); // Path compression to speed up future lookups
    }

    // Union by size (merges smaller component into larger one)
    void union(int u, int v) {
        int rootU = find(u); // Find root of node u
        int rootV = find(v); // Find root of node v
        if (rootU != rootV) { // If they belong to different sets, merge them
            if (size[rootU] < size[rootV]) { // Attach smaller tree to larger one
                parent[rootU] = rootV;
                size[rootV] += size[rootU]; // Update size of the new parent
            } else { 
                parent[rootV] = rootU; // Attach rootV to rootU
                size[rootU] += size[rootV]; // Update size of the new parent
            }
        }
    }
}

class Solution {
    
      // Directions array to explore up, right, down, and left neighbors
    private static final int[] delRow = {-1, 0, 1, 0};
    private static final int[] delCol = {0, 1, 0, -1};

    public int MaxConnection(int grid[][]) {
        // Your code here
        
        int n = grid.length; // Get the size of the grid (n x n)
        DisjointSet ds = new DisjointSet(n * n); // Create Disjoint Set for all n*n cells

        // Step 1: Connect all adjacent land cells (1s) using DSU
        for (int row = 0; row < n; row++) { // Loop through each row
            for (int col = 0; col < n; col++) { // Loop through each column
                if (grid[row][col] == 1) { // If the current cell is land
                    for (int k = 0; k < 4; k++) { // Check all 4 neighbors
                        int newRow = row + delRow[k]; // Calculate new row index
                        int newCol = col + delCol[k]; // Calculate new column index
                        // Check if the neighbor is within bounds and is also land
                        if (newRow >= 0 && newRow < n && newCol >= 0 && newCol < n && grid[newRow][newCol] == 1) {
                            int node = row * n + col; // Convert (row, col) to 1D index
                            int adjNode = newRow * n + newCol; // Convert neighbor to 1D index
                            ds.union(node, adjNode); // Merge the two land components
                        }
                    }
                }
            }
        }

        // Step 2: Try flipping each water cell (0) to land and compute the new island size
        int maxIsland = 0; // Variable to store the maximum island size found
        for (int row = 0; row < n; row++) { // Loop through all rows
            for (int col = 0; col < n; col++) { // Loop through all columns
                if (grid[row][col] == 0) { // If the current cell is water (0)
                    Set<Integer> uniqueIslands = new HashSet<>(); // Set to store unique island roots
                    int totalSize = 1; // Start with size 1 (flipping this 0 to 1)

                    for (int k = 0; k < 4; k++) { // Check all 4 neighbors
                        int newRow = row + delRow[k]; // Calculate neighbor row index
                        int newCol = col + delCol[k]; // Calculate neighbor column index
                        // If neighbor is valid and is land
                        if (newRow >= 0 && newRow < n && newCol >= 0 && newCol < n && grid[newRow][newCol] == 1) {
                            int root = ds.find(newRow * n + newCol); // Find root of the neighbor island
                            if (!uniqueIslands.contains(root)) { // If this island has not been counted
                                uniqueIslands.add(root); // Add to unique set
                                totalSize += ds.size[root]; // Add its size to total
                            }
                        }
                    }
                    maxIsland = Math.max(maxIsland, totalSize); // Update max island size
                }
            }
        }

        // Step 3: If there are no water cells, return the largest existing island
        for (int cell = 0; cell < n * n; cell++) { // Check all land cells
            maxIsland = Math.max(maxIsland, ds.size[ds.find(cell)]); // Get max component size
        }

        return maxIsland; // Return the largest island found
    }
}

```

---

## ✅ **Dry Run Example**

### Input:
```
grid = [
  [1, 0, 1],
  [1, 0, 1],
  [1, 0, 1]
]
```

- Initially connected groups:
  - Column 0 and column 2 have vertical 1s → two groups of size 3.
- Try flipping each `0` cell:
  - At (0,1) → connects to nothing.
  - At (1,1) → connects left (1,0) and right (1,2), and top/bottom → total unique components = 2 → size = 3 (left col) + 3 (right col) + 1 (flip) = **7**.
- Final answer = `7`.

---

## ✅ **Time and Space Complexity**

- **Time:** O(n²) for DSU operations and grid traversal.
- **Space:** O(n²) for DSU arrays.

---
























