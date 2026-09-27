# Hash Map (Char Count) ✅ Optimal

> **Time:** O(m * n) &nbsp;|&nbsp; **Space:** O(m * n)

---

## Intuition

Instead of sorting, build a **character frequency array of size 26** for each string. Since there are only lowercase English letters, this takes O(n) per string. Anagrams will always produce the **same frequency array** — use it as the hash map key.

---

## Why ASCII Values?

We use ASCII values to map each character to an index in a 26-length array.

```
'a' = 97,  'b' = 98,  'c' = 99 ... 'z' = 122
```

To get the index, subtract ASCII value of `'a'` (97) from the character:

```
'a' - 'a' = 0   → index 0
'd' - 'a' = 3   → index 3
'z' - 'a' = 25  → index 25
```

---

## Key Idea

**"eat" and "tea" produce the same array:**

```
"eat":
  e = 101 - 97 = 4  → index 4
  a = 97  - 97 = 0  → index 0
  t = 116 - 97 = 19 → index 19

  a b c d e f ... t  ...
 [1,0,0,0,1,0,...,1,...,0]

"tea":
  t = 116 - 97 = 19 → index 19
  e = 101 - 97 = 4  → index 4
  a = 97  - 97 = 0  → index 0

  a b c d e f ... t  ...
 [1,0,0,0,1,0,...,1,...,0]  ← same!
```

Both produce the same array → same key → same group.

---

## Algorithm

1. For each string `s`, build `count[26]` by iterating characters.
2. Convert `count` to a string key: `"1#0#0#...#1#"` (using `#` as separator to avoid collisions).
3. Push `s` into `map[key]`.
4. Return all values.

---

## Code

```cpp
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        unordered_map<string, vector<string>> ans;

        for (string& s : strs) {
            array<int, 26> count = {0};

            for (char c : s) {
                count[c - 'a']++;
            }

            string key;
            for (int num : count) {
                key += to_string(num) + "#";
            }

            ans[key].push_back(s);
        }

        vector<vector<string>> result;
        for (auto& entry : ans) {
            result.push_back(move(entry.second));
        }
        return result;
    }
};
```

---

## Dry Run

**Input:** `strs = ["eat","tea","tan","ate","nat","bat"]`

| s | count array (a-z) | key (simplified) | group |
|---|-------------------|------------------|-------|
| "eat" | a=1,e=1,t=1 | "1#0#0#0#1#...#1#..." | ["eat"] |
| "tea" | a=1,e=1,t=1 | same key | ["eat","tea"] |
| "tan" | a=1,n=1,t=1 | "1#0#...#1#1#...#1#" | ["tan"] |
| "ate" | a=1,e=1,t=1 | same as "eat" | ["eat","tea","ate"] |
| "nat" | a=1,n=1,t=1 | same as "tan" | ["tan","nat"] |
| "bat" | a=1,b=1,t=1 | "1#1#...#1#" | ["bat"] |

**Output:** `[["eat","tea","ate"],["tan","nat"],["bat"]]`

---

## Complexity

| | |
|--|--|
| **Time** | O(m * n) — O(n) per string, no sorting needed |
| **Space** | O(m * n) — map stores all strings |

> Better than sorting when strings are long since O(n) < O(n log n).
