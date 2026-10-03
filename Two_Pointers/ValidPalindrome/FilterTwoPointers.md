# Filter + Two Pointers

> **Time:** O(n) &nbsp;|&nbsp; **Space:** O(n)

---

## Intuition

First clean the string — keep only alphanumeric characters and convert to lowercase. Then use two pointers from both ends and check if they match all the way to the middle.

---

## Code

```cpp
class Solution {
public:
    bool isPalindrome(string s) {
        string filtered;
        for (char c : s) {
            if (isalnum(c)) {
                filtered += tolower(c);
            }
        }

        int left = 0;
        int right = filtered.size() - 1;

        while (left < right) {
            if (filtered[left] != filtered[right]) {
                return false;
            }
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

After filtering: `"wasitacaroracatisaw"`

| left | right | filtered[left] | filtered[right] | match? |
|------|-------|----------------|-----------------|--------|
| 0 | 18 | 'w' | 'w' | ✅ |
| 1 | 17 | 'a' | 'a' | ✅ |
| 2 | 16 | 's' | 's' | ✅ |
| 3 | 15 | 'i' | 'i' | ✅ |
| ... | ... | ... | ... | ✅ |
| 9 | 9 | left >= right → stop | | ✅ |

**Output:** `true` ✅

---

**Input:** `s = "tab a cat"`

After filtering: `"tabacat"`

| left | right | filtered[left] | filtered[right] | match? |
|------|-------|----------------|-----------------|--------|
| 0 | 6 | 't' | 't' | ✅ |
| 1 | 5 | 'a' | 'a' | ✅ |
| 2 | 4 | 'b' | 'c' | ❌ → return false |

**Output:** `false` ✅

---

## Complexity

| | |
|--|--|
| **Time** | O(n) — one pass to filter, one pass to check |
| **Space** | O(n) — filtered string can be up to length n |

> Uses O(n) extra space for the filtered string. Can we avoid that?

---

## `isalnum` and `tolower`

- `isalnum(c)` returns non-zero if `c` is a letter (a-z, A-Z) or digit (0-9)
- `tolower(c)` converts uppercase to lowercase, leaves others unchanged
- Both are from `<cctype>` — included by default in competitive programming
