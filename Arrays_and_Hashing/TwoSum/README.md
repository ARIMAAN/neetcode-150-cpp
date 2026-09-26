# Two Sum

> **Difficulty:** Easy &nbsp;|&nbsp; **Topic:** Arrays & Hashing &nbsp;|&nbsp; [LeetCode #1](https://leetcode.com/problems/two-sum/)

---

## Problem Statement

Given an array of integers `nums` and an integer `target`, return the indices `i` and `j` such that `nums[i] + nums[j] == target` and `i != j`.

You may assume that every input has **exactly one pair** of indices. Return the answer with the **smaller index first**.

**Example 1:**
```
Input : nums = [3, 4, 5, 6], target = 7
Output: [0, 1]
```

**Example 2:**
```
Input : nums = [4, 5, 6], target = 10
Output: [0, 2]
```

**Example 3:**
```
Input : nums = [5, 5], target = 10
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
| 3 | Hash Map (Two Pass) | O(n) | O(n) | [HashMapTwoPass.md](./HashMapTwoPass.md) |
| 4 | Hash Map (One Pass) ✅ | O(n) | O(n) | [HashMapOnePass.md](./HashMapOnePass.md) |
