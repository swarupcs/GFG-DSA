## Largest Element in Array


https://www.geeksforgeeks.org/problems/largest-element-in-array4009/1

```
Given an array arr[]. The task is to find the largest element and return it.
```


#### Example 1:

```
Input: arr[] = [1, 8, 7, 56, 90]
Output: 90
Explanation: The largest element of the given array is 90.

```

#### Example 2:
```
Input: arr[] = [5, 5, 5, 5]
Output: 5
Explanation: The largest element of the given array is 5.
```

#### Example 3:
```
Input: arr[] = [10]
Output: 10
Explanation: There is only one element which is the largest.
```



#### Constraints:
```
1 <= arr.size()<= 106
0 <= arr[i] <= 106
```

## Solutions

#### Key Points:
```


```

* **Java**

```java
class Solution {
    public static int largest(int[] arr) {
        // Step 1: Initialize max with the first element of the array
        int max = arr[0];

        // Step 2: Iterate through the array
        for(int i = 0; i < arr.length; i++) {
            // Step 3: If current element is greater than max, update max
            if(arr[i] > max) {
                max = arr[i];
            }
        }

        // Step 4: Return the largest element found
        return max;
    }
}


```



---

## **🔍 Approach & Intuition**
1. **Understanding the Problem**  
   - We are given an array of integers.
   - We need to find the **largest element** in the array and return it.
   
2. **Brute Force Approach (Sorting)**
   - Sort the array in **descending order** and return the first element.
   - **Time Complexity**: \(O(n \log n)\) (Not optimal)

3. **Optimal Approach (Linear Scan)**
   - Traverse the array once and keep track of the maximum element encountered so far.
   - **Time Complexity**: \(O(n)\) (Efficient)
   - **Space Complexity**: \(O(1)\) (Only one variable `max` is used)

---

## **📜 Algorithm**
1. **Initialize a variable** `max` with the first element of the array.
2. **Iterate through the array** from the first element to the last.
   - If the current element is **greater** than `max`, update `max`.
3. **After the loop**, return the `max` value as the largest element.

---

## **💻 Code with Line-by-Line Explanation**
```java
class Solution {
    public static int largest(int[] arr) {
        // Step 1: Initialize max with the first element of the array
        int max = arr[0];

        // Step 2: Iterate through the array
        for(int i = 0; i < arr.length; i++) {
            // Step 3: If current element is greater than max, update max
            if(arr[i] > max) {
                max = arr[i];
            }
        }

        // Step 4: Return the largest element found
        return max;
    }
}
```

---

## **🔄 Dry Run**
Let’s take **Example 1**:  
```java
arr[] = [1, 8, 7, 56, 90]
```

| Iteration | `i` | `arr[i]` | `max` before check | Condition (`arr[i] > max`) | `max` after update |
|-----------|----|----------|---------------------|---------------------------|--------------------|
| 1st       | 0  | 1        | 1                   | No                        | 1                  |
| 2nd       | 1  | 8        | 1                   | Yes                       | 8                  |
| 3rd       | 2  | 7        | 8                   | No                        | 8                  |
| 4th       | 3  | 56       | 8                   | Yes                       | 56                 |
| 5th       | 4  | 90       | 56                  | Yes                       | 90                 |

**Final Output:** `90`

---

## **📌 Time & Space Complexity Analysis**
- **Time Complexity**: \(O(n)\) (We iterate through the array once)
- **Space Complexity**: \(O(1)\) (Uses a single variable `max`)

---

## **🔍 Key Takeaways**
✅ **Efficient solution:** Only one scan through the array.  
✅ **Handles all cases:** Works for arrays with unique, duplicate, or single elements.  
✅ **Easy to understand:** Simple condition-based update of the maximum value.  

---




























