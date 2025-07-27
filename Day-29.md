# Count Hills and Valleys in an Array  
**Author**: Harikrishnan120A  
**Date**: 2025-07-27  

## Problem
Given a 0-indexed integer array `nums`, count how many **hills** and **valleys** exist.  
- **Hill**: closest non-equal neighbors on both sides are **smaller** than the current value.  
- **Valley**: closest non-equal neighbors on both sides are **larger** than the current value.  
Adjacent equal values belong to the same hill/valley.

## Constraints
- 3 ≤ nums.length ≤ 100                  
- 1 ≤ nums[i] ≤ 100  

## Solution
```python
class Solution:
    def countHillValley(self, nums):
        # Remove consecutive duplicates
        processed = []
        for num in nums:
            if not processed or num != processed[-1]:
                processed.append(num)

        count = 0
        # Check each middle element
        for i in range(1, len(processed) - 1):
            left, mid, right = processed[i-1], processed[i], processed[i+1]
            if (left < mid and right < mid) or (left > mid and right > mid):
                count += 1
        return count
```
## Complexity

**Time:** O(n)    
**Space:** O(n) for the processed array (can be O(1) with in-place compaction if desired).
