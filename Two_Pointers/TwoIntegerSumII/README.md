# Two Integer Sum II

> **Difficulty:** Medium &nbsp;|&nbsp; **Topic:** Two Pointers &nbsp;|&nbsp; [LeetCode #167](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)

---

## Problem Statement

Given a **sorted** array `numbers`, return the 1-indexed indices `[index1, index2]` of two numbers that add up to `target`.

- `index1 < index2`
- Cannot use the same element twice
- Exactly one valid solution always exists
- Must use **O(1) extra space**

**Example:**
```
Input : numbers = [1,2,3,4], target = 3
Output: [1,2]   (1 + 2 = 3)
```

**Constraints:**
- `2 <= numbers.length <= 30000`
- `-1000 <= numbers[i] <= 1000`
- `-1000 <= target <= 1000`

---

## Approaches

| # | Approach | Time | Space | File |
|---|----------|------|-------|------|
| 1 | Hash Map | O(n) | O(n) | [HashMap.md](./HashMap.md) |
| 2 | Two Pointers ✅ | O(n) | O(1) | [TwoPointers.md](./TwoPointers.md) |

---

## Related Problems

| Problem | Connection |
|---------|------------|
| [1. Two Sum](https://leetcode.com/problems/two-sum/) | Unsorted version, needs hash map |
| [15. 3Sum](https://leetcode.com/problems/3sum/) | Fix one element, two pointers for the rest |
| [11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/) | Same two pointer shrinking pattern |

---

## Key Insight

> The array is **sorted** — this is the hint. A sorted array lets us use two pointers: if the sum is too big, move right pointer left. If too small, move left pointer right.

---

## Difference From Two Sum I

| | Two Sum I | Two Sum II |
|--|-----------|------------|
| Array sorted? | No | Yes |
| Space allowed | O(n) | O(1) |
| Approach | Hash map | Two pointers |
| Indices | 0-indexed | 1-indexed |
