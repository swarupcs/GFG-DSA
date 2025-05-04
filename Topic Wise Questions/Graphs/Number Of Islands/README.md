## Number Of Islands

https://www.geeksforgeeks.org/problems/number-of-islands/1

```
You are given a n,m which means the row and column of the 2D matrix and an array of  size k denoting the number of operations. Matrix elements is 0 if there is water or 1 if there is land. Originally, the 2D matrix is all 0 which means there is no land in the matrix. The array has k operator(s) and each operator has two integer A[i][0], A[i][1] means that you can change the cell matrix[A[i][0]][A[i][1]] from sea to island. Return how many island are there in the matrix after each operation.You need to return an array of size k.
Note : An island means group of 1s such that they share a common side.
```


#### Example 1:

```
Input: n = 4
m = 5
k = 4
A = {{1,1},{0,1},{3,3},{3,4}}

Output: 1 1 2 2
Explanation:
0.  00000
    00000
    00000
    00000
1.  00000
    01000
    00000
    00000
2.  01000
    01000
    00000
    00000
3.  01000
    01000
    00000
    00010
4.  01000
    01000
    00000
    00011

```

#### Example 2:
```
Input: n = 4
m = 5
k = 4
A = {{0,0},{1,1},{2,2},{3,3}}

Output: 1 2 3 4
Explanation:
0.  00000
    00000
    00000
    00000
1.  10000
    00000
    00000
    00000
2.  10000
    01000
    00000
    00000
3.  10000
    01000
    00100
    00000
4.  10000
    01000
    00100
    00010
```
### Your Task:

```
You don't need to read or print anything. Your task is to complete the function numOfIslands() which takes an integer n denoting no. of rows in the matrix, an integer m denoting the number of columns in the matrix and a 2D array of size k denoting  the number of operators.
```

#### Expected Time Complexity: ```O(m * n)```
#### Expected Auxiliary Space: ```O(m * n)```


#### Constraints:
```
1 <= n,m <= 100
1 <= k <= 1000
```

## Solutions

#### Key Points:
```


```

* **Java**

