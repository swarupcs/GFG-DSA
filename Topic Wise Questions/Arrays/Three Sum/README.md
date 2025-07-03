## Three Sum


https://www.geeksforgeeks.org/problems/three-sum/1

<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 14pt;">Given an integer array <strong>arr</strong>, return all the <strong>unique </strong>triplets [arr[i], arr[j], arr[k]] such that<strong> i != j, i != k, and j != k, </strong>and <strong>arr[i] + arr[j] + arr[k] == 0.</strong></span></p>
<p><span style="font-size: 14pt;">Note: The triplets must be returned in <strong>sorted </strong>order, the solution vector should also be <strong>sorted</strong>, and the answer must not contain any <strong>duplicate </strong>triplets.</span></p>
<p><span style="font-size: 18px;"><strong>Examples:</strong></span></p>
<pre><span style="font-size: 18px;"><strong>Input: </strong>arr = [-1,0,1,2,-1,-4]
<strong>Output: </strong>[[-1,-1,2],[-1,0,1]]<strong>
Explanation: </strong>arr[0] + arr[1] + arr[2] = (-1) + 0 + 1 = 0.
arr[1] + arr[2] + arr[4] = 0 + 1 + (-1) = 0.
arr[0] + arr[3] + arr[4] = (-1) + 2 + (-1) = 0.
The distinct triplets are [-1,0,1] and [-1,-1,2].</span>
</pre>
<pre><span style="font-size: 18px;"><strong>Input: </strong>arr = [0,0,0]
<strong>Output: </strong>[[0,0,0]]<strong>
Explanation: </strong>The only possible triplet sums up to 0.</span></pre>
<p><span style="font-size: 18px;"><strong>Expected Time Complexity:</strong> O(n<sup>2</sup>)<br><strong>Expected Auxiliary Space:</strong> O(n<sup>2</sup>)</span></p>
<p><span style="font-size: 18px;"><strong>Constraints:<br></strong></span><span style="font-size: 18px;">3 &lt;= arr.length &lt;= 3000<br></span><span style="font-size: 18px;">-10<sup>5</sup> &lt;= arr[i] &lt;= 10<sup>5</sup></span></p></div>

## Solutions

#### Key Points:
```


```


---

# ✅ Problem:
Given an array `arr`, return all **unique** triplets `[arr[i], arr[j], arr[k]]` such that:
- `i != j != k`
- `arr[i] + arr[j] + arr[k] == 0`
- Triplets must be **sorted in ascending order**.
- The output list of triplets must also be **sorted** and **no duplicates** allowed.

---

# ✨ Intuition:

- **Sorting** the array first makes it easier to avoid duplicates and use a two-pointer approach.
- Fix the first element, and then use two pointers (`left`, `right`) to find the other two elements.
- Move pointers smartly based on the sum:  
  ➔ If sum is less than `0`, move `left` forward.  
  ➔ If sum is greater than `0`, move `right` backward.

This way, we find all possible triplets in **O(n²)** time without duplicates.

---

# 🛠️ Algorithm (Step-by-Step):

1. **Sort** the array.
2. Loop through each element `i`:
   - **Skip duplicate** elements (if `arr[i] == arr[i-1]` and `i > 0`).
3. For each `i`, set two pointers:
   - `j = i + 1` (start just after `i`)
   - `k = n - 1` (start from the end)
4. While `j < k`:
   - Calculate `sum = arr[i] + arr[j] + arr[k]`.
   - If `sum == 0`:
     - Add triplet `[arr[i], arr[j], arr[k]]` to result.
     - Move both pointers and **skip duplicates**.
   - If `sum < 0`:
     - Move `j` forward.
   - If `sum > 0`:
     - Move `k` backward.
5. Return the list of triplets.

---

# 📚 Dry Run Example:

### Input: `arr = [-1, 0, 1, 2, -1, -4]`

1. **Sort:** `[-4, -1, -1, 0, 1, 2]`
2. i = 0 (`-4`):
   - j=1 (`-1`), k=5 (`2`) ➔ sum = -3 ➔ move j++
   - j=2 (`-1`), k=5 (`2`) ➔ sum = -3 ➔ move j++
   - j=3 (`0`), k=5 (`2`) ➔ sum = -2 ➔ move j++
   - j=4 (`1`), k=5 (`2`) ➔ sum = -1 ➔ move j++
3. i = 1 (`-1`):
   - j=2 (`-1`), k=5 (`2`) ➔ sum = 0 ➔ **found [-1, -1, 2]**
   - move j++, k--
   - j=3 (`0`), k=4 (`1`) ➔ sum = 0 ➔ **found [-1, 0, 1]**
   - move j++, k--
