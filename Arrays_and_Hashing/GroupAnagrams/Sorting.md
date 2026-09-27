# Sorting

> **Time:** O(m * n log n) &nbsp;|&nbsp; **Space:** O(m * n)

---

## Intuition

If we sort each character of each string, anagrams will produce the **same sorted string**. Use that sorted string as a key to group them in a hash map.

---

## Algorithm

1. For each string `s`, sort its characters to create a `key`.
2. Push `s` into `map[key]`.
3. Return all values from the map.

---

## Key Idea

```
"eat"  →  "aet"
"tea"  →  "aet"
"tan"  →  "ant"
"ate"  →  "aet"
"nat"  →  "ant"
"bat"  →  "abt"

"aet": ["eat", "tea", "ate"]
"ant": ["tan", "nat"]
"abt": ["bat"]
```

---

## Code

```cpp
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        unordered_map<string, vector<string>> ans;

        for (string& s : strs) {
            string key = s;
            sort(key.begin(), key.end());
            ans[key].push_back(s);
        }

        vector<vector<string>> result;
        for (auto& entry : ans) {
            result.push_back(entry.second);
        }
        return result;
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
| **Time** | O(m * n log n) — sorting each string of length n, for m strings |
| **Space** | O(m * n) — map stores all strings |
