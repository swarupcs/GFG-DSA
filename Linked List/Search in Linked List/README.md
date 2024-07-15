## Search in Linked List


https://www.geeksforgeeks.org/problems/search-in-linked-list-1664434326/0


```
Given a linked list of n nodes and a key , the task is to check if the key is present in the linked list or not.
```


#### Example 1:

```
Input:
n = 4
1->2->3->4
Key = 3
Output:
True
Explanation:
3 is present in Linked List, so the function returns true.

```


### Your Task:

```
Your task is to complete the given function searchKey(), which takes a head reference and key as Input and returns true or false boolean value by checking the key is present or not in the linked list.
Expected Time Complexity: O(n)
Expected Space Complexity: O(1)
```

#### Constraints:
```
1 <= n <= 105
1 <= key <= 105
```

## Solutions

#### Key Points:
```


```

* **Java**

```
class Solution {
    static boolean searchKey(int n, Node head, int key) {
        // Code here
        Node curr = head;
        while(curr != null) {
            if(curr.data == key) {
                return true;
            } else {
                curr = curr.next;
            }
        }
        
        return false;
    }
}
```



























