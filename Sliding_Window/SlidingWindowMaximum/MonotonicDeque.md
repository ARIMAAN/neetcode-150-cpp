# Monotonic Deque

## Intuition

Maintain a deque of indices in **decreasing order of their values**.
The front is always the index of the current window's maximum.
When we add a new element, remove all smaller elements from the back — they're useless.
When the front index falls outside the window, pop it.

> The deque is a "candidates for maximum" list.
> We aggressively prune candidates that can never win.

## Algorithm

1. Use `deque<int> dq` storing indices
2. For each `i` from 0 to n-1:
   - Pop from back while `nums[dq.back()] <= nums[i]`
   - Push `i` to back
   - Pop from front if `dq.front() < i - k + 1` (outside window)
   - If `i >= k - 1`, append `nums[dq.front()]` to result
3. Return result

> We only start appending results when `i >= k - 1` because
> the first complete window ends at index `k - 1`.

## Code

```cpp
vector<int> maxSlidingWindow(vector<int>& nums, int k) {
    deque<int> dq;
    vector<int> result;
    for (int i = 0; i < nums.size(); i++) {
        while (!dq.empty() && nums[dq.back()] <= nums[i])
            dq.pop_back();
        dq.push_back(i);
        if (dq.front() < i - k + 1)
            dq.pop_front();
        if (i >= k - 1)
            result.push_back(nums[dq.front()]);
    }
    return result;
}
```

## Dry Run — `[1,3,-1,-3,5,3,6,7]`, k=3

| i | nums[i] | deque (indices) | deque (values) | output |
|---|---------|-----------------|----------------|--------|
| 0 | 1 | [0] | [1] | - |
| 1 | 3 | [1] | [3] | - (pop 0 since 1<3) |
| 2 | -1 | [1,2] | [3,-1] | 3 |
| 3 | -3 | [1,2,3] | [3,-1,-3] | 3 |
| 4 | 5 | [4] | [5] | 5 (pop all, front 1 < 4-3+1=2) |
| 5 | 3 | [4,5] | [5,3] | 5 |
| 6 | 6 | [6] | [6] | 6 (pop 4,5 since 3,5<6... wait 5>3 so pop 5 first) |
| 7 | 7 | [7] | [7] | 7 |

Output: `[3,3,5,5,6,7]` ✅

## Why `<=` When Popping From Back?

We pop elements `<= nums[i]` (not just `<`).
If equal, the newer element is preferred — it will stay in the window longer.
Keeping the old equal element would give wrong results when it expires.

> Example: `[2,2]`, k=2. If we keep both 2's, when the first expires
> the deque front correctly moves to the second. With `<=` we only keep the newer one
> but the result is the same. Either works for correctness, `<=` is cleaner.

## Edge Cases

| Input | k | Output | Reason |
|-------|---|--------|--------|
| `[1]` | 1 | `[1]` | single element |
| `[1,2,3]` | 3 | `[3]` | one window = whole array |
| `[3,2,1]` | 1 | `[3,2,1]` | k=1, each element is its own window |

> When k=1, every element is its own window — output = input.
> When k=n, there's only one window — output = [max of array].

## Complexity

- **Time**: O(n) — each element pushed and popped from deque at most once
- **Space**: O(k) — deque holds at most k indices at any time

> The while loop inside the for loop is still O(n) total.
> Each element is pushed once and popped at most once — total deque operations = O(2n) = O(n).

## Comparison

| | Brute Force | Monotonic Deque |
|---|---|---|
| Time | O(n · k) | O(n) |
| Space | O(1) | O(k) |
| Key idea | rescan window | maintain decreasing deque |

## Thought Process

Brute force is obvious. The hard part is getting to O(n).
Key observation: if `nums[i] >= nums[j]` and `i > j`, then `j` can never be the max
for any future window (since `i` is in the window whenever `j` is, and `i` is larger).
So we can discard `j`. That's exactly what the deque does.
