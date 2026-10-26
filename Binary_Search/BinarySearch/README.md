# Binary Search

**LeetCode #704** | Difficulty: Easy | [Problem Link](https://leetcode.com/problems/binary-search/)

---

## Problem Statement

Given an array of integers `nums` sorted in ascending order, and an integer `target`, return the index of `target` if it exists, else return `-1`.

You must write an algorithm with `O(log n)` runtime complexity.

**Example 1:**
```
Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
```

**Example 2:**
```
Input: nums = [-1,0,3,5,9,12], target = 2
Output: -1
```

**Constraints:**
- `1 <= nums.length <= 10^4`
- `-10^4 < nums[i], target < 10^4`
- All integers in `nums` are unique
- `nums` is sorted in ascending order

---

## Approaches

| Approach | Time | Space | Notes |
|----------|------|-------|-------|
| [Brute Force](./BruteForce.md) | O(n) | O(1) | Linear scan |
| [Binary Search](./BinarySearch.md) | O(log n) | O(1) | Optimal — halve search space each step |

---

## Key Insight

The array is sorted — so if `nums[mid] < target`, everything to the left of `mid` is also less than target. We can safely discard the left half. Same logic applies to the right half. This halving is what gives us O(log n).

---

## Related Problems

- [Search a 2D Matrix (#74)](https://leetcode.com/problems/search-a-2d-matrix/) — binary search on flattened matrix
- [Find Minimum in Rotated Sorted Array (#153)](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) — modified binary search
- [Search in Rotated Sorted Array (#33)](https://leetcode.com/problems/search-in-rotated-sorted-array/) — binary search with rotation handling
- [Koko Eating Bananas (#875)](https://leetcode.com/problems/koko-eating-bananas/) — binary search on answer space
