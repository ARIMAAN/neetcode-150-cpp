# Two Pointers ✅ Optimal

> **Time:** O(n) &nbsp;|&nbsp; **Space:** O(1)

---

## Intuition

Start with the widest possible container — left at 0, right at n-1. Compute area. Then move the pointer with the **shorter** height inward.

Why? The area is limited by the shorter side. Moving the taller side inward reduces width while the height is still capped by the shorter — guaranteed worse or equal. Moving the shorter side is the only chance to find a taller boundary that compensates for the reduced width.

---

## Why Moving The Shorter Side Is Correct

```
Suppose height[left] < height[right].
Current area = height[left] * (right - left).

If we move right inward:
  - width decreases
  - height still capped at height[left] (shorter side unchanged)
  - area can only decrease or stay same → pointless

If we move left inward:
  - width decreases
  - but height[left] might increase → area could improve
  → this is the only hope
```

> This is a greedy argument. We're not missing any better solution because moving the taller side is provably never better.

---

## Code

```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        int left = 0;
        int right = height.size() - 1;
        int maxWater = 0;

        while (left < right) {
            int width = right - left;
            int h = min(height[left], height[right]);
            int area = width * h;

            maxWater = max(maxWater, area);

            if (height[left] < height[right]) {
                left++;   // shorter side on left, move it
            } else {
                right--;  // shorter side on right (or equal), move it
            }
        }
        return maxWater;
    }
};
```

---

## Dry Run

**Input:** `height = [1,8,6,2,5,4,8,3,7]`

| left | right | h[l] | h[r] | width | area | maxWater | move |
|------|-------|------|------|-------|------|----------|------|
| 0 | 8 | 1 | 7 | 8 | 8 | 8 | l++ |
| 1 | 8 | 8 | 7 | 7 | 49 | 49 | r-- |
| 1 | 7 | 8 | 3 | 6 | 18 | 49 | r-- |
| 1 | 6 | 8 | 8 | 5 | 40 | 49 | r-- |
| 1 | 5 | 8 | 4 | 4 | 16 | 49 | r-- |
| 1 | 4 | 8 | 5 | 3 | 15 | 49 | r-- |
| 1 | 3 | 8 | 2 | 2 | 4 | 49 | r-- |
| 1 | 2 | 8 | 6 | 1 | 6 | 49 | r-- |
| left=right → stop | | | | | | | |

**Output:** `49` ✅

---

**Input:** `height = [1,1]`

| left | right | h[l] | h[r] | area | move |
|------|-------|------|------|------|------|
| 0 | 1 | 1 | 1 | 1 | r-- |
| left=right → stop | | | | | |

**Output:** `1` ✅

---

## What If Heights Are Equal?

```cpp
} else {
    right--;  // handles equal case too
}
```

When `height[left] == height[right]`, moving either pointer is fine — both sides are the same height so neither has an advantage. We just pick right by convention.

---

## Edge Cases

| Case | Output | Note |
|------|--------|------|
| `[1,1]` | 1 | Minimum case |
| All same height | `(n-1) * h` | Max width, same height |
| Increasing array | last two elements | Tallest pair |
| One very tall line | limited by other | min() caps it |

---

## Complexity

| | |
|--|--|
| **Time** | O(n) — each pointer moves inward at most n times total |
| **Space** | O(1) — just two pointers and a running max |
