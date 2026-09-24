# Sorting

> **Time:** O(n log n) &nbsp;|&nbsp; **Space:** O(1)

---

## Intuition

If two strings are anagrams, sorting both will produce the **exact same string**. We just sort both and compare. Simple and clean, but not the fastest.

---

## Algorithm

1. If `s.length() != t.length()`, return `false` immediately.
2. Sort both strings.
3. Return `s == t`.

---

## Code

```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        if (s.length() != t.length()) {
            return false;
        }

        sort(s.begin(), s.end());
        sort(t.begin(), t.end());
        return s == t;
    }
};
```

---

## Dry Run

**Input:** `s = "racecar"`, `t = "carrace"`

| Step | s | t |
|------|---|---|
| Original | `racecar` | `carrace` |
| After sort | `accerrr` | `accerrr` |
| s == t? | ✅ → return `true` | |

---

**Input:** `s = "jar"`, `t = "jam"`

| Step | s | t |
|------|---|---|
| Original | `jar` | `jam` |
| After sort | `ajr` | `ajm` |
| s == t? | ❌ → return `false` | |

---

## Complexity

| | |
|--|--|
| **Time** | O(n log n) — dominated by sort |
| **Space** | O(1) — in-place sort |
