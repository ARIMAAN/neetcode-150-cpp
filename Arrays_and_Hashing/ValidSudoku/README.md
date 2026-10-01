# Valid Sudoku

> **Difficulty:** Medium &nbsp;|&nbsp; **Topic:** Arrays & Hashing &nbsp;|&nbsp; [LeetCode #36](https://leetcode.com/problems/valid-sudoku/)

---

## Problem Statement

Given a 9×9 Sudoku board, return `true` if it is valid, otherwise `false`.

A board is valid if:
- Each **row** contains digits 1-9 without duplicates
- Each **column** contains digits 1-9 without duplicates
- Each of the nine **3×3 sub-boxes** contains digits 1-9 without duplicates

> Note: The board does not need to be full or solvable to be valid. Empty cells are marked with `'.'`.

**Example 1:** → `true`
**Example 2:** → `false` (two `1`s in top-left 3×3 box)

**Constraints:**
- `board.length == 9`
- `board[i].length == 9`
- `board[i][j]` is a digit `1-9` or `'.'`

---

## The Core Challenge

We need to check 3 things simultaneously for every cell:
1. Is this digit already in the same **row**?
2. Is this digit already in the same **column**?
3. Is this digit already in the same **3×3 box**?

The tricky part is mapping a cell `(i, j)` to its box index.

---

## Box Index Formula

```
boxIndex = (i / 3) * 3 + (j / 3)

Row 0-2, Col 0-2 → box 0    Row 0-2, Col 3-5 → box 1    Row 0-2, Col 6-8 → box 2
Row 3-5, Col 0-2 → box 3    Row 3-5, Col 3-5 → box 4    Row 3-5, Col 6-8 → box 5
Row 6-8, Col 0-2 → box 6    Row 6-8, Col 3-5 → box 7    Row 6-8, Col 6-8 → box 8
```

Example: cell `(4, 7)` → `(4/3)*3 + (7/3)` = `1*3 + 2` = **box 5**

Example: cell `(0, 0)` → `(0/3)*3 + (0/3)` = `0*3 + 0` = **box 0**

---

## Approaches

| # | Approach | Time | Space | File |
|---|----------|------|-------|------|
| 1 | Brute Force (3 separate passes) | O(1) | O(1) | [BruteForce.md](./BruteForce.md) |
| 2 | Hash Set Single Pass ✅ | O(1) | O(1) | [HashSet.md](./HashSet.md) |

> Since the board is always 9×9, all complexities are technically O(1) — bounded by constant 81 cells.
