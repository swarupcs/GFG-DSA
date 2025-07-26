## Search in a Row-Column sorted matrix


https://www.geeksforgeeks.org/problems/search-in-a-matrix17201720/1


<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 14pt;">Given a 2D integer matrix <strong>mat</strong>[][] of size <strong>n x m</strong>, where every row and column is sorted in increasing order and a number <strong>x</strong>,<strong> </strong>the task is to find whether element <strong>x</strong> is present in the matrix.</span></p>
<p><strong><span style="font-size: 14pt;">Examples:</span></strong></p>
<pre><span style="font-size: 14pt;"><strong>Input</strong>: mat[][] = [[3, 30, 38],[20, 52, 54],[35, 60, 69]], x = 62
<strong>Output</strong>: false
<strong>Explanation</strong>: 62 is not present in the matrix, so output is false.<br></span></pre>
<pre><span style="font-size: 14pt;"><strong>Input</strong>: mat[][] = [[18, 21, 27],[38, 55, 67]], x = 55
<strong>Output</strong>: true
<strong>Explanation</strong>: 55 is present in the matrix.</span></pre>
<pre><span style="font-size: 14pt;"><strong>Input</strong>: mat[][] = [[1, 2, 3],[4, 5, 6],[7, 8, 9]], x = 3
<strong>Output</strong>: true
<strong>Explanation</strong>: 3 is present in the matrix.<br></span></pre>
<p><span style="font-size: 14pt;"><strong>Constraints</strong>:<br>1 &lt;= n, m &lt;=1000<br>1 &lt;= mat[i][j] &lt;= 10<sup>9 <br></sup>1&lt;= x &lt;= 10<sup>9</sup></span></p></div>


<div class="problems_accordion_tags__JJ2DX problems_active_tags__3RExF"><div class="active title problems_active_tag_title__cgl9e"><div class="problems_tag_container__kWANg"><strong>Expected Complexities</strong>: </div></div><div class="content active animated_content open"><div class="problems_expected_complexities_text__h_eyi"><div class="problems_normal_text__QiKrb">Time Complexity: O(n + m)</div><div class="problems_normal_text__QiKrb">Auxiliary Space: O(1)</div></div></div><div class="ui divider g-mt-3"></div></div>

## Solutions

#### Key Points:
```


```

---

* ✅ Approach
* ✅ Intuition
* ✅ Code Explanation (with line-by-line inline comments)
* ✅ Dry Run
* ✅ Time & Space Complexity

---

## ✅ Problem Summary

You're given a **2D matrix** where:

* Each row is sorted in increasing order.
* Each column is sorted in increasing order.

You are to **search** for an element `x` and return `true` if present, otherwise `false`.

---

## ✅ Intuition

Think of the matrix like a **slope** from top-right to bottom-left:

* If current element > `x`, move **left** to a smaller number.
* If current element < `x`, move **down** to a larger number.
* Start at the **top-right** corner and use this idea.

---

## ✅ Approach

Use a **staircase search**:

* Start from the top-right of the matrix (`mat[0][m-1]`).
* If the current number is equal to `x`, return true.
* If it's greater than `x`, go **left**.
* If it's smaller, go **down**.
* If you go out of bounds, `x` is not present.

---

## ✅ Algorithm (Step-by-Step)

1. Let `n = mat.length` and `m = mat[0].length`
2. Set `row = 0` and `col = m - 1`
3. While `row < n` and `col >= 0`:

   * If `mat[row][col] == x`, return `true`
   * If `mat[row][col] < x`, increment `row`
   * Else decrement `col`
4. Return `false` if loop ends

---

## ✅ Code with Step-by-Step Comments

```java
class Solution {
    public static boolean matSearch(int mat[][], int x) {
        // Get number of rows
        int n = mat.length;

        // Get number of columns
        int m = mat[0].length;

        // Start from the top-right corner
        int row = 0;         // Starting row index
        int col = m - 1;     // Starting column index

        // Loop until we stay within matrix boundaries
        while(row < n && col >= 0) {
            // If we find the element, return true
            if(mat[row][col] == x) {
                return true;
            } 
            // If current element is smaller than x, move down to next row
            else if(mat[row][col] < x) {
                row++;
            } 
            // If current element is greater than x, move left to previous column
            else {
                col--;
            }
        }

        // If loop ends, x is not found
        return false;
    }
}
```

---

## ✅ Dry Run

Let’s dry run this with:

```java
mat = [
  [3, 30, 38],
  [20, 52, 54],
  [35, 60, 69]
]
x = 62
```

Start from top-right → mat\[0]\[2] = 38

* 38 < 62 → go down → row = 1
* mat\[1]\[2] = 54 < 62 → row = 2
* mat\[2]\[2] = 69 > 62 → col = 1
* mat\[2]\[1] = 60 < 62 → row = 3 (out of bounds)

Loop ends → return false

---

## ✅ Time & Space Complexity

### ⏱ Time Complexity: `O(n + m)`

* We at most move `n` times down and `m` times left.
* In the worst case, we check one row or one column at each step.

### 🧠 Space Complexity: `O(1)`

* We use only constant extra space (just variables `row` and `col`).

---

## ✅ Summary

This approach is **optimal** for this matrix configuration:

| Matrix Property        | Value        |
| ---------------------- | ------------ |
| Row-wise sorted        | ✅ Yes        |
| Column-wise sorted     | ✅ Yes        |
| Random access required | ❌ Not needed |
| Time Complexity        | `O(n + m)`   |
| Space Complexity       | `O(1)`       |






























