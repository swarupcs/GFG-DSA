## Remove Duplicates Sorted Array


https://www.geeksforgeeks.org/problems/remove-duplicate-elements-from-sorted-array/1


<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 18px;">Given a <strong>sorted</strong> array<strong> arr.</strong> Return the size of the modified array which contains only distinct elements.<br></span><span style="font-size: 18px;"><em>Note:</em><strong> </strong><br>1.<strong>&nbsp;</strong>Don't use set or HashMap to solve the problem.<br>2. You <strong>must</strong> return the modified array <strong>size only </strong>where distinct elements are present and <strong>modify</strong> the original array such that all the distinct elements come at the beginning of the original array.</span></p>
<p><span style="font-size: 18px;"><strong>Examples :</strong></span></p>
<pre><span style="font-size: 18px;"><strong>Input: </strong>arr = [2, 2, 2, 2, 2]
<strong>Output:</strong> [2]
<strong>Explanation:</strong> After removing all the duplicates only one instance of 2 will remain i.e. [2] so modified array will contains 2 at first position and you should <strong>return 1</strong> after modifying the array, the driver code will print the modified array elements.</span>
</pre>
<pre><span style="font-size: 18px;"><strong>Input: </strong>arr = [1, 2, 4]
<strong>Output:</strong> [1, 2, 4]<br><strong>Explation:  </strong>As the array does not contain any duplicates so you should return 3.</span></pre>
<p><span style="font-size: 18px;"><strong>Constraints:</strong><br>1 ≤ arr.size() ≤ 10<sup>5</sup><br>1 ≤ a<sub>i</sub> ≤ 10<sup>6</sup></span></p></div>



---

## ✅ **Approach: Two-Pointer Technique**

### **Intuition**

Since the array is already **sorted**, all duplicates are grouped together. We can use two pointers:

* `i` → to track the position of the last unique element
* `j` → to scan through the array

Every time we find a new (unique) element, we move `i` forward and overwrite the duplicate at `i` with the new unique value.

---

## ✅ **Algorithm (Step-by-step)**

1. Handle edge case: if the array is empty, return 0.
2. Initialize pointer `i = 0` to store the index of the last unique element.
3. Loop from `j = 1` to `end of array`:

   * If `nums[i] != nums[j]`:

     * Move `i` one step forward.
     * Copy `nums[j]` to `nums[i]`.
4. Finally, return `i + 1` → which is the **length of the array with only unique elements**.

---

## ✅ **Dry Run Example**

### Input: `arr = [1, 1, 2, 2, 2, 3, 3]`

| i | j | nums\[i] | nums\[j] | Action                 | Array after action     |
| - | - | -------- | -------- | ---------------------- | ---------------------- |
| 0 | 1 | 1        | 1        | skip                   | \[1, 1, 2, 2, 2, 3, 3] |
| 0 | 2 | 1        | 2        | i++, nums\[i]=nums\[j] | \[1, 2, 2, 2, 2, 3, 3] |
| 1 | 3 | 2        | 2        | skip                   |                        |
| 1 | 4 | 2        | 2        | skip                   |                        |
| 1 | 5 | 2        | 3        | i++, nums\[i]=nums\[j] | \[1, 2, 3, 2, 2, 3, 3] |
| 2 | 6 | 3        | 3        | skip                   |                        |

📦 Final modified array: `[1, 2, 3]` → return size: `3`

---

## ✅ **Code with Line-by-Line Comments**

```java
class Solution {
    // Function to remove duplicates from the given sorted array
    public int removeDuplicates(int[] nums) {
        // Edge case: If the array is empty, return 0
        if (nums.length == 0) {
            return 0;
        }

        // i points to the last index of the unique elements subarray
        int i = 0;

        // Start from the second element and compare with the last unique element
        for (int j = 1; j < nums.length; j++) {
            // If current element is different from the last unique element
            if (nums[i] != nums[j]) {
                i++; // Move the unique pointer forward
                nums[i] = nums[j]; // Overwrite with the new unique value
            }
        }

        // Return the size of the array with unique elements only
        return i + 1;
    }
}
```

---


## ✅ **Time & Space Complexity**

| Metric           | Value  |
| ---------------- | ------ |
| Time Complexity  | `O(n)` |
| Space Complexity | `O(1)` |

---





























