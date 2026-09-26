# Sorting + Two Pointers

> **Time:** O(n log n) &nbsp;|&nbsp; **Space:** O(n)

---

## Intuition

Sort the array while keeping track of original indices. Use two pointers — one at the start, one at the end. If the sum is too small, move left pointer right. If too large, move right pointer left. Stop when they meet.

---

## Algorithm

1. Create a list of `(value, original_index)` pairs.
2. Sort by value.
3. Use two pointers `l = 0`, `r = n-1`.
4. If `nums[l] + nums[r] == target`, return their original indices.
5. If sum < target, increment `l`.
6. If sum > target, decrement `r`.

---

## Code

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<pair<int, int>> sorted;
        for (int i = 0; i < nums.size(); i++) {
            sorted.push_back({nums[i], i});
        }
        sort(sorted.begin(), sorted.end());

        int l = 0, r = sorted.size() - 1;
        while (l < r) {
            int sum = sorted[l].first + sorted[r].first;
            if (sum == target) {
                return {sorted[l].second, sorted[r].second};
            } else if (sum < target) {
                l++;
            } else {
                r--;
            }
        }
        return {};
    }
};
```

---

## Dry Run

**Input:** `nums = [3, 2, 4]`, `target = 6`

After sorting with indices: `[(2,1), (3,0), (4,2)]`

| l | r | sorted[l] | sorted[r] | Sum | Action |
|---|---|-----------|-----------|-----|--------|
| 0 | 2 | (2,1) | (4,2) | 6 | ✅ → return `[1, 2]` |

---

## Complexity

| | |
|--|--|
| **Time** | O(n log n) — dominated by sort |
| **Space** | O(n) — extra array to store index pairs |

> ⚠️ Extra space needed to preserve original indices after sorting.
