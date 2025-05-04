## Segregate 0s and 1s



https://www.geeksforgeeks.org/problems/segregate-0s-and-1s5106/1


```
Given an array of length n consisting of only 0's and 1's in random order. Modify the array in-place to segregate 0s on the left side and 1s on the right side of the array.
```

#### Example 1:

```
Input:
n = 5
arr[] = {0, 0, 1, 1, 0}
Output: {0, 0, 0, 1, 1}
Explanation: 
After segregate all 0's on the left and 1's on the right modify array will be {0, 0, 0, 1, 1}.

```

#### Example 2:
```
n = 4
arr[] = {1, 1, 1, 1}
Output: {1, 1, 1, 1}
Explanation: There are no 0 in the given array, so the modified array is 1 1 1 1.
```

### Your Task:

```
You don't need to read input or print anything. Your task is to complete the function segregate0and1() which takes arr[] and n as input parameters and modifies arr[] in-place without using any extra memory.
```


#### Constraints:
```
1 ≤ n ≤ 106
0 ≤ arr[i] ≤ 1
```

```
Expected Time Complexity: O(n)
Expected Auxiliary Space: O(1)
```

## Solutions

```
Approach: Two pointer approach

1. Take 2 pointers say s  and e ,one at the beginning and the other at the end of the array
2. Let s point at the beginning of the array and e at the end .
3. Now we want to put all the 1s in the right side of the array , once we do this all 0s will automatically be on the left side of the array
4. So we compare the elements at s , arr[s] =1 then this should be at the right side of the array , so we swap this with element present at e 
5. After swapping , now we know that element at index e will surely be 1 , so now we can decrement e . 
6. Else if theres a 0 then we will increment i 
```

* **Java**

```
class Solution {
    void segregate0and1(int[] arr, int n) {
        // code here
        int start = 0;
		int end = n - 1;
		int temp;
		while(start < end) {
			if(arr[start] == 1) {
				temp = arr[start];
				arr[start] = arr[end];
				arr[end] = temp;
				end--;
			} else {
				start++;
			}
		}
    }

}


```