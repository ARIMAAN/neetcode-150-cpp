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

## Related Problems

| Problem | Connection |
|---------|------------|
| [167. Two Sum II](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/) | Inner loop of 3Sum |
| [18. 4Sum](https://leetcode.com/problems/4sum/) | Same pattern, one more outer loop |
| [16. 3Sum Closest](https://leetcode.com/problems/3sum-closest/) | Same structure, track closest sum |

---

## Key Insight

> Fix one element, then use two pointers on the rest (like Two Sum II). Sort first to enable two pointers and make duplicate skipping easy.

---

## Why Is Duplicate Skipping Tricky?

Consider `[-1,-1,-1,0,1,2]`:
- i=0 gives triplet [-1,0,1]
- i=1 is also -1 → would give same triplet again
- i=2 is also -1 → same again

We skip i=1 and i=2 with `if (i > 0 && nums[i] == nums[i-1]) continue`.

Same logic applies to left and right pointers after finding a valid triplet.
