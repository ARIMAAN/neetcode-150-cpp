# Prefix / Suffix Arrays

> **Time:** O(n) &nbsp;|&nbsp; **Space:** O(n)

---

## Intuition

For each index, water = `min(maxLeft, maxRight) - height[i]`. Precompute the max to the left and max to the right for every index, then sum up the water at each bar.

---

## Code

```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        int n = height.size();
        vector<int> leftMax(n), rightMax(n);

        leftMax[0] = height[0];
        for (int i = 1; i < n; i++)
            leftMax[i] = max(leftMax[i - 1], height[i]);

        rightMax[n - 1] = height[n - 1];
        for (int i = n - 2; i >= 0; i--)
            rightMax[i] = max(rightMax[i + 1], height[i]);

        int water = 0;
        for (int i = 0; i < n; i++)
            water += min(leftMax[i], rightMax[i]) - height[i];

        return water;
    }
};
```

---

## Dry Run

**Input:** `height = [0,2,0,3,1,0,1,3,2,1]`

| i | height | leftMax | rightMax | min | water |
|---|--------|---------|----------|-----|-------|
| 0 | 0 | 0 | 3 | 0 | 0 |
| 1 | 2 | 2 | 3 | 2 | 0 |
| 2 | 0 | 2 | 3 | 2 | 2 |
| 3 | 3 | 3 | 3 | 3 | 0 |
| 4 | 1 | 3 | 3 | 3 | 2 |
| 5 | 0 | 3 | 3 | 3 | 3 |
| 6 | 1 | 3 | 3 | 3 | 2 |
| 7 | 3 | 3 | 3 | 3 | 0 |
| 8 | 2 | 3 | 2 | 2 | 0 |
| 9 | 1 | 3 | 1 | 1 | 0 |

Total = 0+0+2+0+2+3+2+0+0+0 = **9** ✅

---

## Complexity

| | |
|--|--|
| **Time** | O(n) — three passes |
| **Space** | O(n) — two extra arrays |

> Clean and easy to understand. Can we eliminate the extra arrays?

---

## Order Matters: Update Max Before Adding Water

```cpp
leftMax[i] = max(leftMax[i-1], height[i]);
water += min(leftMax[i], rightMax[i]) - height[i];
```

The max must include the current bar itself, otherwise we'd compute negative water at peaks.
