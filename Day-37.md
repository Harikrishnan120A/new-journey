# 🧮 Maximum Count of Positive and Negative Integers

**Author**: Harikrishnan120A  
**Date**: 2025-08-07  
**Difficulty**: Easy  
**Topic**: Arrays, Binary Search  

---

## 📝 Problem

Given an array `nums` **sorted in non-decreasing order**, return the maximum between:

- The number of **positive integers**
- The number of **negative integers**

> Note: `0` is **neither** positive nor negative.

---

## ✅ Examples

### Example 1
**Input:**  
`nums = [-2, -1, -1, 1, 2, 3]`  
**Output:**  
`3`  
**Explanation:** 3 positives and 3 negatives → max = 3

---

### Example 2
**Input:**  
`nums = [-3, -2, -1, 0, 0, 1, 2]`  
**Output:**  
`3`  
**Explanation:** 3 negatives, 2 positives → max = 3

---

### Example 3
**Input:**  
`nums = [5, 20, 66, 1314]`  
**Output:**  
`4`  
**Explanation:** 4 positives, 0 negatives → max = 4

---

## 🚀 Solution (Python)

```python
from bisect import bisect_left, bisect_right

class Solution:
    def maximumCount(self, nums):
        # Count of negative numbers (before first 0)
        neg = bisect_left(nums, 0)
        
        # Count of positive numbers (after last 0)
        pos = len(nums) - bisect_right(nums, 0)
        
        # Return the maximum of the two
        return max(neg, pos)
```


## ⏱️ Time Complexity

**Time:** O(log n)     
**Space:** O(1)     

Efficient because we use binary search via bisect.
