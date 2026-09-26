# Hash Map — Two Pass

> **Time:** O(n) &nbsp;|&nbsp; **Space:** O(n)

---

## Intuition

Split the work into two passes. First pass — build a complete map of all values and their indices. Second pass — for each element, check if its complement `target - nums[i]` exists in the map (making sure it's not the same index).

---

## Algorithm

1. First pass: insert all `nums[i] → i` into `unordered_map`.
2. Second pass: for each `i`, compute `diff = target - nums[i]`.
3. If `diff` exists in map **and** `map[diff] != i`, return `{i, map[diff]}`.

---

## Code

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> indices;
        for (int i = 0; i < nums.size(); i++) {
            indices[nums[i]] = i;
        }
        for (int i = 0; i < nums.size(); i++) {
            int diff = target - nums[i];
            if (indices.count(diff) && indices[diff] != i) {
                return {i, indices[diff]};
            }
        }
        return {};
    }
};
```

---

## Dry Run

**Input:** `nums = [3, 4, 5, 6]`, `target = 7`

**Pass 1 — Build map:**

| i | nums[i] | indices |
|---|---------|---------|
| 0 | 3 | {3:0} |
| 1 | 4 | {3:0, 4:1} |
| 2 | 5 | {3:0, 4:1, 5:2} |
| 3 | 6 | {3:0, 4:1, 5:2, 6:3} |

**Pass 2 — Find complement:**

| i | nums[i] | diff = 7 - nums[i] | In map? | indices[diff] != i? | Action |
|---|---------|---------------------|---------|----------------------|--------|
| 0 | 3 | 4 | ✅ | indices[4]=1 ≠ 0 ✅ | return `[0, 1]` |

---

## Complexity

| | |
|--|--|
| **Time** | O(n) — two separate passes |
| **Space** | O(n) — map stores all n elements |

> Difference from One Pass: builds the full map first, then searches. Slightly more straightforward but uses two loops.
