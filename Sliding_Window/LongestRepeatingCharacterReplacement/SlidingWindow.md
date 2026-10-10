# Sliding Window

## Intuition

Maintain a window `[left, right]`. Track the frequency of each character in the window.
The window is valid if `windowSize - maxFreq <= k`.
If invalid, shrink from the left. Track the max valid window size.

## Algorithm

1. `freq[26] = {0}`, `left = 0`, `maxFreq = 0`, `maxLen = 0`
2. Iterate `right` from 0 to n-1:
   - Increment `freq[s[right] - 'A']`
   - Update `maxFreq = max(maxFreq, freq[s[right] - 'A'])`
   - While `(right - left + 1) - maxFreq > k`: decrement `freq[s[left] - 'A']`, `left++`
   - Update `maxLen = max(maxLen, right - left + 1)`
3. Return `maxLen`

> The condition `(right - left + 1) - maxFreq > k` means:
> "the number of non-dominant characters exceeds k" — we can't fix this window with k replacements.

## Code

```cpp
int characterReplacement(string s, int k) {
    int freq[26] = {0};
    int left = 0, maxFreq = 0, maxLen = 0;
    for (int right = 0; right < s.size(); right++) {
        freq[s[right] - 'A']++;
        maxFreq = max(maxFreq, freq[s[right] - 'A']);
        while ((right - left + 1) - maxFreq > k) {
            freq[s[left] - 'A']--;
            left++;
        }
        maxLen = max(maxLen, right - left + 1);
    }
    return maxLen;
}
```

## Dry Run — `"XYYX"`, k = 2

| right | s[r] | freq | maxFreq | windowSize | replacements | valid? | left | maxLen |
|-------|------|------|---------|------------|--------------|--------|------|--------|
| 0 | X | X:1 | 1 | 1 | 0 | ✅ | 0 | 1 |
| 1 | Y | X:1,Y:1 | 1 | 2 | 1 | ✅ | 0 | 2 |
| 2 | Y | X:1,Y:2 | 2 | 3 | 1 | ✅ | 0 | 3 |
| 3 | X | X:2,Y:2 | 2 | 4 | 2 | ✅ | 0 | 4 |

Final answer: **4** ✅

## Dry Run — `"AAABABB"`, k = 1

| right | s[r] | freq | maxFreq | windowSize | replacements | valid? | left | maxLen |
|-------|------|------|---------|------------|--------------|--------|------|--------|
| 0 | A | A:1 | 1 | 1 | 0 | ✅ | 0 | 1 |
| 1 | A | A:2 | 2 | 2 | 0 | ✅ | 0 | 2 |
| 2 | A | A:3 | 3 | 3 | 0 | ✅ | 0 | 3 |
| 3 | B | A:3,B:1 | 3 | 4 | 1 | ✅ | 0 | 4 |
| 4 | A | A:4,B:1 | 4 | 5 | 1 | ✅ | 0 | 5 |
| 5 | B | A:4,B:2 | 4 | 6 | 2 | ❌ | shrink | 5 |
| 5 | - | A:3,B:2 | 4 | 5 | 1 | ✅ | 1 | 5 |
| 6 | B | A:3,B:3 | 4 | 6 | 2 | ❌ | shrink | 5 |
| 6 | - | A:2,B:3 | 4 | 5 | 1 | ✅ | 2 | 5 |

Final answer: **5** ✅

## The maxFreq Trick

`maxFreq` is never decremented even when we shrink the window.

Why is this okay? Because we only care about finding a window **larger** than the current best.
If `maxFreq` drops after shrinking, the window size stays the same (not smaller) — we just slide.
We only grow `maxLen` when we find a genuinely larger valid window.

This means `maxFreq` might be slightly stale — but it never causes a wrong answer,
only prevents unnecessary shrinking. The window size never decreases below the current best.

> This is a subtle but important optimization. Without it, we'd need to rescan
> the entire window to find the new maxFreq after every shrink — making it O(n · 26).
> With this trick, it stays O(n).

## Edge Cases

| Input | k | Output | Reason |
|-------|---|--------|--------|
| `"A"` | 0 | 1 | single char, always valid |
| `"AAAA"` | 2 | 4 | all same, no replacements needed |
| `"ABCD"` | 0 | 1 | k=0, can't replace anything |
| `"ABCD"` | 4 | 4 | can replace all, entire string valid |

## Complexity

- **Time**: O(n) — each character added and removed from window at most once
- **Space**: O(26) = O(1) — fixed size frequency array for uppercase letters

## Comparison

| | Brute Force | Sliding Window |
|---|---|---|
| Time | O(n²) | O(n) |
| Space | O(1) | O(1) |
| Key idea | restart every i | reuse freq, just slide |
