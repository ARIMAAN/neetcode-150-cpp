# Binary Search — Optimal

## Intuition

The array is sorted. So at any point, if we pick the middle element:
- If it equals target → done
- If it's less than target → target must be in the right half
- If it's greater than target → target must be in the left half

Each comparison eliminates half the remaining elements. That's O(log n).

## Algorithm

1. Set `lo = 0`, `hi = n - 1`
2. While `lo <= hi`:
   - `mid = lo + (hi - lo) / 2`  ← avoids integer overflow vs `(lo+hi)/2`
   - If `nums[mid] == target` → return `mid`
   - If `nums[mid] < target` → `lo = mid + 1`
   - Else → `hi = mid - 1`
3. Return `-1`

## Code

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int lo = 0, hi = nums.size() - 1;
        while (lo <= hi) {
            int mid = lo + (hi - lo) / 2;
            if (nums[mid] == target) return mid;
            else if (nums[mid] < target) lo = mid + 1;
            else hi = mid - 1;
        }
        return -1;
    }
};
```

## Dry Run

`nums = [-1, 0, 3, 5, 9, 12]`, `target = 9`

| lo | hi | mid | nums[mid] | Action |
|----|-----|-----|-----------|--------|
| 0 | 5 | 2 | 3 | 3 < 9 → lo = 3 |
| 3 | 5 | 4 | 9 | 9 == 9 → return 4 ✅ |

`nums = [-1, 0, 3, 5, 9, 12]`, `target = 2`

| lo | hi | mid | nums[mid] | Action |
|----|-----|-----|-----------|--------|
| 0 | 5 | 2 | 3 | 3 > 2 → hi = 1 |
| 0 | 1 | 0 | -1 | -1 < 2 → lo = 1 |
| 1 | 1 | 1 | 0 | 0 < 2 → lo = 2 |
| 2 | 1 | — | — | lo > hi → exit |

Return `-1` ✅

## Loop Invariant

At every iteration: if `target` exists in `nums`, it must be in `nums[lo..hi]`. We maintain this by moving `lo` and `hi` past already-checked indices.

## Why `lo + (hi - lo) / 2` and not `(lo + hi) / 2`

If `lo` and `hi` are both near `INT_MAX`, `lo + hi` overflows. The subtraction form is always safe.

## Termination Proof

Each iteration either returns or strictly shrinks the `[lo, hi]` window (`lo` increases or `hi` decreases). So the loop always terminates in at most O(log n) steps.

## Edge Cases

- Single element array: `lo == hi == 0`, one comparison, works fine
- Target smaller than all elements: `hi` keeps shrinking until `hi < lo`
- Target larger than all elements: `lo` keeps growing until `lo > hi`

## Complexity

- Time: O(log n) — search space halves each iteration
- Space: O(1) — just three pointers

## Thought Process

Classic template. The key decision is always: what does `lo = mid + 1` vs `hi = mid - 1` mean? We move past `mid` (not to `mid`) because we already checked `mid` and it wasn't the answer. The `lo <= hi` condition (not `<`) ensures we don't miss the case where `lo == hi` (single element remaining).
