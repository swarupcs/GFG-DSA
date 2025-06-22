## Max rectangle


https://www.geeksforgeeks.org/problems/max-rectangle/1


<div class="undefined "><div class="problems_header_content__o_4YA"><div class="problems_header_content__title__L2cB2 g-mb-0"><h3 class="g-m-0">Max  rectangle</h3><div style="padding-top: 2px;"><div class="sprint_sprint_popup_container__zCU0K"><i aria-hidden="true" class="bookmark outline icon"></i></div><div class="sprint_sprint_modal_container_mobile__09_Vr"><i aria-hidden="true" class="bookmark outline icon"></i></div></div></div><i id="bug_1" aria-hidden="true" class="bug icon"></i></div><div class="problems_header_description__t_8PB"><span>Difficulty: <strong>Hard</strong></span><span>Accuracy: <strong>36.43%</strong></span><span>Submissions: <strong>115K+</strong></span><span>Points: <strong>8</strong></span><span class="problems_label__MY7nU">Average Time: <strong>35m</strong></span></div><div class="ui divider"></div><div><div class="problems_problem_content__Xm_eO"><p><span style="font-size: 18px;">Given a binary matrix <strong>mat[][] </strong>of size <strong>n * m</strong>. Find the maximum area of a rectangle formed only of <strong>1s</strong> in the given matrix. </span></p>
<p><span style="font-size: 18px;"><strong>Examples:</strong></span></p>
<pre><span style="font-size: 18px;"><strong style="font-size: 18px;">Input: </strong><span style="font-size: 18px;">mat[][] = [[0, 1, 1, 0],
                [1, 1, 1, 1],
                [1, 1, 1, 1],
                [1, 1, 0, 0]]
</span><strong style="font-size: 18px;">Output: </strong><span style="font-size: 18px;">8</span><strong style="font-size: 18px;">
Explanation: </strong><span style="font-size: 18px;">The largest rectangle with only 1’s is from (1, 0) to (2, 3) which is
[1, 1, 1, 1]
[1, 1, 1, 1]
and area is 4 *2 = 8</span></span><span style="font-size: 18px;">.</span></pre>
<pre><span style="font-size: 18px;"><strong>Input:</strong> mat[][] = [[0, 1, 1],
                [1, 1, 1],
                [0, 1, 1]]
<strong>Output:</strong> 6
<strong>Explanation:</strong> The largest rectangle with only 1’s is from (0, 1) to (2, 2) which is
[1, 1]
[1, 1]
[1, 1]</span></pre>
<p><span style="font-size: 18px;"><strong>Constraints:</strong><br>1&lt;= mat.size(), mat[0].size()&lt;=1000<br>0&lt;=mat[][]&lt;=1<br></span></p></div></div>

## Solutions

#### Key Points:
```


```

Here’s a **complete explanation** of the solution to the problem:

> ✅ Given a binary matrix of size `n x m`, find the maximum rectangular area formed only by `1`s.

---

## ✅ 1. **Intuition**

We can treat each row of the matrix as the base of a histogram. If we count the number of consecutive `1`s in every column up to the current row, the matrix transforms into a histogram for each row.
Then, we calculate the **largest rectangle area in that histogram** row by row and return the **maximum area** found.

---

## ✅ 2. **Approach Summary**

* Convert the matrix into a histogram-like prefix sum matrix.
* For each row in the prefix matrix, compute the largest rectangle using a monotonic stack (same as "Largest Rectangle in Histogram" problem).
* Keep track of the maximum area found.

---

## ✅ 3. **Line-by-Line Code with Comments**

```java
class Solution {

    // Returns area of the largest rectangle with all 1s in mat[][]
    static int maxArea(int mat[][]) {
        // Get number of rows and columns
        int n = mat.length;
        int m = mat[0].length;

        // Convert matrix into a histogram-like matrix (prefixSum)
        int[][] prefixSum = new int[n][m];

        // Step 1: Build the prefix sum matrix (column-wise)
        for (int j = 0; j < m; j++) {
            int sum = 0; // Track continuous '1's in column
            for (int i = 0; i < n; i++) {
                sum += mat[i][j]; // Add current element

                // If current cell is 0, reset
                if (mat[i][j] == 0) {
                    prefixSum[i][j] = 0;
                    sum = 0;
                } else {
                    // Store running height of 1s
                    prefixSum[i][j] = sum;
                }
            }
        }

        int maxArea = 0; // Track the maximum area found

        // Step 2: For each row of prefixSum, calculate histogram area
        for (int i = 0; i < n; i++) {
            int area = largestRectangleArea(prefixSum[i]);
            maxArea = Math.max(area, maxArea);
        }

        // Step 3: Return the maximum area found
        return maxArea;
    }

    // Step 4: Calculate largest rectangle area in a histogram
    private static int largestRectangleArea(int[] heights) {
        int n = heights.length;
        Stack<Integer> st = new Stack<>(); // Monotonic stack
        int largestArea = 0; // Max area

        // Traverse all bars of histogram
        for (int i = 0; i < n; i++) {
            // Maintain increasing stack
            while (!st.isEmpty() && heights[st.peek()] >= heights[i]) {
                int height = heights[st.pop()]; // Height of bar
                int left = st.isEmpty() ? -1 : st.peek(); // Previous smaller
                int right = i; // Next smaller is current index
                int width = right - left - 1; // Width between boundaries
                int area = height * width; // Area of current rectangle
                largestArea = Math.max(largestArea, area); // Update max area
            }
            st.push(i); // Push current index to stack
        }

        // Clean up remaining elements in stack
        while (!st.isEmpty()) {
            int height = heights[st.pop()];
            int left = st.isEmpty() ? -1 : st.peek();
            int right = n; // Right boundary is end of histogram
            int width = right - left - 1;
            int area = height * width;
            largestArea = Math.max(largestArea, area);
        }

        return largestArea; // Return the maximum area found
    }
}
```

---

## ✅ 4. **Dry Run Example**

### Input:

```
mat[][] = [
  [0, 1, 1, 0],
  [1, 1, 1, 1],
  [1, 1, 1, 1],
  [1, 1, 0, 0]
]
```

### Step 1: Build `prefixSum` (height matrix for histogram)

```
prefixSum =
[
  [0, 1, 1, 0],
  [1, 2, 2, 1],
  [2, 3, 3, 2],
  [3, 4, 0, 0]
]
```

### Step 2: Apply `largestRectangleArea()` row by row:

* Row 0: \[0,1,1,0] → area = 2
* Row 1: \[1,2,2,1] → area = 4
* Row 2: \[2,3,3,2] → area = 6
* Row 3: \[3,4,0,0] → area = **8 ✅**

### 🔚 Final Answer: `8`

---

## ✅ 5. **Time & Space Complexity**

### Time Complexity:

* Prefix sum construction: `O(n * m)`
* For each row: `O(m)` to calculate largest rectangle → Total: `O(n * m)`

> 🔁 Final Time: `O(n * m)`

### Space Complexity:

* Prefix sum matrix: `O(n * m)`
* Stack for histogram: `O(m)`

> 💾 Final Space: `O(n * m)`

---

## ✅ 6. **Algorithm Summary**

```
1. Convert matrix to prefix height matrix by counting continuous 1s column-wise.
2. For each row in this prefix matrix, treat it as histogram heights.
3. Use stack to find largest rectangle in each histogram row.
4. Return maximum area found.
```

---




























