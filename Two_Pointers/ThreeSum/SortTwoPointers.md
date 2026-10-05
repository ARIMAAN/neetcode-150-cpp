# Sort + Two Pointers ✅ Optimal

> **Time:** O(n²) &nbsp;|&nbsp; **Space:** O(1)

---

## Intuition

Sort the array. Fix one element `nums[i]`, then use two pointers on the remaining subarray to find pairs that sum to `-nums[i]`. This reduces 3Sum to repeated Two Sum II.

Sorting also makes duplicate skipping trivial — duplicates are adjacent, so just skip them.

---

## Why Sort First?

1. Enables two pointers (need sorted order to know which direction to move)
2. Makes duplicate detection easy — same values are adjacent
3. Early termination — if `nums[i] > 0`, no triplet can sum to 0 (all remaining are ≥ nums[i])

> Without sorting, detecting duplicates would require a hash set which adds O(n) space. Sorting makes it O(1).

---

## Algorithm

1. Sort `nums`.
2. For each `i` from `0` to `n-3`:
   - Skip if `nums[i] == nums[i-1]` (duplicate outer element)
   - Skip if `nums[i] > 0` (can't sum to 0)
   - Set `left = i+1`, `right = n-1`
   - While `left < right`:
     - If sum == 0 → add triplet, skip duplicates on both sides, move both pointers
     - If sum > 0 → `right--`
     - If sum < 0 → `left++`
3. Return result.

---

## Code

```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        vector<vector<int>> res;

        for (int i = 0; i < nums.size() - 2; i++) {
            if (nums[i] > 0) break;                        // all remaining > 0, can't sum to 0
            if (i > 0 && nums[i] == nums[i - 1]) continue; // skip duplicate i

            int left = i + 1, right = nums.size() - 1;

            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];

                if (sum == 0) {
                    res.push_back({nums[i], nums[left], nums[right]});
                    while (left < right && nums[left] == nums[left + 1]) left++;   // skip dup left
                    while (left < right && nums[right] == nums[right - 1]) right--; // skip dup right
                    left++;
                    right--;
                } else if (sum > 0) {
                    right--;
                } else {
                    left++;
                }
            }
        }
        return res;
    }
};
```

---

## Dry Run

**Input:** `nums = [-1,0,1,2,-1,-4]`

After sort: `[-4,-1,-1,0,1,2]`

**i=0, nums[i]=-4:** left=1, right=5
- sum = -4+(-1)+2 = -3 < 0 → left++
- sum = -4+(-1)+2 = -3 < 0 → left++
- sum = -4+0+2 = -2 < 0 → left++
- sum = -4+1+2 = -1 < 0 → left++
- left=right, stop

**i=1, nums[i]=-1:** left=2, right=5
- sum = -1+(-1)+2 = 0 ✅ → add [-1,-1,2], skip dups, left=3, right=4
- sum = -1+0+1 = 0 ✅ → add [-1,0,1], left=4, right=3, stop

**i=2, nums[i]=-1:** same as nums[1] → skip (duplicate)

**i=3, nums[i]=0:** left=4, right=5
- sum = 0+1+2 = 3 > 0 → right--
- left=right, stop

**Output:** `[[-1,-1,2],[-1,0,1]]` ✅

---

**Input:** `nums = [0,0,0]`

After sort: `[0,0,0]`

i=0, left=1, right=2: sum=0 → add [0,0,0] ✅

**Output:** `[[0,0,0]]` ✅

---

## Duplicate Skipping Explained

```
After finding a valid triplet at left=l, right=r:

Skip duplicates on left:
  while nums[left] == nums[left+1] → left++
  (don't want same value at left again)

Skip duplicates on right:
  while nums[right] == nums[right-1] → right--
  (don't want same value at right again)

Then move both inward: left++, right--
```

> Common bug: forgetting to do the final `left++; right--` after skipping. The while loops only skip duplicates, they don't advance past the current valid position.

---

## Early Termination

```cpp
if (nums[i] > 0) break;
```

Since array is sorted, if `nums[i] > 0`, then `nums[left] >= nums[i] > 0` and `nums[right] >= nums[left] > 0`. Sum of three positives can never be 0.

> This is a nice optimization. Without it the code still works, just does unnecessary iterations.

---

## Edge Cases

| Case | Output | Note |
|------|--------|------|
| `[0,1,1]` | `[]` | No valid triplet |
| `[0,0,0]` | `[[0,0,0]]` | All zeros |
| All positive | `[]` | Early break on first i |
| All negative | `[]` | Sum always < 0 |

---

## Complexity

| | |
|--|--|
| **Time** | O(n²) — O(n log n) sort + O(n²) two pointer loop |
| **Space** | O(1) — ignoring output array |

> The outer loop runs n times. For each i, the two pointer inner loop runs at most n times. So total = O(n²). Sorting is O(n log n) which is dominated by O(n²).
