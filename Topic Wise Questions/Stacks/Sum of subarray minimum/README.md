## Sum of subarray minimum


https://www.geeksforgeeks.org/problems/sum-of-subarray-minimum/1


<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 14pt;">Given an array <strong>a</strong><strong>rr</strong> containing positive integers, find the sum of the minimum element of all subarrays. Since the answer may be very large, return the answer modulo 10<sup>9</sup>&nbsp;+7.&nbsp;</span></p>
<p><span style="font-size: 14pt;"><strong>Examples:</strong></span></p>
<pre><span style="font-size: 14pt;"><strong>Input: </strong>arr[] = [3, 1, 2, 4]<br><strong>Output: </strong>17<br><strong>Explanation:</strong> subarrays are [3], [1], [2], [4], [3, 1], [1, 2], [2, 4], [3, 1, 2], [1, 2, 4], [3, 1, 2, 4]. Minimums are 3 , 1 , 2 , 4 , 1 , 1 , 2 , 1 , 1 , 1 ans sum of all these are 17.</span></pre>
<pre><span style="font-size: 14pt;"><strong>Input: </strong>arr[] = [71, 55, 82, 55]<br><strong>Output: </strong>593<br><strong>Explanation: </strong>The sum of the minimum of all the subarrays are 593.</span></pre>
<p><span style="font-size: 14pt;"><strong>Constraints:</strong><br>1 ≤ arr.size() ≤ 10<sup>6</sup><br>0 ≤ arr[i]<sub>&nbsp;&nbsp;</sub>≤ 10<sup>6</sup></span></p></div>





---

### ✅ Intuition:

Each element `arr[i]` is the minimum in several subarrays.
To count how many, we compute:

* How many subarrays start with or before `i` and end at or after `i` **where `arr[i]` is the minimum**.

To do that:

* Find **Previous Smaller or Equal Element (PSEE)**: left boundary.
* Find **Next Smaller Element (NSE)**: right boundary.
* Total subarrays where `arr[i]` is the minimum: `(i - PSEE[i]) * (NSE[i] - i)`



---

### ✅ **Algorithm: Sum of Minimums of All Subarrays**

#### **Step 1: Initialize variables**

* Let `n` be the length of array `arr`.
* Initialize `mod = 10^9 + 7` (to take the result modulo).
* Create two arrays:

  * `nse[]`: Next Smaller Element index for each element.
  * `psee[]`: Previous Smaller or Equal Element index for each element.

---

#### **Step 2: Compute Next Smaller Element (NSE) for each element**

* Traverse array from **right to left** (i = n-1 to 0).
* Use a **monotonic increasing stack** (stack that stores indices of increasing values).
* While stack is not empty and `arr[stack.top()] >= arr[i]`, pop the stack.
* If stack is empty, set `nse[i] = n` (no smaller element to right).
* Else set `nse[i] = stack.top()` (index of next smaller).
* Push current index `i` to the stack.

---

#### **Step 3: Compute Previous Smaller or Equal Element (PSEE) for each element**

* Traverse array from **left to right** (i = 0 to n-1).
* Use a **monotonic increasing stack**.
* While stack is not empty and `arr[stack.top()] > arr[i]`, pop the stack.
* If stack is empty, set `psee[i] = -1` (no smaller or equal to the left).
* Else set `psee[i] = stack.top()`.
* Push current index `i` to the stack.

---

#### **Step 4: Compute the contribution of each element to the final sum**

* Initialize `sum = 0`.
* For each index `i` in the array:

  * Compute `left = i - psee[i]` → count of elements to the left including current.
  * Compute `right = nse[i] - i` → count of elements to the right including current.
  * Compute frequency = `left * right`
  * Contribution of `arr[i] = arr[i] * frequency`
  * Add contribution to `sum` → `sum = (sum + contribution) % mod`.

---

#### **Step 5: Return the result**

* Return the final value of `sum` which is the **sum of all subarray minimums** modulo `10^9 + 7`.


---




### ✅ Code (Complete with Comments & Dry Run):

