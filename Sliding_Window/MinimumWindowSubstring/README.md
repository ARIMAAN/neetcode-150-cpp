# Minimum Window Substring

**LeetCode #76** | **Difficulty**: Hard | **Topic**: Sliding Window

---

## Problem Statement

Given strings `s` and `t`, return the minimum window substring of `s` such that every character in `t` (including duplicates) is included in the window. If no such window exists, return `""`.

**Examples**:

| Input | Output | Explanation |
|-------|--------|-------------|
| s=`"ADOBECODEBANC"`, t=`"ABC"` | `"BANC"` | smallest window containing A, B, C |
| s=`"a"`, t=`"a"` | `"a"` | exact match |
| s=`"a"`, t=`"aa"` | `""` | only one 'a' in s, need two |

**Constraints**:
- `1 <= s.length, t.length <= 10^5`
- `s` and `t` consist of uppercase and lowercase English letters

---

## Approaches

| Approach | Time | Space | Notes |
|----------|------|-------|-------|
| Brute Force | O(n² · m) | O(m) | check every substring |
| Sliding Window | O(n + m) | O(m) | expand right, shrink left when valid |

---

## Key Insight

Use a variable-size sliding window. Expand right until the window contains all chars of `t`.
Then shrink from left as much as possible while still valid.
Record the minimum window seen. Repeat.

---

## The `have` / `need` Trick

Track `need` = number of unique chars in `t` that must be satisfied.
Track `have` = number of unique chars currently satisfied in the window.
A char is "satisfied" when its count in the window >= its count in `t`.
When `have == need`, the window is valid — try to shrink.

---

## Related Problems

- [Permutation in String (#567)](../PermutationInString/) — fixed window, easier version
- [Longest Substring Without Repeating Characters (#3)](../LongestSubstringWithoutRepeatingCharacters/) — variable window, simpler condition
- [Find All Anagrams in a String (#438)](https://leetcode.com/problems/find-all-anagrams-in-a-string/) — fixed window variant
