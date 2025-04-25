## Maximum Product Subarray


https://www.geeksforgeeks.org/problems/maximum-product-subarray3604/1

<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 18px;">Given an array&nbsp;<strong>arr[]</strong>&nbsp;that contains positive and negative integers (may contain 0 as well). Find the&nbsp;<strong>maximum</strong>&nbsp;product that we can get in a subarray of&nbsp;<strong>arr[]</strong>.</span></p>
<p><span style="font-size: 18px;">Note: It is guaranteed that the output fits in a 32-bit integer.</span></p>
<p><span style="font-size: 18px;"><strong>Examples<br></strong></span></p>
<pre><span style="font-size: 18px;"><strong>Input:</strong> arr[] = [-2, 6, -3, -10, 0, 2]
<strong>Output:</strong> 180
<strong>Explanation:</strong> The subarray with maximum product is {6, -3, -10} with product = 6 * (-3) * (-10) = 180.</span></pre>
<pre><span style="font-size: 18px;"><strong>Input:</strong> arr[] = [-1, -3, -10, 0, 6]
<strong>Output:</strong> 30
<strong>Explanation:</strong> The subarray with maximum product is {-3, -10} with product = (-3) * (-10) = 30.</span></pre>
<pre><span style="font-size: 18px;"><strong>Input: </strong>arr[] = [2, 3, 4] <br><strong>Output:</strong> 24 <br><strong>Explanation:</strong> For an array with all positive elements, the result is product of all elements. </span></pre>
<p><span style="font-size: 18px;"><strong>Constraints:</strong><br>1 ≤ arr.size() ≤ 10<sup>6</sup><br>-10 &nbsp;≤ &nbsp;arr[i] &nbsp;≤ &nbsp;10</span></p></div>
## Solutions

#### Key Points:
```


```


---

### ✅ Intuition

The product of subarrays can drastically change due to:
- **Negative numbers**: Can flip the sign of the product.
- **Zeros**: Reset the product to 0.
- A **negative × negative = positive** → so we must track both **max and min products**.

We track two running products from:
- **Left to right (prefix)**
- **Right to left (suffix)**

This helps us:
- Avoid issues caused by 0s splitting the array.
- Handle subarrays ending at different positions.

---

### ⚙️ Algorithm

1. Initialize:
   - `ans = Integer.MIN_VALUE` → Stores maximum product found.
   - `prefix = 1`, `suffix = 1` → Running products from left & right.

2. Traverse the array from both ends:
   - Multiply current element from left to `prefix`
   - Multiply current element from right to `suffix`
   - If any becomes 0 → reset to 1 (start fresh after zero).
   - Update `ans` as the maximum of: `ans`, `prefix`, and `suffix`.

3. Return `ans`.

---

### ✅ Code with Comments (Step-by-Step)

```java
class Solution {
    // Function to find maximum product subarray
    int maxProduct(int[] arr) {
        int n = arr.length;
        
        // Step 1: Initialize the answer with the smallest possible value
        int ans = Integer.MIN_VALUE;
        
        // Step 2: Initialize prefix and suffix products
        int prefix = 1;
        int suffix = 1;
        
        // Step 3: Traverse from both directions
        for (int i = 0; i < n; i++) {
            
            // Step 4: If prefix or suffix becomes 0, reset it to 1
            // Because product with 0 restarts the subarray
            if (prefix == 0) prefix = 1;
            if (suffix == 0) suffix = 1;
            
            // Step 5: Update prefix (left-to-right product)
            prefix *= arr[i];
            
            // Step 6: Update suffix (right-to-left product)
            suffix *= arr[n - i - 1];
            
            // Step 7: Update the answer with the max of current products
            ans = Math.max(ans, Math.max(prefix, suffix));
        }
        
        // Step 8: Return the maximum product found
        return ans;
    }
}
```

---

### 🧪 Example Dry Run

Input: `[-2, 6, -3, -10, 0, 2]`

| i | arr[i] | arr[n-i-1] | prefix | suffix | ans |
|--|--------|-------------|--------|--------|-----|
| 0 | -2     | 2           | -2     | 2      | 2   |
| 1 | 6      | 0           | -12    | 0      | 2   |
| 2 | -3     | -10         | 36     | -10    | 36  |
| 3 | -10    | -3          | -360   | 30     | 36  |
| 4 | 0      | 6           | 0 → 1  | 180    | 180 |
| 5 | 2      | -2          | 2      | -360   | 180 |

Final `ans = 180`

✅ Subarray: `[6, -3, -10]`  
✅ Product: `6 * -3 * -10 = 180`

---



























