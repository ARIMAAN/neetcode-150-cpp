# Brute Force

## Intuition

For each window position, scan all `k` elements and find the maximum.
Append it to the result.

> There are `n - k + 1` windows total.
> For `n=8, k=3`: windows at positions 0,1,2,3,4,5 → 6 windows = 8-3+1.

## Algorithm

1. For each `i` from `0` to `n - k`:
2. Scan `nums[i..i+k-1]`, find max
3. Append max to result
4. Return result

## Code

```cpp
vector<int> maxSlidingWindow(vector<int>& nums, int k) {
    vector<int> result;
    for (int i = 0; i <= nums.size() - k; i++) {
        int maxVal = nums[i];
        for (int j = i + 1; j < i + k; j++)
            maxVal = max(maxVal, nums[j]);
        result.push_back(maxVal);
    }
    return result;
}
```

## Dry Run — `[1,3,-1,-3,5,3,6,7]`, k=3

| i | window | max |
|---|--------|-----|
| 0 | [1,3,-1] | 3 |
| 1 | [3,-1,-3] | 3 |
| 2 | [-1,-3,5] | 5 |
| 3 | [-3,5,3] | 5 |
| 4 | [5,3,6] | 6 |
| 5 | [3,6,7] | 7 |

Output: `[3,3,5,5,6,7]` ✅

## Complexity

- **Time**: O(n · k) — n windows, each scanned in O(k)
- **Space**: O(1) extra (not counting output)

> Best case: k=1, each window is one element — O(n).
> Worst case: k=n, one window of size n — O(n²) total.
> Average case for k=n/2: O(n²/2) = O(n²).

## Related Problems

- [Sliding Window Maximum Monotonic Deque](./MonotonicDeque.md) — the O(n) solution
- [Daily Temperatures (#739)](../../Stack/DailyTemperatures/) — monotonic stack, similar idea

## Why This Is Slow

For `n = 10^5` and `k = 10^4`, that's 10^9 operations — TLE.
We're re-scanning overlapping parts of the window every time.

> The overlap between consecutive windows is `k-1` elements.
> We're doing O(k) work per window when only 1 element changes.
> The monotonic deque exploits this by maintaining state across windows.