4. i=2 (`-1`) ➔ skip (duplicate)
5. i=3 (`0`):
   - j=4 (`1`), k=5 (`2`) ➔ sum = 3 ➔ move k--
   - j=4, k=4 ➔ stop
6. i=4 and i=5 no valid triplet

✅ Final Triplets: `[[-1, -1, 2], [-1, 0, 1]]`

---

# ✍️ Code with Full Step-by-Step Comments:

```java
import java.util.*;

class Solution {
    public static ArrayList<ArrayList<Integer>> triplets(int[] arr) {
        // List to store the final triplets
        ArrayList<ArrayList<Integer>> ans = new ArrayList<>();
        
        // Get the number of elements
        int n = arr.length;
        
        // Step 1: Sort the array to easily use two pointers and handle duplicates
        Arrays.sort(arr);
        
        // Step 2: Traverse each element to fix the first number of triplet
        for (int i = 0; i < n; i++) {
            
            // Step 2.1: Skip duplicate elements to avoid duplicate triplets
            if (i > 0 && arr[i] == arr[i - 1]) continue;
            
            // Step 3: Initialize two pointers
            int j = i + 1;      // Left pointer
            int k = n - 1;      // Right pointer
            
            // Step 4: While left pointer is less than right pointer
            while (j < k) {
                // Step 4.1: Calculate sum of the three elements
                int sum = arr[i] + arr[j] + arr[k];
                
                if (sum < 0) {
                    // Step 4.2: If sum is less, move left pointer to right to increase sum
                    j++;
                } else if (sum > 0) {
                    // Step 4.3: If sum is more, move right pointer to left to decrease sum
                    k--;
                } else {
                    // Step 4.4: Sum is exactly zero, valid triplet found
                    ArrayList<Integer> temp = new ArrayList<>();
                    temp.add(arr[i]);
                    temp.add(arr[j]);
                    temp.add(arr[k]);
                    
                    // Add the triplet to the answer
                    ans.add(temp);
                    
                    // Step 5: Move both pointers and skip duplicates
                    j++;
                    k--;
                    
                    // Skip duplicate elements at left pointer
                    while (j < k && arr[j] == arr[j - 1]) j++;
                    
                    // Skip duplicate elements at right pointer
                    while (j < k && arr[k] == arr[k + 1]) k--;
                }
            }
        }
        
        // Step 6: Return the list of triplets
        return ans;
    }
}
```

---

# 🔥 Output Examples:

| Input              | Output                        |
|--------------------|-------------------------------|
| `[-1,0,1,2,-1,-4]` | `[[-1,-1,2], [-1,0,1]]`         |
| `[0,0,0]`          | `[[0,0,0]]`                    |
| `[1,2,3]`          | `[]`                           |
| `[-2,0,1,1,2]`     | `[[-2,0,2], [-2,1,1]]`          |

---

# ⚡ Final Notes:
- **Time Complexity:** `O(n²)`  
  - Outer loop `O(n)` and inner two-pointer loop `O(n)` combined ➔ `O(n²)`.
- **Space Complexity:** `O(n²)` (to store all triplets).

---


Let’s do a **visual dry run** using **pointer movement diagram** for this input:

---

## 🧩 Input:
```
arr = [-1, 0, 1, 2, -1, -4]
```

### Step 1: Sort the array
```
arr = [-4, -1, -1, 0, 1, 2]
```

---

## 🚀 Dry Run with Visual Pointers:

We'll fix `i`, and use two pointers `j` (left) and `k` (right).

---

### 🔵 i = 0 → arr[i] = -4

| i | j  | k  | arr[i] | arr[j] | arr[k] | sum  | Action                  |
|---|----|----|--------|--------|--------|------|-------------------------|
| 0 | 1  | 5  | -4     | -1     | 2      | -3   | sum < 0 ➔ j++            |
| 0 | 2  | 5  | -4     | -1     | 2      | -3   | sum < 0 ➔ j++            |
| 0 | 3  | 5  | -4     | 0      | 2      | -2   | sum < 0 ➔ j++            |
| 0 | 4  | 5  | -4     | 1      | 2      | -1   | sum < 0 ➔ j++            |
| 0 | 5  | 5  |        |        |        |      | j == k (stop inner loop) |

👉 No triplet found for `i=0`

---

### 🔵 i = 1 → arr[i] = -1

| i | j  | k  | arr[i] | arr[j] | arr[k] | sum  | Action                  |
|---|----|----|--------|--------|--------|------|-------------------------|
| 1 | 2  | 5  | -1     | -1     | 2      | 0    | ✅ Found triplet [-1,-1,2] |
| 1 | 3  | 4  | -1     | 0      | 1      | 0    | ✅ Found triplet [-1,0,1]  |
| 1 | 4  | 3  |        |        |        |      | j > k (stop inner loop)   |

