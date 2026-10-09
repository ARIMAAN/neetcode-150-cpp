# Brute Force

## Intuition

Try every possible substring. For each one, check if all characters are unique.
Track the maximum length among all valid substrings.

> Substring = contiguous. Don't confuse with subsequence (non-contiguous).
> `"pwke"` is a subsequence of `"pwwkew"`, not a substring.

## Algorithm

1. For every starting index `i`, for every ending index `j >= i`
2. Extract substring `s[i..j]`, check if all chars are unique using a set
3. If unique, update `maxLen`
4. Return `maxLen`

> The inner loop breaks early when a duplicate is found — no need to check longer substrings starting at `i`.

## Code

```cpp
int lengthOfLongestSubstring(string s) {
    int maxLen = 0;
    for (int i = 0; i < s.size(); i++) {
        unordered_set<char> seen;
        for (int j = i; j < s.size(); j++) {
            if (seen.count(s[j])) break;
            seen.insert(s[j]);
            maxLen = max(maxLen, j - i + 1);
        }
    }
    return maxLen;
}
```

## Dry Run — `"abcabcbb"`

| i | j | seen | maxLen |
|---|---|------|--------|
| 0 | 0 | {a} | 1 |
| 0 | 1 | {a,b} | 2 |
| 0 | 2 | {a,b,c} | 3 |
| 0 | 3 | 'a' duplicate → break | 3 |
| 1 | 1 | {b} | 3 |
| 1 | 2 | {b,c} | 3 |
| 1 | 3 | {b,c,a} | 3 |
| 1 | 4 | 'b' duplicate → break | 3 |
| ... | ... | ... | 3 |

Final answer: **3**

## Complexity

- **Time**: O(n²) — two nested loops
- **Space**: O(n) — set can hold up to n characters

## Edge Cases

| Input | Output |
|-------|--------|
| `""` | `0` |
| `"a"` | `1` |
| `"abcdef"` | `6` |

## Why This Is Slow

For `n = 10^5`, this is `10^10` operations — way too slow (TLE).
We're re-checking overlapping substrings from scratch every time.
