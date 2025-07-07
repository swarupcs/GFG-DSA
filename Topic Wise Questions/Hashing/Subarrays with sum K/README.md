## Subarrays with sum K


https://www.geeksforgeeks.org/problems/subarrays-with-sum-k/1


<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 14pt;">Given an unsorted array <strong>arr[]</strong> of integers, find the <strong>number of subarrays</strong> whose <strong>sum</strong> exactly equal to a given number <strong>k</strong>.</span></p>
<p><span style="font-size: 14pt;"><strong>Examples:</strong></span></p>
<pre><span style="font-size: 14pt;"><strong>Input:</strong><strong> </strong>arr[] = [10, 2, -2, -20, 10], k = -10
<strong>Output:</strong> 3
<strong>Explaination:</strong> Subarrays: arr[0...3], arr[1...4], arr[3...4] have sum exactly equal to -10.</span></pre>
<pre><span style="font-size: 14pt;"><strong>Input:</strong> arr[] = [9, 4, 20, 3, 10, 5], k = 33
<strong>Output:</strong> 2
<strong>Explaination:</strong> Subarrays: arr[0...2], arr[2...4] have sum exactly equal to 33.<br></span></pre>
<pre><span style="font-size: 14pt;"><strong>Input: </strong>arr[] = [1, 3, 5], k = 0<br></span><span style="font-size: 14pt;"><strong>Output:</strong> 0
<strong>Explaination: </strong>No subarray with 0 sum.</span></pre>
<p><strong style="font-size: 14pt; font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;">Constraints:<br></strong><span style="font-size: 14pt;">1 ≤ arr.size() ≤ 10<sup>5<br></sup></span><span style="font-size: 14pt;">-10<sup>3</sup> ≤ arr[i] ≤ 10<sup>3<br></sup></span><span style="font-size: 14pt;">-10<sup>5</sup> ≤ k ≤&nbsp;</span><span style="font-size: 18.6667px;">10</span><sup>5</sup></p></div>

## Solutions

#### Key Points:
```


```

Here’s the **completed Java code** to find the number of subarrays whose sum is exactly equal to `k`, along with:

✅ **Approach & Intuition**
🧠 **Algorithm steps**
💡 **Line-by-line code explanation with comments**
🧪 **Dry run example**
⏱ **Time & Space complexity**

---

### ✅ Problem Summary

Given an **unsorted array** `arr[]` and an integer `k`, return the **count of contiguous subarrays** whose **sum is exactly equal to `k`**.

---

### ✅ Intuition

This is the same concept as the "**Subarray Sum Equals K**" problem.
We will use the **prefix sum** technique along with a **HashMap** to avoid brute force.

---

### 🧠 Algorithm

1. Use a HashMap `prefixSumCount` to store frequency of prefix sums.
2. Initialize `prefixSum = 0`, `count = 0`.
3. Put `0 → 1` in the map initially to handle subarrays starting at index 0.
4. For each element in the array:

   * Add it to `prefixSum`.
   * If `prefixSum - k` exists in map → add its frequency to `count`.
   * Update the frequency of `prefixSum` in the map.
5. Return `count`.

---

### ✅ Java Code with Detailed Comments

```java
import java.util.HashMap;

class Solution {
    public int cntSubarrays(int[] arr, int k) {
        // Map to store prefix sum and their frequencies
        HashMap<Integer, Integer> prefixSumCount = new HashMap<>();

        // Initialize map with sum 0 occurring once (important for subarrays starting at index 0)
        prefixSumCount.put(0, 1);

        int prefixSum = 0; // Stores cumulative sum
        int count = 0;     // Stores number of valid subarrays

        // Traverse the array
        for (int i = 0; i < arr.length; i++) {
            prefixSum += arr[i]; // Update cumulative sum

            // Check if there's a prefix sum such that: prefixSum - k exists in map
            // If yes, then subarray from that index to current index has sum = k
            if (prefixSumCount.containsKey(prefixSum - k)) {
                count += prefixSumCount.get(prefixSum - k);
            }

            // Update the frequency of current prefix sum in the map
            prefixSumCount.put(prefixSum, prefixSumCount.getOrDefault(prefixSum, 0) + 1);
        }

        // Return the total count of subarrays with sum exactly equal to k
        return count;
    }
}
```

---

### 🧪 Dry Run Example

#### Input: `arr = [10, 2, -2, -20, 10], k = -10`

We want:
→ `prefixSum - k = target prefixSum to search in map`

Initial map: `{0: 1}`
Start with `prefixSum = 0`, `count = 0`

| i | arr\[i] | prefixSum | prefixSum-k | Exists? | Add to count        | Updated Map              |
| - | ------- | --------- | ----------- | ------- | ------------------- | ------------------------ |
| 0 | 10      | 10        | 20          | ❌       | 0                   | {0:1, 10:1}              |
| 1 | 2       | 12        | 22          | ❌       | 0                   | {0:1, 10:1, 12:1}        |
| 2 | -2      | 10        | 20          | ❌       | 0                   | {0:1, 10:2, 12:1}        |
| 3 | -20     | -10       | 0           | ✅       | 1                   | {0:1, 10:2, 12:1, -10:1} |
| 4 | 10      | 0         | 10          | ✅       | 2 (10 occurs twice) | {0:2, 10:2, 12:1, -10:1} |

🎯 Final `count = 3`

---

### ⏱ Time & Space Complexity

| Complexity | Value | Explanation                             |
| ---------- | ----- | --------------------------------------- |
| **Time**   | O(n)  | Single pass through array               |
| **Space**  | O(n)  | HashMap may store up to `n` prefix sums |

---

### ✅ Summary

* This prefix sum + HashMap method is the **most efficient approach**.
* Handles **negative values**, **0**, and **large arrays** efficiently.
* Avoids brute-force O(n²) approaches.





























