# Two Pointers ✅ Optimal

> **Time:** O(n) &nbsp;|&nbsp; **Space:** O(1)

---

## Intuition

Instead of precomputing prefix/suffix arrays, maintain `leftMax` and `rightMax` on the fly with two pointers. The key observation:

- If `leftMax < rightMax` → the water at `left` is determined by `leftMax` (right side is guaranteed ≥ rightMax ≥ leftMax, so it won't be the bottleneck)
- Move the pointer on the side with the smaller max inward

---

## Why This Works

```
At any point:
  leftMax  = max height seen from left  up to 'left'
  rightMax = max height seen from right up to 'right'

If leftMax < rightMax:
  Whatever is at right side, it's at least rightMax > leftMax
  So water at current left = leftMax - height[left]
  (right side is guaranteed to not be the limiting factor)
  → process left, move left++

If rightMax <= leftMax:
  Same logic symmetrically
  → process right, move right--
```

> This is the same greedy idea as Container With Most Water — always process the side with the smaller max because the other side is guaranteed to not be the bottleneck.

---

## Code

```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        int left = 0;
        int right = height.size() - 1;
        int leftMax = height[left];
        int rightMax = height[right];
        int water = 0;

        while (left < right) {
            if (leftMax < rightMax) {
                left++;
                leftMax = max(leftMax, height[left]);  // update max before adding water
                water += leftMax - height[left];        // always >= 0 since leftMax >= height[left]
            } else {
                right--;
                rightMax = max(rightMax, height[right]);
                water += rightMax - height[right];
            }
        }
        return water;
    }
};
```

---

## Dry Run

**Input:** `height = [0,2,0,3,1,0,1,3,2,1]`

Initial: left=0, right=9, leftMax=0, rightMax=1

| step | left | right | leftMax | rightMax | action | water added | total |
|------|------|-------|---------|----------|--------|-------------|-------|
| 1 | 0 | 9 | 0 | 1 | lM<rM → left++ | — | 0 |
| 2 | 1 | 9 | 2 | 1 | lM≥rM → right-- | rM=max(1,1)=1, 1-1=0 | 0 |
| 3 | 1 | 8 | 2 | 2 | lM≥rM → right-- | rM=max(1,2)=2, 2-2=0 | 0 |
| 4 | 1 | 7 | 2 | 3 | lM<rM → left++ | lM=max(2,0)=2, 2-0=2 | 2 |
| 5 | 2 | 7 | 2 | 3 | lM<rM → left++ | lM=max(2,3)=3, 3-3=0 | 2 |
| 6 | 3 | 7 | 3 | 3 | lM≥rM → right-- | rM=max(3,1)=3, 3-1=2 | 4 |
| 7 | 3 | 6 | 3 | 3 | lM≥rM → right-- | rM=max(3,0)=3, 3-0=3 | 7 |
| 8 | 3 | 5 | 3 | 3 | lM≥rM → right-- | rM=max(3,1)=3, 3-1=2 | 9 |
| 9 | 3 | 4 | 3 | 3 | left=3 right=4, lM≥rM → right-- | rM=max(3,1)=3, 3-1=2... left=right stop | 9 |

**Output:** `9` ✅

---

## Why `water += leftMax - height[left]` Is Always ≥ 0

After `leftMax = max(leftMax, height[left])`, `leftMax` is guaranteed to be ≥ `height[left]`. So the subtraction never goes negative. No need for a separate check.

> This is the same reason we update `leftMax` BEFORE computing water, not after.

---

## Edge Cases

| Case | Output | Note |
|------|--------|------|
| `[3,0,3]` | 3 | Classic valley |
| `[1,0,1]` | 1 | Minimum trap |
| Monotone increasing | 0 | No water trapped |
| Monotone decreasing | 0 | No water trapped |
| Single bar | 0 | Nothing to trap |

---

## Complexity

| | |
|--|--|
| **Time** | O(n) — each pointer moves inward at most n times |
| **Space** | O(1) — just 4 variables |

---

## Comparison

| Approach | Time | Space | Notes |
|----------|------|-------|-------|
| Prefix/Suffix Arrays | O(n) | O(n) | Easy to understand |
| Two Pointers ✅ | O(n) | O(1) | Same time, no extra arrays |
