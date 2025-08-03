# Minimum Recolors to Get K Consecutive Black Blocks

**Problem Level:** Easy  
**Author:** Harikrishnan120A  
**Date:** 2025-08-03  
**Language:** Python (compatible with all versions)

---

## 📄 Problem Description

You are given a **0-indexed string** `blocks` of length `n`, where `blocks[i]` is either:

- `'B'` for **black**, or  
- `'W'` for **white**.

You are also given an integer `k`.

Each **recolor operation** allows you to **turn a white block `'W'` into a black block `'B'`**.

---

### 🎯 Objective:
Return the **minimum number of operations** needed to obtain **at least one substring of `k` consecutive black (`'B'`) blocks**.

---

## 📥 Input

- A string `blocks` of characters `'B'` and `'W'`.
- An integer `k` (1 ≤ k ≤ n).

### ✅ Constraints:

- `1 <= len(blocks) <= 100`
- `blocks[i]` is either `'B'` or `'W'`
- `1 <= k <= len(blocks)`

---

## 🧠 Approach

- We use a **sliding window** of size `k` to check every possible substring of length `k` in the `blocks` string.
- For each window, count the number of `'W'` characters (white blocks).
- Track the **minimum** number of `'W'`s found — this gives the **minimum operations** needed to recolor that window into `k` consecutive black blocks.

---

## 🧾 Python Code 

```python
class Solution:
    def minimumRecolors(self, blocks, k):
        min_ops = float('inf')  # Start with an infinitely large number
        for i in range(len(blocks) - k + 1):
            window = blocks[i:i+k]            # Slice a window of size k
            white_count = window.count('W')   # Count white blocks in this window
            min_ops = min(min_ops, white_count)  # Track the minimum operations
        return min_ops
```

## 🧪 Example Test Cases

sol = Solution()

### Test Case 1
print(sol.minimumRecolors("WBBWWBBWBW", 7))     # Output: 3

### Test Case 2
print(sol.minimumRecolors("WBWBBBW", 2))         # Output: 0
