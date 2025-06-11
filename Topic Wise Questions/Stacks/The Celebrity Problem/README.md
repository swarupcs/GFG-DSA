## The Celebrity Problem


https://www.geeksforgeeks.org/problems/the-celebrity-problem/1


<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 14pt;">A celebrity is a person who is known to all but&nbsp;<strong>does not know</strong>&nbsp;anyone at a party. A party is being organized by some people. A square matrix&nbsp;<strong>mat[][]&nbsp;</strong>(n*n)&nbsp;is used to represent people at the party such that if an element of <strong>row i and column j is set to 1</strong> it means <strong>ith person knows jth person</strong>.&nbsp;You need to return the <strong>index of the celebrity</strong> in the party, if the celebrity does not exist, return&nbsp;<strong>-1</strong>.</span></p>
<p><span style="font-size: 14pt;"><strong>Note:</strong>&nbsp;Follow <strong>0-based </strong>indexing.</span></p>
<p><span style="font-size: 14pt;"><strong>Examples:</strong></span></p>
<pre><span style="font-size: 14pt;"><strong>Input: </strong>mat[][] = [[1, 1, 0], [0, 1, 0], [0, 1, 1]]
<strong>Output:</strong> 1
<strong>Explanation: </strong>0th and 2nd person both know 1st person. Therefore, 1 is the celebrity person. </span></pre>
<pre><span style="font-size: 14pt;"><strong>Input: </strong>mat[][] = [[1, 1], [1, 1]]
<strong>Output:</strong> -1
<strong>Explanation: </strong>Since both the people at the party know each other. Hence none of them is a celebrity person.</span></pre>
<pre><span style="font-size: 14pt;"><strong>Input: </strong>mat[][] = [[1]]
<strong>Output:</strong> 0</span></pre>
<p><span style="font-size: 14pt;"><strong>Constraints:</strong><br>1 &lt;= mat.size()&lt;= 1000<br>0 &lt;= mat[i][j]&lt;= 1<br>mat[i][i] == 1</span></p></div>

## Solutions

#### Key Points:
```


```

* **Java**



---

### ✅ **Problem**

You're given a matrix `mat[][]` of size `n x n` where `mat[i][j] = 1` means person `i` knows person `j`. A **celebrity** is a person who:

* **Knows no one** (row has all `0`s except diagonal)
* **Is known by everyone** (column has all `1`s except diagonal)

You must return the **index of the celebrity**, or `-1` if there is none.

---

### ✅ **Intuition & Approach**

* If person `A` knows `B`, then `A` **cannot** be a celebrity.
* But if `A` does **not** know `B`, then `B` **cannot** be a celebrity.
* So we can **eliminate one person in each comparison**, and get a **potential candidate**.
* Then **verify** the candidate by checking:

  * Candidate knows nobody.
  * Everybody knows the candidate.

---

### ✅ **Completed Code with Step-by-Step Comments**

```java
class Solution {
    public int celebrity(int[][] mat) {
        int n = mat.length;  // Step 1: Get the number of people

        // Step 2: Assume person 0 is the celebrity candidate
        int candidate = 0;

        // Step 3: Find potential celebrity by elimination
        for (int i = 1; i < n; i++) {
            // If candidate knows i, then candidate is not celebrity
            // So, make i the new candidate
            if (mat[candidate][i] == 1) {
                candidate = i;
            }
            // If candidate does not know i, do nothing (i can't be celebrity)
        }

        // Step 4: Verify the candidate
        for (int i = 0; i < n; i++) {
            if (i == candidate) continue; // Skip checking self

            // If candidate knows someone OR someone doesn't know candidate
            if (mat[candidate][i] == 1 || mat[i][candidate] == 0) {
                return -1; // Candidate fails celebrity conditions
            }
        }

        // Step 5: Return the celebrity index
        return candidate;
    }
}
```

---

### ✅ **Algorithm (Step-by-Step)**

1. Let candidate = 0
2. Loop `i = 1` to `n - 1`

   * If `mat[candidate][i] == 1` → candidate knows `i` → update `candidate = i`
   * Else `i` can't be celebrity, continue
3. Verify:

   * For all `i ≠ candidate`

     * If `mat[candidate][i] == 1` → fails
     * If `mat[i][candidate] == 0` → fails
4. If candidate passes all → return candidate
5. Else → return -1

---

### ✅ **Dry Run Example**

**Input:**

```java
mat = {
  {0, 1, 0},
  {0, 0, 0},
  {0, 1, 0}
}
```

1. `candidate = 0`

   * `mat[0][1] == 1` → candidate = 1
   * `mat[1][2] == 0` → candidate remains 1

**Verification for candidate = 1**

* `mat[1][0] == 0`, `mat[0][1] == 1` ✅
* `mat[1][2] == 0`, `mat[2][1] == 1` ✅

✅ `1` is celebrity → **Output: 1**

---

### ✅ **Time & Space Complexity**

* **Time**: `O(n)` (one pass to find, one pass to verify)
* **Space**: `O(1)` constant






























