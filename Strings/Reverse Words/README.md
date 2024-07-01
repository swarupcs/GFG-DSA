## Reverse Words

https://www.geeksforgeeks.org/problems/reverse-words-in-a-given-string5459/1


```
Given a String S, reverse the string without reversing its individual words. Words are separated by dots.
```


#### Example 1:

```
Input:
S = i.like.this.program.very.much
Output: much.very.program.this.like.i
Explanation: After reversing the whole
string(not individual words), the input
string becomes
much.very.program.this.like.i

```

#### Example 2:
```
Input:
S = pqr.mno
Output: mno.pqr
Explanation: After reversing the whole
string , the input string becomes
mno.pqr
```
### Your Task:

```
You dont need to read input or print anything. Complete the function reverseWords() which takes string S as input parameter and returns a string containing the words in reversed order. Each word in the returning string should also be separated by '.' 
Expected Time Complexity: O(|S|)
Expected Auxiliary Space: O(|S|)
```

#### Constraints:
```
1 <= |S| <= 105
```

## Solutions

```
Key Points:

```

* **Java**

```
class Solution {
    // Function to reverse words in a given string.
    String reverseWords(String S) {
        // Convert the string to a character array
        char[] str = S.toCharArray();
        int n = S.length();
        int start = 0;
        
        // Reverse individual words
        for (int end = 0; end < n; end++) {
            if (str[end] == '.') {
                reverse(str, start, end - 1);
                start = end + 1;
            }
        }
        
        // Reverse the last word
        reverse(str, start, n - 1);
        
        // Reverse the entire string
        reverse(str, 0, n - 1);
        
        // Convert the character array back to a string and return it
        return new String(str);
    }
    
    // Helper function to reverse a part of the character array
    static void reverse(char str[], int low, int high) {
        while (low < high) {
            char temp = str[low];
            str[low] = str[high];
            str[high] = temp;
            low++;
            high--;
        }
    }
    
}

```