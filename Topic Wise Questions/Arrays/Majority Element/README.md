## Majority Element


https://www.geeksforgeeks.org/problems/majority-element-1587115620/1


<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 14pt;">Given an array <strong>arr[]</strong>. Find the <strong>majority element</strong> in the array. If no majority element exists, return <strong>-1</strong>.</span></p>
<p><span style="font-size: 14pt;"><strong>Note:</strong> A majority element in an array is an element that appears <strong>strictly </strong>more than<strong> arr.size()/2 </strong>times in the array.</span></p>
<p><span style="font-size: 14pt;"><strong>Examples:</strong></span></p>
<pre><span style="font-size: 14pt;"><strong>Input: </strong>arr[] = [1, 1, 2, 1, 3, 5, 1]
<strong>Output: </strong>1<strong>
Explanation: </strong>Since, 1 is present more than 7/2 times, so it is the majority element.<br></span></pre>
<pre><span style="font-size: 14pt;"><strong>Input: </strong>arr[] = [7]
<strong>Output: </strong>7<strong>
Explanation: </strong>Since, 7 is single element and present more than 1/2 times, so it is the majority element.</span></pre>
<pre><span style="font-size: 14pt;"><strong>Input: </strong>arr[] = [2, 13]
<strong>Output: </strong>-1<strong>
Explanation: </strong>Since, no element is present more than 2/2 times, so there is no majority element.</span></pre>
<p><span style="font-size: 14pt;"><strong>Constraints:</strong><br>1 ≤ arr.size() ≤ 10<sup>5</sup><br>1 ≤ arr[i] ≤ 10<sup>5</sup></span></p></div>

## Solutions

#### Key Points:
```


```


✅ Approach & Intuition

🧠 Step-by-step algorithm

💡 Code with line-by-line explanation

🧪 Example dry run

⏱ Time & space complexity

---

### ✅ Problem Summary

You are given an array `arr[]`.
You need to return the element that appears **strictly more than ⌊n / 2⌋ times**.
If no such element exists, return `-1`.

---

### ✅ Intuition

This is a classic use case for the **Boyer-Moore Voting Algorithm**, which:

* Finds a **potential candidate** for the majority element in one pass.
* Verifies whether it is truly the majority in a second pass.

---

### 🧠 Algorithm Steps

1. Initialize `count = 0`, `candidate = -1`.
2. Traverse array:

   * If `count == 0`, set current element as candidate.
   * If current element equals candidate → increase count.
   * Else → decrease count.
3. After first pass, count how many times candidate appears.
4. If count > n/2 → return candidate.
5. Else → return -1.

---

### ✅ Java Code (with Comments)

```java
class Solution {
    int majorityElement(int arr[]) {
        int n = arr.length;         // Get size of array
        int count = 0;              // Vote count
        int candidate = -1;         // Possible majority candidate

        // Step 1: Find a potential candidate using Boyer-Moore Voting Algorithm
        for (int i = 0; i < n; i++) {
            if (count == 0) {
                // If count drops to 0, pick a new candidate
                candidate = arr[i];
                count = 1;
            } else if (arr[i] == candidate) {
                // If current element matches candidate, increment count
                count++;
            } else {
                // Otherwise, decrement count
                count--;
            }
        }

        // Step 2: Verify if candidate is truly majority
        int occurrence = 0;
        for (int i = 0; i < n; i++) {
            if (arr[i] == candidate) {
                occurrence++;
            }
        }

        // Step 3: Check if candidate occurs more than n/2 times
        if (occurrence > n / 2) {
            return candidate;
        }

        // No majority element found
        return -1;
    }
}
```

---

### 🧪 Dry Run Example

#### Input:

`arr = [1, 1, 2, 1, 3, 5, 1]`

* n = 7 → ⌊n/2⌋ = 3

**Pass 1 (find candidate)**

| i | arr\[i] | count | candidate | Action               |
| - | ------- | ----- | --------- | -------------------- |
| 0 | 1       | 0     | -         | candidate=1, count=1 |
| 1 | 1       | 1     | 1         | count++ → 2          |
| 2 | 2       | 2     | 1         | count-- → 1          |
| 3 | 1       | 1     | 1         | count++ → 2          |
| 4 | 3       | 2     | 1         | count-- → 1          |
| 5 | 5       | 1     | 1         | count-- → 0          |
| 6 | 1       | 0     | -         | candidate=1, count=1 |

Candidate = 1

**Pass 2 (count occurrences of 1):**
Count = 4 → ✅ 4 > 3 → return `1`

---

### ⏱ Time & Space Complexity

| Complexity | Value  | Explanation              |
| ---------- | ------ | ------------------------ |
| Time       | `O(n)` | Two passes through array |
| Space      | `O(1)` | No extra space used      |

---

### ✅ Summary

* The Boyer-Moore Voting Algorithm is optimal for this problem.
* It ensures **O(n)** time and **O(1)** space, with guaranteed correctness via verification step.






























