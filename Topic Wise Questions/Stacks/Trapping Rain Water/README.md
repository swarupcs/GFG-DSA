## Trapping Rain Water


https://www.geeksforgeeks.org/problems/trapping-rain-water-1587115621/1


<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 18px;">Given an array <strong>arr[] </strong>with non-negative integers representing the height of blocks. If the width of each block is 1, compute how much water can be trapped between the blocks during the rainy season.&nbsp;</span></p>
<p><span style="font-size: 18px;"><strong>Examples:</strong></span></p>
<pre><span style="font-size: 18px;"><strong>Input: </strong>arr[] = [3, 0, 1, 0, 4, 0 2]
<strong>Output: </strong>10<strong>
Explanation: </strong>Total water trapped = 0 + 3 + 2 + 3 + 0 + 2 + 0 = 10 units.<br></span><img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/701211/Web/Other/blobid0_1741784862.png" alt=""></pre>
<pre><span style="font-size: 18px;"><strong>Input: </strong>arr[] = [3, 0, 2, 0, 4]
<strong>Output: </strong>7<strong>
Explanation: </strong>Total water trapped = 0 + 3 + 1 + 3 + 0 = 7 units.</span>
</pre>
<pre><span style="font-size: 18px;"><strong>Input: </strong>arr[] = [1, 2, 3, 4]
<strong>Output: </strong>0<strong>
Explanation: </strong>We cannot trap water as there is no height bound on both sides.</span></pre>
<pre><span style="font-size: 18px;"><strong>Input: </strong>arr[] = [2, 1, 5, 3, 1, 0, 4]
<strong>Output: </strong>9<strong>
Explanation: </strong>Total water trapped = 0 + 1 + 0 + 1 + 3 + 4 + 0 = 9 units.</span></pre>
<p><span style="font-size: 18px;"><strong>Constraints:</strong><br>1 <u>&lt;</u> arr.size() <u>&lt;</u> 10<sup>5</sup><br>0 <u>&lt;</u> arr[i] <u>&lt;</u> 10<sup>3</sup></span></p></div>


---

## ✅ Problem:

Given an array `arr[]` of size `n` representing the elevation map, return the total amount of water that can be trapped after raining.

---

## 💡 Intuition:

To trap water, we need **walls on both sides** of a block. The water above any bar depends on the **shorter of the tallest bars on both its sides**.
Instead of precomputing these values with extra space, we use two pointers and dynamically track `leftMax` and `rightMax`.

---

## 🔍 Approach:

* Use two pointers: `left = 0` and `right = n - 1`
* Track the highest bars seen so far from the left and right
* Move the pointer pointing to the **shorter height** inward
* At each step, if `height[left] < height[right]`:

  * If `arr[left] < leftMax`, trap water
  * Else update `leftMax`
* Do the same for the right side if it's shorter
* Time Complexity: `O(n)`
* Space Complexity: `O(1)`

---

## ✅ Completed Java Code with Step-by-Step Comments:

```java
class Solution {
    public int maxWater(int arr[]) {
        // Step 1: Get length of the array
        int n = arr.length;

        // Step 2: Edge case - if less than 3 bars, no water can be trapped
        if (n < 3) return 0;

        // Step 3: Initialize pointers
        int left = 0;             // Start pointer
        int right = n - 1;        // End pointer

        // Step 4: Variables to track maximum height seen so far from left and right
        int leftMax = 0;
        int rightMax = 0;

        // Step 5: Variable to accumulate total trapped water
        int totalWater = 0;

        // Step 6: Traverse while left is less than right
        while (left < right) {

            // Step 6.1: If height at left is smaller than at right
            if (arr[left] <= arr[right]) {

                // Step 6.2: If current height is less than leftMax, water can be trapped
                if (arr[left] < leftMax) {
                    totalWater += leftMax - arr[left]; // Trap water
                } else {
                    // Step 6.3: Update leftMax if no water can be trapped
                    leftMax = arr[left];
                }

                // Step 6.4: Move left pointer to the right
                left++;
            } 
            // Step 6.5: If height at right is smaller
            else {

                // Step 6.6: If current height is less than rightMax, water can be trapped
                if (arr[right] < rightMax) {
                    totalWater += rightMax - arr[right]; // Trap water
                } else {
                    // Step 6.7: Update rightMax if no water can be trapped
                    rightMax = arr[right];
                }

                // Step 6.8: Move right pointer to the left
                right--;
            }
        }

        // Step 7: Return the accumulated trapped water
        return totalWater;
    }
}
```

---

## 📜 Algorithm:

1. Initialize `left = 0`, `right = n-1`
2. Initialize `leftMax = 0`, `rightMax = 0`, `totalWater = 0`
3. While `left < right`:

   * If `arr[left] <= arr[right]`:

     * If `arr[left] < leftMax`, add `leftMax - arr[left]` to `totalWater`
     * Else update `leftMax = arr[left]`
     * Move `left++`
   * Else:

     * If `arr[right] < rightMax`, add `rightMax - arr[right]` to `totalWater`
     * Else update `rightMax = arr[right]`
     * Move `right--`
4. Return `totalWater`

---

## 🧪 Example + Dry Run

### Input:

```java
int[] arr = {0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1};
```

### Expected Output:

```
6
```

### Dry Run Steps:

* Start: `left = 0`, `right = 11`, `leftMax = 0`, `rightMax = 0`, `totalWater = 0`
* Compare `arr[left]=0` and `arr[right]=1`
* Since 0 <= 1:

  * `arr[left] < leftMax → 0 < 0` → False → update `leftMax = 0`
  * Move `left → 1`
* `arr[1]=1 <= arr[11]=1`:

  * `1 < 0` → False → update `leftMax = 1`
  * Move `left → 2`
* `arr[2]=0 < leftMax=1 → trap 1`

  * `totalWater = 1`
  * Move `left → 3`
* `arr[3]=2 > leftMax → update leftMax = 2`

  * Move `left → 4`
* `arr[4]=1 < leftMax=2 → trap 1`

  * `totalWater = 2`
  * Move `left → 5`
* `arr[5]=0 < leftMax=2 → trap 2`

  * `totalWater = 4`
* `arr[6]=1 < leftMax=2 → trap 1`

  * `totalWater = 5`
* `arr[7]=3 > leftMax → update leftMax = 3`
* `arr[8]=2 < leftMax=3 → trap 1`

  * `totalWater = 6`

✅ Final Answer: `6`






























