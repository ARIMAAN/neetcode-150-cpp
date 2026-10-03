# Valid Palindrome

> **Difficulty:** Easy &nbsp;|&nbsp; **Topic:** Two Pointers &nbsp;|&nbsp; [LeetCode #125](https://leetcode.com/problems/valid-palindrome/)

---

## Problem Statement

Given a string `s`, return `true` if it is a palindrome, otherwise `false`.

A palindrome reads the same forward and backward. It is **case-insensitive** and **ignores all non-alphanumeric characters**.

**Example 1:**
```
Input : s = "Was it a car or a cat I saw?"
Output: true
Explanation: "wasitacaroracatisaw" is a palindrome
```
**Example 2:**
```
Input : s = "tab a cat"
Output: false
Explanation: "tabacat" is not a palindrome
```

**Constraints:**
- `1 <= s.length <= 1000`
- `s` consists of printable ASCII characters

---

## Related Problems

| Problem | Connection |
|---------|------------|
| [234. Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/) | Same two-pointer idea on a linked list |
| [5. Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/) | Expand around center |
| [680. Valid Palindrome II](https://leetcode.com/problems/valid-palindrome-ii/) | Can delete at most one character |

---

## Approaches

| # | Approach | Time | Space | File |
|---|----------|------|-------|------|
| 1 | Filter + Two Pointers | O(n) | O(n) | [FilterTwoPointers.md](./FilterTwoPointers.md) |
| 2 | Two Pointers In-Place ✅ | O(n) | O(1) | [TwoPointersInPlace.md](./TwoPointersInPlace.md) |

---

## Key Takeaway

> Two pointers is the go-to pattern for palindrome checks. The in-place version skips non-alphanumeric characters on the fly instead of building a new string.
