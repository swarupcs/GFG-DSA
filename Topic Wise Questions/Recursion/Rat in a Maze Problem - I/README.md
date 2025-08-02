## Rat in a Maze Problem - I


https://www.geeksforgeeks.org/problems/rat-in-a-maze-problem/1


<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 14pt;">Consider a rat placed at position (0, 0) in an <strong>n x n</strong> square matrix <code><strong>mat[][]</strong></code>. The rat's goal is to reach the destination at position (n-1, n-1). The rat can move in four possible directions:&nbsp;<strong>'U'(up)</strong>,&nbsp;<strong>'D'(down)</strong>,&nbsp;<strong>'L' (left)</strong>,&nbsp;<strong>'R' (right)</strong>.</span></p>
<p><span style="font-size: 14pt;">The matrix contains only two possible values:</span></p>
<ul>
<li><span style="font-size: 14pt;"><code>0</code>: A blocked cell through which the rat <strong>cannot</strong> travel.</span></li>
<li><span style="font-size: 14pt;"><code>1</code>: A free cell that the rat <strong>can</strong> pass through.</span></li>
</ul>
<p><span style="font-size: 14pt;"><span style="font-size: 14pt;">Your task is to find <strong>all possible paths</strong> the rat can take to reach the destination, starting from (0, 0) and ending at (n-1, n-1), under the condition that the rat cannot <strong>revisit</strong> any cell along the same path. Furthermore, the rat can only move to adjacent cells that are within the bounds of the matrix and not blocked.</span><br><span style="font-size: 18.6667px;"><span style="font-size: 18.6667px;">If no path exists, return an <strong>empty list</strong></span><strong style="font-size: 18.6667px;">.</strong></span></span></p>
<p><span style="font-size: 14pt;"><strong>Note:</strong> Return the final result vector in <strong>lexicographically smallest order</strong>.</span></p>
<p><span style="font-size: 14pt;"><strong>Examples:</strong></span></p>
<pre><span style="font-size: 14pt;"><strong>Input</strong>: mat[][] = [[1, 0, 0, 0], [1, 1, 0, 1], [1, 1, 0, 0], [0, 1, 1, 1]]
<strong>Output: </strong>[<span class="hljs-string">"DDRDRR"</span>, <span class="hljs-string">"DRDDRR"</span>]
<strong>Explanation</strong>: The rat can reach the destination at (3, 3) from (0, 0) by two paths - DRDDRR and DDRDRR, when printed in sorted order we get DDRDRR DRDDRR.</span></pre>
<pre><span style="font-size: 14pt;"><strong>Input</strong>: mat[][] = [[1, 0], [1, 0]]
<strong>Output: </strong>[]
<strong>Explanation</strong>: No path exists as the destination cell is blocked.
</span></pre>
<pre><span style="font-size: 14pt;"><strong>Input</strong>: mat = <span class="hljs-string">[[1, 1, 1], [1, 0, 1], [1, 1, 1]]</span>
<strong>Output: </strong>[<span class="hljs-string">"DDRR"</span>, <span class="hljs-string">"RRDD"</span>]
<strong>Explanation</strong>: The rat has two possible paths to reach the destination: <span class="hljs-number" style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;">1.</span><span style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;"> </span><span class="hljs-string" style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;">"DDRR" </span><span class="hljs-number" style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;">2.</span><span style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;"> </span><span class="hljs-string" style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;">"RRDD", </span><span style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;">These are returned </span><span class="hljs-keyword" style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;">in</span><span style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;"> lexicographically sorted order.</span></span></pre>
<p><span style="font-size: 14pt;"><strong>Constraints:</strong><br>2 ≤ mat.size() ≤ 5<br>0 ≤ mat[i][j] ≤ 1</span></p></div>


<div class="problems_accordion_tags__JJ2DX problems_active_tags__3RExF"><div class="active title problems_active_tag_title__cgl9e"><div class="problems_tag_container__kWANg"><strong>Expected Complexities</strong></div></div><div class="content active animated_content open"><div class="problems_expected_complexities_text__h_eyi"><div class="problems_normal_text__QiKrb">Time Complexity: O(4 ^ (n * n))</div><div class="problems_normal_text__QiKrb">Auxiliary Space: O(n * n)</div></div></div><div class="ui divider g-mt-3"></div></div>

## Solutions

#### Key Points:
```


```

* **Java**

Here's a **complete and detailed explanation** of the **"Rat in a Maze"** problem using **backtracking without using a separate `visited[][]` matrix** (modifying the matrix in place with backtracking).

---

## ✅ Problem Summary

