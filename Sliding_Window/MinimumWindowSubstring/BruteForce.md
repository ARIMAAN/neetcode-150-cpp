# Brute Force

## Intuition

Try every substring of `s`. For each one, check if it contains all characters of `t`.
Among all valid substrings, return the shortest one.

> A substring contains all chars of `t` if for every char `c` in `t`,
> the substring has at least `count(c in t)` occurrences of `c`.

## Algorithm

1. For every pair `(i, j)`, extract `s[i..j]`
2. Check if it contains all chars of `t` using a frequency map
3. If valid and shorter than current best, update answer
4. Return best answer or `""` if none found

## Code

```cpp
string minWindow(string s, string t) {
    string result = "";
    for (int i = 0; i < s.size(); i++) {
        unordered_map<char, int> need;
        for (char c : t) need[c]++;
        int count = t.size();
        for (int j = i; j < s.size(); j++) {
            if (need.count(s[j]) && need[s[j]] > 0) count--;
            need[s[j]]--;
            if (count == 0) {
                if (result.empty() || j - i + 1 < result.size())
                    result = s.substr(i, j - i + 1);
                break;
            }
        }
    }
    return result;
}
```

> We `break` as soon as we find the first valid window starting at `i`.
> Any longer window starting at `i` can't be the minimum.

## Dry Run — s=`"ADOBECODEBANC"`, t=`"ABC"`

| i | first valid j | window | length |
|---|---------------|--------|--------|
| 0 | 5 | `"ADOBEC"` | 6 |
| 1 | 9 | `"DOBECODEBA"` | ... longer |
| ... | ... | ... | ... |
| 9 | 12 | `"BANC"` | 4 ← minimum |

Final answer: `"BANC"` ✅

## Complexity

- **Time**: O(n² · m) — two loops, inner check is O(m)
- **Space**: O(m) — frequency map for `t`

> We rebuild the `need` map from scratch for every `i`.
> That's O(m) per outer iteration — another hidden cost on top of O(n²).

## Why Break Early?

Once we find the first valid window starting at `i`, we break.
Any extension of that window (larger `j`) would only make it longer — not a better answer.
So we move `i` forward and try a new starting point.

## Thought Process

Brute force is the natural first attempt. Two nested loops, check each substring.
The key observation that leads to sliding window: when we move `i` forward by 1,
we only lose one character from the left and gain nothing on the right.
Why recheck everything? Just maintain the window state.

## Related Problems

- [Permutation in String (#567)](../PermutationInString/) — fixed window, easier
- [Longest Repeating Character Replacement (#424)](../LongestRepeatingCharacterReplacement/) — find maximum window
