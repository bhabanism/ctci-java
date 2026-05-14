These classes provides two different approaches to solve the problem: **Check if one string is a permutation of another.** 

In the context of this repository, a permutation means that two strings have the same characters but in a different order (also known as an anagram).

### 1. Approach 1: Sorting (`permutation` method)
This is the simplest conceptual approach. If two strings are permutations, they must contain the exact same characters in the exact same quantities. Therefore, if you sort both strings, they should be identical.

*   **`sort(String s)`**: This helper method converts the string to a `char[]`, sorts it using `java.util.Arrays.sort()`, and returns a new string from the sorted array.
*   **`permutation(String s, String t)`**: It calls `sort()` on both inputs and returns `true` if the resulting strings are equal.
*   **Time Complexity**: $O(N \log N)$ due to the sorting algorithm.

---

### 2. Approach 2: Character Counting (`anagram` method)
This is a more efficient approach that uses a frequency map (an array) to count how many times each character appears.

*   **Length Check (Line 15)**: If the strings have different lengths, they cannot be permutations, so it returns `false` immediately.
*   **Frequency Array (Line 17)**: It initializes an array `letters` of size 128 (assuming standard ASCII).
*   **Step 1: Counting `s`**: It iterates through the first string `s`, incrementing the count for each character in the `letters` array. It also tracks `num_unique_chars`.
*   **Step 2: Comparing `t`**: It iterates through the second string `t`:
    *   If it encounters a character that has a count of 0 in `letters`, it means `t` contains a character not in `s` (or more occurrences of it), so it returns `false`.
    *   Otherwise, it decrements the count. 
    *   **Early Exit**: If a character's count hits exactly 0, it increments `num_completed_t`. Once `num_completed_t` matches `num_unique_chars`, it knows all characters are matched and returns `true`.
*   **Time Complexity**: $O(N)$, where $N$ is the length of the strings. This is faster than sorting for large strings.

### Summary of differences
| Method | Logic | Time Complexity | Space Complexity |
| :--- | :--- | :--- | :--- |
| `permutation` | Sort both strings and compare. | $O(N \log N)$ | $O(N)$ |
| `anagram` | Count character frequencies. | $O(N)$ | $O(1)$ (fixed size array) |

> [!NOTE]
> The `anagram` method in this file uses a slightly more complex tracking system (`num_unique_chars`) than the typical implementation, but the core logic remains a linear frequency check.