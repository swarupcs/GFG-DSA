## Parenthesis Checker


http://geeksforgeeks.org/problems/parenthesis-checker2744/1


<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 18px;">Given a string <strong>s</strong>, composed of different combinations of '(' , ')', '{', '}', '[', ']', verify the validity of the arrangement.<br></span><span style="font-size: 18px;">An input string is valid if:</span></p>
<p><span style="font-size: 18px;">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;1. Open brackets must be closed by the same type of brackets.<br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;2. Open brackets must be closed in the correct order.</span></p>
<p><strong><span style="font-size: 18px;">Examples :</span></strong></p>
<pre><span style="font-size: 18px;"><strong>Input: </strong>s = "[{()}]"
<strong>Output:</strong> true
<strong>Explanation: </strong>All the brackets are well-formed.</span></pre>
<pre><span style="font-size: 18px;"><strong>Input: </strong>s = "[()()]{}"
<strong>Output:</strong> true
<strong>Explanation: </strong>All the brackets are well-formed.<br></span></pre>
<pre><strong><span style="font-size: 18px;">Input:</span></strong><span style="font-size: 18px;"> s = "([]"<br><strong>Output: </strong>False<br><strong>Explanation: </strong>The expression is not balanced as there is a missing ')' at the end.<br></span></pre>
<pre><strong><span style="font-size: 18px;">Input:</span></strong><span style="font-size: 18px;"> s = "([{]})"<br><strong>Output: </strong>False<br><strong>Explanation: </strong>The expression is not balanced as there is a closing ']' before the closing '}'.<br></span></pre>
<p><span style="font-size: 14pt;"><strong>Constraints:</strong><br>1 ≤ s.size() ≤ 10<sup>6<br></sup>s[i] ∈ {'{', '}', '(', ')', '[', ']'}</span></p></div>
## Solutions

#### Key Points:
```


```


---

### ✅ **Approach**

Use a **stack** to keep track of opening brackets. For every **closing bracket**, we check:

* Is the stack **non-empty**?
* Does the **top element match** the closing bracket?

If not, the string is **unbalanced**.

At the end, if the stack is **empty**, then all brackets were matched correctly — string is **balanced**.

---

### 💡 **Intuition**

Stack follows **LIFO (Last In First Out)**, which suits this problem. Every **open bracket** must be **closed in reverse order**, making stack the perfect tool.

---

### 🧠 **Algorithm**

1. Initialize an empty stack.
2. Traverse the string:

   * Push opening brackets: `'('`, `'{'`, `'['`
   * For closing brackets: `')'`, `'}'`, `']'`:

     * If stack is empty → return false.
     * Pop the top of the stack.
     * Check if it matches the corresponding opening bracket.
     * If not matched → return false.
3. After traversal:

   * If stack is empty → return true.
   * Else → return false.

---

### ✅ **Java Code with Step-by-Step Comments**

```java
import java.util.Stack;

class Solution {

    // Helper function to check if open and close brackets match
    private boolean isMatched(char open, char close) {
        // Match pairs of brackets
        return (open == '(' && close == ')') ||
               (open == '[' && close == ']') ||
               (open == '{' && close == '}');
    }

    // Function to check if the input string is balanced
    static boolean isBalanced(String s) {
        // Create instance to call the non-static helper function
        Solution sol = new Solution();

        // Step 1: Create an empty stack to store opening brackets
        Stack<Character> stack = new Stack<>();

        // Step 2: Traverse each character in the input string
        for (int i = 0; i < s.length(); i++) {
            char ch = s.charAt(i); // Current character

            // Step 3: If it's an opening bracket, push to the stack
            if (ch == '(' || ch == '[' || ch == '{') {
                stack.push(ch);
            }

            // Step 4: If it's a closing bracket
            else if (ch == ')' || ch == ']' || ch == '}') {

                // Step 4.1: If stack is empty, no matching open bracket
                if (stack.isEmpty()) return false;

                // Step 4.2: Pop the top element (last opening bracket)
                char top = stack.pop();

                // Step 4.3: Check if the opening and closing match
                if (!sol.isMatched(top, ch)) return false;
            }
        }

        // Step 5: If stack is empty, all brackets matched correctly
        return stack.isEmpty();
    }

    // Main method to test
    public static void main(String[] args) {
        String[] testCases = {
            "()", "()[]{}", "(]", "([])", "([)]", "{[()]}", "(", "(()"
        };

        for (String test : testCases) {
            boolean result = isBalanced(test);
            System.out.println("Input: " + test + " -> Balanced: " + result);
        }
    }
}

```

---

### 🔍 **Example Dry Run**

**Input:** `s = "([])"`

1. Stack = `[]`
2. Read `'('` → opening → push → Stack: `['(']`
3. Read `'['` → opening → push → Stack: `['(', '[']`
4. Read `']'` → closing → top = `'['` → match → pop → Stack: `['(']`
5. Read `')'` → closing → top = `'('` → match → pop → Stack: `[]`
6. End of string → stack is empty → ✅ **Balanced**

---

### ✅ **Final Output Example**

```plaintext
Input: () -> Balanced: true
Input: ()[]{} -> Balanced: true
Input: (] -> Balanced: false
Input: ([]) -> Balanced: true
Input: ([)] -> Balanced: false
Input: {[()]} -> Balanced: true
Input: ( -> Balanced: false
Input: (() -> Balanced: false
```

### ✅ **Time and Space Complexity Analysis**

We're analyzing the function:

```java
static boolean isBalanced(String s)
```

---

### ⏱ **Time Complexity: O(n)**

* `n` = length of the input string `s`.
* We **traverse each character exactly once** in a loop: `for (int i = 0; i < s.length(); i++)`.
* Each character is either:

  * Pushed to the stack (if it's an opening bracket), or
  * Popped and checked (if it's a closing bracket).

> There are no nested loops or repeated passes — just a **single linear pass**.

✅ **Time Complexity = O(n)**

---

### 🧠 **Space Complexity: O(n)**

* In the **worst case**, the input string contains **only opening brackets** like `"((((((("`.

  * All characters are pushed to the stack → stack size becomes `n`.
* Even in a mix like `"((({[{["`, the **maximum space** used by the stack is proportional to the unmatched opening brackets at any point.

✅ **Space Complexity = O(n)** (due to stack)

---

### 🧪 Best vs Worst Case

| Case                                     | Time Complexity | Space Complexity |
| ---------------------------------------- | --------------- | ---------------- |
| Best (fully balanced, early exit)        | O(n)            | O(n)             |
| Worst (all opening or mismatched at end) | O(n)            | O(n)             |

---

