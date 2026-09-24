# Hash Set ✅ Optimal

> **Time:** O(n) &nbsp;|&nbsp; **Space:** O(n)

---

## Intuition

Use an `unordered_set` to track elements seen so far. For each element, if it's already in the set — it's a duplicate. Otherwise insert it and move on. Single pass, O(1) average lookup per element.

---

## Algorithm

1. Create an empty `unordered_set<int> seen`.
2. For each element `n` in `nums`:
   - If `seen.count(n) > 0` → return `true`.
   - Else insert `n` into `seen`.
3. Return `false` if loop completes.

---

## Code

```cpp
class Solution {
public:
    bool hasDuplicate(vector<int>& nums) {
        unordered_set<int> seen;
        for (int n : nums) {
            if (seen.count(n)) return true;
            seen.insert(n);
        }
        return false;
    }
};
```

---

## Dry Run

**Input:** `nums = [1, 2, 3, 3]`

| Step | n | seen (before) | In set? | Action |
|------|---|---------------|---------|--------|
| 1 | 1 | {} | ❌ | insert 1 |
| 2 | 2 | {1} | ❌ | insert 2 |
| 3 | 3 | {1,2} | ❌ | insert 3 |
| 4 | 3 | {1,2,3} | ✅ | return `true` |

---

## Complexity

| | |
|--|--|
| **Time** | O(n) — single pass, O(1) avg lookup |
| **Space** | O(n) — set stores up to n elements |
