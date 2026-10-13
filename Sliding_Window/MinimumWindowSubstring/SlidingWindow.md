# Sliding Window

## Intuition

Expand the right pointer until the window contains all chars of `t`.
Then shrink the left pointer as far as possible while still valid.
Record the window size. Move right again. Repeat until right reaches end.

## Algorithm

1. Build `need` map from `t`. Set `have = 0`, `required = need.size()`
2. Expand `right`: add `s[right]` to window map. If its count matches `need`, increment `have`
3. While `have == required`: update result if window is smaller, remove `s[left]`, advance `left`
4. Return result string

> We store `minLeft` and `minLen` instead of the actual substring.
> Only extract the substring at the end with `s.substr(minLeft, minLen)`.
> This avoids O(n) string copies during the loop.

## Code

```cpp
string minWindow(string s, string t) {
    unordered_map<char, int> need, window;
    for (char c : t) need[c]++;
    int have = 0, required = need.size();
    int left = 0, minLen = INT_MAX, minLeft = 0;
    for (int right = 0; right < s.size(); right++) {
        char c = s[right];
        window[c]++;
        if (need.count(c) && window[c] == need[c]) have++;
        while (have == required) {
            if (right - left + 1 < minLen) {
                minLen = right - left + 1;
                minLeft = left;
            }
            window[s[left]]--;
            if (need.count(s[left]) && window[s[left]] < need[s[left]]) have--;
            left++;
        }
    }
    return minLen == INT_MAX ? "" : s.substr(minLeft, minLen);
}
```

## Dry Run — s=`"ADOBECODEBANC"`, t=`"ABC"`

need = {A:1, B:1, C:1}, required = 3

| right | char | have | window valid? | action |
|-------|------|------|---------------|--------|
| 0 | A | 1 | no | expand |
| 1 | D | 1 | no | expand |
| 2 | O | 1 | no | expand |
| 3 | B | 2 | no | expand |
| 4 | E | 2 | no | expand |
| 5 | C | 3 | ✅ | shrink: remove A(left=0)→have=2, left=1 |
| 6 | O | 2 | no | expand |
| 7 | D | 2 | no | expand |
| 8 | E | 2 | no | expand |
| 9 | B | 2 | no | expand |
| 10 | A | 3 | ✅ | shrink: remove D,O,B,E,C one by one → left=9, window="BANC" |
| 11 | N | 2 | no | expand |
| 12 | C | 3 | ✅ | shrink: remove B(left=9)→have=2, left=10 |

Minimum window recorded: `"BANC"` (length 4) ✅

## Why `window[c] == need[c]` and not `>=`?

We only increment `have` when the count exactly hits the required amount.
If `need[A] = 2` and window has 3 A's, `have` was already incremented when count hit 2.
Adding more doesn't double-count. Removing one (count goes 3→2) doesn't decrement `have` either.
Only when count drops below `need[c]` do we decrement `have`.

> This is the trickiest part of this problem.
> The `==` check on increment + `<` check on decrement is the correct pair.

## Edge Cases

| Input | Output | Reason |
|-------|--------|--------|
| s=`"a"`, t=`"aa"` | `""` | not enough chars in s |
| s=`"a"`, t=`"a"` | `"a"` | exact match |
| t longer than s | `""` | can never contain all of t |

> When no valid window exists, `minLen` stays `INT_MAX`.
> The ternary `minLen == INT_MAX ? "" : s.substr(...)` handles this cleanly.

## Complexity

- **Time**: O(n + m) — each char added and removed from window at most once
- **Space**: O(m) — need map + window map, at most O(|t|) unique chars

> The while loop inside the for loop is still O(n) total — same amortized argument:
> left only moves forward, so total left increments across entire run = O(n).

## Comparison

| | Brute Force | Sliding Window |
|---|---|---|
| Time | O(n² · m) | O(n + m) |
| Space | O(m) | O(m) |
| Key idea | try every substring | expand then shrink |

## Thought Process

This is the hardest sliding window problem. The key steps:
1. Realize it's a sliding window (variable size, find minimum)
2. Figure out the validity condition (have all chars of t)
3. Use have/need counters to check validity in O(1)
4. Store indices not substring to avoid copies
