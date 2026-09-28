# Bucket Sort ✅ Optimal

> **Time:** O(n) &nbsp;|&nbsp; **Space:** O(n)

---

## Intuition

The maximum possible frequency of any element is `n` (if all elements are the same). So create a bucket array of size `n+1` where index `i` holds all elements that appear exactly `i` times. Then iterate from the highest frequency bucket downward, collecting elements until we have `k`.

---

## Key Insight

```
freq can only range from 1 to n
→ use freq as the index into a bucket array of size n+1
→ iterate buckets from high to low → naturally sorted by frequency
```

No sorting needed → O(n).

> This is a classic **Counting Sort** variant — works because the value domain (frequency) is bounded.

---

## Algorithm

1. Build `count` map: `num → frequency`.
2. Create `freq` vector of size `n+1` (index = frequency).
3. For each `{num, freq}` in count, push `num` into `freq[freq]`.
4. Iterate `freq` from index `n` down to `1`, collecting nums into result.
5. Stop once `result.size() == k`.

---

## Code

```cpp
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int, int> count;
        for (int n : nums) count[n]++;

        vector<vector<int>> freq(nums.size() + 1);
        for (auto& [num, cnt] : count) {
            freq[cnt].push_back(num);
        }

        vector<int> res;
        for (int i = freq.size() - 1; i > 0; --i) {
            for (int n : freq[i]) {
                res.push_back(n);
                if (res.size() == k) return res;
            }
        }
        return res;
    }
};
```

---

## Dry Run

**Input:** `nums = [1,2,2,3,3,3]`, `k = 2`

**Step 1 — Build count map:**
| num | freq |
|-----|------|
| 1   | 1    |
| 2   | 2    |
| 3   | 3    |

**Step 2 — Fill buckets** (`freq` size = 7):

| index | bucket contents |
|-------|-----------------|
| 0     | []              |
| 1     | [1]             |
| 2     | [2]             |
| 3     | [3]             |
| 4     | []              |
| 5     | []              |
| 6     | []              |

**Step 3 — Iterate from index 6 down:**

| i | bucket | res | size == k? |
|---|--------|-----|------------|
| 6 | [] | [] | No |
| 5 | [] | [] | No |
| 4 | [] | [] | No |
| 3 | [3] | [3] | No |
| 2 | [2] | [3,2] | ✅ return |

**Output:** `[3, 2]` ✅

---

**Input:** `nums = [7,7]`, `k = 1`

Count: `{7:2}` → `freq[2] = [7]`

Iterate from index 2 → push 7 → `res.size() == 1` → return `[7]` ✅

---

## Edge Cases

| Case | Example | Expected |
|------|---------|----------|
| All same elements | `[3,3,3]`, k=1 | `[3]` |
| k = total unique | `[1,2,3]`, k=3 | `[1,2,3]` |
| Single element | `[7,7]`, k=1 | `[7]` |
| All unique | `[1,2,3,4]`, k=2 | any 2 (all freq=1) |

---

## Complexity

| | |
|--|--|
| **Time** | O(n) — count map O(n) + fill buckets O(n) + scan buckets O(n) |
| **Space** | O(n) — count map + freq array both O(n) |

---

## Comparison

| Approach | Time | Space | Notes |
|----------|------|-------|-------|
| Brute Force (Sort) | O(n log n) | O(n) | Simple but slow |
| Min-Heap | O(n log k) | O(n) | Good when k << n |
| Bucket Sort ✅ | O(n) | O(n) | Optimal — exploits freq ≤ n |
