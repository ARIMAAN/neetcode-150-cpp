# Greedy / Sliding Window ✅ Optimal

> **Time:** O(n) &nbsp;|&nbsp; **Space:** O(1)

---

## Intuition

Track the minimum price seen so far (`buyPrice`). For each day, compute profit if we sold today (`prices[i] - buyPrice`). Update the running max profit.

We never need to look back — if we find a lower price, we update our buy point. If we find a higher price, we check if it gives better profit.

---

## Why This Is Correct

At every index `i`, the best possible profit ending at `i` is `prices[i] - min(prices[0..i])`. We maintain that minimum on the fly, so we never miss the optimal buy point.

> We never need to reconsider a past sell day. If today's price is lower than our buy price, it's strictly better to buy today instead — any future sell will give more profit from today's price than from the old buy price.

---

## Code

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int buyPrice = prices[0];
        int profit = 0;

        for (int i = 1; i < prices.size(); i++) {
            if (buyPrice > prices[i]) {
                buyPrice = prices[i]; // found cheaper buy point
            }
            profit = max(profit, prices[i] - buyPrice); // best profit if sold today
        }
        return profit;
    }
};
```

---

## Dry Run

**Input:** `prices = [7,1,5,3,6,4]`

| i | prices[i] | buyPrice | profit = max(profit, p[i]-buy) |
|---|-----------|----------|-------------------------------|
| 0 | — | 7 | 0 (init) |
| 1 | 1 | 1 | max(0, 1-1) = 0 |
| 2 | 5 | 1 | max(0, 5-1) = 4 |
| 3 | 3 | 1 | max(4, 3-1) = 4 |
| 4 | 6 | 1 | max(4, 6-1) = 5 |
| 5 | 4 | 1 | max(5, 4-1) = 5 |

**Output:** `5` ✅

---

**Input:** `prices = [7,6,4,3,1]`

| i | prices[i] | buyPrice | profit |
|---|-----------|----------|--------|
| 0 | — | 7 | 0 |
| 1 | 6 | 6 | max(0, 6-6) = 0 |
| 2 | 4 | 4 | max(0, 4-4) = 0 |
| 3 | 3 | 3 | max(0, 3-3) = 0 |
| 4 | 1 | 1 | max(0, 1-1) = 0 |

**Output:** `0` ✅ (prices only decrease, never profitable)

---

## Sliding Window View

This can also be seen as a sliding window:
- `left` = buy day (min price so far)
- `right` = sell day (current day)
- If `prices[right] < prices[left]` → move left to right (found cheaper buy)
- Otherwise → compute area (profit) and update max

```
[7, 1, 5, 3, 6, 4]
 L
    L  R           → profit = 5-1 = 4
    L     R        → profit = 3-1 = 2
    L        R     → profit = 6-1 = 5 ← max
    L           R  → profit = 4-1 = 3
```

---

## Edge Cases

| Case | Output | Note |
|------|--------|------|
| Single element | 0 | Can't buy and sell same day |
| All decreasing | 0 | buyPrice keeps updating, profit stays 0 |
| All same | 0 | prices[i] - buyPrice = 0 always |
| All increasing | last - first | Buy on day 0, sell on last day |

---

## What If prices Has Only One Element?

```cpp
int buyPrice = prices[0]; // set to only element
for (int i = 1; i < prices.size(); i++) // loop never runs
return profit; // returns 0
```

Handled naturally — no special case needed.

---

## Complexity

| | |
|--|--|
| **Time** | O(n) — single pass |
| **Space** | O(1) — just two variables |
