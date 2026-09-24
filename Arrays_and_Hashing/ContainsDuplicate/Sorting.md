# Sorting

> **Time:** O(n log n) &nbsp;|&nbsp; **Space:** O(1)

---

## Intuition

If we sort the array, duplicate values will always end up **adjacent** to each other. A single pass checking `nums[i] == nums[i+1]` is enough. Better than brute force, but modifies the original array.

---

## Algorithm

1. Sort the array in ascending order.
2. Iterate from index `0` to `n-2`.
3. If `nums[i] == nums[i+1]`, return `true`.
4. If no adjacent duplicates found, return `false`.

---

## Code

```cpp
class Solution {
public:
    bool hasDuplicate(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        for (int i = 0; i + 1 < nums.size(); i++) {
            if (nums[i] == nums[i + 1]) {
                return true;
            }
        }
        return false;
    }
};
```

---

## Dry Run

**Input:** `nums = [1, 2, 3, 3]`

**After sort:** `[1, 2, 3, 3]`

| i | nums[i] | nums[i+1] | Match? |
|---|---------|-----------|--------|
| 0 | 1 | 2 | ❌ |
| 1 | 2 | 3 | ❌ |
| 2 | 3 | 3 | ✅ → return `true` |

---

## Complexity

| | |
|--|--|
| **Time** | O(n log n) — dominated by sort |
| **Space** | O(1) — in-place sort |

> ⚠️ Modifies the original array. Use a copy if the input must be preserved.
