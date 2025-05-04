## Insert in a Sorted List


https://www.geeksforgeeks.org/problems/insert-in-a-sorted-list/1


```
Given a linked list sorted in ascending order and an integer called data, insert data in the linked list such that the list remains sorted.
```


#### Example 1:

```
Input:
LinkedList: 25->36->47->58->69->80
data: 19
Output: 
19 25 36 47 58 69 80
Explanation:
After inserting 19 the sorted linked list will look like the one in the output.

```

#### Example 2:
```
Input:
LinkedList: 50->100
data: 75
Output: 
50 75 100
Explanation:
After inserting 75 the sorted linked list will look like the one in the output.
```
### Your Task:

```
The task is to complete the function sortedInsert() which should insert the element in sorted Linked List and return the head of the linked list

Expected Time Complexity: O(N).
Expected Auxiliary Space: O(1).
```

#### Constraints:
```
1 <= N <= 104
-99999 <= A[i] <= 99999, for each valid i
```

## Solutions

#### Key Points:
```


```

* **Java**

```
class Solution {
    Node sortedInsert(Node head1, int key) {
        // Create a new node with the given data
        Node temp = new Node(key);

        // Case 1: The list is empty
        if (head1 == null) {
            return temp;
        }

        // Case 2: The new node should be the new head
        if (key < head1.data) {
            temp.next = head1;
            return temp;
        }

        // Case 3: Traverse the list to find the correct position
        Node curr = head1;
        while (curr.next != null && curr.next.data < key) {
            curr = curr.next;
        }

        // Insert the new node
        temp.next = curr.next;
        curr.next = temp;

        return head1;
    }
}

```



























