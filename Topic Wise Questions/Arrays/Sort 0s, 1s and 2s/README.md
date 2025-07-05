## Sort 0s, 1s and 2s


https://www.geeksforgeeks.org/problems/sort-an-array-of-0s-1s-and-2s4231/1


<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 18px;">Given an array <strong>arr[]</strong> containing only <strong>0s, 1s, and 2s.</strong> Sort the array in ascending order.</span></p>
<p><span style="font-size: 18px;">You need to solve this problem without utilizing the built-in sort function.</span></p>
<p><span style="font-size: 18px;"><strong>Examples:</strong></span></p>
<pre><span style="font-size: 18px;"><strong>Input: </strong>arr[] = [0, 1, 2, 0, 1, 2]
<strong>Output: </strong>[0, 0, 1, 1, 2, 2]
<strong>Explanation: </strong>0s 1s and 2s are segregated into ascending order.</span></pre>
<pre><span style="font-size: 18px;"><strong style="font-size: 18px;">Input: </strong><span style="font-size: 18px;">arr[] = [0, 1, 1, 0, 1, 2, 1, 2, 0, 0, 0, 1]
</span><strong style="font-size: 18px;">Output: </strong><span style="font-size: 18px;">[0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 2, 2]
</span><strong style="font-size: 18px;">Explanation: </strong><span style="font-size: 18px;">0s 1s and 2s are segregated into ascending order.<br><br><strong>Follow up:</strong> Could you come up with a one-pass algorithm using only constant extra space?</span></span></pre>
<p><span style="font-size: 18px;"><strong>Constraints:</strong><br>1 &lt;= arr.size() &lt;= 10<sup>6</sup><br>0 &lt;= arr[i] &lt;= 2</span></p></div>

## Solutions

#### Key Points:
```


```


* ✅ **Approach**
* 💡 **Intuition**
* 🧠 **Algorithm**
* 🧪 **Dry Run with Example**
* 💻 **Code with line-by-line comments**
* ⏱ **Time & Space Complexity**

---

### ✅ Approach

Use three pointers:

* `low`: points to the beginning of the array, where 0s should go.
* `mid`: traverses the array.
* `high`: points to the end of the array, where 2s should go.

---

### 💡 Intuition

We scan the array once (`mid <= high`):

* If the element is `0`, move it to the beginning (`swap with low`).
* If it’s `1`, it's already in the middle → just move on.
* If it's `2`, move it to the end (`swap with high`), but **do not increment mid** immediately, because the swapped value needs to be checked.

---

### 🧠 Algorithm

1. Initialize three pointers: `low = 0`, `mid = 0`, `high = n-1`
2. Loop while `mid <= high`

   * If `arr[mid] == 0`: swap with `arr[low]`, increment `low` and `mid`
   * If `arr[mid] == 1`: just increment `mid`
   * If `arr[mid] == 2`: swap with `arr[high]`, decrement `high`

---

### 🧪 Dry Run

Input: `arr = [0, 2, 1, 2, 0, 1]`

Initial: `low = 0`, `mid = 0`, `high = 5`

| mid | arr\[mid] | Action         | Array          | low | mid | high |
| --- | --------- | -------------- | -------------- | --- | --- | ---- |
| 0   | 0         | Swap with low  | \[0,2,1,2,0,1] | 1   | 1   | 5    |
| 1   | 2         | Swap with high | \[0,1,1,2,0,2] | 1   | 1   | 4    |
| 1   | 1         | mid++          | \[0,1,1,2,0,2] | 1   | 2   | 4    |
| 2   | 1         | mid++          | \[0,1,1,2,0,2] | 1   | 3   | 4    |
| 3   | 2         | Swap with high | \[0,1,1,0,2,2] | 1   | 3   | 3    |
| 3   | 0         | Swap with low  | \[0,0,1,1,2,2] | 2   | 4   | 3    |

Result: `[0,0,1,1,2,2]`

---

### 💻 Code with Comments

```java
import java.util.*;

class Solution {
    // Function to sort the array containing only 0s, 1s, and 2s
    public void sort012(int[] arr) {
        int low = 0;                  // Pointer for next 0
        int mid = 0;                  // Pointer to scan array
        int high = arr.length - 1;    // Pointer for next 2

        // Traverse the array
        while (mid <= high) {
            if (arr[mid] == 0) {
                swap(arr, low, mid);  // Move 0 to the beginning
                low++;
                mid++;
            } else if (arr[mid] == 1) {
                mid++;                // 1 is in correct place
            } else {
                swap(arr, mid, high); // Move 2 to the end
                high--;
            }
        }
    }

    // Separate helper function to swap elements in array
    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];   // Store value at index i
        nums[i] = nums[j];    // Replace i with j
        nums[j] = temp;       // Replace j with temp (original i)
    }

    public static void main(String[] args) {
        int[] arr = {0, 2, 1, 2, 0, 1};

        Solution sol = new Solution();
        sol.sort012(arr);

        System.out.println("After sorting:");
        for (int num : arr) {
            System.out.print(num + " ");
        }
    }
}

```

---

### ⏱ Time and Space Complexity

* **Time Complexity:** `O(n)` — Each element is processed at most once.
* **Space Complexity:** `O(1)` — In-place sorting using constant space.

---





























