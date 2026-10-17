# Valid Parentheses

**LeetCode #20** | **Difficulty**: Easy | **Topic**: Stack

---

## Problem Statement

Given a string `s` containing only `'('`, `')'`, `'{'`, `'}'`, `'['`, `']'`, determine if the input string is valid.

A string is valid if:
1. Open brackets are closed by the same type of bracket
2. Open brackets are closed in the correct order
3. Every close bracket has a corresponding open bracket

**Examples**:

| Input | Output |
|-------|--------|
| `"()"` | `true` |
| `"()[]{}"` | `true` |
| `"(]"` | `false` |
| `"([)]"` | `false` |
| `"{[]}"` | `true` |

**Constraints**: `1 <= s.length <= 10^4`, `s` consists of brackets only

---

## Approach

| Approach | Time | Space |
|----------|------|-------|
| Stack | O(n) | O(n) |

## Key Insight

Push open brackets onto a stack. When a close bracket is seen,
check if the top of the stack is the matching open bracket.
If not, or if the stack is empty, return false.
At the end, the stack must be empty.

> The stack naturally handles nesting: the most recently opened bracket
> must be the first one closed. LIFO order = correct bracket matching.

## Solution

```cpp
bool isValid(string s) {
    stack<char> st;
    unordered_map<char,char> match = {{')',  '('}, {']', '['}, {'}', '{'}};
    for (char c : s) {
        if (match.count(c)) {
            if (st.empty() || st.top() != match[c]) return false;
            st.pop();
        } else st.push(c);
    }
    return st.empty();
}
```

## Dry Run — `"{[]}"`

| char | action | stack |
|------|--------|-------|
| `{` | push | `{` |
| `[` | push | `{[` |
| `]` | top=`[` matches → pop | `{` |
| `}` | top=`{` matches → pop | empty |

Return `true` ✅

## Edge Cases

| Input | Output | Reason |
|-------|--------|--------|
| `"("` | `false` | unclosed bracket, stack not empty |
| `")"` | `false` | close with empty stack |
| `""` | `true` | empty string is valid |

> The `st.empty()` check before `st.top()` is critical.
> Without it, calling `top()` on an empty stack is undefined behavior.
