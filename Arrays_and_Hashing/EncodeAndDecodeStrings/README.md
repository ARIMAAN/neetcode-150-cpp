# Encode and Decode Strings

> **Difficulty:** Medium &nbsp;|&nbsp; **Topic:** Arrays & Hashing &nbsp;|&nbsp; [LeetCode #271](https://leetcode.com/problems/encode-and-decode-strings/)

---

## Problem Statement

Design an algorithm to encode a list of strings to a single string, and decode it back to the original list. The encoded string is transmitted over a network.

**Example 1:**
```
Input : strs = ["Hello","World"]
Output: ["Hello","World"]
```
**Example 2:**
```
Input : strs = [""]
Output: [""]
```

**Constraints:**
- `0 <= strs.length <= 200`
- `0 <= strs[i].length <= 200`
- `strs[i]` contains any possible characters including special characters

---

## Why Not Just Use JSON or CSV?

- **CSV** breaks on strings with commas
- **JSON** adds overhead and escaping complexity
- **Length prefix** is minimal, O(n), and handles every character natively

---

## The Core Challenge

Since strings can contain **any character** (including delimiters like `,` or `|`), a simple separator won't work:

```
["Hello", "Wo,rld"]  →  "Hello,Wo,rld"  →  ["Hello", "Wo", "rld"]  ❌
```

We need an **unambiguous encoding** that handles any character.

---

## Related Problems

| Problem | Connection |
|---------|------------|
| [297. Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/) | Same encode/decode concept on tree nodes |
| [449. Serialize and Deserialize BST](https://leetcode.com/problems/serialize-and-deserialize-bst/) | Length prefix useful for node values |

---

## Key Takeaway

> Whenever you need to serialize variable-length data without a guaranteed safe delimiter, **length-prefix encoding** is the go-to pattern. It's used in real protocols like HTTP chunked transfer encoding and Protocol Buffers.

---

## Approaches

| # | Approach | Time | Space | File |
|---|----------|------|-------|------|
| 1 | Delimiter (Naive) | O(n) | O(n) | [Delimiter.md](./Delimiter.md) |
| 2 | Length Prefix ✅ | O(n) | O(n) | [LengthPrefix.md](./LengthPrefix.md) |
