# Daily Temperatures

**LeetCode #739** | **Difficulty**: Medium | **Topic**: Stack

---

## Problem Statement

Given an array `temperatures`, return an array `answer` where `answer[i]` is the number of days until a warmer temperature. If no future warmer day exists, `answer[i] = 0`.

**Examples**:

| Input | Output |
|-------|--------|
| `[73,74,75,71,69,72,76,73]` | `[1,1,4,2,1,1,0,0]` |
| `[30,40,50,60]` | `[1,1,1,0]` |
| `[30,60,90]` | `[1,1,0]` |

---

## Approach

| Approach | Time | Space |
|----------|------|-------|
| Brute Force | O(n²) | O(1) |
| Monotonic Stack | O(n) | O(n) |

> Brute force: for each day, scan forward until a warmer day is found.
> Monotonic stack: process each day once, resolve waiting days when warmer day arrives.

## Key Insight

Use a **monotonic decreasing stack** of indices.
When we see a temperature warmer than the stack top, that day is the answer for the top.
Pop and record the difference in indices.

> The stack maintains a list of days waiting for a warmer day.
> When a warmer day arrives, it resolves all days in the stack that are colder.

## Solution

```cpp
vector<int> dailyTemperatures(vector<int>& temperatures) {
    int n = temperatures.size();
    vector<int> answer(n, 0);
    stack<int> st; // indices
    for (int i = 0; i < n; i++) {
        while (!st.empty() && temperatures[i] > temperatures[st.top()]) {
            answer[st.top()] = i - st.top();
            st.pop();
        }
        st.push(i);
    }
    return answer;
}
```

> `answer[st.top()] = i - st.top()` — the number of days to wait is the index difference.
> We store indices (not temperatures) so we can compute this difference.

## Dry Run — `[73,74,75,71,69,72,76,73]`

| i | temp | stack (indices) | pops |
|---|------|-----------------|------|
| 0 | 73 | [0] | - |
| 1 | 74 | [1] | pop 0: ans[0]=1 |
| 2 | 75 | [2] | pop 1: ans[1]=1 |
| 3 | 71 | [2,3] | - |
| 4 | 69 | [2,3,4] | - |
| 5 | 72 | [2,5] | pop 4: ans[4]=1, pop 3: ans[3]=2 |
| 6 | 76 | [6] | pop 5: ans[5]=1, pop 2: ans[2]=4 |
| 7 | 73 | [6,7] | - |

Remaining [6,7] → ans[6]=ans[7]=0 (default) ✅

## Edge Cases

- Decreasing array `[90,80,70]` → `[0,0,0]`, stack never pops
- All same `[50,50,50]` → `[0,0,0]`

> Default initialization `vector<int> answer(n, 0)` handles the no-warmer-day case.
> Elements remaining in the stack at the end never got popped — their answer stays 0.
