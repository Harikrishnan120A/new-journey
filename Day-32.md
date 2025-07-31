# Bitwise ORs of Subarrays

**Problem Title**: Bitwise ORs of Subarrays  
**Difficulty**: Medium  
**Date**: 2025-07-31  
**Author**: Harikrishnan120A  

---

## 🧾 Problem Description

Given an integer array `arr`, return the number of **distinct bitwise ORs** of all the **non-empty subarrays** of `arr`.

- A subarray is a contiguous non-empty sequence of elements within an array.
- The bitwise OR of a subarray is the bitwise OR of each integer in the subarray.

---

## 🧠 Examples

### Example 1:
Input: arr = [0]
Output: 1
Explanation: Only one subarray → [0], and its OR is 0.

### Example 2:
Input: arr = [1,1,2]
Output: 3
Subarrays OR results: 1, 1, 2, 1, 3, 3 → Unique values = {1, 2, 3}

### Example 3:
Input: arr = [1,2,4]
Output: 6
OR values from subarrays: {1, 2, 3, 4, 6, 7}

---

## ✅ Constraints

- 1 ≤ arr.length ≤ 50,000  
- 0 ≤ arr[i] ≤ 1,000,000,000

---

## 🧩 Approach

We use a **set-based sliding window** approach:

- Let `cur` hold all OR results ending at the current index.
- For each number `num`, we generate a new set `cur` as:
  ```python
  cur = {num | x for x in prev} ∪ {num}
Accumulate all results in a global res set to count unique values.

## ⏱ Time Complexity
O(N × log M)
Where N is the array length and M is the maximum number of bits (up to 30 for 10^9).

🧑‍💻 Python Code
✅ Version without type hints for maximum compatibility

```python

class Solution:
    def subarrayBitwiseORs(self, arr):
        res = set()
        prev = set()

        for num in arr:
            cur = {num}
            for p in prev:
                cur.add(p | num)
            prev = cur
            res.update(cur)

        return len(res)
```

## Sample test
sol = Solution()                     
print(sol.subarrayBitwiseORs([0]))        # Output: 1            
print(sol.subarrayBitwiseORs([1, 1, 2]))  # Output: 3              
print(sol.subarrayBitwiseORs([1, 2, 4]))  # Output: 6                 

## 🏁 Output

1           
3           
6
