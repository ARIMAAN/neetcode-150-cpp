# Car Fleet

**LeetCode #853** | **Difficulty**: Medium | **Topic**: Stack

---

## Problem Statement

`n` cars are driving toward a target. Given arrays `position` and `speed`, a car fleet is a group of cars that arrive at the target at the same time. Return the number of car fleets.

A faster car that catches up to a slower car becomes part of that fleet (it can't pass).

**Examples**:

| position | speed | target | Output |
|----------|-------|--------|--------|
| [10,8,0,5,3] | [2,4,1,1,3] | 12 | 3 |
| [3] | [3] | 10 | 1 |
| [0,4,2] | [2,1,3] | 10 | 1 |

---

## Approach

| Approach | Time | Space |
|----------|------|-------|
| Sort + Stack | O(n log n) | O(n) |

## Key Insight

Sort cars by position (descending — closest to target first).
Compute time to reach target for each: `time = (target - pos) / speed`.
Use a stack: if the current car's time > stack top's time, it forms a new fleet.
Otherwise it catches up and joins the fleet ahead.

## Solution

```cpp
int carFleet(int target, vector<int>& position, vector<int>& speed) {
    int n = position.size();
    vector<pair<int,double>> cars(n);
    for (int i = 0; i < n; i++)
        cars[i] = {position[i], (double)(target - position[i]) / speed[i]};
    sort(cars.begin(), cars.end(), greater<>());
    stack<double> st;
    for (auto& [pos, time] : cars) {
        if (st.empty() || time > st.top()) st.push(time);
    }
    return st.size();
}
```

## Dry Run — position=[10,8,0,5,3], speed=[2,4,1,1,3], target=12

Sorted by position desc: [(10,1.0),(8,1.0),(5,7.0),(3,3.0),(0,12.0)]

| car (pos,time) | stack | action |
|----------------|-------|--------|
| (10, 1.0) | [1.0] | push |
| (8, 1.0) | [1.0] | 1.0 == top → same fleet, skip |
| (5, 7.0) | [1.0, 7.0] | 7.0 > top → new fleet |
| (3, 3.0) | [1.0, 7.0] | 3.0 < top → joins fleet ahead |
| (0, 12.0) | [1.0, 7.0, 12.0] | 12.0 > top → new fleet |

Return `3` ✅

## Why Sort Descending?

We process cars from closest to target to farthest.
A car can only be blocked by a car ahead of it (closer to target).
Processing in this order lets us check if each car catches up to the fleet ahead.
