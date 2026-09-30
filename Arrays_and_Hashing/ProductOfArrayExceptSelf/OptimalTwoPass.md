# Prefix & Suffix — O(1) Space ✅ Optimal

> **Time:** O(n) &nbsp;|&nbsp; **Space:** O(1)

---

## Intuition

Instead of storing full prefix and suffix arrays, use a **single running variable** for each direction and write directly into the output array.

- **Left pass:** fill `output[i]` with the product of everything to the left of `i`
- **Right pass:** multiply `output[i]` by the product of everything to the right of `i`

The output array itself serves as the prefix store — no extra arrays needed.

---

## The Space Trick

```
After left pass:
output = [1, 1, 2, 6]   ← output[i] = product of nums[0..i-1]

Running right variable starts at 1, goes right to left:
i=3: output[3] *= 1  → 6×1  = 6,   right = 1×4 = 4
i=2: output[2] *= 4  → 2×4  = 8,   right = 4×3 = 12
i=1: output[1] *= 12 → 1×12 = 12,  right = 12×2 = 24
i=0: output[0] *= 24 → 1×24 = 24,  right = 24×1 = 24

Final output = [24, 12, 8, 6] ✅
```

---

## Algorithm

**Left pass:**
1. Initialize `left = 1`, `output` filled with `1`s.
2. For `i = 0` to `n-1`: `output[i] *= left`, then `left *= nums[i]`.

**Right pass:**
3. Initialize `right = 1`.
4. For `i = n-1` down to `0`: `output[i] *= right`, then `right *= nums[i]`.

5. Return `output`.

---

## Code

```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        vector<int> output(nums.size(), 1);

        // Left pass: output[i] = product of all elements to the LEFT of i
        int left = 1;
        for (int i = 0; i < nums.size(); i++) {
            output[i] *= left;   // store current left product
            left *= nums[i];     // expand left product to include nums[i]
        }

        // Right pass: multiply output[i] by product of all elements to the RIGHT of i
        int right = 1;
        for (int i = nums.size() - 1; i >= 0; i--) {
            output[i] *= right;  // multiply in current right product
            right *= nums[i];    // expand right product to include nums[i]
        }

        return output;
    }
};
```

---

## Dry Run

**Input:** `nums = [1,2,3,4]`

**Left pass** (`left` starts at 1):

| i | output[i] before | output[i] after `*= left` | left after `*= nums[i]` |
|---|-----------------|--------------------------|------------------------|
| 0 | 1 | 1×1 = 1 | 1×1 = 1 |
| 1 | 1 | 1×1 = 1 | 1×2 = 2 |
| 2 | 1 | 1×2 = 2 | 2×3 = 6 |
| 3 | 1 | 1×6 = 6 | 6×4 = 24 |

`output = [1, 1, 2, 6]`

**Right pass** (`right` starts at 1):

| i | output[i] before | output[i] after `*= right` | right after `*= nums[i]` |
|---|-----------------|---------------------------|-------------------------|
| 3 | 6 | 6×1 = 6 | 1×4 = 4 |
| 2 | 2 | 2×4 = 8 | 4×3 = 12 |
| 1 | 1 | 1×12 = 12 | 12×2 = 24 |
| 0 | 1 | 1×24 = 24 | 24×1 = 24 |

`output = [24, 12, 8, 6]` ✅

---

**Input:** `nums = [-1,1,0,-3,3]`

Left pass → `output = [1, -1, -1, 0, 0]`

Right pass:
- i=4: 0×1=0, right=3
- i=3: 0×3=0, right=-9
- i=2: -1×-9=9, right=0
- i=1: -1×0=0, right=0
- i=0: 1×0=0, right=0

`output = [0, 0, 9, 0, 0]` ✅

---

## Edge Cases

| Case | Input | Output | Note |
|------|-------|--------|------|
| Contains zero | `[1,0,3]` | `[0,3,0]` | Only index of zero gets non-zero |
| Two zeros | `[0,0,3]` | `[0,0,0]` | All zeros |
| All ones | `[1,1,1]` | `[1,1,1]` | Product of n-1 ones = 1 |
| Negatives | `[-1,-1]` | `[-1,-1]` | Works naturally |

---

## Interview Tips

- Start by explaining the brute force, then say *"we can avoid recomputing by precomputing prefix and suffix products"*
- The O(1) space insight: *"the output array itself stores the prefix pass, so we don't need a separate prefix array"*
- Always mention the zero edge case — it's why division doesn't work
- Follow-up: *"What if there are multiple zeros?"* — answer: all outputs become 0

---

## Why No Division?

Division would be: `answer[i] = totalProduct / nums[i]`

Problems:
1. **Zero in array** — division by zero is undefined
2. **Problem constraint** — explicitly forbids division

The prefix×suffix approach sidesteps both issues entirely.

---

## Complexity

| | |
|--|--|
| **Time** | O(n) — two linear passes |
| **Space** | O(1) — only two scalar variables (`left`, `right`); output array doesn't count |

---

## Comparison

| Approach | Time | Space | Notes |
|----------|------|-------|-------|
| Brute Force | O(n²) | O(1) | TLE for large n |
| Prefix & Suffix Arrays | O(n) | O(n) | Clean but uses extra arrays |
| Two-Pass O(1) Space ✅ | O(n) | O(1) | Optimal — reuses output array |
