# Two Sum

> **Difficulty:** Easy &nbsp;|&nbsp; **Topic:** Arrays & Hashing &nbsp;|&nbsp; [LeetCode #1](https://leetcode.com/problems/two-sum/)

---

## Problem Statement

Given an array of integers `nums` and an integer `target`, return the **indices** of the two numbers that add up to `target`.

You may assume that each input would have **exactly one solution**, and you may not use the same element twice.

**Example 1:**
```
Input : nums = [2, 7, 11, 15], target = 9
Output: [0, 1]
```

**Example 2:**
```
Input : nums = [3, 2, 4], target = 6
Output: [1, 2]
```

**Example 3:**
```
Input : nums = [3, 3], target = 6
Output: [0, 1]
```

**Constraints:**
- `2 <= nums.length <= 10^4`
- `-10^9 <= nums[i] <= 10^9`
- `-10^9 <= target <= 10^9`
- Only one valid answer exists.

---

## Approaches

| # | Approach | Time | Space | File |
|---|----------|------|-------|------|
| 1 | Brute Force | O(n²) | O(1) | [BruteForce.md](./BruteForce.md) |
| 2 | Sorting + Two Pointers | O(n log n) | O(n) | [Sorting.md](./Sorting.md) |
| 3 | Hash Map ✅ | O(n) | O(n) | [HashMap.md](./HashMap.md) |
