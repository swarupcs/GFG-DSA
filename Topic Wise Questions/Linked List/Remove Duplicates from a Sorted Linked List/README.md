## Remove Duplicates from a Sorted Linked List


https://www.geeksforgeeks.org/problems/remove-duplicate-element-from-sorted-linked-list/1


```
Given a singly linked list consisting of N nodes. The task is to remove duplicates (nodes with duplicate values) from the given list (if exists).
Note: Try not to use extra space. The nodes are arranged in a sorted way.
```


#### Example 1:

```
Input:
LinkedList: 2->2->4->5
Output: 2 4 5
Explanation: In the given linked list 
2 ->2 -> 4-> 5, only 2 occurs more 
than 1 time. So we need to remove it once.

```

#### Example 2:
```
Input:
LinkedList: 2->2->2->2->2
Output: 2
Explanation: In the given linked list 
2 ->2 ->2 ->2 ->2, 2 is the only element
and is repeated 5 times. So we need to remove
any four 2.
```
### Your Task:

```
The task is to complete the function removeDuplicates() which takes the head of input linked list as input. The function should remove the duplicates from linked list and return the head of the linkedlist.

Expected Time Complexity : O(N)
Expected Auxilliary Space : O(1)
```

#### Constraints:
```
1 <= Number of nodes <= 105
```

## Solutions

#### Key Points:
```


```

* **Java**

```
class GfG {
    // Function to remove duplicates from sorted linked list.
    Node removeDuplicates(Node head) {
        // Initialize the current pointer to head
        Node curr = head;
        
        // Traverse the list
        while (curr != null && curr.next != null) {
            // Check if current node and next node have the same data
            if (curr.data == curr.next.data) {
                // Skip the next node
                curr.next = curr.next.next;
            } else {
                // Move the current pointer to the next node
                curr = curr.next;
            }
        }
        
        // Return the modified list
        return head;
    }
}

```



























