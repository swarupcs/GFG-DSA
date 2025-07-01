## Array Leaders


https://www.geeksforgeeks.org/problems/leaders-in-an-array-1587115620/1

<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 14pt;">You are given an array <strong><code>arr</code></strong> of positive integers. Your task is to find all the leaders in the array. An element is considered a leader if it is greater than or equal to all elements to its right. The rightmost element is always a leader.</span></p>
<p><span style="font-size: 14pt;"><strong>Examples:<br></strong></span></p>
<pre><span style="font-size: 14pt;"><strong>Input: </strong>arr = [16, 17, 4, 3, 5, 2]
<strong>Output: </strong>[17, 5, 2]<strong>
Explanation: </strong>Note that there is nothing greater on the right side of 17, 5 and, 2.
</span></pre>
<pre><span style="font-size: 14pt;"><strong>Input: </strong>arr = [10, 4, 2, 4, 1]
<strong>Output: </strong>[10, 4, 4, 1]<br><strong>Explanation:</strong> Note that both of the 4s are in output, as to be a leader an equal element is also allowed on the right. side</span></pre>
<pre><span style="font-size: 14pt;"><strong>Input: </strong>arr = [5, 10, 20, 40]<br><strong>Output: </strong>[40]<br><strong>Explanation:</strong> When an array is sorted in increasing order, only the rightmost element is leader.</span></pre>
<pre><span style="font-size: 14pt;"><strong>Input: </strong>arr = [30, 10, 10, 5]<br><strong>Output:</strong> [30, 10, 10, 5]<br><strong>Explanation:</strong> When an array is sorted in non-increasing order, all elements are leaders.</span></pre>
<p><span style="font-size: 14pt;"><strong>Constraints:</strong><br>1 &lt;= arr.size() &lt;= 10<sup>6</sup><br>0 &lt;= arr[i] &lt;= 10<sup>6</sup></span></p></div>

## Solutions

#### Key Points:
```


```


* ✅ **Approach & Intuition**
* ✅ **Algorithm**
* ✅ **Dry Run**
* ✅ **Fully Commented Code (line by line)**
* ✅ **Time & Space Complexity**

---

## ✅ Problem Clarification:

A **leader** is defined as an element that is **greater than or equal to all elements to its right**.

* The **rightmost element is always a leader**.
* **Duplicates are allowed** if they satisfy the leader condition.

---

## ✅ Approach & Intuition:

We can solve this in **one pass** from **right to left**:

* Start from the last element (always a leader).
* Track the **maximum so far** (`maxRight`).
* For each element from right to left:

  * If it is `>= maxRight`, it's a leader.
  * Update `maxRight`.

---

## ✅ Algorithm:

1. Initialize an empty list `leaders` to store results.
2. Initialize `maxRight = arr[n-1]` (rightmost element).
3. Add `arr[n-1]` to the result.
4. Traverse the array in reverse from `n-2` to `0`:

   * If `arr[i] >= maxRight`, add it to the result.
   * Update `maxRight`.
5. Reverse the result list to maintain original order.
6. Return the result.

---

## ✅ Code with Detailed Line-by-Line Comments

```java
import java.util.*;

class Solution {
    // Function to find all leaders in the array
    public static ArrayList<Integer> findLeaders(int[] arr) {
        // Step 1: Create a list to store leader elements
        ArrayList<Integer> leaders = new ArrayList<>();

        // Step 2: Edge case - if array is empty, return empty list
        if (arr.length == 0) {
            return leaders;
        }

        // Step 3: Initialize the last element as the first leader
        int maxRight = arr[arr.length - 1];  // Rightmost element
        leaders.add(maxRight);               // Always a leader

        // Step 4: Traverse from second last to first element
        for (int i = arr.length - 2; i >= 0; i--) {
            // If current element is >= max so far, it's a leader
            if (arr[i] >= maxRight) {
                leaders.add(arr[i]);     // Add to result
                maxRight = arr[i];       // Update max
            }
        }

        // Step 5: Leaders are added in reverse order → reverse to restore original order
        Collections.reverse(leaders);

        // Step 6: Return final list of leaders
        return leaders;
    }
}
```

---

## ✅ Example with Dry Run

### Input:

```java
arr = [16, 17, 4, 3, 5, 2]
```

### Reverse Traverse:

| Index | Element | maxRight | Is Leader? | leaders     |
| ----- | ------- | -------- | ---------- | ----------- |
| 5     | 2       | -        | ✅ Yes      | \[2]        |
| 4     | 5       | 2        | ✅ Yes      | \[2, 5]     |
| 3     | 3       | 5        | ❌ No       | \[2, 5]     |
| 2     | 4       | 5        | ❌ No       | \[2, 5]     |
| 1     | 17      | 5        | ✅ Yes      | \[2, 5, 17] |
| 0     | 16      | 17       | ❌ No       | \[2, 5, 17] |

🔁 Reverse → \[17, 5, 2]

✅ Output: `[17, 5, 2]`

---

## ✅ Time & Space Complexity

| Metric           | Value | Explanation                                |
| ---------------- | ----- | ------------------------------------------ |
| Time Complexity  | O(n)  | Single traversal + one reversal            |
| Space Complexity | O(k)  | For result list `leaders` (at most size n) |

---

## ✅ Test in Main Method

```java
class Main {
    public static void main(String[] args) {
        int[] arr = {16, 17, 4, 3, 5, 2};
        ArrayList<Integer> leaders = Solution.findLeaders(arr);

        System.out.println("Leaders in the array are:");
        for (int num : leaders) {
            System.out.print(num + " ");
        }
    }
}
```

✅ Output:

```
Leaders in the array are:
17 5 2
```

---






























