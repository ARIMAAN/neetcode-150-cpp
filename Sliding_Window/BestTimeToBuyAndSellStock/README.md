# Best Time to Buy and Sell Stock

> **Difficulty:** Easy &nbsp;|&nbsp; **Topic:** Sliding Window &nbsp;|&nbsp; [LeetCode #121](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

---

## Problem Statement

Given an array `prices` where `prices[i]` is the stock price on day `i`, return the maximum profit from one buy-sell transaction. Must buy before sell. Return `0` if no profit possible.

**Example 1:**
```
Input : prices = [7,1,5,3,6,4]
Output: 5   (buy at 1, sell at 6)
```
**Example 2:**
```
Input : prices = [7,6,4,3,1]
Output: 0   (prices only decrease)
```

**Constraints:**
- `1 <= prices.length <= 10^5`
- `0 <= prices[i] <= 10^4`

---

## Approaches

| # | Approach | Time | Space | File |
|---|----------|------|-------|------|
| 1 | Brute Force | O(n²) | O(1) | [BruteForce.md](./BruteForce.md) |
| 2 | Greedy / Sliding Window ✅ | O(n) | O(1) | [Greedy.md](./Greedy.md) |

---

## Key Insight

> Track the minimum price seen so far. At each day, the best profit is `currentPrice - minSoFar`. Keep a running max of that.
