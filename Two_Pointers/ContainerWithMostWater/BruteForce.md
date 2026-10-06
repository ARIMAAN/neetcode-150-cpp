# Brute Force

> **Time:** O(n²) &nbsp;|&nbsp; **Space:** O(1)

---

## Intuition

Try every pair of lines and compute the area. Track the maximum.

---

## Code

```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        int maxWater = 0;

        for (int i = 0; i < height.size(); i++) {
            for (int j = i + 1; j < height.size(); j++) {
                int area = min(height[i], height[j]) * (j - i);
                maxWater = max(maxWater, area);
            }
        }
        return maxWater;
    }
};
```

---

## Dry Run

**Input:** `height = [1,8,6,2,5,4,8,3,7]`

Checking a few pairs:
| i | j | min(h[i],h[j]) | width | area |
|---|---|----------------|-------|------|
| 0 | 8 | min(1,7)=1 | 8 | 8 |
| 1 | 8 | min(8,7)=7 | 7 | 49 |
| 1 | 6 | min(8,8)=8 | 5 | 40 |

Max found = 49 ✅

---

## Complexity

| | |
|--|--|
| **Time** | O(n²) — every pair checked |
| **Space** | O(1) |

> ⚠️ TLE for n = 10^5.
