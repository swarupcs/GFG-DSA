## Row with max 1s


https://www.geeksforgeeks.org/problems/row-with-max-1s0023/1


```
Given a boolean 2D array, consisting of only 1's and 0's, where each row is sorted. Return the 0-based index of the first row that has the most number of 1s. If no such row exists, return -1.
```


#### Example 1:

```
Input: arr[][] = [[0, 1, 1, 1],
               [0, 0, 1, 1],
               [1, 1, 1, 1],
               [0, 0, 0, 0]]
Output: 2
Explanation: Row 2 contains 4 1's (0-based indexing).

```

#### Example 2:
```
Input: arr[][] = [[0, 0], 
               [1, 1]]
Output: 1
Explanation: Row 1 contains 2 1's (0-based indexing).
```
### Your Task:

```
Expected Time Complexity: O(n+m)
Expected Auxiliary Space: O(1)
```

#### Constraints:
```
1 ≤ number of rows, number of columns ≤ 103
0 ≤ arr[i][j] ≤ 1 
```

## Solutions

#### Approach
```
The provided Java code finds the index of the first row in a given 2D boolean array (arr) that contains the maximum number of 1s. The key points to note about the problem and the code are:

Input: A 2D boolean array arr of size m x n, where each row is sorted and contains only 0s and 1s.
Output: The index of the row with the maximum number of 1s. If no such row exists, return -1.
```
#### Key Points:

Approach and Algorithm
1. **Initialize Variables**:

* **m**: Number of rows in the array.
* **n**: Number of columns in the array.
* **maxOneCount**: Keeps track of the highest number of 1s found in any row.
* **maxOneRow**: Keeps track of the index of the row with the highest number of 1s.
2. **Iterate Through Each Row**:

* For each row i (from 0 to m-1):
    * Initialize a counter oneCount to count the number of 1s in the current row.
    * Iterate through each column j (from 0 to n-1):
        * If arr[i][j] == 1, increment the oneCount.
3. **Update Maximum Count and Row Index**:

* After counting 1s in the current row, check if oneCount is greater than maxOneCount.
* If true, update maxOneCount to oneCount and maxOneRow to the current row index i.
4. **Return Result**:

* After completing the iteration through all rows, return maxOneRow, which is the index of the row with the maximum number of 1s.



* **Java**

```
class Solution {
    public int rowWithMax1s(int arr[][]) {
        // Determine the number of rows (m) and columns (n)
        int m = arr.length;
        int n = arr[0].length;
        
        // Initialize variables to keep track of the maximum number of 1s found
        // and the row index where this maximum number is found
        int maxOneCount = 0;
        int maxOneRow = -1;
        
        // Iterate through each row in the array
        for(int i = 0; i < m; i++) {
            // Count the number of 1s in the current row
            int oneCount = 0;
            for(int j = 0; j < n; j++) {
                if(arr[i][j] == 1) {
                    oneCount++;
                }
            }
            
            // If the current row has more 1s than previously found,
            // update the maximum count and the corresponding row index
            if(oneCount > maxOneCount) {
                maxOneCount = oneCount;
                maxOneRow = i;
            }
        }
        
        // Return the index of the row with the maximum number of 1s
        return maxOneRow;
    }
}

```



























