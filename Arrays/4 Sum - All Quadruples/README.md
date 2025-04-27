## 4 Sum - All Quadruples


https://www.geeksforgeeks.org/problems/find-all-four-sum-numbers1732/1

<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 18px;">Given an array <strong>arr[]</strong> of integers and another integer <strong>target</strong>. Find all <strong>unique&nbsp;</strong>quadruples from the given array that sums up to <strong>target</strong>.</span></p>
<p><span style="font-size: 18px;"><span style="font-size: 18px;"><strong>Note:</strong> All the quadruples should be internally sorted, ie for any quadruple [q1, q2, q3, q4] it should be : q1 &lt;= q2 &lt;= q3 &lt;= q4.</span></span></p>
<p><span style="font-size: 18px;"><strong>Examples :</strong></span></p>
<pre><span style="font-size: 18px;"><strong>Input: </strong>arr[] = [0, 0, 2, 1, 1], target = 3<br><strong>Output:</strong> [0, 0, 1, 2] <strong>
Explanation: </strong>Sum of 0, 0, 1, 2 is equal to 3.</span>
</pre>
<pre><span style="font-size: 18px;"><strong>Input: </strong>arr[] = [10, 2, 3, 4, 5, 7, 8], target = 23
<strong>Output: </strong>[[2, 3, 8, 10], [2, 4, 7, 10], [3, 5, 7, 8]] <strong>
Explanation: </strong>Sum of 2, 3, 8, 10 is 23, sum of 2, 4, 7, 10 is 23 and sum of 3, 5, 7, 8 is also 23.</span></pre>
<pre><span style="font-size: 18px;"><strong>Input: </strong>arr[] = [0, 0, 2, 1, 1], target = 2<br><strong>Output:</strong> [0, 0, 1, 1] <strong>
Explanation: </strong>Sum of 0, 0, 1, 1 is equal to 2.</span></pre>
<p><span style="font-size: 18px;"><strong>Constraints:</strong><br>1 &lt;= arr.size() &lt;= 200<br>-10<sup>6</sup> &lt;= target &lt;= 10<sup>6</sup><br>-10<sup>6</sup> &lt;= arr[i] &lt;= 10<sup>6</sup></span></p></div>

## Solutions

#### Key Points:
```


```


---

# ✅ Approach
We are given an array and a target sum. We need to find all unique quadruplets whose sum is equal to the target.  
Since it is about four numbers, we **sort** the array first and then **fix two numbers** and use the **two-pointer technique** to find the other two numbers.  
This way, the overall time complexity reduces compared to checking all possible quadruples naively.

---

# ✅ Intuition
- Sorting helps easily **skip duplicates** and **efficiently move** two pointers based on the sum.
- Fixing two elements and using two pointers is a pattern seen in 2Sum and 3Sum problems as well.
- Using `long` type sum to prevent integer overflow (especially when numbers are large).

---

# ✅ Algorithm
1. **Sort** the array.
2. **First loop** — pick the first number (`i` from `0` to `n-4`).
   - Skip duplicate values of `i`.
3. **Second loop** — pick the second number (`j` from `i+1` to `n-3`).
   - Skip duplicate values of `j`.
4. Use **two pointers** `k` (starting from `j+1`) and `l` (starting from `n-1`) to find remaining two numbers:
   - Calculate the `sum = nums[i] + nums[j] + nums[k] + nums[l]`
   - If `sum == target`, add quadruplet to answer, move both pointers and skip duplicates.
   - If `sum < target`, move `k++` (increase sum).
   - If `sum > target`, move `l--` (decrease sum).
5. Return the list of quadruplets.

---

# ✅ Example with Dry Run
Input: `nums = [1, -2, 3, 5, 7, 9]`, `target = 7`

- After sorting: `nums = [-2, 1, 3, 5, 7, 9]`
  
- i = 0 (nums[i] = -2)
  - j = 1 (nums[j] = 1)
    - k = 2 (nums[k] = 3), l = 5 (nums[l] = 9)
      - sum = -2 + 1 + 3 + 9 = 11 > 7, so l--
      - sum = -2 + 1 + 3 + 7 = 9 > 7, so l--
      - sum = -2 + 1 + 3 + 5 = 7 == target → Add [-2, 1, 3, 5] to answer
      - Move k and l → k = 3, l = 2 → break inner loop
  - j = 2, 3, 4 → continue but no valid sum

Final Output: `[[-2, 1, 3, 5]]`

---

# ✅ Final Code (with line-by-line Algorithm as Comments)

```java
import java.util.*;

class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        // Initialize a list to store the final list of quadruplets
        List<List<Integer>> ans = new ArrayList<>();
        
        int n = nums.length;
        
        // Step 1: Sort the array
        Arrays.sort(nums);
        
        // Step 2: Start the first loop to fix the first element
        for (int i = 0; i < n; i++) {
            // Step 2a: Skip duplicate values for the first element
            if (i > 0 && nums[i] == nums[i - 1])
                continue;
            
            // Step 3: Start the second loop to fix the second element
            for (int j = i + 1; j < n; j++) {
                // Step 3a: Skip duplicate values for the second element
                if (j > i + 1 && nums[j] == nums[j - 1])
                    continue;
                
                // Step 4: Initialize two pointers
                int k = j + 1;
                int l = n - 1;
                
                // Step 5: Use two pointers to find the other two numbers
                while (k < l) {
                    // Step 5a: Calculate the sum, cast to long to avoid integer overflow
                    long sum = (long) nums[i] + nums[j] + nums[k] + nums[l];
                    
                    // Step 5b: If sum matches the target, add the quadruplet
                    if (sum == target) {
                        // Add the quadruplet to the answer list
                        List<Integer> temp = Arrays.asList(nums[i], nums[j], nums[k], nums[l]);
                        ans.add(temp);
                        
                        // Step 5c: Move both pointers and skip duplicate values
                        k++;
                        l--;
                        
                        // Skip duplicates for the third number
                        while (k < l && nums[k] == nums[k - 1]) 
                            k++;
                        // Skip duplicates for the fourth number
                        while (k < l && nums[l] == nums[l + 1]) 
                            l--;
                    }
                    // Step 5d: If sum is smaller, move the left pointer to increase the sum
                    else if (sum < target) {
                        k++;
                    }
                    // Step 5e: If sum is larger, move the right pointer to decrease the sum
                    else {
                        l--;
                    }
                }
            }
        }
        
        // Step 6: Return the final list of quadruplets
        return ans;
    }
}
```

---





























