# Brute Force (Sort by Frequency)

> **Time:** O(n log n) &nbsp;|&nbsp; **Space:** O(n)

---

## Intuition

Count the frequency of each element using a hash map, then sort the unique elements by their frequency in descending order. Pick the first `k` elements.

---

## Algorithm

1. Build `count` map: `num → frequency`.
2. Extract all unique keys into a vector `keys`.
3. Sort `keys` by `count[key]` descending.
4. Return first `k` elements of sorted `keys`.

---

## Code

```cpp
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int, int> count;
        for (int n : nums) count[n]++;

        vector<int> keys;
        for (auto& entry : count) keys.push_back(entry.first);

        sort(keys.begin(), keys.end(), [&](int a, int b) {
            return count[a] > count[b];
        });

        return vector<int>(keys.begin(), keys.begin() + k);
    }
};
```

> 💡 The lambda `[&]` captures `count` by reference so the comparator can access frequencies.

---

## Dry Run

**Input:** `nums = [1,2,2,3,3,3]`, `k = 2`

Build count map:
| num | freq |
|-----|------|
| 1   | 1    |
| 2   | 2    |
| 3   | 3    |

After sorting keys by freq desc: `[3, 2, 1]`

Return first `k=2`: `[3, 2]` ✅

---

**Input:** `nums = [7,7]`, `k = 1`

Count: `{7:2}` → keys: `[7]` → sorted: `[7]` → return `[7]` ✅

---

## Complexity

| | |
|--|--|
| **Time** | O(n log n) — dominated by sort |
| **Space** | O(n) — count map + keys vector |

> ⚠️ Not optimal — sorting all unique elements is unnecessary when we only need top k.

> ⚠️ Will TLE on large inputs when combined with high unique element count.
