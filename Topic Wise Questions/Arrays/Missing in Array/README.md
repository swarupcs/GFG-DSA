## Missing in Array


https://www.geeksforgeeks.org/problems/missing-number-in-array1416/1


<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 14pt;">You are given an array <strong>arr[]</strong> of size <strong>n - 1</strong> that contains<strong> distinct integers </strong>in the range from 1 to n (inclusive). This array represents a permutation of the integers from 1 to n with <strong>one element missing</strong>. Your task is to identify and return the <strong>missing element</strong>.</span></p>
<p><span style="font-size: 14pt;"><strong>Examples:</strong></span></p>
<pre><span style="font-size: 14pt;"><strong>Input: </strong>arr[] = [1, 2, 3, 5]
<strong>Output: </strong>4
<strong>Explanation: </strong>All the numbers from 1 to 5 are present except 4.<br></span></pre>
<pre><span style="font-size: 14pt;"><strong>Input: </strong>arr[] = [8, 2, 4, 5, 3, 7, 1]
<strong>Output:</strong> 6
<strong>Explanation: </strong>All the numbers from 1 to 8 are present except 6.</span></pre>
<pre><span style="font-size: 14pt;"><strong>Input: </strong>arr[] = [1]
<strong>Output: </strong>2
<strong>Explanation: </strong>Only 1 is present so the missing element is 2.<br></span></pre>
<p><span style="font-size: 14pt;"><strong>Constraints:</strong><br>1 ≤ arr.size() ≤ 10<sup>6</sup><br>1 ≤ arr[i] ≤ arr.size() + 1</span></p></div>

## Solutions

#### Key Points:
```


```



---

### ✅ **Approach: XOR Method**

#### **Intuition**:

* XOR of a number with itself is `0` → `a ^ a = 0`
* XOR of a number with 0 is the number itself → `a ^ 0 = a`
* XOR is **commutative and associative**, so the order doesn't matter.

If we XOR all the numbers from `1` to `n` with all elements in the array, the numbers that appear in both will cancel out, and only the missing number will remain.

---

### ✅ **Algorithm (Step-by-step)**:

1. Initialize two variables:

   * `xor1` = XOR of all numbers from `1` to `n`
   * `xor2` = XOR of all elements in the array
2. Final result = `xor1 ^ xor2`

---

### ✅ Dry Run Example:

Input: `arr = [1, 2, 4, 5]`
`n = 5` (since size is 4)

* `xor1 = 1 ^ 2 ^ 3 ^ 4 ^ 5 = 1 ^ 2 ^ 3 ^ 4 ^ 5 = 1`
* `xor2 = 1 ^ 2 ^ 4 ^ 5`
* Result = `xor1 ^ xor2 = (1 ^ 2 ^ 3 ^ 4 ^ 5) ^ (1 ^ 2 ^ 4 ^ 5) = 3`

✅ Output: `3`

---

### ✅ **Code with Line-by-Line Explanation**:

```java
class Solution {
    // Function to find the missing number using XOR method
    int missingNum(int arr[]) {
        int n = arr.length + 1; // Total numbers should be n

        int xor1 = 0; // XOR of all numbers from 1 to n
        int xor2 = 0; // XOR of all elements in the array

        // Step 1: XOR all numbers from 1 to n
        for (int i = 1; i <= n; i++) {
            xor1 ^= i; // xor1 = xor1 ^ i
        }

        // Step 2: XOR all elements in the array
        for (int num : arr) {
            xor2 ^= num; // xor2 = xor2 ^ num
        }

        // Step 3: The missing number is xor1 ^ xor2
        return xor1 ^ xor2;
    }
}
```

---

### ✅ Time & Space Complexity:

| Metric           | Value  |
| ---------------- | ------ |
| Time Complexity  | `O(n)` |
| Space Complexity | `O(1)` |

---

### ✅ When to Prefer XOR over Sum Method?

Use XOR when:

* There is **risk of integer overflow** with sum formula (very large `n`)
* You want **bitwise tricks** (sometimes asked in interviews for optimization)






























