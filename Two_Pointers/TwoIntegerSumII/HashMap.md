# Hash Map

> **Time:** O(n) &nbsp;|&nbsp; **Space:** O(n)

---

## Intuition

Same as Two Sum I — store each number and its index in a map. For each element, check if `target - nums[i]` already exists.

Works, but uses O(n) space which violates the constraint here.

> Tried this first since I already knew Two Sum I. But the problem says O(1) space so had to think of something better.

---

## Code

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        unordered_map<int, int> seen; // value -> 1-indexed position

        for (int i = 0; i < numbers.size(); i++) {
            int diff = target - numbers[i];
            if (seen.count(diff)) {
                return {seen[diff], i + 1};
            }
            seen[numbers[i]] = i + 1;
        }
        return {};
    }
};
```

---

## Dry Run

**Input:** `numbers = [1,2,3,4]`, `target = 3`

| i | numbers[i] | diff = 3 - numbers[i] | in map? | map after |
|---|------------|----------------------|---------|-----------|
| 0 | 1 | 2 | ❌ | {1:1} |
| 1 | 2 | 1 | ✅ | return [1, 2] |

**Output:** `[1,2]` ✅

---

**Input:** `numbers = [2,7,11,15]`, `target = 9`

| i | numbers[i] | diff | in map? | map after |
|---|------------|------|---------|----------|
| 0 | 2 | 7 | ❌ | {2:1} |
| 1 | 7 | 2 | ✅ | return [1, 2] |

**Output:** `[1,2]` ✅

---

## Complexity

| | |
|--|--|
| **Time** | O(n) |
| **Space** | O(n) — violates the O(1) space constraint |

> ⚠️ Doesn't satisfy the problem's O(1) space requirement. Use two pointers instead.

---

## Why Not Use This Here?

The problem explicitly says O(1) space. Also, the sorted property is a strong hint that two pointers is the intended approach. Hash map ignores the sorted order entirely.
