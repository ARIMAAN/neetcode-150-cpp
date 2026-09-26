# Hash Map ✅ Optimal

> **Time:** O(n) &nbsp;|&nbsp; **Space:** O(n)

---

## Intuition

For each element `nums[i]`, we need `target - nums[i]` to exist somewhere in the array. Store each number and its index in a hash map as we iterate. For every new element, check if its complement already exists in the map — if yes, we're done.

---

## Algorithm

1. Create an empty `unordered_map<int, int> prevMap` (value → index).
2. For each `i`, compute `diff = target - nums[i]`.
3. If `diff` exists in `prevMap`, return `{prevMap[diff], i}`.
4. Otherwise, store `nums[i] → i` in the map.

---

## Code

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> prevMap;
        for (int i = 0; i < nums.size(); i++) {
            int diff = target - nums[i];
            if (prevMap.count(diff)) {
                return {prevMap[diff], i};
            }
            prevMap[nums[i]] = i;
        }
        return {};
    }
};
```

---

## Dry Run

**Input:** `nums = [2, 7, 11, 15]`, `target = 9`

| i | nums[i] | diff = 9 - nums[i] | In map? | prevMap after |
|---|---------|---------------------|---------|---------------|
| 0 | 2 | 7 | ❌ | {2:0} |
| 1 | 7 | 2 | ✅ | → return `[0, 1]` |

---

**Input:** `nums = [3, 2, 4]`, `target = 6`

| i | nums[i] | diff = 6 - nums[i] | In map? | prevMap after |
|---|---------|---------------------|---------|---------------|
| 0 | 3 | 3 | ❌ | {3:0} |
| 1 | 2 | 4 | ❌ | {3:0, 2:1} |
| 2 | 4 | 2 | ✅ | → return `[1, 2]` |

---

## Complexity

| | |
|--|--|
| **Time** | O(n) — single pass |
| **Space** | O(n) — map stores up to n elements |
