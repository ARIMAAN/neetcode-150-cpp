# Brute Force

> **Time:** O(n² * k) &nbsp;|&nbsp; **Space:** O(n * k)

---

## Intuition

For every string, compare it against all other strings to check if they are anagrams (by sorting both and comparing). Group them together if they match. Visited strings are skipped.

---

## Algorithm

1. Maintain a `visited` boolean array to skip already grouped strings.
2. For each unvisited string `strs[i]`, create a new group.
3. For each subsequent string `strs[j]` (j > i), check if `sort(strs[i]) == sort(strs[j])`.
4. If yes, add `strs[j]` to the current group and mark it visited.
5. Add the group to the result.

---

## Code

```cpp
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        int n = strs.size();
        vector<bool> visited(n, false);
        vector<vector<string>> result;

        for (int i = 0; i < n; i++) {
            if (visited[i]) continue;
            vector<string> group;
            group.push_back(strs[i]);
            string sorted_i = strs[i];
            sort(sorted_i.begin(), sorted_i.end());

            for (int j = i + 1; j < n; j++) {
                if (visited[j]) continue;
                string sorted_j = strs[j];
                sort(sorted_j.begin(), sorted_j.end());
                if (sorted_i == sorted_j) {
                    group.push_back(strs[j]);
                    visited[j] = true;
                }
            }
            result.push_back(group);
        }
        return result;
    }
};
```

---

## Dry Run

**Input:** `strs = ["eat","tea","tan","ate","nat","bat"]`

| i | strs[i] | sorted_i | Group formed |
|---|---------|----------|--------------|
| 0 | "eat" | "aet" | "tea"(1)✅, "ate"(3)✅ → ["eat","tea","ate"] |
| 2 | "tan" | "ant" | "nat"(4)✅ → ["tan","nat"] |
| 5 | "bat" | "abt" | no match → ["bat"] |

**Output:** `[["eat","tea","ate"],["tan","nat"],["bat"]]`

---

## Complexity

| | |
|--|--|
| **Time** | O(n² * k) — n² pairs, each sort costs O(k log k) |
| **Space** | O(n * k) — storing all strings in result |

> ⚠️ Slow for large inputs due to O(n²) comparisons.
