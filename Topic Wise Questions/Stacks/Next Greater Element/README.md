## Next Greater Element


https://www.geeksforgeeks.org/problems/next-larger-element-1587115620/1


```
Given an array arr[ ] of n elements, the task is to find the next greater element for each element of the array in order of their appearance in the array. Next greater element of an element in the array is the nearest element on the right which is greater than the current element.
If there does not exist next greater of current element, then next greater element for current element is -1. For example, next greater of the last element is always -1.
```


#### Example 1:

```
Input: arr[] = [1 3 2 4], n = 4
Output: 3 4 4 -1
Explanation: The next larger element to 1 is 3, 3 is 4, 2 is 4 and for 4, since it doesn't exist, it is -1.

```

#### Example 2:
```
Input: arr[] [6 8 0 1 3], n = 5
Output: 8 -1 1 3 -1
Explanation: The next larger element to 6 is 8, for 8 there is no larger elements hence it is -1, for 0 it is 1 , for 1 it is 3 and then for 3 there is no larger element on right and hence -1.
```

#### Example 3:
```
Input: arr[] [6 8 0 1 3], n = 5
Output: 8 -1 1 3 -1
Explanation: The next larger element to 6 is 8, for 8 there is no larger elements hence it is -1, for 0 it is 1 , for 1 it is 3 and then for 3 there is no larger element on right and hence -1.
```
#### Example 3:

```
Input: arr[] [10, 20, 30, 50], n = 4
Output: 20 30 50 -1
Explanation: For a sorted array, the next element is next greater element also exxept for the last element.
```

#### Example 3:
```
Input: arr[] [50, 40, 30, 10], n = 4
Output: -1 -1 -1 -1
Explanation: For a reverse sorted array, the next greater element is always 1.
```

#### Constraints:
```
1 ≤ n ≤ 106
0 ≤ arr[i] ≤ 1018
```


## Solutions

#### Key Points:
```


```

* **Java**


---

### ✅ **Intuition**

We want to find for each element the **nearest greater element to its right**. Using a stack helps efficiently track candidates for NGE while traversing from right to left.

---

### ✅ **Algorithm Steps**

1. Create a result array `ans[]` of size `n` to store next greater elements.
2. Use a stack to keep elements in **monotonic decreasing order**.
3. Traverse from **right to left**:

   * While the stack is not empty and top of stack ≤ current element, pop the stack.
   * If stack is empty, no greater element → put `-1`.
   * Else, top of stack is the NGE → store it in `ans[i]`.
   * Push the current element onto the stack.
4. Return the result array.

---

### ✅ **Code with Line-by-Line Explanation**

```java
import java.util.*;

class Solution {

    // Function to find the next greater element for each element
    public ArrayList<Integer> nextLargerElement(int[] arr) {
        int n = arr.length; // Size of input array

        // Array to store next greater elements
        int[] ans = new int[n];

        // Stack to store the potential next greater elements
        Stack<Integer> st = new Stack<>();

        // Traverse the array from right to left
        for (int i = n - 1; i >= 0; i--) {
            int currEle = arr[i]; // Current element

            // Pop smaller or equal elements from stack
            while (!st.isEmpty() && st.peek() <= currEle) {
                st.pop(); // Not greater, discard
            }

            // If stack is empty → no next greater element
            if (st.isEmpty()) {
                ans[i] = -1;
            } else {
                // Top of stack is next greater element
                ans[i] = st.peek();
            }

            // Push current element onto stack for next iteration
            st.push(currEle);
        }

        // Convert the result array to ArrayList to match method signature
        ArrayList<Integer> result = new ArrayList<>();
        for (int val : ans) {
            result.add(val);
        }

        return result; // Final result
    }
}
```

---

### ✅ **Dry Run Example**

**Input:** `arr = [1, 3, 2, 4]`

**Steps:**

* Start from right → `4`: no greater → `-1`
* `2`: next greater is `4`
* `3`: next greater is `4`
* `1`: next greater is `3`

**Output:** `[3, 4, 4, -1]`

---

### ✅ **Time and Space Complexity**

* **Time:** `O(n)` → each element is pushed and popped once
* **Space:** `O(n)` → for the stack and result array

---




























