## Implement two stacks in an array


https://www.geeksforgeeks.org/problems/implement-two-stacks-in-an-array/1


```
Your task is to implement  2 stacks in one array efficiently. You need to implement 4 methods.

twoStacks : Initialize the data structures and variables to be used to implement  2 stacks in one array.
push1 : pushes element into first stack.
push2 : pushes element into second stack.
pop1 : pops element from first stack and returns the popped element. If first stack is empty, it should return -1.
pop2 : pops element from second stack and returns the popped element. If second stack is empty, it should return -1.
```


#### Example 1:

```
Input:
push1(2)
push1(3)
push2(4)
pop1()
pop2()
pop2()
Output:
3 4 -1
Explanation:
push1(2) the stack1 will be {2}
push1(3) the stack1 will be {2,3}
push2(4) the stack2 will be {4}
pop1()   the poped element will be 3 from stack1 and stack1 will be {2}
pop2()   the poped element will be 4 from stack2 and now stack2 is empty
pop2()   the stack2 is now empty hence returned -1.

```

#### Example 2:
```
Input:
push1(1)
push2(2)
pop1()
push1(3)
pop1()
pop1()
Output:
1 3 -1
Explanation:
push1(1) the stack1 will be {1}
push2(2) the stack2 will be {2}
pop1()   the poped element will be 1 from stack1 and stack1 will be empty
push1(3) the stack1 will be {3}
pop1()   the poped element will be 3 from stack1 and stack1 will be empty
pop1()   the stack1 is now empty hence returned -1.
```
### Your Task:

```
You don't need to read input or print anything. You are required to complete the 4 methods push1, push2 which takes one argument an integer 'x' to be pushed into stack one and two and pop1, pop2 which returns the integer poped out from stack one and two. If no integer is present in the stack return -1.

Expected Time Complexity: O(1) for all the four methods.
Expected Auxiliary Space: O(1) for all the four methods.

Constraints:
1 <= Number of queries <= 104
1 <= Number of elements in the stack <= 100
The sum of count of elements in both the stacks < size of the given array
```

#### Constraints:
```

```

## Solutions

#### Key Points:
```


```

* **Java**

```
class twoStacks {
    int size; // Size of the array to store two stacks
    int top1, top2; // Top pointers for stack1 and stack2
    int arr[]; // Array to store elements of both stacks

    // No-argument constructor to initialize the data structure with default size of 100
    twoStacks() {
        size = 100; // Default size of the array
        arr = new int[size]; // Initialize the array
        top1 = -1; // Initialize top pointer for stack1
        top2 = size; // Initialize top pointer for stack2
    }

    // Function to push an integer into stack1
    void push1(int x) {
        // Check for available space before stack1 meets stack2
        if (top1 < top2 - 1) {
            top1++; // Increment top pointer for stack1
            arr[top1] = x; // Add the element to stack1
        } else {
            System.out.println("Stack Overflow"); // Print overflow message if no space is available
        }
    }

    // Function to push an integer into stack2
    void push2(int x) {
        // Check for available space before stack1 meets stack2
        if (top1 < top2 - 1) {
            top2--; // Decrement top pointer for stack2
            arr[top2] = x; // Add the element to stack2
        } else {
            System.out.println("Stack Overflow"); // Print overflow message if no space is available
        }
    }

    // Function to remove and return the top element from stack1
    int pop1() {
        // Check if stack1 is not empty
        if (top1 >= 0) {
            int x = arr[top1]; // Get the top element from stack1
            top1--; // Decrement top pointer for stack1
            return x; // Return the popped element
        } else {
            return -1; // Return -1 if stack1 is empty
        }
    }

    // Function to remove and return the top element from stack2
    int pop2() {
        // Check if stack2 is not empty
        if (top2 < size) {
            int x = arr[top2]; // Get the top element from stack2
            top2++; // Increment top pointer for stack2
            return x; // Return the popped element
        } else {
            return -1; // Return -1 if stack2 is empty
        }
    }

    // Main method to demonstrate the usage of twoStacks class
    public static void main(String[] args) {
        twoStacks ts = new twoStacks(); // Create an instance of twoStacks

        ts.push1(2); // Push 2 into stack1
        ts.push1(3); // Push 3 into stack1
        ts.push2(4); // Push 4 into stack2

        System.out.print(ts.pop1() + " "); // Pop and print element from stack1 (should print 3)
        System.out.print(ts.pop2() + " "); // Pop and print element from stack2 (should print 4)
        System.out.print(ts.pop2() + " "); // Pop and print element from stack2 (should print -1 as stack2 is empty)
    }
}

```