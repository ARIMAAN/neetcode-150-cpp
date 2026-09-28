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

---

## Related Problems

| Problem | Connection |
|---------|------------|
| [692. Top K Frequent Words](https://leetcode.com/problems/top-k-frequent-words/) | Same pattern, strings instead of ints |
| [451. Sort Characters By Frequency](https://leetcode.com/problems/sort-characters-by-frequency/) | Bucket sort on char frequency |
| [973. K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/) | Top-k with min-heap on distance |

---

## Key Takeaway

> Bucket Sort wins here because frequency is bounded by `n`, turning an O(n log n) problem into O(n). Always ask: *"Is the value domain bounded?"* — if yes, counting/bucket sort is likely optimal.
