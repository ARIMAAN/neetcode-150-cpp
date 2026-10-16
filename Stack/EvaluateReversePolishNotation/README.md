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

> Each token is processed once. Numbers are pushed, operators pop two and push one.
> Stack size grows by 1 for numbers, shrinks by 1 for operators (net -1 per operator).

## Complexity

- **Time**: O(n) — one pass through tokens
- **Space**: O(n) — stack holds at most n/2 numbers (half the tokens are numbers in worst case)

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

> Pop `b` first, then `a`. Order matters for `-` and `/`.
> `a - b` and `a / b` where `a` was pushed before `b`.

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

> C++ integer division already truncates toward zero for positive/negative combos.
> So `-7/2 = -3` in C++ — matches the problem requirement without extra handling.
