## Palindrome String


https://www.geeksforgeeks.org/problems/palindrome-string0817/1


```
Given a string S, check if it is palindrome or not.
```


#### Example 1:

```
Input: S = "abba"
Output: 1
Explanation: S is a palindrome

```

#### Example 2:
```
Input: S = "abc" 
Output: 0
Explanation: S is not a palindrome
```
### Your Task:

```
You don't need to read input or print anything. Complete the function isPalindrome()which accepts string S and returns an integer value 1 or 0.

Expected Time Complexity: O(Length of S)
Expected Auxiliary Space: O(1)
```

#### Constraints:
```
1 <= Length of S<= 2*105
```

## Solutions

```
Key Points:

```

* **Java**

```
class Solution {
    int isPalindrome(String S) {
        // code here
        int begin = 0;
        int end = S.length() - 1;
        while(begin <= end) {
            if(S.charAt(begin) != S.charAt(end)) {
                return 0;
            }
            begin++;
            end--;
        }
        return 1;
    }
};

```