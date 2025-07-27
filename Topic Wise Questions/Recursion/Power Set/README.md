## Power Set


https://www.geeksforgeeks.org/problems/power-set4302/1

<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 18px;">Given a string <strong>s </strong>of length<strong> n</strong>, find all the <strong>possible non-empty <a href="https://www.geeksforgeeks.org/data-structures/string-subsequence-substring/">subsequences</a> </strong>of the string <strong>s</strong> in <strong>lexicographically-sorted </strong>order.</span></p>
<p><span style="font-size: 18px;"><strong>Example 1:</strong></span></p>
<pre><span style="font-size: 18px;"><strong>Input : <br></strong>s = "abc"
<strong>Output: <br></strong>a ab abc ac b bc c
<strong>Explanation : <br></strong>There are a total 7 number of subsequences possible for the given string, and they are mentioned above in lexicographically sorted order.</span>
</pre>
<p><span style="font-size: 18px;"><strong>Example 2:</strong></span></p>
<pre><span style="font-size: 18px;"><strong>Input: <br></strong>s = "aa"
<strong>Output: <br></strong>a a aa
<strong>Explanation : <br></strong></span><span style="font-size: 18px;">There are a total 3 number of subsequences possible for the given string, and they are mentioned above in lexicographically sorted order.</span></pre>
<p><span style="font-size: 18px;"><strong>Your Task:</strong><br>You don't need to read input or print anything.&nbsp;</span><span style="font-size: 18px;">Your t</span><span style="font-size: 18px;">ask is to complete the function&nbsp;<strong>AllPossibleStrings()&nbsp;</strong>which takes a string <strong>s</strong> as the input parameter and <strong>returns a list </strong>of all possible <strong>subsequences (non-empty)</strong> that can be formed from <strong>s</strong> in <strong>lexicographically sorted </strong>order.</span></p>
<p><span style="font-size: 18px;"><strong>Expected Time Complexity:&nbsp;</strong>O( n*2<sup>n&nbsp; </sup>)<br><strong>Expected Space Complexity:&nbsp;</strong>O( n * 2<sup>n </sup>)</span></p>
<p><strong><span style="font-size: 18px;">Constraints:&nbsp;</span></strong><br><span style="font-size: 18px;">1 &lt;= n &lt;= 16<br><strong>s</strong> constitutes of lower case english alphabets</span></p></div>

## Solutions

#### Key Points:
```


```



---

## 🔍 **Problem Overview**

Given a string `s`, **generate all non-empty subsequences** of `s` in **lexicographically sorted order**.

---

## 💡 **Intuition**

Each character of the string has two choices:

1. Include it in the subsequence.
2. Exclude it from the subsequence.

Thus, for a string of length `n`, there are `2^n` total combinations (including the empty string), and `2^n - 1` **non-empty** subsequences.

We’ll use **backtracking (recursion)** to generate all possible subsequences, then **sort them** lexicographically before returning.

---

## 🧠 **Approach**

1. Use **backtracking** to explore all possible character combinations.
2. Skip empty subsequence.
3. Store the valid subsequences in a list.
4. Sort the list before returning.

---

## ✅ **Algorithm**

1. Create a helper function: `generateSubsequences(index, currentSubsequence)`.
2. If `index == s.length()`, check if `currentSubsequence` is non-empty → store it.
3. Else:

   * **Exclude** current character → recurse.
   * **Include** current character → add to `currentSubsequence` → recurse → backtrack (remove last char).
4. Finally, sort the list and return it.

---

## ✅ **Java Code (with Full Comments)**

```java
import java.util.*;

class Solution {

    // Function to generate all non-empty subsequences of a string in lexicographical order
    public List<String> AllPossibleStrings(String s) {
        List<String> result = new ArrayList<>(); // To store all subsequences
        StringBuilder current = new StringBuilder(); // To build current subsequence
        generateSubsequences(0, s, current, result); // Start backtracking

        Collections.sort(result); // Sort all subsequences in lexicographical order
        return result;
    }

    // Helper function for backtracking
    private void generateSubsequences(int index, String s, StringBuilder current, List<String> result) {
        // Base case: if index reaches end of string
        if (index == s.length()) {
            if (current.length() > 0) { // Add only non-empty subsequences
                result.add(current.toString());
            }
            return;
        }

        // Recursive case 1: Exclude the current character
        generateSubsequences(index + 1, s, current, result);

        // Recursive case 2: Include the current character
        current.append(s.charAt(index)); // Add current char
        generateSubsequences(index + 1, s, current, result); // Recurse

        // Backtrack: remove last character to explore other options
        current.deleteCharAt(current.length() - 1);
    }
}
```

---

## 🧪 **Example Dry Run**

**Input**: `s = "abc"`

### Recursive Tree:

```
Path → Subsequence

"" → (skip)
"a" → include 'a'
"ab" → include 'b'
"abc" → include 'c'
"ac" → skip 'b', include 'c'
"b"
"bc"
"c"
```

**Collected Subsequences (before sorting)**:
`["c", "b", "bc", "a", "ac", "ab", "abc"]`

**After sorting**:
`["a", "ab", "abc", "ac", "b", "bc", "c"]`

✅ Matches expected result.

---

## ⏱ **Time and Space Complexity**

### Time Complexity: `O(n * 2^n)`

* We generate all `2^n` subsets.
* For each, string concatenation (on average `O(n)` due to building strings).
* Sorting `2^n` strings takes `O(2^n log(2^n))` extra.

### Space Complexity: `O(n * 2^n)`

* Total of `2^n` subsequences stored.
* Each can be up to length `n`.

---

## 📌 Summary

* We used **backtracking** to explore every combination.
* We collected **only non-empty** subsequences.
* **Sorted** the result list before returning.

This approach is efficient for `n <= 16` due to `2^16 = 65536` being manageable.





























