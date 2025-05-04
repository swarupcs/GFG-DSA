## Bitonic Point

https://www.geeksforgeeks.org/problems/maximum-value-in-a-bitonic-array3001/1

<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 14pt;">Given an array of integers <strong>arr[] </strong>that is first <strong>strictly increasing </strong>and then maybe <strong>strictly decreasing</strong>, find the <strong>bitonic point</strong>, that is the maximum element in the array.<br>Bitonic Point is a point before which elements are strictly increasing and after which elements are strictly decreasing.</span></p>
<p><span style="font-size: 14pt;"><strong>Note:</strong> It is guaranteed that the array contains <strong>exactly one</strong> bitonic point.</span></p>
<p><span style="font-size: 14pt;"><strong>Examples:</strong></span></p>
<pre><span style="font-size: 14pt;"><strong>Input: </strong>arr[] = [1, 2, 4, 5, 7, 8, 3]
<strong>Output:</strong> 8
<strong>Explanation:</strong> Elements before 8 are strictly increasing [1, 2, 4, 5, 7] and elements after 8 are strictly decreasing [3].</span></pre>
<pre><span style="font-size: 14pt;"><strong>Input: </strong>arr[] = [10, 20, 30, 40, 50]
<strong>Output:</strong> 50
<strong>Explanation:</strong> Elements before 50 are strictly increasing [10, 20, 30 40] and there are no elements after 50.<br></span></pre>
<pre><span style="font-size: 14pt;"><strong>Input: </strong>arr[] = [120, 100, 80, 20, 0]
<strong>Output:</strong> 120
<strong>Explanation:</strong> There are no elements before 120 and elements after 120 are strictly decreasing [100, 80, 20, 0].</span></pre>
<p><span style="font-size: 14pt;"><strong>Constraints:</strong><br>3 ≤ arr.size() ≤ 10<sup>5</sup><br>1 ≤ arr[i] ≤ 10<sup>6</sup></span></p></div>

## Solutions

#### Key Points:
```


```


---

## ✅ Problem Statement Recap

Given an array `arr[]` that first strictly increases and then maybe strictly decreases, **find the bitonic point**, i.e., the **maximum element** in the array.

---

## ✅ Intuition

This problem can be solved using a **modified binary search**, because the array has a distinct structure:

* Strictly increasing until the bitonic point.
* Strictly decreasing after the bitonic point.

At the **bitonic point**, we observe:

* `arr[mid] > arr[mid-1] && arr[mid] > arr[mid+1]`

We can use this property to **narrow down** the search space using binary search.

---

## ✅ Algorithm (Step-by-Step)

1. Initialize `low = 0` and `high = arr.length - 1`.
2. Run a loop while `low <= high`:

   * Compute `mid = low + (high - low) / 2`.
   * Check if `arr[mid] > arr[mid + 1]`:

     * If true, we're on the **decreasing part** (or at peak) → candidate for max → update answer and move `high = mid - 1`.
   * Else:

     * We're on the **increasing part** → move right → `low = mid + 1`.
3. Return the stored `ans` as the bitonic point.

---

## ✅ Code with Detailed Comments

```java
class Solution {
    public int findMaximum(int[] arr) {
        // Initialize answer as -1 (default), and pointers for binary search
        int ans = -1;
        int low = 0, high = arr.length - 1;

        // Binary Search Loop
        while (low <= high) {
            // Compute mid without overflow
            int mid = low + (high - low) / 2;

            // Check if we are at the last element (to avoid index out of bounds)
            if (mid == arr.length - 1 || arr[mid] > arr[mid + 1]) {
                // If current element is greater than the next, we are in decreasing part
                // This could be the peak or we need to search on the left
                ans = arr[mid];
                high = mid - 1;
            } else {
                // Else we are in increasing part, move to right half
                low = mid + 1;
            }
        }

        // Return the max found
        return ans;
    }
}
```

---

## ✅ Dry Run with Example

### Input: `[1, 2, 4, 5, 7, 8, 3]`

```
Initial: low = 0, high = 6

Iteration 1:
- mid = (0 + 6) / 2 = 3 → arr[3] = 5
- arr[3] < arr[4] (5 < 7) → move right → low = 4

Iteration 2:
- mid = (4 + 6) / 2 = 5 → arr[5] = 8
- arr[5] > arr[6] (8 > 3) → potential max → ans = 8, high = 4

Iteration 3:
- mid = (4 + 4) / 2 = 4 → arr[4] = 7
- arr[4] < arr[5] (7 < 8) → move right → low = 5

Exit loop: low > high

Final answer: 8
```

---

## ✅ Output

```java
Input: [1, 2, 4, 5, 7, 8, 3] → Output: 8
Input: [10, 20, 30, 40, 50] → Output: 50
Input: [120, 100, 80, 20, 0] → Output: 120
```

---




























