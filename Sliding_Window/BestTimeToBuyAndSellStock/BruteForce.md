# Brute Force

> **Time:** O(n²) &nbsp;|&nbsp; **Space:** O(1)

---

## Intuition

Try every pair (buy day, sell day) where buy < sell. Track the maximum profit.

---

## Code

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int profit = 0;

        for (int i = 0; i < prices.size(); i++) {
            for (int j = i + 1; j < prices.size(); j++) {
                profit = max(profit, prices[j] - prices[i]);
            }
        }
        return profit;
    }
};
```

---

## Dry Run

**Input:** `prices = [7,1,5,3,6,4]`

| buy(i) | sell(j) | profit | max |
|--------|---------|--------|-----|
| 7 | 1 | -6 | 0 |
| 7 | 5 | -2 | 0 |
| 1 | 5 | 4 | 4 |
| 1 | 3 | 2 | 4 |
| 1 | 6 | 5 | 5 |
| 1 | 4 | 3 | 5 |

**Output:** `5` ✅

---

## Complexity

| | |
|--|--|
| **Time** | O(n²) — every pair checked |
| **Space** | O(1) |

> ⚠️ TLE for n = 10^5.
