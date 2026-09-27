# Hash Map (Char Count) ✅ Optimal

> **Time:** O(n * k) &nbsp;|&nbsp; **Space:** O(n * k)

---

## Intuition

Instead of sorting (O(k log k)), build a **character frequency array of size 26** for each string. This takes O(k) and uniquely identifies any anagram group. Use this array (converted to a string key) as the hash map key.

---

## Algorithm

1. For each string `s`, build a `count[26]` array of character frequencies.
2. Convert `count` to a string key like `"1#0#0#...#1#"`.
3. Use this key in `unordered_map<string, vector<string>>`.
4. Append `s` to `map[key]`.
5. Return all values.

---

## Code

```cpp
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        unordered_map<string, vector<string>> map;
        for (auto& s : strs) {
            vector<int> count(26, 0);
            for (char c : s) count[c - 'a']++;
            string key = "";
            for (int i = 0; i < 26; i++) {
                key += to_string(count[i]) + "#";
            }
            map[key].push_back(s);
        }
        vector<vector<string>> result;
        for (auto& pair : map) {
            result.push_back(pair.second);
        }
        return result;
    }
};
```

---

## Dry Run

**Input:** `strs = ["eat","tea","tan","ate","nat","bat"]`

| s | count (a-z relevant) | key (simplified) | group |
|---|----------------------|------------------|-------|
| "eat" | a=1,e=1,t=1 | "1#0#...#1#...#1#" | ["eat"] |
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
| **Time** | O(n * k) — O(k) per string, no sorting |
| **Space** | O(n * k) — map stores all strings |

> Better than sorting when `k` is large since O(k) < O(k log k).
