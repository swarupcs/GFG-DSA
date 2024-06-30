## Anagram Strings


https://www.geeksforgeeks.org/problems/java-anagram-strings3549/1


```
Given two strings S1 and S2 . Print "1" if both strings are anagrams otherwise print "0" .

Note: An anagram of a string is another string with exactly the same quantity of each character in it, in any order.
```


#### Example 1:

```
Input: S1 = "cdbkdub" , S2 = "dsbkcsdn"
Output: 0 
Explanation: Length of S1 is not same
as length of S2.

```

#### Example 2:
```
Input: S1 = "geeks" , S2 = "skgee"
Output: 1
Explanation: S1 has the same quantity 
of each character in it as S2.
```
### Your Task:

```
You don't need to read input or print anything. Your task is to complete the function areAnagram() which takes S1 and S2 as input and returns "1" if both strings are anagrams otherwise returns "0".
```
```
Expected Time Complexity: O(n)
Expected Auxiliary Space: O(K) ,Where K= Contstant
```

#### Constraints:
```
1 <= |S1| <= 1000
1 <= |S2| <= 1000 
```

## Solutions


#### Key Points:



1. Check if the lengths of S1 and S2 are equal. If not, return false.
2. Initialize an array count of size CHAR (256, to cover all possible ASCII characters) to zero.
3. Traverse each character of S1 and S2 simultaneously:
    * Increment the count for the character in S1.
    * Decrement the count for the character in S2.
4. After processing both strings, check if all counts are zero:
    * If any count is not zero, return false.
    * Otherwise, return true.

* **Java**

```
class Solution {
    static int areAnagram(String S1, String S2) {
        if (S1.length() != S2.length()) {
            return 0;
        }
        
        // Assuming only lowercase English letters, use an array of size 26
        int[] count = new int[26];
        
        // Count frequencies in S1
        for (int i = 0; i < S1.length(); i++) {
            count[S1.charAt(i) - 'a']++;
        }
        
        // Decrement frequencies for S2
        for (int i = 0; i < S2.length(); i++) {
            count[S2.charAt(i) - 'a']--;
        }
        
        // Check if all counts are zero
        for (int i = 0; i < 26; i++) {
            if (count[i] != 0) {
                return 0;
            }
        }
        
        return 1;
    }
}


```