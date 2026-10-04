# Two Pointers ✅ Optimal

> **Time:** O(n) &nbsp;|&nbsp; **Space:** O(1)

---

## Intuition

Since the array is sorted, place one pointer at the start and one at the end. Check their sum:
- Sum == target → found it
- Sum > target → right pointer moves left (need smaller value)
- Sum < target → left pointer moves right (need larger value)

The sorted order guarantees we'll always find the answer.

---

## Why This Works

```
numbers = [1, 2, 3, 4],  target = 3

left=0 (val=1), right=3 (val=4)
sum = 5 > 3  → move right left

left=0 (val=1), right=2 (val=3)
sum = 4 > 3  → move right left

left=0 (val=1), right=1 (val=2)
sum = 3 == 3 → return [1, 2]  ✅
```

> Key: sorted order means moving left pointer always increases sum, moving right pointer always decreases sum. So every move is a deliberate decision, not a guess.

---

## Code

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        int left = 0, right = numbers.size() - 1;

        while (left < right) {
            int sum = numbers[left] + numbers[right];

            if (sum == target) {
                return {left + 1, right + 1}; // convert to 1-indexed
            } else if (sum > target) {
                right--; // sum too big, shrink from right
            } else {
                left++;  // sum too small, grow from left
            }
        }
        return {}; // guaranteed to find answer, never reaches here
    }
};
```

---

## Dry Run

**Input:** `numbers = [1,2,3,4]`, `target = 3`

| left | right | numbers[left] | numbers[right] | sum | action |
|------|-------|---------------|----------------|-----|--------|
| 0 | 3 | 1 | 4 | 5 | 5>3 → right-- |
| 0 | 2 | 1 | 3 | 4 | 4>3 → right-- |
| 0 | 1 | 1 | 2 | 3 | 3==3 → return [1,2] |

**Output:** `[1,2]` ✅

---

**Input:** `numbers = [2,7,11,15]`, `target = 9`

| left | right | sum | action |
|------|-------|-----|--------|
| 0 | 3 | 2+15=17 | 17>9 → right-- |
| 0 | 2 | 2+11=13 | 13>9 → right-- |
| 0 | 1 | 2+7=9 | ==9 → return [1,2] |

**Output:** `[1,2]` ✅

---

**Input:** `numbers = [-3,-1,0,2,4]`, `target = 1`

| left | right | sum | action |
|------|-------|-----|--------|
| 0 | 4 | -3+4=1 | ==1 → return [1,5] |

**Output:** `[1,5]` ✅

---

## Why Two Pointers Works On Sorted Arrays

```
If sum > target:
  We need a smaller sum.
  Left is already the smallest available → must shrink right.

If sum < target:
  We need a larger sum.
  Right is already the largest available → must grow left.

Each step eliminates one element from consideration → O(n) total.
```

---

## Edge Cases

| Case | Note |
|------|------|
| Two elements | `left=0, right=1` — checked immediately |
| Negatives | Works fine, same logic |
| Answer at ends | `left=0, right=n-1` — found on first check |

---

## Complexity

| | |
|--|--|
| **Time** | O(n) — at most n steps, each pointer moves inward |
| **Space** | O(1) — just two integer pointers |

---

## Comparison

| Approach | Time | Space | Satisfies Constraint? |
|----------|------|-------|-----------------------|
| Hash Map | O(n) | O(n) | ❌ |
| Two Pointers ✅ | O(n) | O(1) | ✅ |
