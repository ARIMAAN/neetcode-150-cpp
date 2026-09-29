# Delimiter (Naive) ⚠️

> **Time:** O(n) &nbsp;|&nbsp; **Space:** O(n)

---

## Intuition

Join all strings with a special delimiter (e.g. `|`) and split on decode. Simple, but **breaks** if any string contains the delimiter character.

---

## Algorithm

**Encode:**
1. Join all strings with `|` separator.

**Decode:**
1. Split the encoded string on `|`.

---

## Code

```cpp
class Solution {
public:
    string encode(vector<string>& strs) {
        string res;
        for (int i = 0; i < strs.size(); i++) {
            res += strs[i];
            if (i != strs.size() - 1) res += "|";
        }
        return res;
    }

    vector<string> decode(string s) {
        vector<string> res;
        string cur;
        for (char c : s) {
            if (c == '|') {
                res.push_back(cur);
                cur.clear();
            } else {
                cur += c;
            }
        }
        res.push_back(cur);
        return res;
    }
};
```

---

## Escaping Alternative

Another valid approach is **escape sequences** — treat `|` as delimiter but escape any `|` inside strings as `\|`. This works but adds O(n) preprocessing and makes decode more complex.

> Length prefix is simpler and more elegant — no escaping needed.

---

## Why This Fails

```
Input : ["Hello", "Wo|rld"]
Encoded: "Hello|Wo|rld"
Decoded: ["Hello", "Wo", "rld"]  ❌  (3 strings instead of 2)
```

The delimiter `|` inside a string is indistinguishable from the separator.

---

## Complexity

| | |
|--|--|
| **Time** | O(n) — single pass encode and decode |
| **Space** | O(n) — output string / vector |

> ⚠️ Only works if strings are guaranteed to not contain the delimiter. Not safe for general use.