```java
import java.util.*;

class Solution {

    // Function to find index of Next Smaller Element (NSE)
    private int[] findNSE(int[] arr) {
        int n = arr.length;
        int[] ans = new int[n];
        Stack<Integer> st = new Stack<>();

        // Traverse from right to left
        for (int i = n - 1; i >= 0; i--) {
            // Pop all elements >= current
            while (!st.isEmpty() && arr[st.peek()] >= arr[i]) {
                st.pop();
            }

            // If stack is empty, no smaller element to right
            ans[i] = st.isEmpty() ? n : st.peek();

            // Push current index
            st.push(i);
        }

        return ans;
    }

    // Function to find index of Previous Smaller or Equal Element (PSEE)
    private int[] findPSEE(int[] arr) {
        int n = arr.length;
        int[] ans = new int[n];
        Stack<Integer> st = new Stack<>();

        // Traverse from left to right
        for (int i = 0; i < n; i++) {
            // Pop elements > current
            while (!st.isEmpty() && arr[st.peek()] > arr[i]) {
                st.pop();
            }

            // If empty, no smaller/equal on left
            ans[i] = st.isEmpty() ? -1 : st.peek();

            // Push current index
            st.push(i);
        }

        return ans;
    }

    // Main function to return sum of subarray minimums
    public static int sumSubarrayMins(int[] arr) {
        int n = arr.length;
        int mod = (int)1e9 + 7;

        Solution sol = new Solution();

        // Get next smaller and previous smaller or equal indices
        int[] nse = sol.findNSE(arr);
        int[] psee = sol.findPSEE(arr);

        long sum = 0;

        // Traverse array and compute contribution of each element
        for (int i = 0; i < n; i++) {
            // Count of subarrays where arr[i] is the minimum
            long left = i - psee[i];     // How many elements on left
            long right = nse[i] - i;     // How many elements on right

            // Total subarrays = left * right
            long freq = left * right;

            // Add contribution to sum
            long contribution = (freq * arr[i]) % mod;
            sum = (sum + contribution) % mod;
        }

        return (int)sum;
    }

    // Test driver
    public static void main(String[] args) {
        int[] arr1 = {3, 1, 2, 4};
        int[] arr2 = {71, 55, 82, 55};

        System.out.println("Output 1: " + sumSubarrayMins(arr1)); // 17
        System.out.println("Output 2: " + sumSubarrayMins(arr2)); // 593
    }
}
```

---

### ✅ Dry Run: `arr = [3, 1, 2, 4]`

| Subarray   | Min |
| ---------- | --- |
| \[3]       | 3   |
| \[1]       | 1   |
| \[2]       | 2   |
| \[4]       | 4   |
| \[3,1]     | 1   |
| \[1,2]     | 1   |
| \[2,4]     | 2   |
| \[3,1,2]   | 1   |
| \[1,2,4]   | 1   |
| \[3,1,2,4] | 1   |

✅ Total: `3 + 1 + 2 + 4 + 1 + 1 + 2 + 1 + 1 + 1 = 17`

---


### ✅ Example Dry Run:

For `arr = [3, 1, 2, 4]`:

* PSEE = \[-1, -1, 1, 2]
* NSE = \[1, 4, 3, 4]

| i | arr\[i] | PSEE | NSE | Left | Right | Freq | Contribution |
| - | ------- | ---- | --- | ---- | ----- | ---- | ------------ |
| 0 | 3       | -1   | 1   | 1    | 1     | 1    | 3            |
| 1 | 1       | -1   | 4   | 2    | 3     | 6    | 6            |
| 2 | 2       | 1    | 3   | 1    | 1     | 1    | 2            |
| 3 | 4       | 2    | 4   | 1    | 1     | 1    | 4            |

➡️ **Total = 3 + 6 + 2 + 4 = 17**

---

### ✅ Time and Space Complexity

* **Time:** `O(n)` – single pass for each of `nse`, `psee`, and main loop.
* **Space:** `O(n)` – stack + arrays.

---





























































































































































































































