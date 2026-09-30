# Brute Force

> **Time:** O(n²) &nbsp;|&nbsp; **Space:** O(1)

---

## Intuition

For every index `i`, iterate through the entire array and multiply all elements except `nums[i]`. Simple and direct, but checks every pair — quadratic time.

---

## Algorithm

1. For each index `i` from `0` to `n-1`:
   - Initialize `product = 1`.
   - For each index `j`, if `j != i`, multiply `product *= nums[j]`.
   - Set `answer[i] = product`.
2. Return `answer`.

---

## Code

```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n = nums.size();
        vector<int> answer(n);

        for (int i = 0; i < n; i++) {
            int product = 1;
            for (int j = 0; j < n; j++) {
                if (j != i) product *= nums[j]; // skip index i
            }
            answer[i] = product;
        }
        return answer;
    }
};
```

---

## Dry Run

**Input:** `nums = [1,2,3,4]`

| i | j skipped | product | answer[i] |
|---|-----------|---------|-----------|
| 0 | 0 | 2×3×4 | 24 |
| 1 | 1 | 1×3×4 | 12 |
| 2 | 2 | 1×2×4 | 8 |
| 3 | 3 | 1×2×3 | 6 |

**Output:** `[24,12,8,6]` ✅

---

## Complexity

| | |
|--|--|
| **Time** | O(n²) — nested loop over all pairs |
| **Space** | O(1) — no extra space beyond output |

> ⚠️ Will TLE for `n = 10^5`. Division is not used but time constraint is violated.

---

## When Is Brute Force Acceptable?

- `n` is very small (e.g. `n <= 100` in a non-competitive context)
- Used as a **verifier** to cross-check the optimal solution during testing
