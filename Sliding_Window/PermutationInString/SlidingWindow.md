# Sliding Window

## Intuition

Two strings are anagrams if and only if their character frequency arrays are identical.
Slide a fixed window of size `len(s1)` across `s2`. At each position, compare freq arrays.
If they match, we found a permutation.

## Algorithm

1. Build `freq1[26]` from `s1`, `freq2[26]` from first `len(s1)` chars of `s2`
2. If `freq1 == freq2`, return `true`
3. Slide window right: add `s2[right]`, remove `s2[left]`, compare again
4. Return `false` if no match found

> `left = right - n` where `n = len(s1)`. We don't need an explicit left pointer
> since the window size is fixed — left is always `right - n`.

## Code

```cpp
bool checkInclusion(string s1, string s2) {
    if (s1.size() > s2.size()) return false;
    int freq1[26] = {0}, freq2[26] = {0};
    int n = s1.size();
    for (int i = 0; i < n; i++) {
        freq1[s1[i] - 'a']++;
        freq2[s2[i] - 'a']++;
    }
    if (equal(freq1, freq1 + 26, freq2)) return true;
    for (int i = n; i < s2.size(); i++) {
        freq2[s2[i] - 'a']++;
        freq2[s2[i - n] - 'a']--;
        if (equal(freq1, freq1 + 26, freq2)) return true;
    }
    return false;
}
```

## Dry Run — s1=`"ab"`, s2=`"eidbaooo"`

n = 2, freq1 = {a:1, b:1}

| window | freq2 | match? |
|--------|-------|--------|
| `"ei"` | {e:1, i:1} | ❌ |
| `"id"` | {i:1, d:1} | ❌ |
| `"db"` | {d:1, b:1} | ❌ |
| `"ba"` | {b:1, a:1} | ✅ |

Return `true` ✅

## Dry Run — s1=`"ab"`, s2=`"eidboaoo"`

n = 2, freq1 = {a:1, b:1}

| window | freq2 | match? |
|--------|-------|--------|
| `"ei"` | {e:1,i:1} | ❌ |
| `"id"` | {i:1,d:1} | ❌ |
| `"db"` | {d:1,b:1} | ❌ |
| `"bo"` | {b:1,o:1} | ❌ |
| `"oa"` | {o:1,a:1} | ❌ |
| `"ao"` | {a:1,o:1} | ❌ |
| `"oo"` | {o:2} | ❌ |

Return `false` ✅

## Edge Cases

| Input | Output | Reason |
|-------|--------|--------|
| s1 longer than s2 | `false` | can't fit, handled upfront |
| s1 == s2 | `true` | s2 itself is a permutation |
| s1 = `"a"`, s2 = `"a"` | `true` | single char match |
| s1 = `"aab"`, s2 = `"ab"` | `false` | s1 longer than s2 |

## Why `equal()` Instead of Manual Loop?

`equal(freq1, freq1+26, freq2)` compares two arrays element by element — O(26) = O(1).
Could also do a manual loop, but `equal` is cleaner.

## Complexity

- **Time**: O(n + m) — build initial window O(n), slide O(m), each comparison O(26) = O(1)
- **Space**: O(26) = O(1) — two fixed frequency arrays

## Comparison

| | Brute Force | Sliding Window |
|---|---|---|
| Time | O(n! · m) | O(n + m) |
| Space | O(n) | O(1) |
| Key idea | enumerate permutations | compare frequencies |
