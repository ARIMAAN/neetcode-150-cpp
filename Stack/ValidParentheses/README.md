# Valid Parentheses

**LeetCode #20** | **Difficulty**: Easy | **Topic**: Stack

---

## Problem Statement

Given a string `s` containing only `'('`, `')'`, `'{'`, `'}'`, `'['`, `']'`, determine if the input string is valid.

A string is valid if:
1. Open brackets are closed by the same type of bracket
2. Open brackets are closed in the correct order
3. Every close bracket has a corresponding open bracket

> Rule 3 is implied by rules 1 and 2, but worth stating explicitly.
> An empty string satisfies all rules vacuously — it's valid.

**Examples**:

| Input | Output |
|-------|--------|
| `"()"` | `true` |
| `"()[]{}"` | `true` |
| `"(]"` | `false` |
| `"([)]"` | `false` |
| `"{[]}"` | `true` |

> `"([)]"` is the classic trick case — each bracket has a match but the order is wrong.
> The stack catches this because `]` doesn't match `(` on top.

## Related Problems

- [Min Stack (#155)](../MinStack/) — stack with extra tracking
- [Generate Parentheses (#22)](../GenerateParentheses/) — generate valid strings
- [Largest Rectangle in Histogram (#84)](../LargestRectangleInHistogram/) — monotonic stack

**Constraints**: `1 <= s.length <= 10^4`, `s` consists of brackets only

> Odd-length strings are always invalid — can short-circuit early.
> `if (s.size() % 2 != 0) return false;`

---

## Approach

| Approach | Time | Space |
|----------|------|-------|
| Stack | O(n) | O(n) |

> Space is O(n) worst case: a string like `"(((((("` pushes all n chars onto the stack.
> Best case O(1) if every open is immediately closed.

## Thought Process

First instinct: count opens and closes. But that fails for `")("` — counts match but invalid.
Then: need to track order. Stack is the natural structure for ordered matching.

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

> The map stores close → open pairs.
> When we see a close bracket, we look up its expected open bracket and compare with stack top.
> This is cleaner than a chain of if-else for each bracket type.

## Dry Run — `"{[]}"`

| char | action | stack |
|------|--------|-------|
| `{` | push | `{` |
| `[` | push | `{[` |
| `]` | top=`[` matches → pop | `{` |
| `}` | top=`{` matches → pop | empty |

Return `true` ✅

## Dry Run — `"([)]"`

| char | action | stack |
|------|--------|-------|
| `(` | push | `(` |
| `[` | push | `([` |
| `)` | top=`[` ≠ `(` → return false | - |

Return `false` ✅

## Edge Cases

| Input | Output | Reason |
|-------|--------|--------|
| `"("` | `false` | unclosed bracket, stack not empty |
| `")"` | `false` | close with empty stack |
| `""` | `true` | empty string is valid |

> The `st.empty()` check before `st.top()` is critical.
> Without it, calling `top()` on an empty stack is undefined behavior.

## Complexity

- **Time**: O(n) — single pass through the string
- **Space**: O(n) — stack holds at most n/2 open brackets
