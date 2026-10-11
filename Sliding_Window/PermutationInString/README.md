# Permutation in String

**LeetCode #567** | **Difficulty**: Medium | **Topic**: Sliding Window

---

## Problem Statement

Given two strings `s1` and `s2`, return `true` if `s2` contains a permutation of `s1`, or `false` otherwise.

In other words, return `true` if any substring of `s2` is an anagram of `s1`.

**Examples**:

| Input | Output | Explanation |
|-------|--------|-------------|
| s1=`"ab"`, s2=`"eidbaooo"` | `true` | `"ba"` is a permutation of `"ab"` |
| s1=`"ab"`, s2=`"eidboaoo"` | `false` | no permutation of `"ab"` in `s2` |

**Constraints**:
- `1 <= s1.length, s2.length <= 10^4`
- `s1` and `s2` consist of lowercase English letters

---

## Approaches

| Approach | Time | Space | Notes |
|----------|------|-------|-------|
| Brute Force | O(n! · m) | O(n) | generate all permutations, check each |
| Sliding Window (freq array) | O(n + m) | O(26) | fixed-size window = len(s1) |

---

## Key Insight

A permutation of `s1` is just an anagram — same characters, different order.
So we need to find a window in `s2` of length `len(s1)` with the exact same character frequencies.

Use a **fixed-size sliding window** of size `len(s1)` and slide it across `s2`.
At each position, compare frequency arrays. If they match → found a permutation.

> Two strings are anagrams ↔ their sorted forms are equal ↔ their freq arrays are equal.
> Sorting would be O(n log n) per window. Freq array comparison is O(26) = O(1).

---

## Why Fixed-Size Window?

Unlike "longest substring" problems where window size varies,
here the target length is fixed: any valid permutation must have exactly `len(s1)` characters.
So we slide a window of exactly that size — no shrinking needed.

---

## Related Problems

- [Longest Repeating Character Replacement (#424)](../LongestRepeatingCharacterReplacement/) — variable size window
- [Minimum Window Substring (#76)](../MinimumWindowSubstring/) — variable size, harder version
- [Find All Anagrams in a String (#438)](https://leetcode.com/problems/find-all-anagrams-in-a-string/) — same idea, return all positions
