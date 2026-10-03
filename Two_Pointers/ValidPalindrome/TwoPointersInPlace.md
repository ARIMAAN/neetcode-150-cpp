# Two Pointers In-Place ✅ Optimal

> **Time:** O(n) &nbsp;|&nbsp; **Space:** O(1)

---

## Intuition

Skip the filtered string entirely. Use two pointers directly on the original string — skip non-alphanumeric characters on the fly, compare lowercase versions of valid characters.

Same logic, no extra string needed.

> Realized after writing the filter approach that we don't actually need to build the filtered string. We can just skip bad characters while moving the pointers.

---

## Code

```cpp
class Solution {
public:
    bool isPalindrome(string s) {
        int left = 0, right = s.size() - 1;

        while (left < right) {
            // skip non-alphanumeric from left
            while (left < right && !isalnum(s[left])) left++;
            // skip non-alphanumeric from right
            while (left < right && !isalnum(s[right])) right--;

            if (tolower(s[left]) != tolower(s[right])) return false;

            left++;
            right--;
        }
        return true;
    }
};
```

---

## Dry Run

**Input:** `s = "Was it a car or a cat I saw?"`

| left | right | s[left] | s[right] | skip? | match? |
|------|-------|---------|----------|-------|--------|
| 0 | 27 | 'W' | '?' | right skips to 26 ('w') | tolower('W')==tolower('w') ✅ |
| 1 | 25 | 'a' | 'a' | — | ✅ |
| 2 | 24 | 's' | 's' | — | ✅ |
| 3 | 23 | ' ' | 'i' | left skips to 4 ('i') | ✅ |
| ... | ... | ... | ... | ... | ✅ |

**Output:** `true` ✅

---

**Input:** `s = "tab a cat"`

| left | right | s[left] | s[right] | match? |
|------|-------|---------|----------|--------|
| 0 | 8 | 't' | 't' | ✅ |
| 1 | 7 | 'a' | 'a' | ✅ |
| 2 | 6 | 'b' | 'c' | ❌ → return false |

**Output:** `false` ✅

---

## Why `left < right` Inside Inner While?

```cpp
while (left < right && !isalnum(s[left])) left++;
```

Without the `left < right` guard, if the entire string is non-alphanumeric (e.g. `"!!!"`), `left` would go past `right` and we'd compare garbage indices.

---

## What Happens With All Non-Alphanumeric?

```
s = "!!!"
left=0, right=2
inner while: left skips to 3, but left < right stops it at 2
outer while: left(2) < right(2) is false → exit
return true  ← empty string is a palindrome
```

---

## Complexity

| | |
|--|--|
| **Time** | O(n) — each character visited at most once |
| **Space** | O(1) — no extra string, just two pointers |

---

## Comparison

| Approach | Time | Space | Notes |
|----------|------|-------|-------|
| Filter + Two Pointers | O(n) | O(n) | Cleaner to read, extra string |
| Two Pointers In-Place ✅ | O(n) | O(1) | Optimal, skip non-alnum on the fly |
