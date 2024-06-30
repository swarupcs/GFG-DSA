## Check for subsequence


https://www.geeksforgeeks.org/problems/check-for-subsequence4930/1


```

```


#### Example 1:

```
Input:
A = AXY 
B = YADXCP
Output: 0 
Explanation: A is not a subsequence of B
as 'Y' appears before 'A'.

```

#### Example 2:
```
Input:
A = gksrek
B = geeksforgeeks
Output: 1
Explanation: A is a subsequence of B.
```
### Your Task:

```
You dont need to read input or print anything. Complete the function isSubSequence() which takes A and B as input parameters and returns a boolean value denoting if A is a subsequence of B or not. 

 

Expected Time Complexity: O(N) where N is length of string B.
Expected Auxiliary Space: O(1)
```

#### Constraints:
```
1<= |A|,|B| <=104
```

## Solutions

#### Approach

To determine if string A is a subsequence of string B, we need to check if all characters of A appear in B in the same order as they appear in A. A subsequence does not require the characters to be contiguous but maintains the relative order.

#### Intuition

1. Use two pointers to traverse the strings A and B.
2. Start both pointers at the beginning of their respective strings.
3. If the current character in A matches the current character in B, move the pointer in A to the next character.
4. Always move the pointer in B to the next character regardless of whether there was a match.
5. If we reach the end of A while performing the above steps, it means all characters of A were found in B in the correct order, so A is a subsequence of B.
6. If we finish traversing B without finding all characters of A, then A is not a subsequence of B.

#### Algorithm
1. Initialize a pointer j to 0 for string A.
2. Traverse string B using a for loop with a pointer i.
3. For each character in B:
   * If the character at the current position of B (B[i]) matches the character at the current position of A (A[j]), increment j to move to the next character in A.
4. After the loop, check if j is equal to the length of A. If it is, return true indicating that A is a subsequence of B.
5. If j is not equal to the length of A, return false indicating that A is not a subsequence of B.

* **Java**

```

class Solution {
    boolean isSubSequence(String A, String B) {
        int n = A.length();
        int m = B.length();

        // Pointer for A
        int j = 0;

        // Traverse B using a for loop
        for (int i = 0; i < m && j < n; i++) {
            // If characters match, move the pointer for A
            if (A.charAt(j) == B.charAt(i)) {
                j++;
            }
        }

        // If we have traversed all characters of A
        return (j == n);
    }
}


```