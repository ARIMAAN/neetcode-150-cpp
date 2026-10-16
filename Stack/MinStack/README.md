# Min Stack

**LeetCode #155** | **Difficulty**: Medium | **Topic**: Stack

---

## Problem Statement

Design a stack that supports `push`, `pop`, `top`, and `getMin` — all in O(1) time.

**Constraints**: `-2^31 <= val <= 2^31 - 1`, at most `3 * 10^4` calls

> The challenge: a regular stack gives O(1) push/pop/top but O(n) getMin.
> We need to do better.

---

## Approach

| Approach | Time | Space |
|----------|------|-------|
| Two Stacks | O(1) all ops | O(n) |

> The naive approach: scan the entire stack for min on each `getMin()` call — O(n).
> Two stacks trades space for O(1) time on all operations.

## Complexity

- **Time**: O(1) for all operations — push, pop, top, getMin
- **Space**: O(n) — two stacks, each up to n elements

## Key Insight

Maintain a second stack `minStack` that tracks the current minimum at each level.
When pushing `val`, push `min(val, minStack.top())` onto `minStack`.
When popping, pop from both stacks.
`getMin()` just returns `minStack.top()`.

> The key: `minSt` is always in sync with `st` — same size, same push/pop rhythm.
> `minSt.top()` always reflects the minimum of the current stack state.

## Solution

```cpp
class MinStack {
    stack<int> st, minSt;
public:
    void push(int val) {
        st.push(val);
        minSt.push(minSt.empty() ? val : min(val, minSt.top()));
    }
    void pop() { st.pop(); minSt.pop(); }
    int top() { return st.top(); }
    int getMin() { return minSt.top(); }
};
```

> `minSt.empty() ? val : min(val, minSt.top())` handles the first push correctly.
> On first push, there's no previous min to compare against, so we just use `val`.

## Dry Run — push(5), push(3), push(7), getMin, pop, getMin

| op | st | minSt | result |
|----|----|----|--------|
| push(5) | [5] | [5] | - |
| push(3) | [5,3] | [5,3] | - |
| push(7) | [5,3,7] | [5,3,3] | - |
| getMin | - | - | 3 |
| pop | [5,3] | [5,3] | - |
| getMin | - | - | 3 |

> Notice push(7): minSt gets `min(7, 3) = 3`, not 7.
> So even though 7 is on top of st, getMin still correctly returns 3.

## Dry Run — push(2), push(2), pop, getMin

| op | st | minSt | result |
|----|----|----|--------|
| push(2) | [2] | [2] | - |
| push(2) | [2,2] | [2,2] | - |
| pop | [2] | [2] | - |
| getMin | - | - | 2 |

> Duplicate values: both stacks pop together, min is preserved correctly.

## Why This Works

`minSt[i]` = minimum of all elements from bottom to position `i`.
When we pop the top, the minimum of the remaining elements is `minSt[i-1]` — already stored.
No need to rescan.

> Alternative: only push to `minSt` when `val <= minSt.top()`.
> Then pop from `minSt` only when the popped value equals `minSt.top()`.
> Saves space when many pushes are larger than current min.

## Related Problems

- [Valid Parentheses (#20)](../ValidParentheses/) — basic stack usage
- [Daily Temperatures (#739)](../DailyTemperatures/) — monotonic stack
