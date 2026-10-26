# Brute Force — Linear Scan

## Intuition

Just scan every element from left to right. Return the index when we find the target. No tricks needed — but also no use of the sorted property.

This is the naive approach you'd use if the array wasn't sorted.

## Algorithm

1. Loop `i` from `0` to `n-1`
2. If `nums[i] == target`, return `i`
3. If loop ends without finding, return `-1`

## Code

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] == target) return i;
        }
        return -1;
    }
};
```

## Dry Run

`nums = [-1, 0, 3, 5, 9, 12]`, `target = 9`

| i | nums[i] | == target? |
|---|---------|------------|
| 0 | -1 | No |
| 1 | 0 | No |
| 2 | 3 | No |
| 3 | 5 | No |
| 4 | 9 | ✅ return 4 |

## Complexity

- Time: O(n) — worst case we scan the whole array
- Space: O(1) — no extra memory

## Why This Is Terrible Here

The problem explicitly says O(log n) is required. Also, the array is sorted — ignoring that is wasteful. If n = 10^4, linear scan does 10,000 comparisons. Binary search does ~14.
