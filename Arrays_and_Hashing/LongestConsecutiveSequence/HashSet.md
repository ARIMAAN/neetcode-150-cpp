# Hash Set ✅ Optimal

> **Time:** O(n) &nbsp;|&nbsp; **Space:** O(n)

---

## Key Insight

The whole trick is: **only start counting from the beginning of a sequence**.

How do we know if `num` is a sequence start? Check if `num - 1` exists in the set. If it doesn't, `num` has nothing before it — it's a start.

```
numSet = {2, 3, 4, 5, 10, 20}

num=2  → 1 not in set → START → count 2,3,4,5 → length 4
num=3  → 2 in set     → SKIP
num=4  → 3 in set     → SKIP
num=5  → 4 in set     → SKIP
num=10 → 9 not in set → START → count 10 → length 1
num=20 → 19 not in set → START → count 20 → length 1
```

---

## Intuition

Put all numbers in a hash set for O(1) lookup. For each number, only start counting a sequence if it's the **start** of a sequence — meaning `num - 1` does NOT exist in the set. Then count upward as far as possible.

This avoids redundant work: we never start counting from the middle of a sequence.

---

## Why Only Start From Sequence Beginnings?

If we started counting from every number, we'd recount the same sequences multiple times. For example with `[2,3,4,5]`:
- Starting from 3 → counts 3,4,5 (length 3) — redundant
- Starting from 2 → counts 2,3,4,5 (length 4) — correct

By checking `num - 1` not in set, we only start from `2` and skip `3,4,5`.

---

## Code

```cpp
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        unordered_set<int> numSet(nums.begin(), nums.end());
        int longest = 0;

        for (int num : numSet) {
            // only start a sequence from its beginning
            if (numSet.find(num - 1) == numSet.end()) {
                int length = 1;

                while (numSet.find(num + length) != numSet.end()) {
                    length++;
                }
                longest = max(longest, length);
            }
        }
        return longest;
    }
};
```

---

## Dry Run

**Input:** `nums = [2,20,4,10,3,4,5]`

numSet = `{2,20,4,10,3,5}` (duplicates removed)

| num | num-1 in set? | start sequence? | count up | length |
|-----|---------------|-----------------|----------|--------|
| 2 | 1 → ❌ | ✅ yes | 2→3→4→5, 6 missing | 4 |
| 20 | 19 → ❌ | ✅ yes | 21 missing | 1 |
| 4 | 3 → ✅ | ❌ skip | — | — |
| 10 | 9 → ❌ | ✅ yes | 11 missing | 1 |
| 3 | 2 → ✅ | ❌ skip | — | — |
| 5 | 4 → ✅ | ❌ skip | — | — |

**longest = 4** ✅

---

**Input:** `nums = [0,3,2,5,4,6,1,1]`

numSet = `{0,1,2,3,4,5,6}`

Only `0` has no `num-1` in set → count: 0→1→2→3→4→5→6 → length = 7

**Output:** `7` ✅

---

## Why Is This O(n)?

The while loop looks like it could make this O(n²), but each number is visited **at most twice**:
1. Once when iterating over the set
2. Once inside a while loop (only if it's part of a sequence started by another number)

Total work across all while loops = n. So overall O(n).

> Concrete example: `[1,2,3,4,5]` — only `1` triggers the while loop, which runs 4 times. Numbers `2,3,4,5` are each visited once in the outer loop (skipped) and once in the while loop. Total = 5+4 = 9 ops, not 25.

---

## Edge Cases

| Case | Output | Note |
|------|--------|------|
| Empty array | 0 | `longest` starts at 0 |
| All duplicates `[3,3,3]` | 1 | set deduplicates, one sequence of length 1 |
| Single element | 1 | one sequence of length 1 |
| Already consecutive `[1,2,3]` | 3 | starts from 1 |

---

## Complexity

| | |
|--|--|
| **Time** | O(n) — each element visited at most twice total |
| **Space** | O(n) — hash set stores all unique elements |
