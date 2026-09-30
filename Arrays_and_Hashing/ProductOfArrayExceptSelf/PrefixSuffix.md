# Prefix & Suffix Arrays

> **Time:** O(n) &nbsp;|&nbsp; **Space:** O(n)

---

## Intuition

Precompute two arrays:
- `prefix[i]` = product of all elements **to the left** of index `i`
- `suffix[i]` = product of all elements **to the right** of index `i`

Then `answer[i] = prefix[i] * suffix[i]`.

---

## Why This Works

```
nums     = [1,  2,  3,  4]

prefix   = [1,  1,  2,  6]   ← prefix[i] = product of nums[0..i-1]
suffix   = [24, 12, 4,  1]   ← suffix[i] = product of nums[i+1..n-1]

answer   = [1×24, 1×12, 2×4, 6×1]
         = [24,   12,   8,   6]  ✅
```

---

## Algorithm

1. Build `prefix[n]`: `prefix[0] = 1`, then `prefix[i] = prefix[i-1] * nums[i-1]`.
2. Build `suffix[n]`: `suffix[n-1] = 1`, then `suffix[i] = suffix[i+1] * nums[i+1]`.
3. `answer[i] = prefix[i] * suffix[i]`.

---

## Code

```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n = nums.size();
        vector<int> prefix(n), suffix(n), answer(n);

        // prefix[i] = product of all elements before index i
        prefix[0] = 1;
        for (int i = 1; i < n; i++)
            prefix[i] = prefix[i - 1] * nums[i - 1];

        // suffix[i] = product of all elements after index i
        suffix[n - 1] = 1;
        for (int i = n - 2; i >= 0; i--)
            suffix[i] = suffix[i + 1] * nums[i + 1];

        // answer[i] = left product * right product
        for (int i = 0; i < n; i++)
            answer[i] = prefix[i] * suffix[i];

        return answer;
    }
};
```

---

## Dry Run

**Input:** `nums = [1,2,3,4]`

**Build prefix:**

| i | prefix[i] | meaning |
|---|-----------|---------|
| 0 | 1 | nothing to the left |
| 1 | 1 | just nums[0]=1 |
| 2 | 2 | 1×2 |
| 3 | 6 | 1×2×3 |

**Build suffix:**

| i | suffix[i] | meaning |
|---|-----------|---------|
| 3 | 1 | nothing to the right |
| 2 | 4 | just nums[3]=4 |
| 1 | 12 | 3×4 |
| 0 | 24 | 2×3×4 |

**Multiply:**

| i | prefix[i] | suffix[i] | answer[i] |
|---|-----------|-----------|-----------|
| 0 | 1 | 24 | 24 |
| 1 | 1 | 12 | 12 |
| 2 | 2 | 4 | 8 |
| 3 | 6 | 1 | 6 |

**Output:** `[24,12,8,6]` ✅

---

## Complexity

| | |
|--|--|
| **Time** | O(n) — three separate linear passes |
| **Space** | O(n) — two extra arrays of size n |

> ✅ Correct and O(n), but uses O(n) extra space. Can we do better?
