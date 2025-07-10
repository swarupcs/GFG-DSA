## Binary Search

https://leetcode.com/problems/trapping-rain-water/


<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 14pt;">Given a sorted array <strong>arr</strong> and an integer <strong>k</strong>, find the position(0-based indexing) at which k is present in the array using binary search.</span></p>
<p><span style="font-size: 14pt;">Note: If multiple occurrences are there, please return the smallest index.</span></p>
<p><span style="font-size: 14pt;"><strong>Examples:</strong></span></p>
<pre><span style="font-size: 14pt;"><strong>Input: </strong>arr[] = [1, 2, 3, 4, 5], k = 4
<strong>Output:</strong> 3
<strong>Explanation:</strong> 4 appears at index 3.</span></pre>
<pre><span style="font-size: 14pt;"><strong>Input: </strong>arr[] = [11, 22, 33, 44, 55], k = 445
<strong>Output:</strong> -1
<strong>Explanation:</strong> 445 is not present.<br></span></pre>
<pre><span style="font-size: 14pt;"><strong>Input: </strong>arr[] = [1, 1, 1, 1, 2], k = 1
<strong>Output:</strong> 0
<strong>Explanation:</strong> 1 appears at index 0.</span></pre>
<p><span style="font-size: 14pt;"><strong>Constraints:<br></strong>1 ≤ arr.size() ≤ 10<sup>5<br></sup>1 ≤ arr[i] ≤ 10<sup>6<br></sup>1 ≤ k ≤ 10<sup>6</sup></span></p>
<div id="highlighter--hover-tools" style="display: none;">
<div id="highlighter--hover-tools--container">
<div class="highlighter--icon highlighter--icon-copy" title="Copy">&nbsp;</div>
<div class="highlighter--icon highlighter--icon-change-color" title="Change Color">&nbsp;</div>
<div class="highlighter--icon highlighter--icon-delete" title="Delete">&nbsp;</div>
</div>
</div></div>

---

To solve this problem, we need to **find the first (smallest) index of a target `k` in a sorted array using binary search**.
We modify the standard binary search to **continue searching the left half** even after we find the target, to ensure we get the smallest index.

---

### ✅ Problem Summary

**Goal:** Given a sorted array `arr[]` and a target `k`, return the **first occurrence** (smallest index) of `k`.
Return `-1` if the target doesn't exist.

---

### ✅ Intuition

Since the array is **sorted**, binary search allows us to search in **O(log n)** time.
To get the **first occurrence**, we **don't stop** at the first match; instead, we:

* Store the match index.
* Move left (`high = mid - 1`) to check if there's an earlier occurrence.

---

### 🧠 Algorithm (Modified Binary Search)

1. Initialize `low = 0`, `high = n - 1`, `result = -1`.
2. While `low <= high`:

   * Compute `mid = low + (high - low) / 2`.
   * If `arr[mid] == k`:

     * Update `result = mid`.
     * Continue searching on the **left** side (`high = mid - 1`).
   * If `arr[mid] > k`: move left (`high = mid - 1`).
   * If `arr[mid] < k`: move right (`low = mid + 1`).
3. Return `result`.

---

### ✅ Final Java Code with Comments

```java
class Solution {
    public int binarysearch(int[] arr, int k) {
        int low = 0;
        int high = arr.length - 1;
        int result = -1; // Store the first occurrence index

        // Binary Search loop
        while (low <= high) {
            int mid = low + (high - low) / 2; // To avoid overflow

            // If match found, update result and search left
            if (arr[mid] == k) {
                result = mid;        // Potential answer
                high = mid - 1;      // Keep searching in left half
            }
            // If current mid is greater than target, search left
            else if (arr[mid] > k) {
                high = mid - 1;
            }
            // If current mid is less than target, search right
            else {
                low = mid + 1;
            }
        }

        return result; // Return first occurrence index or -1 if not found
    }
}
```

---

### 🧪 Dry Run Example

#### Input: `arr = [1, 1, 1, 1, 2]`, `k = 1`

| Step | low | high | mid | arr\[mid] | result | Action              |
| ---- | --- | ---- | --- | --------- | ------ | ------------------- |
| 1    | 0   | 4    | 2   | 1         | 2      | move left (high=1)  |
| 2    | 0   | 1    | 0   | 1         | 0      | move left (high=-1) |

🔚 Final result: `0`

---

### ⏱ Time & Space Complexity

| Complexity | Value    | Explanation                   |
| ---------- | -------- | ----------------------------- |
| **Time**   | O(log n) | Binary search in sorted array |
| **Space**  | O(1)     | Iterative, no extra space     |

---

### ✅ Summary

* Modified binary search gives **first occurrence** in `O(log n)` time.
* Key idea: keep searching **left** after finding a match.


























