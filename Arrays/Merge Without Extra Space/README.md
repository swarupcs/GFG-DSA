## Merge Without Extra Space


https://www.geeksforgeeks.org/problems/merge-two-sorted-arrays-1587115620/1

<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 18px;">Given two sorted arrays <strong>a[]</strong> and <strong>b[] </strong>of size <strong>n </strong>and <strong>m </strong>respectively, the task is to merge them in sorted order without using any <strong>extra space</strong>. Modify <strong>a[]</strong> so that it contains the first <strong>n</strong> elements and modify <strong>b[]</strong> so that it contains the last <strong>m</strong> elements.</span></p>
<p><span style="font-size: 18px;"><strong>Examples:</strong></span></p>
<pre><span style="font-size: 18px;"><strong>Input</strong>: a[] = [2, 4, 7, 10], b[] = [2, 3]
<strong>Output</strong>:<br>2 2 3 4<br>7 10
<strong>Explanation</strong>: After merging the two non-decreasing arrays, we get, 2 2 3 4 7 10</span></pre>
<pre><span style="font-size: 18px;"><strong>Input</strong>: a[] = [1, 5, 9, 10, 15, 20], b[] = [2, 3, 8, 13]
<strong>Output</strong>:<br>1 2 3 5 8 9<br>10 13 15 20
<strong>Explanation</strong>: After merging two sorted arrays we get 1 2 3 5 8 9 10 13 15 20.</span>
</pre>
<pre><span style="font-size: 18px;"><strong>Input</strong>: a[] = [0, 1], b[] = [2, 3]
<strong>Output</strong>:<br>0 1<br>2 3
<strong>Explanation</strong>: After merging two sorted arrays we get 0 1 2 3.</span></pre>
<p><span style="font-size: 18px;"><strong>Constraints:</strong></span><br><span style="font-size: 18px;">1 &lt;= a.size(), b.size() &lt;= 10<sup>5</sup><br>0 &lt;= a[i], b[i]&nbsp;&lt;= 10<sup>7</sup></span></p></div>

## Solutions

#### Key Points:
```


```

To solve this problem **without using extra space**, we can use the **Gap Algorithm**, inspired by the Shell Sort technique.

---

## ✅ Approach: Gap Method

### 🔥 Intuition:
Treat both arrays `a[]` and `b[]` as one virtual array. Start with a **gap** value and compare elements that are `gap` apart, swapping them if they are out of order. Keep reducing the gap until it becomes 0.

---

## 🧠 Algorithm Steps:

1. Calculate initial `gap = ceil((n + m) / 2)`.
2. Compare and swap elements `i` and `i + gap` if out of order.
   - If both in `a[]`, compare `a[i]` and `a[i + gap]`.
   - If `i` in `a[]` and `i + gap` in `b[]`, compare `a[i]` and `b[j]`.
   - If both in `b[]`, compare `b[i]` and `b[i + gap]`.
3. Reduce the gap using:  
   ```java
   gap = (gap <= 1) ? 0 : (gap + 1) / 2;
   ```
4. Repeat until gap is 0.

---

## ✅ Complete Java Code with Comments

```java
class Solution {
    // Function to merge arrays a and b using Gap method
    public void mergeArrays(int[] a, int[] b) {
        int n = a.length;
        int m = b.length;
        int gap = nextGap(n + m); // Step 1: Initialize the gap

        // Step 2: Keep reducing the gap and compare elements
        while (gap > 0) {
            int i = 0, j = gap;

            while (j < n + m) {
                // Step 3: Determine the values at i and j
                int val1 = getValue(a, b, i, n);
                int val2 = getValue(a, b, j, n);

                // Step 4: Swap if needed
                if (val1 > val2) {
                    setValue(a, b, i, val2, n);
                    setValue(a, b, j, val1, n);
                }

                i++;
                j++;
            }

            // Step 5: Reduce the gap
            gap = nextGap(gap);
        }
    }

    // Helper: Get element from virtual array
    private int getValue(int[] a, int[] b, int index, int n) {
        return index < n ? a[index] : b[index - n];
    }

    // Helper: Set element in virtual array
    private void setValue(int[] a, int[] b, int index, int value, int n) {
        if (index < n) a[index] = value;
        else b[index - n] = value;
    }

    // Helper: Calculate next gap
    private int nextGap(int gap) {
        if (gap <= 1) return 0;
        return (gap + 1) / 2;
    }
}
```

---

## 🔍 Example Dry Run

### Input:
```java
a = [1, 5, 9, 10, 15, 20]
b = [2, 3, 8, 13]
```

### Output:
```
a = [1, 2, 3, 5, 8, 9]
b = [10, 13, 15, 20]
```

---



























