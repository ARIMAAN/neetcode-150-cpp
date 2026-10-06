# Container With Most Water

> **Difficulty:** Medium &nbsp;|&nbsp; **Topic:** Two Pointers &nbsp;|&nbsp; [LeetCode #11](https://leetcode.com/problems/container-with-most-water/)

---

## Problem Statement

Given an integer array `height` of length `n`, find two lines that together with the x-axis form a container that holds the most water. Return the maximum area.

```
area = min(height[left], height[right]) * (right - left)
```

**Example 1:**
```
Input : height = [1,8,6,2,5,4,8,3,7]
Output: 49
```
**Example 2:**
```
Input : height = [1,1]
Output: 1
```

**Constraints:**
- `n == height.length`
- `2 <= n <= 10^5`
- `0 <= height[i] <= 10^4`

---

## Approaches

| # | Approach | Time | Space | File |
|---|----------|------|-------|------|
| 1 | Brute Force | O(n²) | O(1) | [BruteForce.md](./BruteForce.md) |
| 2 | Two Pointers ✅ | O(n) | O(1) | [TwoPointers.md](./TwoPointers.md) |

---

## Key Insight

> Always move the pointer with the **shorter** height. Moving the taller one can only decrease or maintain width while the height is still bounded by the shorter — so it can never improve the area.
