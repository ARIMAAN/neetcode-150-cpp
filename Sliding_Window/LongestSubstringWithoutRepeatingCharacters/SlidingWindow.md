# Sliding Window

## Intuition

Maintain a window `[left, right]` where all characters are unique.
Expand right every step. If `s[right]` is already in the window, shrink from left until it's removed.
At each step, the window is always valid — so just track the max size.

## Algorithm

1. Use an `unordered_set<char>` to track chars in current window
2. `left = 0`, iterate `right` from 0 to n-1
3. While `s[right]` is in the set → remove `s[left]` from set, `left++`
4. Insert `s[right]` into set
5. Update `maxLen = max(maxLen, right - left + 1)`
6. Return `maxLen`

## Code

```cpp
int lengthOfLongestSubstring(string s) {
    unordered_set<char> window;
    int left = 0, maxLen = 0;
    for (int right = 0; right < s.size(); right++) {
        while (window.count(s[right]))
            window.erase(s[left++]);
        window.insert(s[right]);
        maxLen = max(maxLen, right - left + 1);
    }
    return maxLen;
}
```

## Dry Run — `"abcabcbb"`

| right | s[right] | window before | action | left | window after | maxLen |
|-------|----------|---------------|--------|------|--------------|--------|
| 0 | a | {} | insert a | 0 | {a} | 1 |
| 1 | b | {a} | insert b | 0 | {a,b} | 2 |
| 2 | c | {a,b} | insert c | 0 | {a,b,c} | 3 |
| 3 | a | {a,b,c} | remove a (left=1), insert a | 1 | {b,c,a} | 3 |
| 4 | b | {b,c,a} | remove b (left=2), insert b | 2 | {c,a,b} | 3 |
| 5 | c | {c,a,b} | remove c (left=3), insert c | 3 | {a,b,c} | 3 |
| 6 | b | {a,b,c} | remove a(left=4), remove b(left=5)... wait — remove a,b,c one by one until b gone | 5 | {c,b} | 3 |
| 7 | b | {c,b} | remove c(left=6), remove b(left=7)... | 7 | {b} | 3 |

Final answer: **3** ✅

## Dry Run — `"pwwkew"`

| right | s[right] | action | left | maxLen |
|-------|----------|--------|------|--------|
| 0 | p | insert | 0 | 1 |
| 1 | w | insert | 0 | 2 |
| 2 | w | remove p? no — remove w (left=1), insert w | 1 | 2 |

wait — window is {p,w}, s[right]='w' is in window → remove s[left]='p' → left=1, window={w}, still 'w' in window → remove s[left]='w' → left=2, window={}, insert 'w' → window={w}

| right | s[right] | window before | left after shrink | window after | maxLen |
|-------|----------|---------------|-------------------|--------------|--------|
| 0 | p | {} | 0 | {p} | 1 |
| 1 | w | {p} | 0 | {p,w} | 2 |
| 2 | w | {p,w} | 2 | {w} | 2 |
| 3 | k | {w} | 2 | {w,k} | 2 |
| 4 | e | {w,k} | 2 | {w,k,e} | 3 |
| 5 | w | {w,k,e} | 3 | {k,e,w} | 3 |

Final answer: **3** ✅

## Edge Cases

| Input | Output | Reason |
|-------|--------|--------|
| `""` | `0` | empty string, loop never runs |
| `"a"` | `1` | single char |
| `"abcdef"` | `6` | all unique, window grows to full string |
| `"aaaaaa"` | `1` | all same, window always size 1 |

## Why the While Loop (not if)?

When a duplicate is found, we shrink left one step at a time.
We need a `while` because after removing `s[left]`, the duplicate might still be in the window
(e.g., if the same char appeared multiple times before — though with a set that can't happen,
but the while is the correct pattern for sliding window shrinking).

Actually with a set, one removal is always enough since the set only holds unique chars.
But `while` is the standard pattern and works correctly regardless.

## Complexity

- **Time**: O(n) — each character is added and removed from the set at most once
- **Space**: O(min(n, 26)) — set holds at most the alphabet size (or charset size)
