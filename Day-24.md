# Maximum Erasure Value

**Date:** 22nd July 2025  
**Author:** Harikrishnan120A

## Problem Statement
You are given an array of positive integers `nums` and want to erase a subarray containing unique elements. The score you get by erasing the subarray is equal to the sum of its elements. Return the maximum score you can get by erasing exactly one subarray.

An array `b` is called a subarray of `a` if it forms a contiguous subsequence of `a`, that is, if it is equal to `a[l], a[l+1], ..., a[r]` for some `(l, r)`.

### Examples
1. **Input:** `nums = [4,2,4,5,6]`  
   **Output:** `17`  
   **Explanation:** The optimal subarray here is `[2,4,5,6]`.

2. **Input:** `nums = [5,2,1,2,5,2,1,2,5]`  
   **Output:** `8`  
   **Explanation:** The optimal subarray here is `[5,2,1]` or `[1,2,5]`.

## Approach
The solution uses the **Sliding Window Technique** to maintain a window of unique elements. Here's a breakdown of the approach:

1. **Sliding Window:** Expand the window by moving the right pointer forward. If a duplicate element is encountered, shrink the window from the left until all elements are unique again.
2. **Hash Set:** Use a set to track elements currently in the window for O(1) average time complexity checks.
3. **Current Sum:** Maintain the sum of the current window. Adjust it by subtracting elements removed from the left and adding new elements from the right.
4. **Maximum Sum:** Continuously update the maximum sum encountered during the traversal.

## Solution Code
```python
class Solution:
    def maximumUniqueSubarray(self, nums):
        max_sum = 0
        current_sum = 0
        unique_elements = set()
        left = 0
        
        for right in range(len(nums)):
            while nums[right] in unique_elements:
                current_sum -= nums[left]
                unique_elements.remove(nums[left])
                left += 1
            unique_elements.add(nums[right])
            current_sum += nums[right]
            max_sum = max(max_sum, current_sum)
        
        return max_sum
```

## Explanation

1. **Initialization:** max_sum stores the highest sum found, current_sum tracks the sum of the current window, and unique_elements is a set to check for duplicates.

2. **Sliding Window:** The right pointer expands the window. If a duplicate is found, the left pointer moves right, removing elements from the set and subtracting their values from current_sum until the window is valid.

3. **Updating Sums:** Valid elements are added to the set and current_sum. max_sum is updated if current_sum exceeds it.

4. **Result:** After processing all elements, max_sum contains the maximum sum of a contiguous subarray with unique elements.
