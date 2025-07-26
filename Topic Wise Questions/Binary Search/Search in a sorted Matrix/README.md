## Search in a sorted Matrix


https://www.geeksforgeeks.org/problems/search-in-a-matrix-1587115621/1


<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 14pt;">Given a strictly sorted 2D matrix<strong> mat</strong>[][] of size <strong>n x m&nbsp;</strong>and<strong>&nbsp;</strong>a number&nbsp;<strong>x.</strong> Find whether the number <strong>x</strong> is present in the matrix or not.<br><strong>Note:</strong> In a strictly sorted matrix, each row is sorted in strictly increasing order, and&nbsp;the first element of the <strong>i</strong><sup>th</sup>&nbsp;row (<strong>i</strong>!=0) is greater than the last element of the (<strong>i-1</strong>)<sup>th&nbsp;</sup>row.</span><br style="font-size: 18px;"><br><span style="font-size: 14pt;"><strong>Examples:</strong></span></p>
<pre><span style="font-size: 14pt;"><strong>Input</strong>: mat[][] = [[1, 5, 9], [14, 20, 21], [30, 34, 43]], x = 14
<strong>Output</strong>: true
<strong>Explanation</strong>: 14 is present in the matrix, so output is true.
</span></pre>
<pre><span style="font-size: 14pt;"><strong>Input</strong>: mat[][] = [[1, 5, 9, 11], [14, 20, 21, 26], [30, 34, 43, 50]], x = 42<br><strong>Output</strong>: false
<strong>Explanation</strong>: 42 is not present in the matrix.<br></span></pre>
<pre><span style="font-size: 14pt;"><strong>Input</strong>: mat[][] = [[87, 96, 99], [101, 103, 111]], x = 101</span><br><span style="font-size: 14pt;"><strong>Output</strong>: true
<strong>Explanation</strong>: 101 is present in the matrix.</span></pre>
<p><span style="font-size: 14pt;"><strong>Constraints:<br></strong>1 ≤ n, m ≤ 1000<br>1 ≤ mat[i][j] ≤ 10<sup>9</sup><br>1 ≤ x ≤ 10<sup>9</sup></span></p></div>

<div class="problems_accordion_tags__JJ2DX problems_active_tags__3RExF"><div class="active title problems_active_tag_title__cgl9e"><div class="problems_tag_container__kWANg"><strong>Expected Complexities</strong>: </div></div><div class="content active animated_content open"><div class="problems_expected_complexities_text__h_eyi"><div class="problems_normal_text__QiKrb">Time Complexity: O(log(n * m))</div><div class="problems_normal_text__QiKrb">Auxiliary Space: O(1)</div></div></div><div class="ui divider g-mt-3"></div></div>
## Solutions

#### Key Points:
```


```

Here’s a complete explanation of the `searchMatrix` problem and solution using **Binary Search** on a **flattened 2D matrix**, including:

* ✅ Intuition
* ✅ Approach
* ✅ Code with detailed comments
* ✅ Algorithm steps
* ✅ Dry run with example
* ✅ Time and space complexity analysis

---

## ✅ Intuition

The matrix is **strictly sorted**, meaning:

* Each row is sorted in strictly increasing order.
* The **first element of a row is greater than the last element of the previous row**.

This means the matrix behaves like a **flattened sorted array**. So, we can perform **binary search** on it.

We treat the entire matrix as a **1D sorted array**, where index `i` in this 1D array corresponds to:

```
row = i / number of columns (m)
col = i % number of columns (m)
```

---

## ✅ Approach

1. Use binary search with `low = 0` and `high = n * m - 1`, where `n` is rows, `m` is columns.
2. Convert mid index to matrix cell using:

   * `row = mid / m`
   * `col = mid % m`
3. Compare `mat[row][col]` with `x` and adjust `low` or `high` accordingly.
4. If found, return `true`, otherwise return `false`.

---

## ✅ Code with Line-by-Line Comments

```java
class Solution {
    public boolean searchMatrix(int[][] mat, int x) {
        // Step 1: Get the number of rows (n) and columns (m)
        int n = mat.length;
        int m = mat[0].length;

        // Step 2: Initialize low and high pointers for binary search
        int low = 0;
        int high = (n * m) - 1; // Treat 2D matrix as 1D

        // Step 3: Binary search loop
        while (low <= high) {
            // Step 4: Find the middle index of the virtual 1D array
            int mid = (low + high) / 2;

            // Step 5: Convert mid to 2D matrix coordinates
            int row = mid / m;
            int col = mid % m;

            // Step 6: Compare the element at (row, col) with x
            if (mat[row][col] == x) {
                return true; // Element found
            } else if (mat[row][col] < x) {
                low = mid + 1; // Move to the right half
            } else {
                high = mid - 1; // Move to the left half
            }
        }

        // Step 7: If loop ends, element not found
        return false;
    }
}
```

---

## ✅ Algorithm Steps

1. Let `n = mat.length`, `m = mat[0].length`.
2. Initialize:

   * `low = 0`
   * `high = n * m - 1`
3. While `low <= high`:

   * Compute `mid = (low + high) / 2`
   * Convert `mid` to matrix index:
     `row = mid / m`, `col = mid % m`
   * If `mat[row][col] == x`: return `true`
   * Else if `mat[row][col] < x`: set `low = mid + 1`
   * Else: set `high = mid - 1`
4. If not found, return `false`

---

## ✅ Dry Run Example

**Input:**

```java
mat = [[1, 5, 9], 
       [14, 20, 21], 
       [30, 34, 43]]
x = 14
```

Matrix has `n = 3` rows and `m = 3` columns
Total elements = 9
Search range: `low = 0`, `high = 8`

### Iteration 1:

* `mid = (0 + 8) / 2 = 4`
* `row = 4 / 3 = 1`, `col = 4 % 3 = 1`
* `mat[1][1] = 20`
* `20 > 14 → high = 3`

### Iteration 2:

* `mid = (0 + 3) / 2 = 1`
* `row = 1 / 3 = 0`, `col = 1 % 3 = 1`
* `mat[0][1] = 5`
* `5 < 14 → low = 2`

### Iteration 3:

* `mid = (2 + 3) / 2 = 2`
* `row = 2 / 3 = 0`, `col = 2 % 3 = 2`
* `mat[0][2] = 9`
* `9 < 14 → low = 3`

### Iteration 4:

* `mid = (3 + 3) / 2 = 3`
* `row = 3 / 3 = 1`, `col = 3 % 3 = 0`
* `mat[1][0] = 14`
* ✅ Match found → return `true`

---

## ✅ Time and Space Complexity

### Time Complexity: **O(log(n \* m))**

* Binary search over `n * m` elements

### Space Complexity: **O(1)**

* Constant extra space

---

## ✅ Summary

* We flattened the matrix logically and used binary search on it.
* Converted 1D indices to 2D coordinates on-the-fly.
* This approach gives optimal time complexity without using extra space.






























