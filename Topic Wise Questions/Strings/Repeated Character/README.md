## Repeated Character


https://www.geeksforgeeks.org/problems/repeated-character2058/1


```
Given a string consisting of lowercase english alphabets. Find the repeated character present first in the string.

NOTE - If there are no repeating characters return '#'.
```


#### Example 1:

```
Input:
S = "geeksforgeeks"
Output: g
Explanation: g, e, k and s are the repeating
characters. Out of these, g occurs first. 

```

#### Example 2:
```
Input: 
S = "abcde"
Output: -1
Explanation: No repeating character present. (You need to return '#')
```
### Your Task:

```
You don't need to read input or print anything. Your task is to complete the function firstRep() which takes the string S as input and returns the the first repeating character in the string. In case there's no repeating character present, return '#'.
Expected Time Complexity: O(|S|).
Expected Auxiliary Space: O(1).
```

#### Constraints:
```
1<=|S|<=105
```

## Solutions

```
Key Points:

```

* **Java**

```

//{ Driver Code Starts
//Initial Template for Java

import java.io.*;
import java.util.*;

class GFG
{
    public static void main(String args[])throws IOException
    {
        Scanner sc = new Scanner(System.in);
        int t = sc.nextInt();
        while(t-- > 0)
        {
            String s;
            s = sc.next();
            
            Solution ob = new Solution();
            char res = ob.firstRep(s);
            if (res == '#')
                System.out.println(-1);
            else
                System.out.println(res);
             
        }
    }
}
// } Driver Code Ends


//User function Template for Java
class Solution {
    static final int CHAR = 256;

    char firstRep(String S) {
        // Initialize an array to store the first index of each character
        int[] fIndex = new int[CHAR];
        Arrays.fill(fIndex, -1);
        
        int res = Integer.MAX_VALUE;
        
        // Traverse through the string
        for (int i = 0; i < S.length(); i++) {
            char currentChar = S.charAt(i);
            
            // Check if the character has been seen before
            if (fIndex[currentChar] == -1) {
                // First time encountering the character, store its index
                fIndex[currentChar] = i;
            } else {
                // Character has been seen before, update the result index
                res = Math.min(res, fIndex[currentChar]);
            }
        }
        
        // Check the result index to determine the output
        if (res == Integer.MAX_VALUE) {
            // No repeating character found
            return '#';
        } else {
            // Return the first repeating character
            return S.charAt(res);
        }
    }
}

```