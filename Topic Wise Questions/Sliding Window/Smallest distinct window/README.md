## Smallest distinct window


https://www.geeksforgeeks.org/problems/smallest-distant-window3132/1
<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 14pt;">Given a string&nbsp;<strong>str,</strong>&nbsp;your task is to find the&nbsp;<strong>length</strong>&nbsp;of the&nbsp;<strong>smallest&nbsp;</strong>window that contains<strong>&nbsp;all&nbsp;</strong>the characters of the given string at least once.</span></p>
<p><span style="font-size: 14pt;"><strong>Example:</strong></span></p>
<div>
<pre><span style="font-size: 14pt;"><strong>Input:</strong> str = "aabcbcdbca"
<strong>Output:</strong> 4
<strong>Explanation:</strong> Sub-String "dbca" has the smallest length that contains all the characters of str.
</span></pre>
</div>
<pre><span style="font-size: 14pt;"><strong>Input:</strong> str = "aaab"
<strong>Output:</strong> 2
<strong>Explanation:</strong> Sub-String "ab" has the smallest length that contains all the characters of str.</span></pre>
<pre><span style="font-size: 14pt;"><strong>Input:</strong> str = "geeksforgeeks"
<strong>Output:</strong> 8
<strong>Explanation:</strong> There are multiple substring with smallest length that contains all characters of str, "geeksfor" and "forgeeks". </span></pre>
<p><span style="font-size: 14pt;"><strong>Constraints:</strong><br>1 ≤ str.size() ≤ 10<sup>5</sup><br>str contains only lower-case english alphabets.</span></p></div>

<div class="problems_accordion_tags__JJ2DX problems_active_tags__3RExF"><div class="active title problems_active_tag_title__cgl9e"><div class="problems_tag_container__kWANg"><strong>Expected Complexities</strong></div></div><div class="content active animated_content open"><div class="problems_expected_complexities_text__h_eyi"><div class="problems_normal_text__QiKrb">Time Complexity: O(n)</div><div class="problems_normal_text__QiKrb">Auxiliary Space: O(1)</div></div></div><div class="ui divider g-mt-3"></div></div>

## Solutions

#### Key Points:
```


```


---

## ✅ **Problem Statement**

Given a string `str`, find the **length of the smallest substring (window)** that contains **all the unique characters** present in the original string.

---

## 💡 **Intuition**

* We are given a string and asked to find the minimum length of a substring which includes **every unique character** from the original string **at least once**.
* We use a **sliding window** approach with two pointers and a **hash map** to count character frequencies.
* We also use a **hash set** to identify all **unique characters** in the original string.

---

## 📋 **Algorithm**

1. Get the set of all unique characters in the input string `str`.
2. Initialize a sliding window with two pointers `l` (left) and `r` (right).
3. Move the right pointer `r` through the string and keep counting characters using a `map`.
4. When the map contains all unique characters (i.e., `map.size() == set.size()`):

   * Try to shrink the window from the left while still keeping all characters.
   * Update the minimum window size (`cnt`) accordingly.
5. Return the smallest window length.

---

## ✅ Java Code with Step-by-Step Comments

```java
class Solution {
    public int findSubString(String str) {
        // Step 1: Get all unique characters from the input string
        Set<Character> st = new HashSet<>();
        for (char c : str.toCharArray()) {
            st.add(c); // add all characters to set to get unique characters
        }

        // Step 2: Initialize sliding window pointers and answer variable
        int cnt = Integer.MAX_VALUE;  // to store the minimum length of window
        int l = 0, r = 0; // left and right pointers

        // Step 3: Map to store the frequency of characters in current window
        Map<Character, Integer> map = new LinkedHashMap<>();

        // Step 4: Start sliding the window
        while (r < str.length()) {
            // Add the current character to the map (increase frequency)
            char currentChar = str.charAt(r);
            map.put(currentChar, map.getOrDefault(currentChar, 0) + 1);

            // Step 5: When current window has all unique characters
            if (map.size() == st.size()) {
                // Try to shrink the window from the left while it is still valid
                while (map.size() == st.size()) {
                    // Update minimum length
                    cnt = Math.min(cnt, r - l + 1);

                    // Remove the leftmost character from map (decrease frequency)
                    char leftChar = str.charAt(l);
                    map.put(leftChar, map.get(leftChar) - 1);

                    // If frequency becomes 0, remove the character completely
                    if (map.get(leftChar) == 0) {
                        map.remove(leftChar);
                    }

                    // Move the left pointer forward
                    l++;
                }
            }

            // Move the right pointer forward
            r++;
        }

        return cnt;
    }
}
```

---

## 🧪 **Example Dry Run**

Input: `str = "aabcbcdbca"`

### Step 1: Unique Characters:

`Set = {a, b, c, d}` → Total unique = 4

### Sliding window:

| r | str\[r] | Window   | Map                  | l | Action                        | Result |
| - | ------- | -------- | -------------------- | - | ----------------------------- | ------ |
| 0 | a       | a        | {a:1}                | 0 | Not full set yet              |        |
| 1 | a       | aa       | {a:2}                | 0 | Not full set yet              |        |
| 2 | b       | aab      | {a:2, b:1}           | 0 | Not full set yet              |        |
| 3 | c       | aabc     | {a:2, b:1, c:1}      | 0 | Not full set yet              |        |
| 4 | b       | aabcb    | {a:2, b:2, c:1}      | 0 | Not full set yet              |        |
| 5 | c       | aabcbc   | {a:2, b:2, c:2}      | 0 | Not full set yet              |        |
| 6 | d       | aabcbcd  | {a:2, b:2, c:2, d:1} | 0 | All unique found, try shrink  |        |
| → |         | abcbcd   | {a:1, b:2, c:2, d:1} | 1 | Still all unique              |        |
| → |         | bcbcd    | {a:0, b:2, c:2, d:1} | 2 | a count = 0 → remove from map | 5      |
| 7 | b       | cbcd b   | {b:3, c:2, d:1}      | 2 | Not full set yet              |        |
| 8 | c       | cbcd bc  | {b:3, c:3, d:1}      | 2 | Not full set yet              |        |
| 9 | a       | cbcd bca | {a:1, b:3, c:3, d:1} | 2 | All unique again, try shrink  |        |
| → |         | bcd bca  | {a:1, b:2, c:3, d:1} | 3 | Still valid                   |        |
| → |         | cd bca   | {a:1, b:1, c:2, d:1} | 4 | Still valid                   |        |
| → |         | d bca    | {a:1, b:0, c:1, d:1} | 5 | b count = 0 → remove, invalid | 4      |

✅ **Final result = 4**

---

## 🧾 Summary

* **Time Complexity:** O(N), where N is the length of the string
* **Space Complexity:** O(1), since at most 26 lowercase English letters are stored




























