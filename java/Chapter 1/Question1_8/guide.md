This class implements an algorithm to determine if one string is a **rotation** of another (e.g., `"waterbottle"` is a rotation of `"erbottlewat"`) using only one call to a substring helper method.

### Logic Breakdown

#### 1. The Core Trick: `s1 + s1`
The most critical part of the logic is in the `isRotation` method:
```java
String s1s1 = s1 + s1;
return isSubstring(s1s1, s2);
```
If `s2` is a rotation of `s1`, it means `s1` was split at some point $x$ into two parts, $A$ and $B$, such that $s1 = AB$ and $s2 = BA$. 
*   Example: $s1 = \text{"waterbottle"}$
*   $A = \text{"wat"}$, $B = \text{"erbottle"}$
*   $s2 = BA = \text{"erbottlewat"}$

By concatenating $s1$ with itself ($s1s1 = ABAB$), the rotated string $BA$ will **always** appear as a substring in the middle ($A[BA]B$).

#### 2. `isRotation(String s1, String s2)`
*   **Length Check**: It first checks if `s1` and `s2` have the same length and are not empty. If lengths differ, a rotation is impossible.
*   **Concatenation**: It creates `s1s1`.
*   **Substring Check**: it calls `isSubstring` to see if `s2` exists within `s1s1`.

#### 3. `isSubstring(String big, String small)`
*   This is a simple wrapper around Java's built-in `indexOf()` method. If `indexOf` returns a value $\ge 0$, the string was found.

#### 4. `main(String[] args)`
*   It tests the logic with three pairs:
    *   `apple` / `pleap`: **True** (Rotation)
    *   `waterbottle` / `erbottlewat`: **True** (Rotation)
    *   `camera` / `macera`: **False** (Permutation, but not a rotation)

### Complexity Analysis
*   **Time Complexity**: $O(N)$, where $N$ is the length of the strings. The concatenation takes $O(N)$ and `indexOf` (depending on the JVM implementation) generally performs in $O(N)$ or $O(N+M)$.
*   **Space Complexity**: $O(N)$ to store the newly created `s1s1` string.