# Contains Duplicate

> **Difficulty:** Easy &nbsp;|&nbsp; **Topic:** Arrays & Hashing &nbsp;|&nbsp; [LeetCode #217](https://leetcode.com/problems/contains-duplicate/)

---

## Problem Statement

Given an integer array `nums`, return `true` if any value appears **more than once**, otherwise return `false`.

**Example 1:**
```
Input : nums = [1, 2, 3, 3]
Output: true
```
**Example 2:**
```
Input : nums = [1, 2, 3, 4]
Output: false
```

**Constraints:**
- `0 <= nums.length <= 10^5`
- `-10^9 <= nums[i] <= 10^9`

---

## Approaches

| # | Approach | Time | Space | File |
|---|----------|------|-------|------|
| 1 | Brute Force | O(n²) | O(1) | [BruteForce.md](./BruteForce.md) |
| 2 | Sorting | O(n log n) | O(1) | [Sorting.md](./Sorting.md) |
| 3 | Hash Set ✅ | O(n) | O(n) | [HashSet.md](./HashSet.md) |
