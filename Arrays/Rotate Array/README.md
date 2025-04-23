## Rotate Array


https://www.geeksforgeeks.org/problems/rotate-array-by-n-elements-1587115621/1


<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 14pt;">Given an array <em>arr[]</em><em><strong>.</strong></em>&nbsp;Rotate the array to the left (counter-clockwise direction) by<strong> </strong><em>d</em> steps, where <em>d</em> is a positive integer.&nbsp;Do the mentioned change in the&nbsp;<strong>array in place</strong>.</span></p>
<p><span style="font-size: 14pt;">Note:<strong> </strong>Consider the array as circular.</span></p>
<p><span style="font-size: 14pt;"><strong>Examples :<br></strong></span></p>
<pre><span style="font-size: 14pt;"><strong>Input: </strong>arr[] = [1, 2, 3, 4, 5], d = 2
<strong>Output: </strong>[3, 4, 5, 1, 2]
<strong>Explanation:</strong> when rotated by 2 elements, it becomes 3 4 5 1 2.</span></pre>
<pre><span style="font-size: 14pt;"><strong>Input: </strong>arr[] = [2, 4, 6, 8, 10, 12, 14, 16, 18, 20], d = 3
<strong>Output: </strong>[8, 10, 12, 14, 16, 18, 20, 2, 4, 6]<strong>
Explanation: </strong>when rotated by 3 elements, it becomes 8 10 12 14 16 18 20 2 4 6.<br></span></pre>
<pre><span style="font-size: 14pt;"><strong>Input: </strong>arr[] = [7, 3, 9, 1], d = 9
<strong>Output: </strong>[3, 9, 1, 7]<strong>
Explanation: </strong>when we rotate 9 times, we'll get 3 9 1 7 as resultant array.</span></pre>
<p><span style="font-size: 14pt;"><strong>Constraints:</strong><br>1 &lt;= arr.size(), d &lt;= 10<sup>5</sup></span><br><span style="font-size: 14pt;">0 &lt;=&nbsp;arr[i] &lt;= 10<sup>5</sup></span></p></div>

<div class="problems_accordion_tags__JJ2DX problems_active_tags__3RExF"><div class="active title problems_active_tag_title__cgl9e"><div class="problems_tag_container__kWANg"><strong>Expected Complexities</strong></div></div><div class="content active animated_content open"><div class="problems_expected_complexities_text__h_eyi"><div class="problems_normal_text__QiKrb">Time Complexity: O(n)</div><div class="problems_normal_text__QiKrb">Auxiliary Space: O(1)</div></div></div><div class="ui divider g-mt-3"></div></div>

## Solutions

#### Key Points:
```


```


---

### ✅ **Approach (Reversal Algorithm)**

To rotate the array to the left by `d` positions **in-place**, we use a 3-step reverse strategy:

1. **Reverse the first `d` elements**
2. **Reverse the remaining `n - d` elements**
3. **Reverse the entire array**

This achieves a left rotation in O(n) time and O(1) space.

---

### 🧠 **Why Reverse Works?**

Let array be:  
`[A1, A2, A3, A4, A5], d = 2`

- Step 1: Reverse first 2 → `[A2, A1, A3, A4, A5]`
- Step 2: Reverse rest → `[A2, A1, A5, A4, A3]`
- Step 3: Reverse whole → `[A3, A4, A5, A1, A2]` ✅ Rotated!

---

### ✅ Clean Java Code with Step-by-Step Comments:

```java
class Solution {
    // Function to rotate an array to the left by d positions
    static void rotateArr(int arr[], int d) {
        int n = arr.length; // Get array length

        // Step 1: If d >= n, reduce it to d % n to avoid unnecessary full rotations
        d = d % n;

        // Step 2: Reverse first d elements (from index 0 to d-1)
        reverseArray(arr, 0, d - 1);

        // Step 3: Reverse remaining n - d elements (from index d to n-1)
        reverseArray(arr, d, n - 1);

        // Step 4: Reverse the whole array (from index 0 to n-1)
        reverseArray(arr, 0, n - 1);
    }

    // Utility function to reverse elements between two indices in-place
    private static void reverseArray(int[] arr, int start, int end) {
        // Swap elements from start to end while moving inward
        while (start < end) {
            int temp = arr[start];       // Store value at start
            arr[start] = arr[end];       // Copy value from end to start
            arr[end] = temp;             // Copy stored value to end
            start++;                     // Move start forward
            end--;                       // Move end backward
        }
    }
}
```

---

### 🧪 Dry Run Example:

#### Input:
```java
arr = [1, 2, 3, 4, 5], d = 2
```

#### After steps:
- Reverse 0–1: `[2, 1, 3, 4, 5]`
- Reverse 2–4: `[2, 1, 5, 4, 3]`
- Reverse all: `[3, 4, 5, 1, 2]` ✅

---

### 📌 Time & Space Complexity:

- **Time:** O(n)
- **Space:** O(1) (in-place)

---





























