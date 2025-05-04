# Alien Dictionary

https://www.geeksforgeeks.org/problems/alien-dictionary/1


<p>A new alien language uses the English alphabet, but the order of letters is unknown. You are given a list of <strong>words[] </strong>from the alien language’s dictionary, where the words are claimed to be <strong>sorted lexicographically</strong> according to the language’s rules.</p>
<p>Your task is to <strong>determine the correct order of letters</strong> in this alien language based on the given words. If the order is valid, return a string containing the unique letters in lexicographically increasing order as per the new language's rules. If there are multiple valid orders, return any one of them.</p>
<p>However, if the given arrangement of words is inconsistent with any possible letter ordering, return an <strong>empty string ("")</strong>.</p>
<blockquote>
<p>A string <strong>a</strong> is lexicographically smaller than a string <strong>b</strong> if, at the first position where they differ, the character in <strong>a</strong> appears earlier in the alien language than the corresponding character in <strong>b</strong>. If all characters in the shorter word match the beginning of the longer word, the shorter word is considered smaller.</p>
</blockquote>
<p>Your implementation will be tested using a driver code. It will print <strong>true </strong>if your returned order correctly follows the alien language’s lexicographic rules; otherwise, it will print <strong>false</strong>.</p>
<p><strong>Examples:</strong></p>
<pre><strong>Input:</strong> words[] = ["cb", "cba", "a", "bc"]<br><strong>Output:</strong> true<br><strong>Explanation: </strong>You need to return "cab" as the correct order of letters in the alien dictionary.</pre>
<pre><strong>Input: </strong>words[] = ["ab", "aa", "a"]<br><strong>Output:</strong> ""<br><strong>Explanation:</strong> You need to return "" because "aa" is lexicographically larger than "a", making the order invalid.</pre>
<pre><strong>Input:</strong> words[] = ["ab", "cd", "ef", "ad"]<br><strong>Output:</strong> ""<br><strong>Explanation:</strong> You need to return "" because "a" appears before "e", but then "e" appears before "a", which contradicts the ordering rules.</pre>
<p><strong>Constraints:</strong></p>
<ul>
<li>1 &lt;= words.length &lt;= 500</li>
<li>1 &lt;= words[i].length &lt;= 100</li>
<li>words[i] consists only of lowercase English letters.</li>
</ul></div></div>




---

## ✅ **Problem Summary**
You are given a list of words sorted according to a new alien language. Your task is to find the correct **order of characters** in this alien language.

---

## 🧠 **Intuition**
This is a **graph problem**. Here’s the insight:

- If two words differ at some index, the first different character tells us about the **relative order** of the letters in the alien alphabet.
- For example:
  - If "abc" comes before "abd", then we know `'c'` comes before `'d'` in the alien language.
- We can model this as a **Directed Acyclic Graph (DAG)**, where each edge `u -> v` means `u` comes before `v`.
- Then, we perform a **Topological Sort** to find a valid character ordering.

---

## 🪜 **Algorithm**
1. Create an **adjacency list** for each character.
2. Compare each pair of adjacent words and extract **order relationships**.
3. Use **Kahn’s Algorithm** (BFS-based Topological Sort) to determine a valid order.
4. If there's a **cycle**, return `""` (invalid ordering).
5. Otherwise, return the topologically sorted order.

---

## 🔍 **Dry Run Example**
Input: `["cb", "cba", "a", "bc"]`

Let’s compare:
- "cb" vs "cba" → `b` comes before `a`
- "cba" vs "a" → `c` comes before `a`
- "a" vs "bc" → `a` comes before `b`

So:
- `b -> a`
- `c -> a`
- `a -> b` ← conflict! Because we already have `b -> a`

This introduces a **cycle**, so output is `""`.

---

## ✅ Final Code with Step-by-Step Comments

```java
import java.util.*;

class Solution {
    public String findOrder(String[] words) {
        // Step 1: Create graph and inDegree map for characters
        Map<Character, List<Character>> graph = new HashMap<>(); // Graph: char -> list of next chars
        Map<Character, Integer> inDegree = new HashMap<>();      // inDegree: char -> count of incoming edges

        // Step 2: Initialize graph and inDegree for all unique characters
        for (String word : words) {
            for (char ch : word.toCharArray()) {
                graph.putIfAbsent(ch, new ArrayList<>());  // Create entry in graph
                inDegree.putIfAbsent(ch, 0);               // Initialize in-degree to 0
            }
        }

        // Step 3: Build graph by comparing adjacent words
        for (int i = 0; i < words.length - 1; i++) {
            String w1 = words[i];
            String w2 = words[i + 1];

            // Step 3a: Check for invalid input (e.g., ["abc", "ab"] is invalid)
            if (w1.length() > w2.length() && w1.startsWith(w2)) {
                return ""; // Prefix rule violation → invalid order
            }

            // Step 3b: Compare characters of the two words
            for (int j = 0; j < Math.min(w1.length(), w2.length()); j++) {
                char c1 = w1.charAt(j);
                char c2 = w2.charAt(j);

                // Step 3c: When characters differ, we found a relation: c1 < c2
                if (c1 != c2) {
                    graph.get(c1).add(c2);                        // Add edge c1 -> c2
                    inDegree.put(c2, inDegree.get(c2) + 1);       // Increment in-degree of c2
                    break; // Only first difference matters for ordering
                }
            }
        }

        // Step 4: Perform topological sort using Kahn's Algorithm (BFS)
        Queue<Character> queue = new LinkedList<>(); // Queue for BFS
        StringBuilder result = new StringBuilder();  // To store the final order

        // Step 4a: Add all nodes with in-degree 0 (no dependencies)
        for (char ch : inDegree.keySet()) {
            if (inDegree.get(ch) == 0) {
                queue.offer(ch); // Ready to process
            }
        }

        // Step 4b: BFS traversal
        while (!queue.isEmpty()) {
            char curr = queue.poll(); // Get current character with in-degree 0
            result.append(curr);      // Add to result (order of alien language)

            // Step 4c: Reduce in-degree of all neighbors by 1
            for (char neighbor : graph.get(curr)) {
                inDegree.put(neighbor, inDegree.get(neighbor) - 1);

                // If in-degree becomes 0, add to queue
                if (inDegree.get(neighbor) == 0) {
                    queue.offer(neighbor);
                }
            }
        }

        // Step 5: Check if result includes all characters
        if (result.length() < graph.size()) {
            return ""; // There was a cycle → invalid ordering
        }

        return result.toString(); // Return the valid topological order
    }
}

```

- **Cycle Detection**: If not all characters are in the result, there's a cycle (invalid order).

---

## 🔁 Dry Run on Valid Input

Input: `["wrt", "wrf", "er", "ett", "rftt"]`

Compare:
- wrt vs wrf → `t -> f`
- wrf vs er → `w -> e`
- er vs ett → `r -> t`
- ett vs rftt → `e -> r`

Graph:
```
t -> f
w -> e
r -> t
e -> r
```

Topological order (one possible): `w -> e -> r -> t -> f`

✅ Output: `"wertf"`

---

Let me know if you want a **DFS version** of topological sort too!