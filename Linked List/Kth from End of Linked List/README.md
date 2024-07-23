## Kth from End of Linked List


https://www.geeksforgeeks.org/problems/nth-node-from-end-of-linked-list/1


```
Given head of a linked list and a number k, your task is to find the kth node from the end. If k is more than the number of nodes, then the output should be -1.
The following is internal representation of every test case (three inputs).
n :  Size of the linked list
k : Postion (from end) of the node to be found
value[] :  An array of values that represents values of nodes.
```


#### Example 1:

```
Input: n = 9, k = 2, value[] = {1,2,3,4,5,6,7,8,9}
Output: 8
Explanation: The given linked list is 1->2->3->4->5->6->7->8->9. The 2nd node from end is 8. 

```

#### Example 2:
```
Input: n = 4, k = 5, value[] = {10,5,100,5}
Output: -1
Explanation: The given linked list is 10->5->100->5. Since 'k' is more than the number of nodes, the output is -1.
```
### Your Task:

```
Note:  Try to solve in a single traversal.

Expected Time Complexity: O(n).
Expected Auxiliary Space: O(1).
```

#### Constraints:
```
1 <= n <= 106
1 <= k <= 106
```

## Solutions

#### Key Points:
```


```

* **Java**

```
class Solution {

    // Function to find the data of the kth node from
    // the end of a linked list.
    int getKthFromLast(Node head, int k) {
        // If the list is empty, return -1
        if (head == null) {
            return -1;
        }

        // Initialize the first pointer to head
        Node first = head;

        // Move the first pointer k nodes ahead
        for (int i = 0; i < k; i++) {
            // If the list has fewer than k nodes, return -1
            if (first == null) {
                return -1;
            }
            first = first.next;
        }

        // Initialize the second pointer to head
        Node second = head;

        // Move both pointers until the first pointer reaches the end
        while (first != null) {
            second = second.next;
            first = first.next;
        }

        // The second pointer now points to the kth node from the end
        return second.data;
    }
}

```



























