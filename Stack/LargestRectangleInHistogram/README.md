# Largest Rectangle in Histogram

**LeetCode #84** | **Difficulty**: Hard | **Topic**: Stack

---

## Problem Statement

Given an array `heights` representing a histogram, return the area of the largest rectangle that can be formed.

**Examples**:

| Input | Output |
|-------|--------|
| `[2,1,5,6,2,3]` | `10` |
| `[2,4]` | `4` |

**Constraints**: `1 <= heights.length <= 10^5`, `0 <= heights[i] <= 10^4`

---

## Approaches

| Approach | Time | Space |
|----------|------|-------|
| Brute Force | O(n²) | O(1) |
| Monotonic Stack | O(n) | O(n) |

> This is a Hard problem. The monotonic stack approach is not intuitive.
> The key realization: when a shorter bar arrives, it defines the right boundary
> for all taller bars currently in the stack.

## Complexity

- **Time**: O(n) — each bar pushed and popped at most once
- **Space**: O(n) — stack holds at most n indices

---

## Key Insight

For each bar, the largest rectangle using that bar's height extends left and right
until a shorter bar is encountered. Use a monotonic increasing stack to find,
for each bar, the first shorter bar to its left and right.

> Brute force: for each bar, scan left and right to find boundaries — O(n) per bar = O(n²).
> Monotonic stack: find both boundaries for all bars in a single O(n) pass.

---

## Why Monotonic Stack?

When we pop a bar from the stack (because a shorter bar arrived),
we know the right boundary for that bar's rectangle.
The new stack top gives the left boundary.
Area = `height * (right - left - 1)`.

> The stack maintains bars in increasing height order.
> A bar is popped when a shorter bar arrives — that shorter bar is the right boundary.
> The bar now at stack top is the left boundary (first bar shorter than the popped bar to its left).

> Width formula: `w = st.empty() ? i : i - st.top() - 1`
> If stack is empty after pop, the bar extends all the way to the left edge (width = i).

---

## Solution

```cpp
int largestRectangleArea(vector<int>& heights) {
    stack<int> st;
    int maxArea = 0;
    heights.push_back(0); // sentinel to flush remaining stack
    for (int i = 0; i < heights.size(); i++) {
        while (!st.empty() && heights[i] < heights[st.top()]) {
            int h = heights[st.top()]; st.pop();
            int w = st.empty() ? i : i - st.top() - 1;
            maxArea = max(maxArea, h * w);
        }
        st.push(i);
    }
    return maxArea;
}
```

> `heights.push_back(0)` appends a sentinel bar of height 0.
> This forces all remaining bars in the stack to be popped and processed at the end.
> Without it, bars that are never shorter than anything to their right would be missed.

## Dry Run — `[2,1,5,6,2,3]`

Append 0 → `[2,1,5,6,2,3,0]`

| i | h[i] | stack | pops | maxArea |
|---|------|-------|------|---------|
| 0 | 2 | [0] | - | 0 |
| 1 | 1 | [1] | pop 0: h=2,w=1→2 | 2 |
| 2 | 5 | [1,2] | - | 2 |
| 3 | 6 | [1,2,3] | - | 2 |
| 4 | 2 | [1,4] | pop 3: h=6,w=1→6; pop 2: h=5,w=2→10 | 10 |
| 5 | 3 | [1,4,5] | - | 10 |
| 6 | 0 | [] | pop 5: h=3,w=1→3; pop 4: h=2,w=3→6; pop 1: h=1,w=6→6 | 10 |

Return `10` ✅

> At i=4, popping index 2 (h=5): right=4, left=st.top()=1, width=4-1-1=2. Area=10.
> This is the `[5,6]` rectangle — height 5, width 2.

## Edge Cases

- All same height: `[3,3,3]` → `9` (width=3, height=3)
- Single bar: `[5]` → `5`
- Decreasing: `[5,4,3,2,1]` → `9` (height=3, width=3)

> For `[5,4,3,2,1]`: the optimal rectangle is height=3, width=3 (bars at indices 2,3,4).
> Or height=1, width=5 = 5. Or height=2, width=2 = 4. Max is 9.

## Complexity

- **Time**: O(n) — each bar pushed and popped at most once
- **Space**: O(n) — stack

> Same amortized argument as other monotonic stack problems.
> Total push + pop operations = O(2n) = O(n).

## Thought Process

Brute force is obvious. Getting to O(n) requires the insight:
for each bar, we need the nearest shorter bar on both sides.
Monotonic stack gives us both in one pass — right boundary when popped, left boundary from new stack top.
