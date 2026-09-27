# Sorting

> **Time:** O(n * k log k) &nbsp;|&nbsp; **Space:** O(n * k)

---

## Intuition

Anagrams always produce the **same string when sorted**. Use the sorted string as a key in a hash map. All strings that share the same sorted key are anagrams — group them together.

---

## Algorithm

1. Create an `unordered_map<string, vector<string>> map`.
2. For each string `s`, sort it to get key.
3. Append `s` to `map[key]`.
4. Return all values from the map.

---

## Code

```cpp
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        unordered_map<string, vector<string>> gana;
        for (string s : strs) {
            string word = s;
            sort(word.begin(), word.end());
            gana[word].push_back(s);
        }
        vector<vector<string>> res;
        for (auto x : gana) {
            res.push_back(x.second);
        }
        return res;
    }
};
```

---

## Dry Run

**Input:** `strs = ["eat","tea","tan","ate","nat","bat"]`

| s | sorted key | map state |
|---|------------|-----------|
| "eat" | "aet" | {"aet": ["eat"]} |
| "tea" | "aet" | {"aet": ["eat","tea"]} |
| "tan" | "ant" | {"aet": ["eat","tea"], "ant": ["tan"]} |
| "ate" | "aet" | {"aet": ["eat","tea","ate"], "ant": ["tan"]} |
| "nat" | "ant" | {"aet": ["eat","tea","ate"], "ant": ["tan","nat"]} |
| "bat" | "abt" | {"aet": [...], "ant": [...], "abt": ["bat"]} |

**Output:** `[["eat","tea","ate"],["tan","nat"],["bat"]]`

---

## Complexity

| | |
|--|--|
| **Time** | O(n * k log k) — sorting each string of length k |
| **Space** | O(n * k) — map stores all strings |
