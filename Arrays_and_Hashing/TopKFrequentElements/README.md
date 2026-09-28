# Top K Frequent Elements

> **Difficulty:** Medium &nbsp;|&nbsp; **Topic:** Arrays & Hashing &nbsp;|&nbsp; [LeetCode #347](https://leetcode.com/problems/top-k-frequent-elements/)

---

## Problem Statement

Given an integer array `nums` and an integer `k`, return the `k` most frequent elements within the array.

The test cases are generated such that the answer is always unique. You may return the output in any order.

**Example 1:**
```
Input : nums = [1,2,2,3,3,3], k = 2
Output: [2,3]
```
**Example 2:**
```
Input : nums = [7,7], k = 1
Output: [7]
```

**Constraints:**
- `1 <= nums.length <= 10^5`
- `-10^4 <= nums[i] <= 10^4`
- `1 <= k <= number of unique elements`
- Answer is always unique

---

## Approaches

| # | Approach | Time | Space | File |
|---|----------|------|-------|------|
| 1 | Brute Force (Sort by Freq) | O(n log n) | O(n) | [BruteForce.md](./BruteForce.md) |
| 2 | Min-Heap | O(n log k) | O(n) | [MinHeap.md](./MinHeap.md) |
| 3 | Bucket Sort ✅ | O(n) | O(n) | [BucketSort.md](./BucketSort.md) |
