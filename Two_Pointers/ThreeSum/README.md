# 3Sum

> **Difficulty:** Medium &nbsp;|&nbsp; **Topic:** Two Pointers &nbsp;|&nbsp; [LeetCode #15](https://leetcode.com/problems/3sum/)

---

## Problem Statement

Given an integer array `nums`, return all triplets `[nums[i], nums[j], nums[k]]` such that they sum to `0` and all indices are distinct. No duplicate triplets in output.

**Example 1:**
```
Input : nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
```
**Example 2:**
```
Input : nums = [0,1,1]
Output: []
```
**Example 3:**
```
Input : nums = [0,0,0]
Output: [[0,0,0]]
```

**Constraints:**
- `3 <= nums.length <= 3000`
- `-10^5 <= nums[i] <= 10^5`

---

## Approaches

| # | Approach | Time | Space | File |
|---|----------|------|-------|------|
| 1 | Brute Force | O(n³) | O(1) | [BruteForce.md](./BruteForce.md) |
| 2 | Sort + Two Pointers ✅ | O(n²) | O(1) | [SortTwoPointers.md](./SortTwoPointers.md) |

---

## Key Insight

> Fix one element, then use two pointers on the rest (like Two Sum II). Sort first to enable two pointers and make duplicate skipping easy.
