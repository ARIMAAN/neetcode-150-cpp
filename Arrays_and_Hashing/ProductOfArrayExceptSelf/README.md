# Product of Array Except Self

> **Difficulty:** Medium &nbsp;|&nbsp; **Topic:** Arrays & Hashing &nbsp;|&nbsp; [LeetCode #238](https://leetcode.com/problems/product-of-array-except-self/)

---

## Problem Statement

Given an integer array `nums`, return an array `answer` such that `answer[i]` is equal to the product of all elements of `nums` **except** `nums[i]`.

You must write an algorithm that runs in **O(n) time** and **without using the division operation**.

**Example 1:**
```
Input : nums = [1,2,3,4]
Output: [24,12,8,6]
```
**Example 2:**
```
Input : nums = [-1,1,0,-3,3]
Output: [0,0,9,0,0]
```

**Constraints:**
- `2 <= nums.length <= 10^5`
- `-30 <= nums[i] <= 30`
- Answer is guaranteed to fit in a 32-bit integer

---

## The Core Challenge

For each index `i`, we need the product of everything to its **left** × everything to its **right** — without dividing the total product by `nums[i]` (division is forbidden, and zeros break division anyway).

```
nums    =  [1,  2,  3,  4]
           ↑               ↑
        left product    right product
answer[i] = leftProduct[i] * rightProduct[i]
```

---

## Approaches

| # | Approach | Time | Space | File |
|---|----------|------|-------|------|
| 1 | Brute Force | O(n²) | O(1) | [BruteForce.md](./BruteForce.md) |
| 2 | Prefix & Suffix Arrays | O(n) | O(n) | [PrefixSuffix.md](./PrefixSuffix.md) |
| 3 | Prefix & Suffix O(1) Space ✅ | O(n) | O(1) | [OptimalTwoPass.md](./OptimalTwoPass.md) |

---

## Key Takeaway

> `answer[i] = product of all elements to the LEFT of i × product of all elements to the RIGHT of i`
> The O(1) space trick: use the output array itself to accumulate the left pass, then multiply the right pass in-place.
