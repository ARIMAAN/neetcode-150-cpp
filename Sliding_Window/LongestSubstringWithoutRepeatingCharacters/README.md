# Longest Substring Without Repeating Characters

**LeetCode #3** | **Difficulty**: Medium | **Topic**: Sliding Window

---

## Problem Statement

Given a string `s`, find the length of the longest substring without duplicate characters.

**Examples**:

| Input | Output | Explanation |
|-------|--------|-------------|
| `"abcabcbb"` | `3` | `"abc"` |
| `"bbbbb"` | `1` | `"b"` |
| `"pwwkew"` | `3` | `"wke"` |

**Constraints**:
- `0 <= s.length <= 10^5`
- `s` consists of English letters, digits, symbols and spaces

---

## Approaches

| Approach | Time | Space | Notes |
|----------|------|-------|-------|
| Brute Force | O(n²) | O(n) | check every substring |
| Sliding Window + Set | O(n) | O(n) | shrink window on duplicate |

---

## Key Insight

Use a sliding window with a set to track characters in the current window.
When a duplicate is found, shrink from the left until it's gone.
The answer is the max window size seen at any point.

---

## Why a Set and Not Just Counting?

We need O(1) lookup to check if a character is already in the window.
A set gives us that — and we can add/remove as the window expands/shrinks.

---

## Related Problems

- [Best Time to Buy and Sell Stock (#121)](../BestTimeToBuyAndSellStock/) — sliding window on array
- [Longest Repeating Character Replacement (#424)](../LongestRepeatingCharacterReplacement/) — sliding window with frequency count
- [Permutation in String (#567)](../PermutationInString/) — fixed-size sliding window
