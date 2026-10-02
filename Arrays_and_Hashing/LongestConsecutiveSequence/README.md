# Longest Consecutive Sequence

> **Difficulty:** Medium &nbsp;|&nbsp; **Topic:** Arrays & Hashing &nbsp;|&nbsp; [LeetCode #128](https://leetcode.com/problems/longest-consecutive-sequence/)

---

## Problem Statement

Given an array of integers `nums`, return the length of the longest consecutive sequence.

A consecutive sequence is where each element is exactly 1 greater than the previous. Elements don't need to be adjacent in the original array.

Must run in **O(n)** time.

**Example 1:**
```
Input : nums = [2,20,4,10,3,4,5]
Output: 4   (sequence: 2,3,4,5)
```
**Example 2:**
```
Input : nums = [0,3,2,5,4,6,1,1]
Output: 7   (sequence: 0,1,2,3,4,5,6)
```

**Constraints:**
- `0 <= nums.length <= 100,000`
- `-10^9 <= nums[i] <= 10^9`

---

## Why Sorting Doesn't Work Here (for O(n))

Sorting is O(n log n). The problem explicitly asks for O(n). The hash set approach achieves this by trading space for time — O(n) space to get O(n) time.

---

## Approaches

| # | Approach | Time | Space | File |
|---|----------|------|-------|------|
| 1 | Sorting | O(n log n) | O(1) | [Sorting.md](./Sorting.md) |
| 2 | Hash Set ✅ | O(n) | O(n) | [HashSet.md](./HashSet.md) |

---

## Key Takeaway

> The O(n) trick: put everything in a set, then only start counting from numbers that have no predecessor (`num-1` not in set). This guarantees each number is processed at most twice total.
