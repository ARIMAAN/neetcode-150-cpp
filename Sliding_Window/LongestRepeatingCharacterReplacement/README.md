# Longest Repeating Character Replacement

**LeetCode #424** | **Difficulty**: Medium | **Topic**: Sliding Window

---

## Problem Statement

Given a string `s` of only uppercase English characters and an integer `k`, you can replace **at most k characters** in the string with any uppercase character.

Return the length of the longest substring that contains only one distinct character after at most `k` replacements.

**Examples**:

| Input | k | Output | Explanation |
|-------|---|--------|-------------|
| `"XYYX"` | 2 | 4 | Replace both X's with Y (or both Y's with X) |
| `"AAABABB"` | 1 | 5 | `"AABAB"` → replace one B → `"AAAAB"` or `"AABAA"` |

**Constraints**:
- `1 <= s.length <= 100,000`
- `0 <= k <= s.length`
- `s` consists of only uppercase English characters

---

## Approaches

| Approach | Time | Space | Notes |
|----------|------|-------|-------|
| Brute Force | O(n² · 26) | O(26) | check every substring |
| Sliding Window | O(n) | O(26) | track max frequency char in window |

---

## Key Insight

For a window of length `L`, the minimum replacements needed = `L - maxFreq`
where `maxFreq` is the count of the most frequent character in the window.

If `L - maxFreq <= k`, the window is valid.

---

## Why maxFreq Works

We want to keep as many of one character as possible and replace the rest.
The best character to keep is the one that appears most — that minimizes replacements.
So: `replacements needed = windowSize - count of most frequent char`.

---

## Related Problems

- [Longest Substring Without Repeating Characters (#3)](../LongestSubstringWithoutRepeatingCharacters/) — sliding window, shrink on duplicate
- [Permutation in String (#567)](../PermutationInString/) — fixed-size sliding window
- [Minimum Window Substring (#76)](../MinimumWindowSubstring/) — harder sliding window
