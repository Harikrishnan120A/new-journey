# Smallest Subarrays With Maximum Bitwise OR

**Author:** Harikrishnan120A                                             
**Date:** 2025-07-29  
**Difficulty:** Medium  
**Topics:** Bit Manipulation, Sliding Window, Hash Map

---

## 🧩 Problem Statement

You are given a 0-indexed array `nums` of length `n`, consisting of non-negative integers.  
For each index `i` from `0` to `n - 1`, you must determine the **length of the smallest subarray** starting at `i` (inclusive) that has the **maximum possible bitwise OR**.

### 🔍 Definition:
- Let `Bij` be the bitwise OR of the subarray `nums[i...j]`.
- You need to find the **smallest subarray starting at `i`** such that its OR is equal to the maximum of all `Bik` for `i <= k <= n - 1`.

---

### ✨ Example 1:

**Input:**  
`nums = [1, 0, 2, 1, 3]`  
**Output:**  
`[3, 3, 2, 2, 1]`

**Explanation:**
- The maximum bitwise OR from any index is `3`.
- From index 0 → `[1, 0, 2]` gives OR = 3 → length = 3
- From index 1 → `[0, 2, 1]` → OR = 3 → length = 3
- From index 2 → `[2, 1]` → OR = 3 → length = 2
- From index 3 → `[1, 3]` → OR = 3 → length = 2
- From index 4 → `[3]` → OR = 3 → length = 1

---

### ✨ Example 2:

**Input:**  
`nums = [1, 2]`  
**Output:**  
`[2, 1]`

---

## 🧠 Approach

- We process the array **right to left**, maintaining a map of all OR values that can be achieved starting from the current index.
- For each index, we compute all new OR values by combining the current number with previously stored OR values.
- We store the **minimum length** needed to achieve each OR value.
- Finally, for the **maximum OR value**, we store its corresponding length as the result.

---

## ✅ Python Solution (Compatible with Python 2 & 3)

```python
class Solution:
    def smallestSubarrays(self, nums):
        n = len(nums)
        answer = [0] * n
        prev = dict()

        for i in range(n - 1, -1, -1):
            cur = {}
            cur[nums[i]] = 1

            for or_val in prev:
                new_or = or_val | nums[i]
                cur[new_or] = min(cur.get(new_or, float('inf')), prev[or_val] + 1)

            max_or = max(cur.keys())
            answer[i] = cur[max_or]
            prev = cur

        return answer
```

# Example usage:
sol = Solution()           
print(sol.smallestSubarrays([1, 0, 2, 1, 3]))  # Output: [3, 3, 2, 2, 1]            
print(sol.smallestSubarrays([1, 2]))          # Output: [2, 1]


## ⏱️ Time & Space Complexity

**Time Complexity:** O(n * 30) — at most 30 unique OR values (since numbers are ≤ 10^9)

**Space Complexity:** O(30) per step for storing intermediate OR values

## 🔚 Conclusion
This approach efficiently calculates the minimum subarray lengths that achieve the maximum OR starting from each index, using a bit manipulation trick and dictionary tracking.
