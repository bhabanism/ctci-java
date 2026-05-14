This class contains two different implementations to solve the problem: **"Is Unique: Implement an algorithm to determine if a string has all unique characters."**

Both methods assume the character set is **ASCII** (128 characters).

### 1. `isUniqueChars(String str)` — Bit Vector Approach
This version is the most space-efficient because it uses a single `int` as a bit vector to keep track of seen characters.

*   **Pigeonhole Principle (Lines 6-8):** If the string length exceeds 128, it *must* have duplicates (assuming a 128-character ASCII set), so it returns `false` immediately.
*   **The Bitmask (Lines 9-14):**
    *   `int checker = 0;`: This 32-bit integer acts as a collection of flags.
    *   `int val = str.charAt(i) - 'a';`: It calculates the distance from 'a'. **Note:** This specific implementation assumes the input is only lowercase 'a-z' (since an `int` only has 32 bits and there are 26 letters).
    *   `(checker & (1 << val)) > 0`: It shifts `1` to the left by `val` positions and uses a bitwise `AND`. If the result is greater than 0, it means that bit was already set (the character was seen before).
    *   `checker |= (1 << val)`: It uses a bitwise `OR` to set the bit at position `val` to `1`, marking the character as "seen".

### 2. `isUniqueChars2(String str)` — Boolean Array Approach
This is the standard approach using extra space to map character frequencies.

*   **Boolean Array (Line 22):** It creates a `boolean` array of size 128.
*   **Lookup (Lines 23-27):** For every character in the string, it checks the corresponding index in the `char_set`.
    *   If `char_set[val]` is already `true`, a duplicate is found $\rightarrow$ return `false`.
    *   Otherwise, set `char_set[val]` to `true`.

### Comparison
| Feature | `isUniqueChars` | `isUniqueChars2` |
| :--- | :--- | :--- |
| **Time Complexity** | $O(n)$ | $O(n)$ |
| **Space Complexity**| $O(1)$ (1 integer) | $O(1)$ (128 booleans) |
| **Constraint** | Limited to 32 characters (e.g., lowercase a-z) | Works for all 128 ASCII characters |

Both methods effectively use a **Frequency Map** logic, but the bitwise version is a "compact" optimization of the boolean array.