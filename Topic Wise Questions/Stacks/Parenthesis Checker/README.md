## Parenthesis Checker


https://leetcode.com/problems/trapping-rain-water/


```
Given an expression string x. Examine whether the pairs and the orders of {,},(,),[,] are correct in exp.
For example, the function should return 'true' for exp = [()]{}{[()()]()} and 'false' for exp = [(]).

Note: The drive code prints "balanced" if function return true, otherwise it prints "not balanced".
```


#### Example 1:

```
Input:
{([])}
Output: 
true
Explanation: 
{ ( [ ] ) }. Same colored brackets can form 
balanced pairs, with 0 number of 
unbalanced bracket.

```

#### Example 2:
```
Input: 
()
Output: 
true
Explanation: 
(). Same bracket can form balanced pairs, 
and here only 1 type of bracket is 
present and in balanced way.
```

#### Example 2:
```
Input: 
([]
Output: 
false
Explanation: 
([]. Here square bracket is balanced but 
the small bracket is not balanced and 
Hence , the output will be unbalanced.
```


### Your Task:

```
This is a function problem. You only need to complete the function ispar() that takes a string as a parameter and returns a boolean value true if brackets are balanced else returns false. The printing is done automatically by the driver code.

Expected Time Complexity: O(|x|)
Expected Auixilliary Space: O(|x|)
```

#### Constraints:
```
1 ≤ |x| ≤ 32000
```

## Solutions

#### Key Points:
```


```

* **Java**

```
class Solution
{
    // Function to check if brackets are balanced or not.
    static boolean ispar(String x)
    {
        // Create a stack to keep track of opening brackets.
        Stack<Character> s = new Stack<Character>();
        
        // Traverse the input string.
        for(int i = 0; i < x.length(); i++) {
            // If the current character is an opening bracket, push it onto the stack.
            if(x.charAt(i) == '(' || x.charAt(i) == '{' || x.charAt(i) == '[') {
                s.add(x.charAt(i));
            } else {
                // If the stack is empty and we encounter a closing bracket, return false.
                if(s.isEmpty()) {
                    return false;
                // If the current closing bracket does not match the top of the stack, return false.
                } else if(matching(s.peek(), x.charAt(i)) == false) {
                    return false;
                // If the current closing bracket matches the top of the stack, pop the stack.
                } else {
                    s.pop();
                }
            }
        }
        
        // If the stack is empty at the end, all brackets were balanced.
        return s.isEmpty();
    }
    
    // Function to check if a pair of brackets matches.
    public static boolean matching(char a, char b) {
        return ((a == '(' && b == ')') || (a == '[' && b == ']') || (a == '{' && b == '}'));
    }
}


```