## Square Root


https://www.geeksforgeeks.org/problems/square-root/0


<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 14pt;">Given a positive integer <strong>n,</strong> find the<strong> square root </strong>of n. If <strong>n</strong> is not a perfect square, then return the <strong>floor value</strong>.</span></p>
<p><span style="font-size: 14pt;"><strong>Floor value </strong>of any number is the greatest Integer which is less than or equal to that number</span></p>
<p><span style="font-size: 14pt;"><strong>Examples:</strong></span><span style="font-size: 14pt;"> </span></p>
<pre><span style="font-size: 14pt;"><strong>Input: </strong>n = 4
<strong>Output: </strong>2<strong>
Explanation: </strong>Since, 4 is a perfect square, so its square root is 2.<br></span></pre>
<pre><span style="font-size: 14pt;"><strong>Input: </strong>n = 11
<strong>Output: </strong>3<strong>
Explanation: </strong>Since, 11 is not a perfect square, floor of square root of 11 is 3.</span></pre>
<pre><span style="font-size: 14pt;"><strong>Input: </strong>n = 1
<strong>Output: </strong>1</span></pre>
<p><span style="font-size: 14pt;"><strong>Constraints:</strong></span><br><span style="font-size: 14pt;">1 ≤ n ≤ 3*10<sup>4</sup></span></p></div>

<div class="problems_accordion_tags__JJ2DX problems_active_tags__3RExF"><div class="active title problems_active_tag_title__cgl9e"><div class="problems_tag_container__kWANg"><strong>Expected Complexities</strong></div></div><div class="content active animated_content open"><div class="problems_expected_complexities_text__h_eyi"><div class="problems_normal_text__QiKrb">Time Complexity: O(log n)</div><div class="problems_normal_text__QiKrb">Auxiliary Space: O(1)</div></div></div><div class="ui divider g-mt-3"></div></div>

## Solutions

#### Key Points:
```


```
----

Below is a **complete, interview‑ready explanation and implementation** for computing the **floor of the square root** of a positive integer `n` using **binary search**. It includes:

* ✅ Problem restatement
* ✅ Intuition
* ✅ Step‑by‑step algorithm
* ✅ Fully commented Java code (line‑by‑line)
* ✅ Dry run examples
* ✅ Time & space complexity

---

## 1. Problem Restatement

Given a positive integer `n`, return:

* `√n` if `n` is a perfect square, else
* `⌊√n⌋` — the greatest integer ≤ `√n`.

**Constraints:** `1 ≤ n ≤ 3 * 10^4` (so `n` fits easily in `int`, and `mid*mid` will not overflow `int` in Java because `30000^2 = 900,000,000 < 2,147,483,647`).

---

## 2. Intuition

The square root of `n` lies between `1` and `n` (inclusive). Because the function `f(x) = x²` is **monotonic increasing** for non‑negative integers, we can use **binary search** on this range:

* Pick `mid`.
* If `mid² == n` → done.
* If `mid² < n` → try larger numbers (move right) and remember `mid` as a candidate answer.
* If `mid² > n` → try smaller numbers (move left).

At the end, the best recorded `mid` that did not overshoot (`mid² ≤ n`) is our floor square root.

---

## 3. Step‑by‑Step Algorithm

**Input:** integer `n` (n ≥ 1)
**Output:** floor of √n

1. If `n == 1`, return `1` immediately (quick out; optional—loop also handles it).
2. Set:

   * `low = 1`
   * `high = n` (tightening to `n/2` is fine but not required under constraints)
   * `ans = 0` (stores best floor candidate so far)
3. While `low <= high`:

   1. `mid = low + (high - low) / 2` (overflow‑safe midpoint formula)
   2. Compute `sq = mid * mid` (safe within constraints)
   3. If `sq == n` → return `mid` (perfect square)
   4. If `sq < n`:

      * `ans = mid` (mid is valid floor candidate)
      * Search right: `low = mid + 1`
   5. Else (`sq > n`):

      * Search left: `high = mid - 1`
