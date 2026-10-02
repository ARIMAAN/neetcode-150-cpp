# Sorting

> **Time:** O(n log n) &nbsp;|&nbsp; **Space:** O(1)

---

## Intuition

Sort the array. Then scan linearly — if the next element is exactly 1 more than current, extend the streak. If it's the same (duplicate), skip it. If it's more than 1 away, reset the streak.

> First thing I tried. Simple to code and easy to understand, just doesn't hit O(n).

---

## Code

```cpp
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        if (nums.empty()) return 0;
        sort(nums.begin(), nums.end());

        int longest = 1, current = 1;

        for (int i = 1; i < nums.size(); i++) {
            if (nums[i] == nums[i - 1]) continue;       // skip duplicates
            if (nums[i] == nums[i - 1] + 1) current++;  // extend streak
            else current = 1;                            // reset streak
            longest = max(longest, current);
        }
        return longest;
    }
};
```

---

## Dry Run

**Input:** `nums = [2,20,4,10,3,4,5]`

After sort: `[2,3,4,4,5,10,20]`

| i | nums[i] | nums[i-1] | action | current | longest |
|---|---------|-----------|--------|---------|---------|
| 1 | 3 | 2 | extend | 2 | 2 |
| 2 | 4 | 3 | extend | 3 | 3 |
| 3 | 4 | 4 | skip dup | 3 | 3 |
| 4 | 5 | 4 | extend | 4 | 4 |
| 5 | 10 | 5 | reset | 1 | 4 |
| 6 | 20 | 10 | reset | 1 | 4 |

**Output:** `4` ✅

---

## Complexity

| | |
|--|--|
| **Time** | O(n log n) — dominated by sort |
| **Space** | O(1) — sorts in place |

> ⚠️ Doesn't meet the O(n) requirement. Use hash set approach for that.
