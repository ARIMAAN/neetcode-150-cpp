# Min-Heap

> **Time:** O(n log k) &nbsp;|&nbsp; **Space:** O(n)

---

## Intuition

Use a **min-heap of size k** to maintain the top k frequent elements. For each unique element, push it into the heap. If the heap exceeds size `k`, pop the minimum (least frequent). At the end, the heap contains exactly the k most frequent elements.

---

## Why Min-Heap?

A max-heap would require sorting all elements. A min-heap of size `k` lets us evict the least frequent element whenever we exceed `k`, keeping only the top k at all times.

```
Heap stores: (frequency, num)
Min-heap → smallest frequency is at top → easy to evict
```

---

## Algorithm

1. Build `count` map: `num → frequency`.
2. Use `priority_queue` (min-heap) storing `{freq, num}`.
3. For each entry in `count`:
   - Push `{freq, num}`.
   - If heap size > k, pop (removes least frequent).
4. Extract all elements from heap into result.

---

## Code

```cpp
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int, int> count;
        for (int n : nums) count[n]++;

        // min-heap: {frequency, num}
        priority_queue<pair<int,int>, vector<pair<int,int>>, greater<>> minHeap;

        for (auto& [num, freq] : count) {
            minHeap.push({freq, num});
            if (minHeap.size() > k) minHeap.pop();
        }

        vector<int> res;
        while (!minHeap.empty()) {
            res.push_back(minHeap.top().second);
            minHeap.pop();
        }
        return res;
    }
};
```

---

## Dry Run

**Input:** `nums = [1,2,2,3,3,3]`, `k = 2`

Count map: `{1:1, 2:2, 3:3}`

| Step | Push | Heap (freq,num) | Size > k? | Action |
|------|------|-----------------|-----------|--------|
| 1 | (1,1) | [(1,1)] | No | — |
| 2 | (2,2) | [(1,1),(2,2)] | No | — |
| 3 | (3,3) | [(1,1),(2,2),(3,3)] | Yes (3>2) | pop min → remove (1,1) |

Heap: `[(2,2),(3,3)]` → result: `[2,3]` ✅

---

## Complexity

| | |
|--|--|
| **Time** | O(n log k) — each push/pop on heap of size k costs O(log k) |
| **Space** | O(n) — count map; heap is O(k) |

> ✅ Better than brute force when k << n. Still not O(n) though.
