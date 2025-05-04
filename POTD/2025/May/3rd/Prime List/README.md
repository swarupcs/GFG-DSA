## Prime List


https://www.geeksforgeeks.org/problems/prime-list--170646/1
<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 14pt;">You are given the head of a linked list. You have to replace all the values of the nodes with the nearest <strong>prime</strong> number. If more than one prime number exists at an equal distance, choose the <strong>smallest</strong> one. Return the <strong>head</strong> of the modified linked list.</span></p>
<p><span style="font-size: 14pt;"><strong>Examples :</strong></span></p>
<pre><span style="font-size: 14pt;"><strong>Input: </strong>head =<strong> </strong>2 → 6 → 10
<strong>Output: </strong>2 → 5 → 11<br><img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/713591/Web/Other/blobid0_1723009310.png" width="267" height="167"><br><strong>Explanation: </strong>The nearest prime of 2 is 2 itself. The nearest primes of 6 are 5 and 7, since 5 is smaller so, 5 will be chosen. The nearest prime of 10 is 11.</span></pre>
<pre><span style="font-size: 14pt;"><strong>Input: </strong>head =<strong> </strong>1 → 15 → 20
<strong>Output: </strong>2 → 13 → 19<br><img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/713591/Web/Other/blobid1_1723009344.png" width="266" height="166"><br><strong>Explanation: </strong>The nearest prime of 1 is 2. The nearest primes of 15 are 13 and 17, since 13 is smaller so, 13 will be chosen. The nearest prime of 20 is 19.</span></pre>
<p><span style="font-size: 14pt;"><strong>Constraints:</strong><br>1 &lt;= no. of Nodes &lt;= 10<sup>4</sup><br>1 &lt;= node.val &lt;= 10<sup>4</sup></span></p></div>

<div class="problems_accordion_tags__JJ2DX problems_active_tags__3RExF"><div class="active title problems_active_tag_title__cgl9e"><div class="problems_tag_container__kWANg"><strong>Expected Complexities</strong></div></div><div class="content active animated_content open"><div class="problems_expected_complexities_text__h_eyi"><div class="problems_normal_text__QiKrb">Time Complexity: O(n * sqrt(node.val))</div><div class="problems_normal_text__QiKrb">Auxiliary Space: O(1)</div></div></div><div class="ui divider g-mt-3"></div></div>

## Solutions

#### Key Points:
```


```

Here's a detailed, interview-friendly solution to the **"Replace each node with the nearest prime"** problem using:

* ✅ **Time Complexity**: `O(n * sqrt(val))`
* ✅ **Auxiliary Space**: `O(1)`
* ✅ No sieve (space efficient)
* ✅ Step-by-step **approach**, **algorithm**, **dry run**, and **code comments**

---

## ✅ Problem Summary

You're given the head of a singly linked list. Replace each node's value with its **nearest prime number**. If two primes are equidistant, pick the **smaller** one.

---

## ✅ Intuition

A number might not be a prime, so to make the list "prime-only", we must replace non-primes with the **closest** prime. Since we cannot use extra space (no Sieve), we manually check primality using the `O(sqrt(n))` method.

---

## ✅ Approach

1. Traverse the linked list node by node.
2. For each node's value:

   * If it's already a prime, leave it.
   * Otherwise, expand outward (left and right) to find the closest prime.
   * Choose the **smaller one** if both distances are equal.
3. Replace the node value and continue.

---

## ✅ Algorithm (Step-by-Step)

1. Define `isPrime(n)` to check if a number is prime using trial division up to `sqrt(n)`.
2. Define `findNearestPrime(val)`:

   * If `val` is prime → return it.
   * Initialize `left = val - 1`, `right = val + 1`.
   * Loop outward: return `left` or `right` as soon as a prime is found (favor `left` if both are equidistant).
3. Traverse the linked list.

   * For each node: replace `node.val = findNearestPrime(node.val)`
4. Return the modified list.

---

## ✅ Java Code (With Detailed Comments)

```java
// Assume this is given:
// class Node {
//     int val;
//     Node next;
//     Node(int val) { this.val = val; }
// }

class Solution {
    
    // Function to check if a number is prime
    private boolean isPrime(int num) {
        if (num < 2) return false; // 0 and 1 are not prime
        for (int i = 2; i * i <= num; i++) {
            if (num % i == 0) return false; // Found a divisor → not prime
        }
        return true;
    }

    // Function to find the nearest prime number to a given value
    private int findNearestPrime(int val) {
        // If the number itself is prime, return it
        if (isPrime(val)) return val;

        // Initialize pointers to search left and right
        int left = val - 1;
        int right = val + 1;

        // Expand outward until we find the nearest prime
        while (true) {
            // Prefer the smaller prime in case of tie
            if (left >= 2 && isPrime(left)) return left;
            if (isPrime(right)) return right;
            left--;
            right++;
        }
    }

    // Main function to replace all node values with nearest prime
    Node primeList(Node head) {
        // Start with the head node
        Node current = head;

        // Traverse the linked list
        while (current != null) {
            // Replace value with nearest prime
            current.val = findNearestPrime(current.val);
            current = current.next; // Move to the next node
        }

        // Return the modified list head
        return head;
    }
}
```

---

## ✅ Dry Run Example

### Input:

```
head = 1 → 15 → 20
```

### Processing:

1 → not prime → nearest = 2
15 → not prime → nearest = 13 (13 and 17 equally distant, pick 13)
20 → not prime → nearest = 19

### Output:

```
2 → 13 → 19
```

---

## ✅ Time and Space Complexity

| Metric | Complexity                |
| ------ | ------------------------- |
| Time   | O(n \* √val)              |
| Space  | O(1) auxiliary (in-place) |

---






