4. Loop ends; return `ans`.

---

## 4. Fully Commented Java Code

```java
class Solution {
    int floorSqrt(int n) {
        // ----------------------------------------------------
        // Edge case: n == 0 never occurs (constraint n >= 1),
        // but we handle small n defensively: sqrt(1) = 1.
        // (The binary search also works without this shortcut.)
        // ----------------------------------------------------
        if (n == 1) return 1;

        int low = 1;     // Lowest candidate for sqrt
        int high = n;    // Highest candidate (safe; can tighten to n/2)
        int ans = 0;     // Best floor sqrt found so far

        // ----------------------------------------------------
        // Binary Search Loop: shrink [low, high] until done.
        // ----------------------------------------------------
        while (low <= high) {

            // Midpoint (overflow-safe): avoids (low + high) overflow
            int mid = low + (high - low) / 2;

            // Compute square; safe because n <= 30,000 -> mid^2 <= 900,000,000
            int sq = mid * mid;

            if (sq == n) {
                // Perfect square found: exact answer
                return mid;
            } else if (sq < n) {
                // mid^2 is still <= n -> mid is a valid floor candidate
                ans = mid;        // record it
                low = mid + 1;    // try to find a larger sqrt
            } else {
                // mid^2 > n -> need smaller numbers
                high = mid - 1;
            }
        }

        // Loop finished: no exact square; ans holds floor(sqrt(n))
        return ans;
    }
}
```

---

## 5. Line‑by‑Line Explanation

**`if (n == 1) return 1;`**
A quick shortcut; the loop also handles it, but this saves work.

**`int low = 1, high = n;`**
Search space: all possible integer roots. (You can optimize `high = n / 2`, but not required.)

**`int ans = 0;`**
Will store the **largest mid** such that `mid² ≤ n`.

**Inside loop:**

* `mid = low + (high - low) / 2;` → safe midpoint.
* `sq = mid * mid;` → square once; constraints guarantee no overflow.
* If exact → return.
* If `sq < n`, `mid` is valid; record it and move right to see if a bigger valid root exists.
* Else `sq > n`, shrink right boundary.

**After loop:**
No exact square found; `ans` is the floor (largest valid candidate recorded).

---

## 6. Dry Run Examples

### Example A: n = 4

Initial: low=1, high=4, ans=0

| low | high | mid | mid² | compare | ans | next low | next high |
| --- | ---- | --- | ---- | ------- | --- | -------- | --------- |
| 1   | 4    | 2   | 4    | == n    | —   | return 2 | —         |

**Output:** 2 ✅

---

### Example B: n = 11

Initial: low=1, high=11, ans=0

| low | high | mid | mid² | compare | ans | next low | next high |
| --- | ---- | --- | ---- | ------- | --- | -------- | --------- |
| 1   | 11   | 6   | 36   | > n     | 0   | 1        | 5         |
| 1   | 5    | 3   | 9    | < n     | 3   | 4        | 5         |
| 4   | 5    | 4   | 16   | > n     | 3   | 4        | 3         |

Loop ends (`low=4 > high=3`). Return `ans = 3`.

**Output:** 3 ✅

---

### Example C: n = 1

Shortcut triggers: return 1. ✅

---

## 7. Time & Space Complexity

| Measure   | Complexity | Explanation                                               |
| --------- | ---------- | --------------------------------------------------------- |
| **Time**  | O(log n)   | Each loop halves the search interval.                     |
| **Space** | O(1)       | Only a few local variables; no recursion or extra memory. |

For `n ≤ 30,000`, the binary search runs in at most \~15 iterations.

---

## 8. Optional Robustness Notes

Even though `mid * mid` is safe under given constraints, using a defensive pattern is good practice for larger ranges:

* Replace `int sq = mid * mid;` with `if (mid <= n / mid)` to avoid overflow in bigger problems.
* Or cast: `long sq = (long) mid * mid;`

If you'd like I can show an **overflow‑proof version** that scales to full 32‑bit inputs.

---





























