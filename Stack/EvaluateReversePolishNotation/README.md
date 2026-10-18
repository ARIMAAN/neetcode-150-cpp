# Evaluate Reverse Polish Notation

**LeetCode #150** | **Difficulty**: Medium | **Topic**: Stack

---

## Problem Statement

Evaluate an expression in Reverse Polish Notation (postfix). Operators are `+`, `-`, `*`, `/` (integer division truncating toward zero).

**Examples**:

| Input | Output |
|-------|--------|
| `["2","1","+","3","*"]` | `9` → `(2+1)*3` |
| `["4","13","5","/","+"]` | `6` → `4+(13/5)` |
| `["10","6","9","3","+","-11","*","/","*","17","+","5","+"]` | `22` |

---

## Approach

| Approach | Time | Space |
|----------|------|-------|
| Stack | O(n) | O(n) |

## Key Insight

Push numbers onto a stack. When an operator is seen, pop two numbers,
apply the operator, push the result back. Final answer is the only element left.

> RPN eliminates the need for parentheses and operator precedence rules.
> The stack naturally handles the order of operations.

## Solution

```cpp
int evalRPN(vector<string>& tokens) {
    stack<long> st;
    for (auto& t : tokens) {
        if (t == "+" || t == "-" || t == "*" || t == "/") {
            long b = st.top(); st.pop();
            long a = st.top(); st.pop();
            if (t == "+") st.push(a + b);
            else if (t == "-") st.push(a - b);
            else if (t == "*") st.push(a * b);
            else st.push(a / b);
        } else st.push(stol(t));
    }
    return st.top();
}
```

## Dry Run — `["2","1","+","3","*"]`

| token | action | stack |
|-------|--------|-------|
| "2" | push | [2] |
| "1" | push | [2,1] |
| "+" | pop 1,2 → push 3 | [3] |
| "3" | push | [3,3] |
| "*" | pop 3,3 → push 9 | [9] |

Return `9` ✅

## Edge Cases

- Negative numbers: `"-3"` is a valid token, `stol` handles it
- Division truncates toward zero: `-7/2 = -3` not `-4`
- Use `long` to avoid overflow during intermediate multiplications
