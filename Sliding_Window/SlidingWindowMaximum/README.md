# Sliding Window Maximum

**LeetCode #239** | **Difficulty**: Hard | **Topic**: Sliding Window

---

## Problem Statement

Given an integer array `nums` and a sliding window of size `k`, return an array of the maximum value in each window position as it slides from left to right.

**Examples**:

| Input | k | Output |
|-------|---|--------|
| `[1,3,-1,-3,5,3,6,7]` | 3 | `[3,3,5,5,6,7]` |
| `[1]` | 1 | `[1]` |

**Constraints**:
- `1 <= nums.length <= 10^5`
- `-10^4 <= nums[i] <= 10^4`
- `1 <= k <= nums.length`

---

## Approaches

| Approach | Time | Space | Notes |
|----------|------|-------|-------|
| Brute Force | O(n · k) | O(1) | scan each window for max |
| Monotonic Deque | O(n) | O(k) | deque stores indices in decreasing order |

---

## Key Insight

Use a **monotonic deque** (decreasing) that stores indices.
The front of the deque is always the index of the maximum in the current window.
Before adding a new element, pop from the back any elements smaller than it — they can never be the max.

---

## Why a Deque?

We need two operations efficiently:
- Remove from front when the front index falls outside the window
- Remove from back when a new larger element makes old elements useless

A deque supports both O(1) front and back operations.

---

## Related Problems

- [Minimum Window Substring (#76)](../MinimumWindowSubstring/) — sliding window with maps
- [Jump Game (#55)](https://leetcode.com/problems/jump-game/) — greedy, similar thinking