```java
import java.util.*;

// Class representing Disjoint Set Union (DSU) or Union-Find Data Structure
class DisjointSet {
    int[] rank;  // Rank array to store the rank of each set
    int[] parent; // Parent array to store the representative (leader) of each set
    int[] size;  // Size array to store the size of each set
    
    // Constructor to initialize DSU for 'n' elements
    DisjointSet(int n) {
        rank = new int[n + 1];
        parent = new int[n + 1];
        size = new int[n + 1];
        
        // Initializing each element as its own parent (self-loop)
        for(int i = 0; i <= n; i++) {
            parent[i] = i;
            size[i] = 1; // Initially, each set contains a single element
        }
    }
    
    // Find function with path compression to find the ultimate parent of 'node'
    int findUParent(int node) {
        if(node == parent[node]) {
            return node; // If node is its own parent, return it
        }
        
        return parent[node] = findUParent(parent[node]); // Path compression for optimization
    }
    
    // Union function by rank: attaches smaller rank tree under higher rank tree
    void unionByRank(int u, int v) {
        int ulp_u = findUParent(u); // Find ultimate parent of 'u'
        int ulp_v = findUParent(v); // Find ultimate parent of 'v'
        
        if(ulp_u == ulp_v) return; // If both have same parent, they are already in the same set
        
        // Union by rank logic
        if(rank[ulp_u] < rank[ulp_v]) {
            parent[ulp_u] = ulp_v; // Attach smaller tree under larger tree
        } else if(rank[ulp_v] < rank[ulp_u]) {
            parent[ulp_v] = ulp_u; 
        } else {
            parent[ulp_v] = ulp_u;
            rank[ulp_u]++; // Increment rank when both have the same rank
        }
    }
    
    // Union function by size: attaches smaller set under the larger set
    void unionBySize(int u, int v) {
        int ulp_u = findUParent(u);
        int ulp_v = findUParent(v);
        
        if(ulp_u == ulp_v) return; // Already in the same set
        
        // Union by size logic
        if(size[ulp_u] < size[ulp_v]) {
            parent[ulp_u] = ulp_v;
            size[ulp_v] += size[ulp_u]; // Update size of new parent
        } else {
            parent[ulp_v] = ulp_u;
            size[ulp_u] += size[ulp_v];
        }
    }
}

// Solution class to find the number of islands after each operation
class Solution {
    
    // Directions for moving in 4 possible adjacent cells (up, right, down, left)
    int[] delRow = {-1, 0, 1, 0};
    int[] delCol = {0, 1, 0, -1};
    
    // Function to check if a given cell (i, j) is within the grid boundaries
    boolean isValid(int i, int j, int n, int m) {
        return (i >= 0 && i < n && j >= 0 && j < m);
    }
    
    // Function to compute number of islands after each land addition
    public List<Integer> numOfIslands(int rows, int cols, int[][] operators) {
        DisjointSet ds = new DisjointSet(rows * cols); // Create Disjoint Set for grid cells
        int[][] vis = new int[rows][cols]; // Visited matrix to track land cells
        
        // Initialize the visited matrix with all 0s (water)
        for(int[] row : vis) {
            Arrays.fill(row, 0);
        }
        
        int cnt = 0; // Counter to track number of islands
        List<Integer> ans = new ArrayList<>(); // List to store results after each operation
        
        // Process each operation
        for(int[] it : operators) {
            int row = it[0];
            int col = it[1];
            
            // If the cell is already land, no new island is formed
            if(vis[row][col] == 1) {
                ans.add(cnt);
                continue;
            }
            
            vis[row][col] = 1; // Mark the cell as land
            cnt++; // Assume a new island is formed
            
            // Check all four possible directions
            for(int i = 0; i < 4; i++) {
                int newRow = row + delRow[i];
                int newCol = col + delCol[i];
                
                // If adjacent cell is valid and already land, perform union
                if(isValid(newRow, newCol, rows, cols) && vis[newRow][newCol] == 1) {
                    int nodeNo = row * cols + col; // Convert (row, col) to 1D index
                    int adjNode = newRow * cols + newCol; // Convert adjacent (row, col) to 1D index
                    
                    // If both cells belong to different components, merge them
                    if(ds.findUParent(nodeNo) != ds.findUParent(adjNode)) {
                        cnt--; // Merging two islands decreases the island count
                        ds.unionBySize(nodeNo, adjNode); // Merge components
                    }
                }
            }
            
            ans.add(cnt); // Store the current count of islands after this operation
        }
        
        return ans; // Return the final list of island counts
    }
}

```



### **Approach & Intuition**
The problem requires us to determine the number of islands after each operation (turning a water cell into land). An island is a group of connected land cells (horizontally or vertically). We use **Disjoint Set Union (DSU)** to efficiently manage the merging of islands.

### **Algorithm**
1. **Initialize DSU:** Create a Disjoint Set data structure for `n * m` cells.
2. **Track visited cells:** Maintain a `vis[][]` array to mark land cells.
3. **Process each operation:**
   - If the cell is already land, store the current island count.
   - Otherwise, mark it as land and assume a new island is formed.
   - Check the 4 possible directions (up, right, down, left).
   - If an adjacent cell is land and belongs to a different island, merge them and reduce the island count.
4. **Store results:** After processing each operation, store the updated island count.

### **Dry Run Example**
#### **Input:**
```
n = 3, m = 3
operators = [[0, 0], [0, 1], [1, 2], [1, 1], [0, 2]]
```
#### **Step-by-step execution:**
| Operation | Grid State | Islands |
|-----------|-----------|---------|
| (0,0) | 1 0 0 <br> 0 0 0 <br> 0 0 0 | 1 |
| (0,1) | 1 1 0 <br> 0 0 0 <br> 0 0 0 | 1 |
| (1,2) | 1 1 0 <br> 0 0 1 <br> 0 0 0 | 2 |
| (1,1) | 1 1 0 <br> 0 1 1 <br> 0 0 0 | 2 |
| (0,2) | 1 1 1 <br> 0 1 1 <br> 0 0 0 | 1 |

#### **Final Output:** `[1, 1, 2, 2, 1]`

This approach ensures efficient merging of islands using **path compression and union by size**, leading to an optimal **O(α(n)) ≈ O(1) per operation**.

Let me know if you need further clarification! 🚀