Given an `n x n` matrix `maze[][]`, find **all possible paths** from the top-left `(0, 0)` to bottom-right `(n-1, n-1)` such that:

* The rat can move only on cells with `1`.
* It can move in **4 directions**: Up `'U'`, Down `'D'`, Left `'L'`, Right `'R'`.
* It cannot revisit the same cell in the same path.
* Return all paths in **lexicographical order**.

---

## ✅ Approach & Intuition

We use **Depth-First Search (DFS)** with **backtracking**:

1. From each cell, try all 4 directions.
2. Mark the cell as visited by changing `maze[row][col] = -1`.
3. If you reach the destination, record the path.
4. After exploring, **backtrack** by resetting `maze[row][col] = 1`.
5. Sort the paths lexicographically at the end.

---

## ✅ Algorithm (Step-by-Step)

1. Start from cell `(0, 0)`. If blocked, return empty list.
2. Call a recursive DFS function with current position and path.
3. For each call:

   * If current is the destination, add path to result.
   * Otherwise, try moving in all 4 directions.
   * If valid, move recursively and build path.
   * Backtrack by resetting the cell.
4. Return the sorted result.

---

## ✅ Java Code with Comments as Algorithm and Explanation

```java
import java.util.*;

class Solution {
    public ArrayList<String> ratInMaze(int[][] maze) {
        ArrayList<String> result = new ArrayList<>();
        int n = maze.length;

        // Step 1: Edge case - if start or end is blocked, return empty
        if (maze[0][0] == 0 || maze[n - 1][n - 1] == 0)
            return result;

        // Step 2: Start DFS from (0, 0) with empty path
        dfs(0, 0, "", maze, result, n);

        // Step 6: Sort result in lexicographically smallest order
        Collections.sort(result);
        return result;
    }

    // DFS function to explore all paths
    private void dfs(int row, int col, String path, int[][] maze, ArrayList<String> result, int n) {
        // Step 3: Base Case - If reached destination, add path to result
        if (row == n - 1 && col == n - 1) {
            result.add(path);
            return;
        }

        // Step 4: Direction vectors and direction chars
        int[] dr = {1, 0, 0, -1};         // D, L, R, U
        int[] dc = {0, -1, 1, 0};
        char[] dir = {'D', 'L', 'R', 'U'};

        // Step 5: Mark current cell as visited
        maze[row][col] = -1;

        // Step 6: Try all 4 directions
        for (int i = 0; i < 4; i++) {
            int newRow = row + dr[i];
            int newCol = col + dc[i];

            // Step 7: If move is safe (within bounds and unvisited)
            if (isSafe(newRow, newCol, maze, n)) {
                dfs(newRow, newCol, path + dir[i], maze, result, n);
            }
        }

        // Step 8: Backtrack - unmark current cell
        maze[row][col] = 1;
    }

    // Utility to check if move is within grid and not visited or blocked
    private boolean isSafe(int row, int col, int[][] maze, int n) {
        return (row >= 0 && row < n && col >= 0 && col < n && maze[row][col] == 1);
    }
}
```

---

## ✅ Dry Run Example

Input:

```java
maze = {
  {1, 0, 0, 0},
  {1, 1, 0, 1},
  {1, 1, 0, 0},
  {0, 1, 1, 1}
}
```

### Execution:

Start from (0,0)

1. Move Down → (1,0) → D
2. Move Down → (2,0) → DD
3. Move Right → (2,1) → DDR
4. Move Down → Invalid
5. Move Right → Invalid
6. Move Up → Invalid
7. Backtrack
8. Try alternate path (1,0) → (1,1) → DDRD
9. → (1,1) → (3,1) → (3,2) → (3,3) → DDRDRR ✅

Another valid path → DRDDRR ✅

Final output (sorted):
`["DDRDRR", "DRDDRR"]`

---

## ✅ Time and Space Complexity

### Time Complexity:

* In the **worst case**, each cell may have up to 4 possible directions.
* So time = **O(4^(n\*n))** in the worst case (exponential).
* But due to pruning (blocked cells), practical performance is much better.

### Space Complexity:

* **O(n\*n)** stack space for recursion.
* **O(k)** for storing results where `k` = number of valid paths.

---

## ✅ Summary

| Aspect        | Value                                    |
| ------------- | ---------------------------------------- |
| Technique     | DFS + Backtracking                       |
| Moves         | 4 directions: U, D, L, R                 |
| No Revisiting | Mark current cell as `-1`, restore after |
| Result Order  | Lexicographically sorted                 |
| Visited Space | In-place (`maze[row][col] = -1`)         |

---






























