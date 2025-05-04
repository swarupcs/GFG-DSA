## Alternate Positive Negative


https://www.geeksforgeeks.org/problems/array-of-alternate-ve-and-ve-nos1401/1

<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 18px;">Given an unsorted array <strong>arr </strong>containing<strong> </strong>both<strong> </strong><strong>positive</strong> and <strong>negative</strong> numbers. Your task is to rearrange the array and convert it into an array of alternate positive and negative numbers without changing the relative order.<br><br></span><span style="font-size: 18px;"><strong>Note: <br></strong></span><span style="font-size: 18px;">- Resulting array <strong>should start</strong> with a positive integer (0 will also be considered as a positive integer). <br></span><span style="font-size: 18px;">- If any of the positive or negative integers are exhausted, then add the remaining integers in the answer as it is by maintaining the relative order.<br>- The array <strong>may</strong> or <strong>may not</strong> have the <strong>equal</strong> number of positive and negative integers.</span></p>
<p><span style="font-size: 18px;"><strong>Examples:</strong></span></p>
<pre><span style="font-size: 18px;"><strong>Input: </strong>arr[] = [9, 4, -2, -1, 5, 0, -5, -3, 2]
<strong>Output: </strong>[9, -2, 4, -1, 5, -5, 0, -3, 2]
<strong>Explanation: </strong>The positive numbers are [9, 4, 5, 0, 2] and the negative integers are [-2, -1, -5, -3]. Since, we need to start with the positive integer first and then negative integer and so on (by maintaining the relative order as well), hence we will take 9 from the positive set of elements and then -2 after that 4 and then -1 and so on.
</span></pre>
<pre><span style="font-size: 18px;"><strong>Input: </strong>arr[] = [-5, -2, 5, 2, 4, 7, 1, 8, 0, -8]
<strong>Output: </strong>[5, -5, 2, -2, 4, -8, 7, 1, 8, 0]
<strong>Explanation : </strong>The positive numbers are [5, 2, 4, 7, 1, 8, 0] and the negative integers are [-5,-2,-8]. According to the given conditions we will start from the positive integer 5 and then -5 and so on. After reaching -8 there are no negative elements left, so according to the given rule, we will add the remaining elements (in this case positive elements are remaining) as it in by maintaining the relative order.</span></pre>
<pre><span style="font-size: 18px;"><strong>Input: </strong>arr[] = [9, 5, -2, -1, 5, 0, -5, -3, 2]
<strong>Output: </strong>[9, -2, 5, -1, 5, -5, 0, -3, 2]
<strong>Explanation: </strong>The positive numbers are [9, 5, 5, 0, 2] and the negative integers are [-2, -1, -5, -3]. Since, we need to start with the positive integer first and then negative integer and so on (by maintaining the relative order as well), hence we will take 9 from the positive set of elements and then -2 after that 5 and then -1 and so on.</span></pre>
<p><span style="font-size: 18px;"><strong>Constraints:</strong><br>1 ≤ arr.size() ≤ 10<sup>6</sup><br>-10<sup>6</sup> ≤ arr[i] ≤ 10<sup>6</sup></span></p></div>


---

### ✅ **Problem Summary**
Rearrange the array into alternate positive and negative numbers:
- Must **start with a positive** number (0 is also considered positive).
- Maintain **relative order** of both positives and negatives.
- If one of the types (positive/negative) gets exhausted, append the remaining elements as they are.

---

### ✅ **Approach / Intuition**
1. Separate the array into two lists:
   - `positives`: to store positive numbers and 0.
   - `negatives`: to store negative numbers.
2. Iterate and alternately add one from each list to the original array.
   - Start with a **positive number**.
3. After exhausting one list, append the remaining elements from the other.

---

### ✅ **Algorithm**
1. Create two lists: `positives` and `negatives`.
2. Loop through the array:
   - Add positive numbers (≥ 0) to `positives`.
   - Add negative numbers to `negatives`.
3. Use two pointers to merge the two lists back into the original array in alternating order.
   - If any list is longer, add its remaining elements.

---

### ✅ **Dry Run**
Input: `[9, 4, -2, -1, 5, 0, -5, -3, 2]`  
Positives: `[9, 4, 5, 0, 2]`  
Negatives: `[-2, -1, -5, -3]`  
Merged: `[9, -2, 4, -1, 5, -5, 0, -3, 2]`

---

### ✅ **Java Code with Comments**

```java
class Solution {
    void rearrange(ArrayList<Integer> arr) {
        // Step 1: Create two lists to store positives and negatives
        ArrayList<Integer> pos = new ArrayList<>();
        ArrayList<Integer> neg = new ArrayList<>();

        // Step 2: Traverse the array and separate positives and negatives
        for (int num : arr) {
            if (num >= 0) {
                pos.add(num);  // 0 is considered positive
            } else {
                neg.add(num);
            }
        }

        // Step 3: Clear the original array to rebuild it in required format
        arr.clear();

        // Step 4: Use pointers to merge positives and negatives alternately
        int i = 0, j = 0;

        // Step 5: Start with positive and alternate
        while (i < pos.size() && j < neg.size()) {
            arr.add(pos.get(i++));  // Add positive
            arr.add(neg.get(j++));  // Add negative
        }

        // Step 6: Add remaining positive elements, if any
        while (i < pos.size()) {
            arr.add(pos.get(i++));
        }

        // Step 7: Add remaining negative elements, if any
        while (j < neg.size()) {
            arr.add(neg.get(j++));
        }
    }
}
```

---

### ⏱️ **Time Complexity:**  
- O(N), where N = size of array (single pass for separation + single pass for reconstruction).

### 🧠 **Space Complexity:**  
- O(N), due to storing elements in separate positive and negative lists.

---





























