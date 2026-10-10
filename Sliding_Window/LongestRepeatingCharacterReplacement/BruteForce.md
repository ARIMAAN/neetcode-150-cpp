# Brute Force

## Intuition

Try every possible substring. For each substring, find the most frequent character.
The replacements needed = `length - maxFreq`. If that's `<= k`, it's valid — update the answer.

> The key observation: we always want to keep the most frequent character and replace everything else.
> So we only need to know the max frequency, not which character it is.

## Algorithm

1. For every pair `(i, j)`, consider substring `s[i..j]`
2. Count frequency of each character using `freq[26]`
3. Find `maxFreq = max of freq[]`
4. If `(j - i + 1) - maxFreq <= k`, update `maxLen`
5. Return `maxLen`

> We track `maxFreq` incrementally: after adding `s[j]`, update `maxFreq = max(maxFreq, freq[s[j]-'A'])`.
> This avoids scanning all 26 entries every step, keeping inner loop O(1) instead of O(26).

## Code

```cpp
int characterReplacement(string s, int k) {
    int maxLen = 0;
    for (int i = 0; i < s.size(); i++) {
        int freq[26] = {0};
        int maxFreq = 0;
        for (int j = i; j < s.size(); j++) {
            freq[s[j] - 'A']++;
            maxFreq = max(maxFreq, freq[s[j] - 'A']);
            if ((j - i + 1) - maxFreq <= k)
                maxLen = max(maxLen, j - i + 1);
        }
    }
    return maxLen;
}
```

## Dry Run — `"AAABABB"`, k = 1

| i | j | substring | maxFreq | replacements | valid? | maxLen |
|---|---|-----------|---------|--------------|--------|--------|
| 0 | 0 | A | 1 | 0 | ✅ | 1 |
| 0 | 1 | AA | 2 | 0 | ✅ | 2 |
| 0 | 2 | AAA | 3 | 0 | ✅ | 3 |
| 0 | 3 | AAAB | 3 | 1 | ✅ | 4 |
| 0 | 4 | AAABA | 4 | 1 | ✅ | 5 |
| 0 | 5 | AAABAB | 4 | 2 | ❌ | 5 |
| 0 | 6 | AAABABB | 4 | 3 | ❌ | 5 |
| 1 | ... | ... | ... | ... | ... | 5 |

Final answer: **5** ✅

## Complexity

- **Time**: O(n² · 26) — two loops + scanning freq array for max each time
  - Can be O(n²) if we track maxFreq incrementally (as in code above)
- **Space**: O(26) = O(1) — fixed size frequency array

## Why This Is Slow

For `n = 100,000`, O(n²) = 10^10 operations — TLE.
We're recomputing frequency from scratch for every starting index.
