## Intersection of two sorted arrays


https://www.geeksforgeeks.org/problems/intersection-of-two-sorted-array-1587115620/1


<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 18px;">&nbsp;Given two sorted arrays <strong>arr1</strong>[] and <strong>arr</strong>2[]. Your task is to return the <strong>intersection </strong>of both arrays.</span></p>
<blockquote>
<p><span style="font-size: 18px;">Intersection of two arrays is said to be elements that are common in both arrays.&nbsp;</span><span style="font-size: 18px;">The intersection should not count duplicate elements.</span></p>
</blockquote>
<p><span style="font-size: 18px;">Note</span><span style="font-size: 18px;">:</span><span style="font-size: 18px;">&nbsp;</span><span style="color: #1e2229; font-family: Nunito; font-size: 14pt; background-color: #ffffff;">If there is no intersection then return an empty array.</span></p>
<p><span style="font-size: 18px;"><strong>Examples</strong></span><strong style="font-size: 18px;">:</strong></p>
<pre><span style="font-size: 18px;"><strong>Input</strong>: arr1[] = [1, 2, 3, 4], arr2[] = [2, 4, 6, 7, 8]
<strong>Output</strong>: [2, 4]
<strong>Explanation</strong>: 2 and 4 are only common elements in both the arrays.</span></pre>
<pre><span style="font-size: 18px;"><strong>Input</strong>: arr1[] = [1, 2, 2, 3, 4], arr2[] = [2, 2, 4, 6, 7, 8]
<strong>Output</strong>: [2, 4]
<strong>Explanation</strong>: 2 and 4 are the only common elements.</span></pre>
<pre><span style="font-size: 18px;"><strong>Input</strong>: arr1[] = [1, 2], arr2[] = [3, 4]
<strong>Output</strong>: []
<strong>Explanation</strong>: No common elements.</span></pre>
<p><span style="font-size: 18px;"><strong>Expected Time Complexity:</strong> O(n + m)<br><strong>Expected Auxiliary Space:</strong> O(min(n,m))</span><br><br>&nbsp;<span style="font-size: 18px;"><strong>Constraints:</strong><br>1 &lt;= arr1.size(),arr2.size() &lt;= 10<sup>5</sup><br>1 &lt;= arr1[i], arr2[i] &lt;= 10<sup>6</sup></span></p></div>

## Solutions

#### Key Points:
```


```

---

## ✅ Problem Summary

* **Input**: Two **sorted** integer arrays `arr1[]` and `arr2[]`
* **Output**: Return a list containing the **unique** intersection of both arrays
* **No duplicates allowed** in output
* If no intersection → return an empty list

---

## ✅ Constraints

* `1 <= arr1.length, arr2.length <= 10^5`
* `1 <= arr1[i], arr2[i] <= 10^6`
* Arrays are sorted → this enables an O(n + m) solution

---

## ✅ Approach & Intuition (Two Pointers)

* Since both arrays are sorted, we can use two pointers (`i` for `arr1`, `j` for `arr2`) and traverse both arrays in a **linear scan**.
* If elements match and are **not duplicates**, add to the result.
* Skip over duplicates within the arrays using conditions like `arr1[i] == arr1[i - 1]`.

---

## ✅ Algorithm

1. Initialize two pointers `i = 0`, `j = 0` and an empty result list.
2. Loop until either pointer reaches the end of its array:

   * If `arr1[i] < arr2[j]` → move `i++`
   * If `arr1[i] > arr2[j]` → move `j++`
   * If both are equal:

     * If it's **not a duplicate** of last added element, add it to result
     * Move both `i++` and `j++`
3. Return the result list

---

## ✅ Code with Line-by-Line Explanation

```java
import java.util.*;

class Solution {
    // Function to return a list containing the intersection of two sorted arrays.
    static ArrayList<Integer> intersection(int arr1[], int arr2[]) {
        // Step 1: Initialize result list to store unique intersection elements
        ArrayList<Integer> result = new ArrayList<>();

        // Step 2: Initialize two pointers for arr1 and arr2
        int i = 0, j = 0;

        // Step 3: Traverse both arrays until one ends
        while (i < arr1.length && j < arr2.length) {

            // Case 1: arr1[i] is smaller → increment i
            if (arr1[i] < arr2[j]) {
                i++;
            }

            // Case 2: arr2[j] is smaller → increment j
            else if (arr2[j] < arr1[i]) {
                j++;
            }

            // Case 3: arr1[i] == arr2[j] → possible match
            else {
                // To avoid adding duplicates in the result
                if (result.isEmpty() || result.get(result.size() - 1) != arr1[i]) {
                    result.add(arr1[i]); // Add only if not already in result
                }

                // Move both pointers ahead
                i++;
                j++;
            }
        }

        // Step 4: Return the result list
        return result;
    }
}
```

---

## ✅ Dry Run

### Input:

```java
arr1 = [1, 2, 2, 3, 4]
arr2 = [2, 2, 4, 6, 7, 8]
```

### Steps:

| i | j | arr1\[i] | arr2\[j] | Action                                         | Result  |
| - | - | -------- | -------- | ---------------------------------------------- | ------- |
| 0 | 0 | 1        | 2        | arr1\[i] < arr2\[j] → i++                      | \[]     |
| 1 | 0 | 2        | 2        | Equal → add 2 → i++, j++                       | \[2]    |
| 2 | 1 | 2        | 2        | Equal but 2 already in result → skip, i++, j++ | \[2]    |
| 3 | 2 | 3        | 4        | arr1\[i] < arr2\[j] → i++                      | \[2]    |
| 4 | 2 | 4        | 4        | Equal → add 4 → i++, j++                       | \[2, 4] |
| 5 | 3 | -        | 6        | i out of bounds → exit                         | \[2, 4] |

✅ Output: `[2, 4]`

---

## ✅ Time and Space Complexity

### ⏱ Time Complexity: `O(n + m)`

* Each element in both arrays is visited **once**.
* Efficient for large arrays due to sorting assumption.

### 🧠 Space Complexity: `O(min(n, m))`

* The result list stores only **unique common elements**.

---

## ✅ Summary

| Feature                     | Value                          |
| --------------------------- | ------------------------------ |
| Input sorted                | ✅ Required for two-pointer     |
| Handles duplicates          | ✅ Yes                          |
| Returns unique intersection | ✅ Yes                          |
| Output order                | ✅ Sorted (since inputs sorted) |
| Time Complexity             | `O(n + m)`                     |
| Space Complexity            | `O(min(n, m))`                 |

---





























