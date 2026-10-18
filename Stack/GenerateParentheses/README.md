# Generate Parentheses

**LeetCode #22** | **Difficulty**: Medium | **Topic**: Stack / Backtracking

---

## Problem Statement

Given `n` pairs of parentheses, generate all combinations of well-formed parentheses.

**Examples**:

| n | Output |
|---|--------|
| 1 | `["()"]` |
| 3 | `["((()))","(()())","(())()","()(())","()()()"]` |

**Constraints**: `1 <= n <= 8`

---

## Approach

| Approach | Time | Space |
|----------|------|-------|
| Backtracking | O(4^n / √n) | O(n) |

## Key Insight

At each step, we can add `(` if `open < n`, or `)` if `close < open`.
Recurse until `open == close == n`.

## Solution

```cpp
vector<string> generateParenthesis(int n) {
    vector<string> result;
    function<void(string, int, int)> bt = [&](string cur, int open, int close) {
        if (cur.size() == 2 * n) { result.push_back(cur); return; }
        if (open < n) bt(cur + "(", open + 1, close);
        if (close < open) bt(cur + ")", open, close + 1);
    };
    bt("", 0, 0);
    return result;
}
```

## Dry Run — n=2

```
bt("", 0, 0)
  bt("(", 1, 0)
    bt("((", 2, 0)
      bt("(()", 2, 1)
        bt("(())", 2, 2) → add "(())"
    bt("()", 1, 1)
      bt("()(", 2, 1)
        bt("()()", 2, 2) → add "()()"
```

Output: `["(())", "()()"]` ✅

## Why This Is Correct

- `open < n`: we can still add more open brackets
- `close < open`: we can only close if there's an unmatched open bracket
- These two conditions guarantee every generated string is valid
