# Brute Force

## Intuition

Generate all permutations of `s1`. For each permutation, check if it appears as a substring in `s2`.
If any does, return `true`.

> This approach is correct but completely impractical.
> Even for `s1 = "abc"` (3 chars), we generate 6 permutations.
> For `s1 = "abcde"` (5 chars), that's 120. For 10 chars, 3.6 million.

## Algorithm

1. Generate all permutations of `s1`
2. For each permutation, use `s2.find(perm) != string::npos`
3. If found, return `true`
4. Return `false`

> `next_permutation` only works correctly if the string is sorted first.
> It generates permutations in lexicographic order and returns false when it wraps back to the first.

## Code

```cpp
bool checkInclusion(string s1, string s2) {
    sort(s1.begin(), s1.end());
    do {
        if (s2.find(s1) != string::npos) return true;
    } while (next_permutation(s1.begin(), s1.end()));
    return false;
}
```

> `next_permutation` generates permutations in lexicographic order.
> We sort first so we start from the smallest permutation and cover all of them.

## Dry Run — s1=`"ab"`, s2=`"eidbaooo"`

Permutations of `"ab"`: `"ab"`, `"ba"`
- `s2.find("ab")` → not found
- `s2.find("ba")` → found at index 3 ✅

Return `true`

## Complexity

- **Time**: O(n! · m) — n! permutations, each `find` is O(m)
- **Space**: O(n) — storing current permutation

## Related Problems

- [Permutation in String Sliding Window](./SlidingWindow.md) — the O(n+m) solution
- [Next Permutation (#31)](https://leetcode.com/problems/next-permutation/) — uses `next_permutation` correctly

## Why This Is Terrible

For `s1 = "abcdefghij"` (10 chars), that's 10! = 3,628,800 permutations.
For `s1` of length 20, it's 20! ≈ 2.4 × 10^18. Completely unusable.
We don't need to enumerate permutations — we just need to compare frequencies.

> The key realization: two strings are anagrams iff their freq arrays match.
> We never need to look at actual permutations at all.

> This approach is correct but completely impractical.
> Even for `s1 = "abc"` (3 chars), we generate 6 permutations.
> For `s1 = "abcde"` (5 chars), that's 120. For 10 chars, 3.6 million.
