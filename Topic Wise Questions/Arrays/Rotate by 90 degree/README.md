## Rotate by 90 degree


https://www.geeksforgeeks.org/problems/rotate-by-90-degree0356/0

<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 18px;">Given a<strong> </strong>square&nbsp;<strong>mat[][]</strong>. The task is to rotate it by<strong> 90 degrees in clockwise</strong> direction without using any extra space.</span></p>
<p><span style="font-size: 18px;"><strong>Examples:</strong></span></p>
<pre><span style="font-size: 18px;"><strong>Input: </strong>mat[][] = [[1 2 3], [4 5 6], [7 8 9]]
<strong>Output:</strong>
7 4 1 <br>8 5 2<br>9 6 3</span></pre>
<pre><span style="font-size: 18px;"><strong>Input: </strong>mat[][] = [1 2], [3 4]<br><strong>Output:<br></strong>3 1 <br>4 2<br></span></pre>
<pre><strong><span style="font-size: 14pt;">Input: </span></strong><span style="font-size: 14pt;">mat[][] = [[1]]<br><strong>Output:<br></strong></span><span style="font-size: 14pt;">1</span></pre>
<p><span style="font-size: 18px;"><strong style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;">Constraints:<br></strong></span><span style="font-size: 18px;">1 ≤ mat.size() ≤ 1000<br></span><span style="font-size: 18px;">1 &lt;= mat[][] &lt;= 100</span></p></div>

## Solutions

#### Key Points:
```


```


---

# ✅ Approach
To rotate a matrix 90 degrees **clockwise in-place**, we **cannot** use extra space (like another matrix).

The steps:
1. **Transpose** the matrix (swap rows and columns).
2. **Reverse each row** individually.

---

# ✅ Intuition
- **Transpose** converts rows into columns.
- But after transpose, **the order of elements** is still wrong for 90° rotation.
- So, **reversing each row** fixes the order.
  
Example:  
Original 1st row → becomes last column after rotation.  
Hence **Transpose + Reverse each row**.

---

# ✅ Algorithm

1. Get the size of the matrix `n`.
2. **Transpose**:
   - For each `i` from 0 to `n-1`
   - For each `j` from `i+1` to `n-1`
   - Swap `mat[i][j]` with `mat[j][i]`
3. **Reverse each row**:
   - For each row:
     - Swap the elements from start to end till the middle.

---

# ✅ Code with Detailed Step-by-Step Comments

```java
class GFG {
    
    static void rotate(int mat[][]) {
        int n = mat.length; // Step 1: Find the size of matrix
        
        // Step 2: Transpose the matrix
        for (int i = 0; i < n; i++) { // Iterate over each row
            for (int j = i + 1; j < n; j++) { // Iterate only above diagonal
                // Swap mat[i][j] and mat[j][i]
                int temp = mat[i][j];
                mat[i][j] = mat[j][i];
                mat[j][i] = temp;
            }
        }
        
        // Step 3: Reverse each row
        for (int i = 0; i < n; i++) { // Iterate through each row
            int start = 0, end = n - 1;
            
            while (start < end) { // Until the middle is reached
                // Swap mat[i][start] and mat[i][end]
                int temp = mat[i][start];
                mat[i][start] = mat[i][end];
                mat[i][end] = temp;
                
                start++;
                end--;
            }
        }
    }
}
```

---

# ✅ Dry Run Example

Input:
```
mat = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
]
```

### Step 1: Transpose

Swap `mat[i][j]` with `mat[j][i]` for all `i < j`.

- Swap mat[0][1] and mat[1][0]: (2 ↔ 4)
- Swap mat[0][2] and mat[2][0]: (3 ↔ 7)
- Swap mat[1][2] and mat[2][1]: (6 ↔ 8)

**After transpose**:

```
[
  [1, 4, 7],
  [2, 5, 8],
  [3, 6, 9]
]
```

---

### Step 2: Reverse Each Row

- Row 0: [1, 4, 7] → [7, 4, 1]
- Row 1: [2, 5, 8] → [8, 5, 2]
- Row 2: [3, 6, 9] → [9, 6, 3]

**Final matrix**:

```
[
  [7, 4, 1],
  [8, 5, 2],
  [9, 6, 3]
]
```

✅ Done!

---

# ✅ Summary

| Step         | Action                           |
| ------------ | --------------------------------- |
| Transpose    | Swap across the diagonal          |
| Reverse Rows | Swap elements in each row         |
| Space Used   | In-place (O(1) extra space)        |
| Time         | O(N²) — Full matrix traversal     |

---

# 📌 Notes:
- We use `j = i + 1` in the transpose to avoid reswapping or touching the diagonal elements.
- During row reversal, we swap elements until the middle using two pointers.

---




























