## Asteroid Collision


https://www.geeksforgeeks.org/problems/asteroid-collision/1


<div class="problems_problem_content__Xm_eO"><p><span style="font-size:18px">We are given an integer array <strong>asteroids</strong>&nbsp;of size <strong>N</strong> representing asteroids in a row. For&nbsp;each asteroid, the absolute value represents its size, and the sign represents its direction (positive meaning right, negative meaning left). Each asteroid moves at the same speed.<br>
Find out the state of the asteroids after all collisions. If two asteroids meet, the smaller one will explode. If both are of&nbsp;same size, both will explode. Two asteroids moving in the same direction will never meet.</span><br>
&nbsp;</p>

<p><span style="font-size:18px"><strong>Example 1:</strong></span></p>

<div style=" border: 1px solid rgb(204, 204, 204); padding: 5px 10px; --darkreader-inline-bgimage: initial; --darkreader-inline-bgcolor:#222426; --darkreader-inline-border-top:#3e4446; --darkreader-inline-border-right:#3e4446; --darkreader-inline-border-bottom:#3e4446; --darkreader-inline-border-left:#3e4446;"><span style="font-size:18px"><strong>Input:</strong><br>
N = 3<br>
asteroids[ ] = {3,&nbsp;5, -3}<br>
<strong>Output:&nbsp;</strong>{3, 5}<br>
<strong>Explanation:</strong>&nbsp;The asteroid 5 and -3&nbsp;collide resulting in 5. The 5 and 3 never collide.</span></div>

<p><span style="font-size:18px"><strong>Example 2:</strong></span></p>

<div style=" border: 1px solid rgb(204, 204, 204); padding: 5px 10px; --darkreader-inline-bgimage: initial; --darkreader-inline-bgcolor:#222426; --darkreader-inline-border-top:#3e4446; --darkreader-inline-border-right:#3e4446; --darkreader-inline-border-bottom:#3e4446; --darkreader-inline-border-left:#3e4446;"><span style="font-size:18px"><strong>Input:</strong><br>
N = 2<br>
asteroids[ ] = {10, -10}<br>
<strong>Output:&nbsp;</strong>{ }<br>
<strong>Explanation:</strong>&nbsp;The asteroid -10&nbsp;and 10&nbsp;collide exploding each other.</span></div>

<p><span style="font-size:18px"><strong>Your Task:</strong><br>
You don't need to read input or print anything. Your task is to complete the function <strong>asteroidCollision()</strong>&nbsp;which takes the&nbsp;array of&nbsp;integers <strong>asteroids&nbsp;</strong>and <strong>N&nbsp;</strong>as parameters and returns the state of asteroids after all collisions.</span></p>

<p><span style="font-size:18px"><strong>Expected Time Complexity:</strong>&nbsp;O(N)<br>
<strong>Expected Auxiliary Space:</strong>&nbsp;O(N)</span></p>

<p><span style="font-size:18px"><strong>Constraints:</strong><br>
1 ≤ N ≤ 10<sup>5</sup><br>
-1000 ≤ asteroids<sub>i&nbsp; </sub>≤ 1000<br>
asteroids[i]!=0</span></p>
</div>

## Solutions

#### Key Points:
```


```


---

## ✅ **Intuition**

* Asteroids move in a line. Positive values move right, negative move left.
* Collisions happen **only between a right-moving asteroid and a left-moving one**.
* Use a **stack** to simulate this:

  * Push right-moving asteroids onto the stack.
  * When encountering a left-moving asteroid, simulate collisions:

    * Pop smaller right-moving asteroids.
    * Equal size: both explode.
    * If the stack is empty or the top is left-moving, the current asteroid survives.

---

## ✅ **Algorithm**

1. Create an empty stack (using `ArrayList`).
2. Traverse through the asteroid array.
3. For each asteroid:

   * If moving right (positive), push to stack.
   * If moving left:

     * Pop all smaller right-moving asteroids.
     * If same size asteroid exists, pop it too and break.
     * If stack is empty or top is left-moving, push current asteroid.
4. Convert the stack to array and return.

---

## ✅ **Completed Code with Comments**

```java
import java.util.*;

class Solution {
    // Function to find the state of asteroids after all collisions
    public static int[] asteroidCollision(int N, int[] asteroids) {
        // Using ArrayList as a dynamic stack
        List<Integer> st = new ArrayList<>();

        // Loop through each asteroid
        for (int i = 0; i < N; i++) {

            // If the asteroid is moving to the right, push to stack
            if (asteroids[i] > 0) {
                st.add(asteroids[i]);
            } 
            // If the asteroid is moving to the left
            else {
                // Resolve collisions while top of stack is smaller and moving right
                while (!st.isEmpty() && st.get(st.size() - 1) > 0 &&
                        st.get(st.size() - 1) < Math.abs(asteroids[i])) {
                    st.remove(st.size() - 1); // right asteroid destroyed
                }

                // If both are equal size, destroy both
                if (!st.isEmpty() && st.get(st.size() - 1) == Math.abs(asteroids[i])) {
                    st.remove(st.size() - 1); // both explode
                }
                // If no collision or left-moving on top, add current asteroid
                else if (st.isEmpty() || st.get(st.size() - 1) < 0) {
                    st.add(asteroids[i]); // survives
                }
                // Else, do nothing (current asteroid is destroyed)
            }
        }

        // Convert result list to array
        int[] result = new int[st.size()];
        for (int i = 0; i < st.size(); i++) {
            result[i] = st.get(i);
        }

        return result; // Return final asteroid state
    }

    // Test the implementation
    public static void main(String[] args) {
        int[] asteroids = {3, 5, -3}; // Example input

        int[] result = asteroidCollision(asteroids.length, asteroids);

        System.out.println("The state of asteroids after collisions is:");
        for (int num : result) {
            System.out.print(num + " ");
        }
    }
}
```

---

## ✅ **Dry Run of Example 1**

Input: `{3, 5, -3}`
Stack state trace:

| Step | Asteroid | Stack   | Action                             |
| ---- | -------- | ------- | ---------------------------------- |
| 1    | 3        | \[3]    | Move right → push                  |
| 2    | 5        | \[3, 5] | Move right → push                  |
| 3    | -3       | \[3, 5] | Collides with 5 → 5 wins → -3 gone |

✅ Output: `[3, 5]`

---

## ✅ Time and Space Complexity

* **Time Complexity:** `O(N)`
  Every asteroid is pushed/popped from stack **at most once**.

* **Space Complexity:** `O(N)`
  Stack may hold all asteroids in worst case (no collisions).

---





























