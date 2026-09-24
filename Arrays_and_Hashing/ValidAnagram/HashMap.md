# Hash Map ✅ Optimal

> **Time:** O(n) &nbsp;|&nbsp; **Space:** O(1)

---

## Intuition

Count the frequency of each character in both strings using two hash maps. If both maps are identical, the strings are anagrams. Since the input is only lowercase English letters, the space is bounded at 26 characters — effectively O(1).

---

## Algorithm

1. If `s.length() != t.length()`, return `false` immediately.
2. Build `countS` — frequency map for `s`.
3. Build `countT` — frequency map for `t`.
4. Return `countS == countT`.

---

## Code

```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        if (s.length() != t.length()) {
            return false;
        }

        unordered_map<char, int> countS;
        unordered_map<char, int> countT;
        for (int i = 0; i < s.length(); i++) {
            countS[s[i]]++;
            countT[t[i]]++;
        }
        return countS == countT;
    }
};
```

---

## Dry Run

**Input:** `s = "racecar"`, `t = "carrace"`

Building frequency maps:

| char | countS | countT |
|------|--------|--------|
| r | 2 | 2 |
| a | 2 | 2 |
| c | 2 | 2 |
| e | 1 | 1 |

`countS == countT` → ✅ return `true`

---

**Input:** `s = "jar"`, `t = "jam"`

| char | countS | countT |
|------|--------|--------|
| j | 1 | 1 |
| a | 1 | 1 |
| r | 1 | 0 |
| m | 0 | 1 |

`countS != countT` → ❌ return `false`

---

## Complexity

| | |
|--|--|
| **Time** | O(n) — single pass through both strings |
| **Space** | O(1) — at most 26 keys (lowercase letters only) |
