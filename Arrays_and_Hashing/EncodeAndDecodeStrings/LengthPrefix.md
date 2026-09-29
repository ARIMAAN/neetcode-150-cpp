# Length Prefix ✅ Optimal

> **Time:** O(n) &nbsp;|&nbsp; **Space:** O(n)

---

## Why `#` as Separator Between Length and String?

The length is a variable-width number (could be `1`, `10`, `200`). We need to know where the number ends and the string begins. `#` acts as a terminator for the length field.

```
"10#HelloWorld"  →  length=10, string="HelloWorld"
"1#a"            →  length=1,  string="a"
```

> Any character that is NOT a digit works as the separator. `#` is conventional.

---

## Intuition

Prefix each string with its **length followed by `#`**. On decode, read the length, skip past `#`, then extract exactly that many characters. Since we use the length to jump — not a delimiter to split — any character inside the string is safe.

---

## Encoding Format

```
["Hello", "World"]  →  "5#Hello5#World"
["Hi", ""]          →  "2#Hi0#"
["a#b", "c"]        →  "3#a#b1#c"   ← # inside string is safe!
```

Pattern per string: `<length>#<string>`

---

## Decode — Two Pointer Walkthrough

```
s = "5#Hello5#World"
     ^
     i=0, scan j until s[j]=='#'
          j=1 → s[1]='#'
          length = stoi("5") = 5
          i = j+1 = 2
          extract s[2..6] = "Hello"
          i = 7

     i=7, scan j until s[j]=='#'
          j=8 → s[8]='#'
          length = stoi("5") = 5
          i = j+1 = 9
          extract s[9..13] = "World"
          i = 14  → loop ends
```

---

## Algorithm

**Encode:**
1. For each string `s`, append `len(s) + "#" + s` to result.

**Decode:**
1. `i = 0`, scan forward with `j` until `s[j] == '#'`.
2. Parse `length = s[i..j]`.
3. Move `i = j + 1`, extract `s[i..i+length]`.
4. Advance `i += length`, repeat.

---

## Code

```cpp
class Solution {
public:
    // Encode: prefix each string with "<len>#"
    string encode(vector<string>& strs) {
        string res;
        for (string s : strs) {
            res.append(to_string(s.size())); // write length
            res.push_back('#');              // write separator
            res.append(s);                   // write actual string
        }
        return res;
    }

    // Decode: read length, skip '#', extract exactly 'length' chars
    vector<string> decode(string s) {
        vector<string> res;
        int i = 0;
        while (i < s.size()) {
            int j = i;
            while (s[j] != '#') j++;          // find the '#'
            int length = stoi(s.substr(i, j - i)); // parse length
            i = j + 1;                         // move past '#'
            res.push_back(s.substr(i, length)); // extract string
            i += length;                        // advance to next entry
        }
        return res;
    }
};
```

---

## Dry Run

**Input:** `strs = ["Hello", "World"]`

**Encode:**

| s | appended | res so far |
|---|----------|------------|
| "Hello" | `5#Hello` | `"5#Hello"` |
| "World" | `5#World` | `"5#Hello5#World"` |

**Decode:** `s = "5#Hello5#World"`

| i | j (at '#') | length | extracted | i after |
|---|------------|--------|-----------|---------|
| 0 | 1 | 5 | "Hello" | 7 |
| 7 | 8 | 5 | "World" | 14 |

**Output:** `["Hello", "World"]` ✅

---

**Input:** `strs = ["a#b", "c"]`

**Encode:** `"3#a#b1#c"`

**Decode:**

| i | j | length | extracted | i after |
|---|---|--------|-----------|---------|
| 0 | 1 | 3 | "a#b" | 5 |
| 5 | 6 | 1 | "c" | 8 |

**Output:** `["a#b", "c"]` ✅ — `#` inside string handled correctly

---

**Input:** `strs = [""]`

**Encode:** `"0#"`

**Decode:** length=0 → extract `""` → `[""]` ✅

---

## Edge Cases

| Case | Input | Encoded | Decoded |
|------|-------|---------|---------|
| Empty string | `[""]` | `"0#"` | `[""]` |
| String with `#` | `["a#b"]` | `"3#a#b"` | `["a#b"]` |
| Empty list | `[]` | `""` | `[]` |
| Multiple empty | `["",""]` | `"0#0#"` | `["",""]` |

---

## Interview Tips

- Interviewer will likely ask: *"What if the string contains `#`?"* — answer: the length tells us exactly how many chars to read, so `#` inside the string is never mistaken for a separator
- Follow-up: *"What if length itself is very large?"* — `int` handles up to ~2 billion, well beyond the constraint of 200
- Always walk through the empty string `[""]` edge case — encoded as `"0#"`, decoded back to `[""]`

---

## Complexity

| | |
|--|--|
| **Time** | O(n) — encode: one pass; decode: one pass total across all characters |
| **Space** | O(n) — encoded string + result vector |

> `substr` calls are O(length) each, but total characters across all substrings = n, so overall decode is still O(n).

---

## Comparison

| Approach | Handles Special Chars? | Time | Notes |
|----------|----------------------|------|-------|
| Delimiter | ❌ No | O(n) | Breaks if delimiter appears in string |
| Length Prefix ✅ | ✅ Yes | O(n) | Always safe — length tells us exactly where to stop |
