# Hash Set Single Pass ✅ Optimal

> **Time:** O(1) &nbsp;|&nbsp; **Space:** O(1) &nbsp; *(board is always 9×9)*

---

## Intuition

Instead of three separate passes, do everything in **one pass**. For each cell `(i, j)`, simultaneously check and update:
- `rows[i]` — set of digits seen in row `i`
- `cols[j]` — set of digits seen in col `j`
- `boxes[boxIndex]` — set of digits seen in the corresponding 3×3 box

If any digit already exists in any of the three sets → invalid.

---

## Box Index Formula

```
boxIndex = (i / 3) * 3 + (j / 3)
```

Integer division groups rows into bands of 3 and cols into bands of 3:

```
(0,0)→0  (0,3)→1  (0,6)→2
(3,0)→3  (3,3)→4  (3,6)→5
(6,0)→6  (6,3)→7  (6,6)→8
```

> Trick to remember: `i/3` gives the row-band (0,1,2), `j/3` gives the col-band (0,1,2). Multiply row-band by 3 and add col-band to get a unique index 0-8.

---

## Algorithm

1. Create `rows[9]`, `cols[9]`, `boxes[9]` — each an `unordered_set<char>`.
2. For each cell `(i, j)`:
   - Skip if `board[i][j] == '.'`
   - Compute `boxIndex = (i/3)*3 + (j/3)`
   - If `value` exists in `rows[i]`, `cols[j]`, or `boxes[boxIndex]` → return `false`
   - Insert `value` into all three sets
3. Return `true`.

---

## Code

```cpp
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        unordered_set<char> rows[9];
        unordered_set<char> cols[9];
        unordered_set<char> boxes[9];

        for (int i = 0; i < 9; i++) {
            for (int j = 0; j < 9; j++) {
                if (board[i][j] == '.') continue;  // skip empty cells

                char value = board[i][j];
                int boxIndex = (i / 3) * 3 + (j / 3);  // map cell to box 0-8

                // if value already seen in row, col, or box → invalid
                if (rows[i].count(value) || cols[j].count(value) || boxes[boxIndex].count(value)) {
                    return false;
                }

                rows[i].insert(value);
                cols[j].insert(value);
                boxes[boxIndex].insert(value);
            }
        }
        return true;
    }
};
```

---

## Dry Run

**Input (Example 2 — invalid board)**

Top-left 3×3 box contains:
```
"1" "2" "."
"4" "." "."
"." "9" "1"   ← second "1" here
```

| i | j | value | boxIndex | rows[0] | cols check | boxes[0] | result |
|---|---|-------|----------|---------|------------|----------|--------|
| 0 | 0 | '1' | 0 | {} | {} | {} | insert all |
| 0 | 1 | '2' | 0 | {1} | {} | {1} | insert all |
| 1 | 0 | '4' | 0 | {} | {1} | {1,2} | insert all |
| 2 | 1 | '9' | 0 | {} | {2} | {1,2,4} | insert all |
| 2 | 2 | '1' | 0 | {} | {} | {1,2,4,9} | **'1' in boxes[0]!** → return `false` ✅ |

---

**Input (Example 1 — valid board)**

All 81 cells processed, no duplicate found in any row/col/box → return `true` ✅

---

## Edge Cases

| Case | Expected | Reason |
|------|----------|--------|
| All `'.'` | `true` | Empty board is valid |
| One digit repeated in same row | `false` | rows[i] catches it |
| One digit repeated in same col | `false` | cols[j] catches it |
| One digit repeated in same box | `false` | boxes[k] catches it |
| Same digit in different row/col/box | `true` | No constraint violated |

---

## Why Arrays of Sets?

```cpp
unordered_set<char> rows[9];
```

This creates 9 independent sets — one per row. Same for cols and boxes. Each set tracks which digits have been seen in that row/col/box so far.

> Alternative: use `unordered_set<string>` with encoded keys like `"r0:5"`, `"c3:5"`, `"b1:5"` — same idea, slightly more overhead.

---

## What Happens If We Use a Single Set?

If we used one global set with just the digit, we'd mix up rows/cols/boxes. For example, digit `'5'` in row 0 and digit `'5'` in row 1 are both valid — a single set would wrongly flag this as a duplicate. That's why we need **separate sets per row, col, and box**.

---

## Complexity

| | |
|--|--|
| **Time** | O(1) — exactly 81 cells, each processed once |
| **Space** | O(1) — 27 sets, each holding at most 9 chars = 243 chars max |

---

## Comparison

| Approach | Passes | Time | Space | Notes |
|----------|--------|------|-------|-------|
| Brute Force (3 passes) | 3 | O(1) | O(1) | Simple but redundant |
| Hash Set Single Pass ✅ | 1 | O(1) | O(1) | Cleaner, one loop |
