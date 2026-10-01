# Brute Force (3 Separate Passes)

> **Time:** O(1) &nbsp;|&nbsp; **Space:** O(1) &nbsp; *(board is always 9×9)*

---

## Intuition

Check each constraint separately in three passes:
1. Scan all 9 rows for duplicates
2. Scan all 9 columns for duplicates
3. Scan all 9 boxes for duplicates

Simple to understand but repeats work — visits all 81 cells three times.

---

## Algorithm

1. For each row `i`: collect all non-`'.'` values, check for duplicates with a set.
2. For each col `j`: collect all non-`'.'` values, check for duplicates with a set.
3. For each box `(br, bc)` where `br, bc ∈ {0,1,2}`: collect all non-`'.'` values in the 3×3 block, check for duplicates.
4. Return `true` if all pass.

---

## Code

```cpp
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        // check rows
        for (int i = 0; i < 9; i++) {
            unordered_set<char> seen;
            for (int j = 0; j < 9; j++) {
                if (board[i][j] == '.') continue;
                if (seen.count(board[i][j])) return false;
                seen.insert(board[i][j]);
            }
        }
        // check cols
        for (int j = 0; j < 9; j++) {
            unordered_set<char> seen;
            for (int i = 0; i < 9; i++) {
                if (board[i][j] == '.') continue;
                if (seen.count(board[i][j])) return false;
                seen.insert(board[i][j]);
            }
        }
        // check 3x3 boxes
        for (int br = 0; br < 3; br++) {
            for (int bc = 0; bc < 3; bc++) {
                unordered_set<char> seen;
                for (int i = br * 3; i < br * 3 + 3; i++) {
                    for (int j = bc * 3; j < bc * 3 + 3; j++) {
                        if (board[i][j] == '.') continue;
                        if (seen.count(board[i][j])) return false;
                        seen.insert(board[i][j]);
                    }
                }
            }
        }
        return true;
    }
};
```

---

## Dry Run

**Checking row 0:** `["1","2",".",".",".","3",".",".",".","."]`

| j | value | seen before | duplicate? |
|---|-------|-------------|------------|
| 0 | '1' | {} | ❌ → insert |
| 1 | '2' | {1} | ❌ → insert |
| 2 | '.' | — | skip |
| 4 | '3' | {1,2} | ❌ → insert |

No duplicate in row 0 ✅

**Checking top-left box (Example 2):** contains `1`, `2`, `4`, `9`, `1` → duplicate `1` found → return `false` ✅

---

**Checking col 0:** `["1","4",".","5",".","7",".",".","."]`

| i | value | seen before | duplicate? |
|---|-------|-------------|------------|
| 0 | '1' | {} | ❌ → insert |
| 1 | '4' | {1} | ❌ → insert |
| 2 | '.' | — | skip |
| 3 | '5' | {1,4} | ❌ → insert |
| 5 | '7' | {1,4,5} | ❌ → insert |

No duplicate in col 0 ✅

---

## Complexity

| | |
|--|--|
| **Time** | O(1) — 81 cells visited 3 times = 243 ops, constant |
| **Space** | O(1) — sets hold at most 9 chars each |

> ⚠️ Visits every cell 3 times. The single-pass approach does it in 1.

---

## Why 3 Passes Is Still O(1)

Even though we loop 3 times, the board is always fixed at 9×9 = 81 cells. So 3×81 = 243 operations — a constant. This is why both approaches are O(1) time and space.
