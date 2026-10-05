# Brute Force

> **Time:** O(n³) &nbsp;|&nbsp; **Space:** O(1)

---

## Intuition

Try every combination of three indices. If they sum to 0, add to result. Use a set to avoid duplicate triplets.

---

## Code

```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        int n = nums.size();
        set<vector<int>> res;

        for (int i = 0; i < n - 2; i++) {
            for (int j = i + 1; j < n - 1; j++) {
                for (int k = j + 1; k < n; k++) {
                    if (nums[i] + nums[j] + nums[k] == 0) {
                        vector<int> triplet = {nums[i], nums[j], nums[k]};
                        sort(triplet.begin(), triplet.end());
                        res.insert(triplet);
                    }
                }
            }
        }
        return vector<vector<int>>(res.begin(), res.end());
    }
};
```

---

## Dry Run

**Input:** `nums = [-1,0,1,2,-1,-4]`

Checking all triplets that sum to 0:
- i=0,j=1,k=2: -1+0+1 = 0 ✅ → [-1,0,1]
- i=0,j=1,k=4: -1+0+(-1) = -2 ❌
- i=0,j=2,k=4: -1+1+(-1) = -1 ❌
- i=0,j=3,k=4: -1+2+(-1) = 0 ✅ → [-1,-1,2]
- ... (many more checks)

**Output:** `[[-1,-1,2],[-1,0,1]]` ✅

---

## Complexity

| | |
|--|--|
| **Time** | O(n³) — three nested loops |
| **Space** | O(1) ignoring output |

> ⚠️ TLE for n=3000. Need O(n²) solution.
