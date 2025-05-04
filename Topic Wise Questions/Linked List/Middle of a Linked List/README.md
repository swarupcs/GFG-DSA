## Middle of a Linked List


https://www.geeksforgeeks.org/problems/finding-middle-element-in-a-linked-list/1


```
Given head of a linked list, the task is to find the middle. For example, the middle of 1-> 2->3->4->5 is 3. If there are two middle nodes (even count), return the second middle. For example, middle of 1->2->3->4->5->6 is 4.

The following is internal representation of every test case (two inputs).
n : Size of the linked list
value[] :  An array of values that represents values of nodes.
```


#### Example 1:

```
Input: n = 5, value[] = {1,2,3,4,5}
Output: 3 
Explanation: The given linked list is 1->2->3->4->5 and its middle is 3.

```

#### Example 2:
```
Input: n = 6, value[] = {2,4,6,7,5,1}
Output: 7 
Explanation: The given linked list is 2->4->6->7->5->1 and its middle is 7.
```
### Your Task:

```
Expected Time Complexity: O(N).
Expected Auxiliary Space: O(1).
```

#### Constraints:
```
Constraints:
1 <= n <= 5000
```

## Solutions

#### Key Points:
```


```

* **Java**

```
class Solution {
    int getMiddle(Node head) {
        // Your code here.
        if(head == null) {
            return 0;
        }
        
        Node slow = head, fast = head;
        while(fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        
        return slow.data;
    }
}
```



























