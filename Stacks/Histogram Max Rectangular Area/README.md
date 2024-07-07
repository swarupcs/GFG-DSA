## Histogram Max Rectangular Area

https://www.geeksforgeeks.org/problems/maximum-rectangular-area-in-a-histogram-1587115620/1


```
Find the largest rectangular area possible in a given histogram where the largest rectangle can be made of a number of contiguous bars. For simplicity, assume that all bars have the same width and the width is 1 unit, there will be N bars height of each bar will be given by the array arr.
```


#### Example 1:

```
Input:
N = 7
arr[] = {6,2,5,4,5,1,6}
Output: 12
Explanation: In this example the largest area would be 12 of height 4 and width 3. We can achieve this 
area by choosing 3rd, 4th and 5th bars.

```

#### Example 2:
```
Input:
N = 8
arr[] = {7 2 8 9 1 3 6 5}
Output: 16
Explanation: Maximum size of the histogram 
will be 8  and there will be 2 consecutive 
histogram. And hence the area of the 
histogram will be 8x2 = 16.
```
### Your Task:

```
The task is to complete the function getMaxArea() which takes the array arr[] and its size N as inputs and finds the largest rectangular area possible and returns the answer.

Expected Time Complxity : O(N)
Expected Auxilliary Space : O(N)
```

#### Constraints:
```
1 ≤ N ≤ 106
0 ≤ arr[i] ≤ 1012
```

## Solutions

#### Key Points:
```


```

* **Java**

```
class Solution
{
    //Function to find largest rectangular area possible in a given histogram.
    public static long getMaxArea(long hist[], long n) 
    {
        // your code here
        long res = 0;
        long[] ps = new long[(int) n];
        long[] ns = new long[(int) n];

        // Calculate Previous Smaller Elements
        Stack<Integer> s = new Stack<>();
        s.push(0);
        for (int i = 0; i < n; i++) {
            while (!s.isEmpty() && hist[s.peek()] >= hist[i])
                s.pop();
            long pse = s.isEmpty() ? -1 : s.peek();
            ps[i] = pse;
            s.push(i);
        }

        // Clear the stack
        s.clear();

        // Calculate Next Smaller Elements
        s.push((int) (n - 1));
        for (int i = (int) (n - 1); i >= 0; i--) {
            while (!s.isEmpty() && hist[s.peek()] >= hist[i])
                s.pop();
            long nse = s.isEmpty() ? n : s.peek();
            ns[i] = nse;
            s.push(i);
        }

        // Calculate maximum area
        for (int i = 0; i < n; i++) {
            long curr = hist[i];
            long width = ns[i] - ps[i] - 1;
            long area = curr * width;
            res = Math.max(res, area);
        }

        return res;
    }
        
}
```



