👉 Found two triplets:  
`[-1, -1, 2]` and `[-1, 0, 1]`

---

### 🔵 i = 2 → arr[i] = -1

- Skip this `i` because `arr[i] == arr[i-1]` (duplicate)

---

### 🔵 i = 3 → arr[i] = 0

| i | j  | k  | arr[i] | arr[j] | arr[k] | sum  | Action                  |
|---|----|----|--------|--------|--------|------|-------------------------|
| 3 | 4  | 5  | 0      | 1      | 2      | 3    | sum > 0 ➔ k--            |
| 3 | 4  | 4  |        |        |        |      | j == k (stop inner loop) |

👉 No triplet found for `i=3`

---

### 🔵 i = 4 → arr[i] = 1
- Only 2 elements left ➔ Not enough for a triplet ➔ Skip

### 🔵 i = 5 → arr[i] = 2
- Only 1 element left ➔ Not enough for a triplet ➔ Skip

---

# ✨ Final Triplets:
```
[[-1, -1, 2], [-1, 0, 1]]
```

---

# 📈 Summary Diagram (Flow)

```
Fix i
 |
Sort the array
 |
For each i -> two pointers (j, k)
 |
Move j and k based on sum
 |
Avoid duplicates
 |
Collect triplets
```

---

# ⚡ Visualization Animation Idea (if we animated):

- Pointers j ➡️ and k ⬅️ move towards each other.
- When sum == 0 ➔ 🎯 Lock a triplet and move both.
- If sum < 0 ➔ move j ➡️
- If sum > 0 ➔ move k ⬅️

---


---

# 📽️ GIF-like Example for:  
Input → `arr = [-1, 0, 1, 2, -1, -4]`

---

## 🎬 **Frame 1: Sorting**
```
Sorted array:
[-4, -1, -1, 0, 1, 2]
```

---

## 🎬 **Frame 2: i = 0 (arr[i] = -4)**

Pointers:
```
 i   j               k
[-4, -1, -1, 0, 1, 2]

sum = -4 + (-1) + 2 = -3
```
Action:  
**sum < 0 ➔ Move j to right**

---

## 🎬 **Frame 3: i = 0, j = 2, k = 5**

Pointers:
```
 i       j           k
[-4, -1, -1, 0, 1, 2]

sum = -4 + (-1) + 2 = -3
```
Action:  
**sum < 0 ➔ Move j to right**

---

## 🎬 **Frame 4: i = 0, j = 3, k = 5**

Pointers:
```
 i           j       k
[-4, -1, -1, 0, 1, 2]

sum = -4 + 0 + 2 = -2
```
Action:  
**sum < 0 ➔ Move j to right**

---

## 🎬 **Frame 5: i = 0, j = 4, k = 5**

Pointers:
```
 i             j     k
[-4, -1, -1, 0, 1, 2]

sum = -4 + 1 + 2 = -1
```
Action:  
**sum < 0 ➔ Move j to right**

---

## 🎬 **Frame 6: j == k (loop ends for i=0)**

---

## 🎬 **Frame 7: i = 1 (arr[i] = -1)**

Pointers:
```
     i   j         k
[-4, -1, -1, 0, 1, 2]

sum = -1 + (-1) + 2 = 0 ✅
```
Action:  
🎯 **Triplet found** → `[-1, -1, 2]`

Move **j++ and k--**

---

## 🎬 **Frame 8: i = 1, j = 3, k = 4**

Pointers:
```
     i       j     k
[-4, -1, -1, 0, 1, 2]

sum = -1 + 0 + 1 = 0 ✅
```
Action:  
🎯 **Triplet found** → `[-1, 0, 1]`

Move **j++ and k--**

---

## 🎬 **Frame 9: j >= k (loop ends for i=1)**

---

## 🎬 **Frame 10: i = 2 (arr[i] = -1)**

Duplicate of previous `-1`, so **skip** to next.

---

## 🎬 **Frame 11: i = 3 (arr[i] = 0)**

Pointers:
```
         i   j   k
[-4, -1, -1, 0, 1, 2]

sum = 0 + 1 + 2 = 3
```
Action:  
**sum > 0 ➔ Move k to left**

---

## 🎬 **Frame 12: j == k (loop ends for i=3)**

---

# ✨ Final Result:
```
[[-1, -1, 2], [-1, 0, 1]]
```

---

# 🎥 Visual Flow Summary:
```
Start with sorted array ➔ Fix i ➔ move j ➡️ and k ⬅️
Whenever sum == 0 ➔ 🎯 Save triplet
Skip duplicates
Done!
```

---




























