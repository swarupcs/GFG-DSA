## Majority Element II


https://www.geeksforgeeks.org/problems/majority-vote/1


```
You are given an array of integer arr[] where each number represents a vote to a candidate. Return the candidates that have votes greater than one-third of the total votes, If there's not a majority vote, return an empty array. 

Note: The answer should be returned in an increasing format.
```


#### Example 1:

```
Input: arr[] = [2, 1, 5, 5, 5, 5, 6, 6, 6, 6, 6]
Output: [5, 6]
Explanation: 5 and 6 occur more n/3 times.

```

#### Example 2:
```
Input: arr[] = [1, 2, 3, 4, 5]
Output: []
Explanation: o candidate occur more than n/3 times.
```


#### Expected Time Complexity: ```O(m * n)```
#### Expected Auxiliary Space: ```O(m * n)```

#### Constraints:
```
1 <= arr.size() <= 10^6
-10^9 <= arr[i] <= 10^9
```

## Solutions

#### Key Points:
```


```

* **Java**

```java
import java.util.*;

class Solution {
    public List<Integer> findMajority(int[] nums) {
        int n = nums.length;

        // Step 1: Initialize two potential candidates and their respective counts
        int count1 = 0, count2 = 0;
        int element1 = Integer.MIN_VALUE, element2 = Integer.MIN_VALUE;

        // Step 2: First Pass - Find two potential majority candidates using the Boyer-Moore algorithm
        for (int num : nums) {
            if (count1 == 0 && num != element2) {
                count1 = 1;
                element1 = num;  // Assign a new candidate
            } else if (count2 == 0 && num != element1) {
                count2 = 1;
                element2 = num;  // Assign a new candidate
            } else if (num == element1) {
                count1++;  // Increment count of first candidate
            } else if (num == element2) {
                count2++;  // Increment count of second candidate
            } else {
                count1--;  // Decrement both counts (neutralizing effect)
                count2--;
            }
        }

        // Step 3: Reset counts for validation
        count1 = 0;
        count2 = 0;

        // Count actual occurrences of element1 and element2 in the array
        for (int num : nums) {
            if (num == element1) count1++;
            if (num == element2) count2++;
        }

        // Step 4: Check if candidates appear more than ⌊n/3⌋ times
        int minimumCount = n / 3 + 1;
        List<Integer> result = new ArrayList<>();

        if (count1 >= minimumCount) result.add(element1);
        if (count2 >= minimumCount && element1 != element2) result.add(element2);

        // Step 5: Ensure result is sorted in increasing order
        Collections.sort(result);

        return result;
    }
}
```


## **Approach & Intuition**
This problem is a variation of the **Boyer-Moore Majority Vote Algorithm**, which efficiently finds elements appearing more than **⌊n/3⌋** times in an array. Unlike the classic majority element problem (**⌊n/2⌋**), we must track two potential majority elements because at most two elements can appear more than **n/3** times.

### **Key Observations:**
1. A number appearing more than **n/3** times can be at most **2** numbers.
2. We **first find two potential candidates** using a variation of **Boyer-Moore Voting Algorithm**.
3. We **validate the candidates** by counting their occurrences.
4. We **return the candidates sorted in ascending order** to meet the problem’s constraints.

---

## **Algorithm**
1. **Initialize** two potential candidates (`element1`, `element2`) and their respective counters (`count1`, `count2`).
2. **First Pass (Finding Candidates)**
   - Traverse the array, updating `element1` and `element2` based on the Boyer-Moore voting principle.
   - If `count1` or `count2` drops to `0`, assign the current element as a new candidate.
3. **Second Pass (Validating Candidates)**
   - Count the occurrences of `element1` and `element2` to confirm they appear more than **⌊n/3⌋** times.
4. **Sort and return the result**.



---

## **Example and Dry Run**
### **Input**
```plaintext
nums = [2, 1, 6, 6, 6, 6, 6, 5, 5, 5, 5]
```

### **Step 1: Finding Candidates**
| Index | Num | `element1` | `count1` | `element2` | `count2` | Action |
|--------|----|------------|----------|------------|----------|---------|
| 0  | 2  | 2  | 1  | -∞ | 0 | `element1 = 2` |
| 1  | 1  | 2  | 1  | 1  | 1 | `element2 = 1` |
| 2  | 6  | 2  | 0  | 1  | 0 | Reset both counts |
| 3  | 6  | 6  | 1  | 1  | 0 | `element1 = 6` |
| 4  | 6  | 6  | 2  | 1  | 0 | `count1++` |
| 5  | 6  | 6  | 3  | 1  | 0 | `count1++` |
| 6  | 6  | 6  | 4  | 1  | 0 | `count1++` |
| 7  | 6  | 6  | 5  | 1  | 0 | `count1++` |
| 8  | 5  | 6  | 4  | 5  | 1 | `element2 = 5` |
| 9  | 5  | 6  | 3  | 5  | 2 | `count2++` |
| 10 | 5  | 6  | 2  | 5  | 3 | `count2++` |

After first pass: **Candidates: `element1 = 6`, `element2 = 5`**

---

### **Step 2: Validating Candidates**
| Element | Count |
|---------|-------|
| 6 | 5 |
| 5 | 4 |

Since both `5` and `6` appear more than **n/3** times, we return `[5, 6]`.

### **Final Output**
```plaintext
[5, 6]
```

---

## **Time & Space Complexity Analysis**
- **First Pass (Finding candidates):** **O(n)**
- **Second Pass (Counting occurrences):** **O(n)**
- **Sorting the result:** **O(2 log 2) ≈ O(1)**
- **Overall Time Complexity:** **O(n)**
- **Space Complexity:** **O(1)** (Only a constant amount of extra space is used)

---

### **Key Takeaways**
✔ **Uses Boyer-Moore Majority Vote Algorithm** to reduce time complexity.  
✔ **Efficient, O(n) complexity**, handles large arrays (`10^6`).  
✔ **Ensures output is sorted** using `Collections.sort(result)`.  
✔ **Handles edge cases**, like no majority elements.  

























