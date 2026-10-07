# Trapping Rain Water

> **Difficulty:** Hard &nbsp;|&nbsp; **Topic:** Two Pointers &nbsp;|&nbsp; [LeetCode #42](https://leetcode.com/problems/trapping-rain-water/)

---

## Problem Statement

Given an array `height` representing an elevation map where each bar has width 1, return the total water that can be trapped.

**Example:**
```
Input : height = [0,2,0,3,1,0,1,3,2,1]
Output: 9
```

**Constraints:**
- `1 <= height.length <= 20,000`
- `0 <= height[i] <= 100,000`

---

## Core Idea

Water at index `i` = `min(maxLeft, maxRight) - height[i]`

The water above any bar is bounded by the shorter of the tallest bar to its left and the tallest bar to its right.

```
water[i] = min(maxLeft[i], maxRight[i]) - height[i]
```

---

## Visual

```
height = [0,2,0,3,1,0,1,3,2,1]

         _       _
   _     | |     | |_
   |_  _ | | _ _ | | |_
   | || || || || || |  |
   0  2  0  3  1  0  1  3  2  1

water trapped (shown as ~):
         _       _
   _~~~~~| |~~~~~| |_
   |_~~_~| |~_~_~| |~|_
```

Total = 9

---

## Approaches

| # | Approach | Time | Space | File |
|---|----------|------|-------|------|
| 1 | Prefix/Suffix Arrays | O(n) | O(n) | [PrefixSuffix.md](./PrefixSuffix.md) |
| 2 | Two Pointers ✅ | O(n) | O(1) | [TwoPointers.md](./TwoPointers.md) |

---

## Related Problems

| Problem | Connection |
|---------|------------|
| [11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/) | Simpler version, same two pointer idea |
| [238. Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/) | Prefix/suffix array pattern |

---

## Key Insight

> If `leftMax < rightMax`, the water at the left pointer is determined by `leftMax` (the right side is guaranteed taller). Move left inward. Same logic applies symmetrically for the right side.
