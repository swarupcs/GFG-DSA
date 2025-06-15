## Histogram Max Rectangular Area

https://www.geeksforgeeks.org/problems/maximum-rectangular-area-in-a-histogram-1587115620/1


```
Find the largest rectangular area possible in a given histogram where the largest rectangle can be made of a number of contiguous bars. For simplicity, assume that all bars have the same width and the width is 1 unit, there will be N bars height of each bar will be given by the array arr.
```


#### Example 1:

```
Input:
N = 7
arr[] = {6,2,5,4,5,1,6}
Output: 12
Explanation: In this example the largest area would be 12 of height 4 and width 3. We can achieve this 
area by choosing 3rd, 4th and 5th bars.

```

#### Example 2:
```
Input:
N = 8
arr[] = {7 2 8 9 1 3 6 5}
Output: 16
Explanation: Maximum size of the histogram 
will be 8  and there will be 2 consecutive 
histogram. And hence the area of the 
histogram will be 8x2 = 16.
```
### Your Task:

```
The task is to complete the function getMaxArea() which takes the array arr[] and its size N as inputs and finds the largest rectangular area possible and returns the answer.

Expected Time Complxity : O(N)
Expected Auxilliary Space : O(N)
```

#### Constraints:
```
1 ≤ N ≤ 106
0 ≤ arr[i] ≤ 1012
```

## Solutions

#### Key Points:
```


```

To solve the **Largest Rectangular Area in a Histogram** problem, we can use a **monotonic stack** approach. This method is optimal with a **time complexity of O(n)**.

---

### ✅ **Approach & Intuition**

* For every bar, we want to find:

  * The **nearest smaller element to the left (NSL)**
  * The **nearest smaller element to the right (NSR)**
* Using these, we calculate the **width** of the rectangle that can be extended for each bar.
* The **area = height × width**, and we update the max area.

---

### ✅ **Algorithm**

1. Initialize a stack to store indices.
2. Traverse the histogram to find the **NSL** for each bar.
3. Traverse from the end to find the **NSR** for each bar.
4. Use `NSR[i] - NSL[i] - 1` to calculate the width of the rectangle for each bar.
5. For every index `i`, calculate `height[i] * width[i]`.
6. Track the **maximum area** found.

---

### ✅ **Java Code with Step-by-Step Comments**

```java
import java.util.*;

class Solution {
    public static int getMaxArea(int[] arr) {
        int n = arr.length;
        Stack<Integer> stack = new Stack<>();
        
        // Arrays to store index of nearest smaller to left and right
        int[] nsl = new int[n]; // Nearest Smaller to Left
        int[] nsr = new int[n]; // Nearest Smaller to Right
        
        // Step 1: Calculate NSL (Nearest Smaller to Left)
        for (int i = 0; i < n; i++) {
            // Pop from stack while elements are >= current height
            while (!stack.isEmpty() && arr[stack.peek()] >= arr[i]) {
                stack.pop();
            }

            // If stack is empty, no smaller element to the left
            nsl[i] = stack.isEmpty() ? -1 : stack.peek();

            // Push current index to stack
            stack.push(i);
        }

        // Clear stack to reuse for NSR
        stack.clear();

        // Step 2: Calculate NSR (Nearest Smaller to Right)
        for (int i = n - 1; i >= 0; i--) {
            // Pop from stack while elements are >= current height
            while (!stack.isEmpty() && arr[stack.peek()] >= arr[i]) {
                stack.pop();
            }

            // If stack is empty, no smaller element to the right
            nsr[i] = stack.isEmpty() ? n : stack.peek();

            // Push current index to stack
            stack.push(i);
        }

        // Step 3: Calculate the maximum area
        int maxArea = 0;
        for (int i = 0; i < n; i++) {
            int width = nsr[i] - nsl[i] - 1; // Total width that can be covered
            int area = arr[i] * width;      // Area with current height
            maxArea = Math.max(maxArea, area);
        }

        return maxArea;
    }
}
```

---

### ✅ **Example & Dry Run**

#### Input:

```
arr = [60, 20, 50, 40, 10, 50, 60]
```

#### Step-by-step:

* `NSL = [-1, -1, 1, 1, -1, 4, 5]`
* `NSR = [1, 4, 3, 4, 7, 7, 7]`

Now compute width and area for each:

* i = 0 → width = 1 - (-1) - 1 = 1 → area = 60×1 = 60
* i = 1 → width = 4 - (-1) - 1 = 4 → area = 20×4 = 80
* i = 2 → width = 3 - 1 - 1 = 1 → area = 50×1 = 50
* i = 3 → width = 4 - 1 - 1 = 2 → area = 40×2 = 80
* i = 4 → width = 7 - (-1) - 1 = 7 → area = 10×7 = 70
* i = 5 → width = 7 - 4 - 1 = 2 → area = 50×2 = **100**
* i = 6 → width = 7 - 5 - 1 = 1 → area = 60×1 = 60

✅ **Maximum area = 100**

---

### ✅ **Time and Space Complexity**

* **Time:** O(n)
* **Space:** O(n) (for NSL, NSR, and stack)






























