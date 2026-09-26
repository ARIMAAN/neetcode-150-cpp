# Brute Force

> **Time:** O(n²) &nbsp;|&nbsp; **Space:** O(1)

---

## Intuition

Check every pair `(i, j)` where `i < j`. If `nums[i] + nums[j] == target`, return `[i, j]`. No extra space needed but slow for large inputs.

---

## Algorithm

1. Use an outer loop with pointer `i` from `0` to `n-1`.
2. Use an inner loop with pointer `j` from `i+1` to `n-1`.
3. If `nums[i] + nums[j] == target`, return `{i, j}`.

---

## Code

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        for (int i = 0; i < nums.size(); i++) {
            for (int j = i + 1; j < nums.size(); j++) {
                if (nums[i] + nums[j] == target) {
                    return {i, j};
                }
            }
        }
        return {};
    }
};
```

---

## Dry Run

**Input:** `nums = [2, 7, 11, 15]`, `target = 9`

| i | j | nums[i] | nums[j] | Sum | == target? |
|---|---|---------|---------|-----|------------|
| 0 | 1 | 2 | 7 | 9 | ✅ → return `[0, 1]` |

---

**Input:** `nums = [3, 2, 4]`, `target = 6`

| i | j | nums[i] | nums[j] | Sum | == target? |
|---|---|---------|---------|-----|------------|
| 0 | 1 | 3 | 2 | 5 | ❌ |
| 0 | 2 | 3 | 4 | 7 | ❌ |
| 1 | 2 | 2 | 4 | 6 | ✅ → return `[1, 2]` |

---

## Complexity

| | |
|--|--|
| **Time** | O(n²) — every pair is checked |
| **Space** | O(1) — no extra data structures |

> ⚠️ Will TLE on large inputs (`n = 10^4`).
