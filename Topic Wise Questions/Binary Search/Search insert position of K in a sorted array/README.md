## Search insert position of K in a sorted array


https://www.geeksforgeeks.org/problems/search-insert-position-of-k-in-a-sorted-array/1


<div class="problems_problem_content__Xm_eO"><p><span style="font-size:18px">Given a sorted array&nbsp;<strong>Arr[]</strong>(0-index based)&nbsp;consisting of&nbsp;<strong>N&nbsp;</strong>distinct integers and an integer <strong>k</strong>, the task is to find the index of k, if its present in the array <strong>Arr[]</strong>. Otherwise, find the index where <strong>k</strong>&nbsp;must be inserted to keep the array sorted.</span></p>

<p><br>
<span style="font-size:18px"><strong>Example 1:</strong></span></p>

<pre><span style="font-size:18px"><strong>Input:</strong>
N = 4
Arr = {1, 3, 5, 6}
k = 5
<strong>Output:</strong> 2
<strong>Explaination:</strong> Since 5 is found at index 2 
as Arr[2] = 5, the output is 2.</span></pre>

<p><br>
<span style="font-size:18px"><strong>Example 2:</strong></span></p>

<pre><span style="font-size:18px"><strong>Input:</strong>
N = 4
Arr = {1, 3, 5, 6}
k = 2
<strong>Output:</strong> 1
<strong>Explaination:</strong> Since 2 is not present in 
the array but can be inserted at index 1 
to make the array sorted.</span>
</pre>

<p><br>
<span style="font-size:18px"><strong>Your Task:</strong><br>
You don't need to read input or print anything. Your task is to complete the function&nbsp;<strong>searchInsertK()</strong>&nbsp;which takes the array <strong>Arr[]</strong> and its size <strong>N </strong>and <strong>k&nbsp;</strong>as input parameters&nbsp;and returns the index.</span></p>

<p><br>
<span style="font-size:18px"><strong>Expected Time Complexity:</strong> O(logN)<br>
<strong>Expected Auxiliary Space:</strong> O(1)</span></p>

<p><br>
<span style="font-size:18px"><strong>Constraints:</strong><br>
1 ≤ N ≤ 10<sup>4</sup><br>
-10<sup>3</sup> ≤ Arr[i]&nbsp;≤ 10<sup>3</sup><br>
-10<sup>3</sup>&nbsp;≤ k&nbsp;≤ 10<sup>3</sup></span></p>
</div>

## Solutions

#### Key Points:
```


```
---

Here is the **completed Java code** for the `searchInsertK()` function using **binary search**, which returns either:

* the **index** of the element `k` in a sorted array `Arr[]`, or
* the **position where `k` should be inserted** to maintain sorted order.

It includes:

* ✅ Approach & Intuition
* 🧠 Step-by-step algorithm
* 💬 Line-by-line code explanation with comments
* 🧪 Dry run example
* ⏱ Time and space complexity

---

### ✅ Problem Summary

You're given:

* A **sorted array** `Arr[]` of size `N` with **distinct integers**.
* An integer `k`.

You must return:

* The index of `k` if it's found.
* Otherwise, the index where `k` should be inserted to keep the array sorted.

---

### ✅ Intuition

This is a classic **binary search with a slight twist**. Instead of just returning `-1` if not found, we keep track of a potential **insert position**.

---

### 🧠 Algorithm

1. Initialize `low = 0`, `high = N - 1`, `ans = N`.
2. While `low <= high`:

   * Compute `mid = (low + high) / 2`.
   * If `Arr[mid] >= k`:

     * Set `ans = mid` (could be answer).
     * Search in **left half**.
   * Else:

     * Search in **right half**.
3. Return `ans`.

---

### ✅ Complete Code with Comments

```java
// User function Template for Java

class Solution {
    // Function to search or find insert position of k in sorted array
    static int searchInsertK(int Arr[], int N, int k) {
        int low = 0;          // Start of search space
        int high = N - 1;     // End of search space
        int ans = N;          // Default insertion point is at the end

        // Binary search loop
        while (low <= high) {
            int mid = (low + high) / 2;  // Calculate mid index

            // If mid element is greater than or equal to target
            if (Arr[mid] >= k) {
                ans = mid;         // Possible answer (index or insert position)
                high = mid - 1;    // Try to find smaller index on the left
            } else {
                low = mid + 1;     // Move to right half
            }
        }

        return ans;  // Final result: index if found or insert position
    }
}
```

---

### 🧪 Dry Run

#### Input:

```java
Arr = [1, 3, 5, 6], N = 4, k = 2
```

**Trace:**

* `low = 0`, `high = 3`, `ans = 4`
* `mid = 1`, `Arr[mid] = 3 >= 2` → `ans = 1`, `high = 0`
* `mid = 0`, `Arr[mid] = 1 < 2` → `low = 1`
* loop ends → return `ans = 1`

✅ **Output:** `1`

---

### ⏱ Time & Space Complexity

| Complexity | Value    | Reason              |
| ---------- | -------- | ------------------- |
| Time       | O(log N) | Binary search       |
| Space      | O(1)     | No extra space used |

---

### ✅ Summary

* Efficiently finds **index or insert position** using binary search.
* Ideal for sorted arrays with **distinct elements**.
* Common in real-world search problems (autocomplete, range finding, etc).






























