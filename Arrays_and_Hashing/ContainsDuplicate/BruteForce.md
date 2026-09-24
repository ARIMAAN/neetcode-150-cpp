# Brute Force

> **Time:** O(n²) &nbsp;|&nbsp; **Space:** O(1)

---

## Intuition

Check every pair of distinct indices `(i, j)` where `i < j`. If `nums[i] == nums[j]` for any pair, a duplicate exists. No extra space needed, but slow for large inputs.

---

## Algorithm

1. Use an outer loop with pointer `i` from `0` to `n-1`.
2. Use an inner loop with pointer `j` from `i+1` to `n-1`.
3. If `nums[i] == nums[j]`, return `true`.
4. If all pairs checked with no match, return `false`.

---

## Code

```cpp
class Solution {
public:
    bool hasDuplicate(vector<int>& nums) {
        for (int i = 0; i < nums.size(); i++) {
            for (int j = i + 1; j < nums.size(); j++) {
                if (nums[i] == nums[j]) {
                    return true;
                }
            }
        }
        return false;
    }
};
```

---

## Dry Run

**Input:** `nums = [1, 2, 3, 3]`

| i | j | nums[i] | nums[j] | Match? |
|---|---|---------|---------|--------|
| 0 | 1 | 1 | 2 | ❌ |
| 0 | 2 | 1 | 3 | ❌ |
| 0 | 3 | 1 | 3 | ❌ |
| 1 | 2 | 2 | 3 | ❌ |
| 1 | 3 | 2 | 3 | ❌ |
| 2 | 3 | 3 | 3 | ✅ → return `true` |

---

## Complexity

| | |
|--|--|
| **Time** | O(n²) — every pair is compared |
| **Space** | O(1) — no extra data structures |

> ⚠️ Will TLE on large inputs (`n = 10^5`).
