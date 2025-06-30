# Longest Harmonious Subsequence

**Date:** 2025-06-30 07:24:32 UTC  
**User:** Harikrishnan120A  
**Difficulty:** Easy

## Problem Description

We define a harmonious array as an array where the difference between its maximum value and its minimum value is exactly 1.

Given an integer array `nums`, return the length of its longest harmonious subsequence among all its possible subsequences.

## Examples

### Example 1:
```
Input: nums = [1,3,2,2,5,2,3,7]
Output: 5
Explanation: The longest harmonious subsequence is [3,2,2,2,3].
```

### Example 2:
```
Input: nums = [1,2,3,4]
Output: 2
Explanation: The longest harmonious subsequences are [1,2], [2,3], and [3,4], all of which have a length of 2.
```

### Example 3:
```
Input: nums = [1,1,1,1]
Output: 0
Explanation: No harmonic subsequence exists.
```

## Constraints

- `1 <= nums.length <= 2 * 10^4`
- `-10^9 <= nums[i] <= 10^9`

## Solution

```python
class Solution:
    def findLHS(self, nums):
        """
        Find the length of the longest harmonious subsequence.
        
        A harmonious subsequence has a difference of exactly 1 between
        its maximum and minimum values.
        
        Args:
            nums: List[int] - List of integers
            
        Returns:
            int: Length of longest harmonious subsequence
        """
        # Count frequency of each number
        freq = {}
        for num in nums:
            freq[num] = freq.get(num, 0) + 1
        
        max_length = 0
        
        # For each unique number, check if num+1 exists
        for num in freq:
            if num + 1 in freq:
                # If both num and num+1 exist, their combined count
                # gives us a valid harmonious subsequence
                current_length = freq[num] + freq[num + 1]
                max_length = max(max_length, current_length)
        
        return max_length

# Alternative solution using Counter
from collections import Counter

class SolutionCounter:
    def findLHS(self, nums):
        count = Counter(nums)
        max_length = 0
        
        for num in count:
            if num + 1 in count:
                max_length = max(max_length, count[num] + count[num + 1])
        
        return max_length

# Test driver function
def _driver():
    solution = Solution()
    
    # Test Case 1
    param_1 = [1,3,2,2,5,2,3,7]
    ret = solution.findLHS(param_1)
    print(f"Test 1 - Input: {param_1}")
    print(f"Output: {ret}, Expected: 5")
    print(f"Result: {'✓ PASS' if ret == 5 else '✗ FAIL'}")
    print()
    
    # Test Case 2
    param_2 = [1,2,3,4]
    ret = solution.findLHS(param_2)
    print(f"Test 2 - Input: {param_2}")
    print(f"Output: {ret}, Expected: 2")
    print(f"Result: {'✓ PASS' if ret == 2 else '✗ FAIL'}")
    print()
    
    # Test Case 3
    param_3 = [1,1,1,1]
    ret = solution.findLHS(param_3)
    print(f"Test 3 - Input: {param_3}")
    print(f"Output: {ret}, Expected: 0")
    print(f"Result: {'✓ PASS' if ret == 0 else '✗ FAIL'}")
    print()
    
    # Additional edge case
    param_4 = [1]
    ret = solution.findLHS(param_4)
    print(f"Test 4 - Input: {param_4}")
    print(f"Output: {ret}, Expected: 0")
    print(f"Result: {'✓ PASS' if ret == 0 else '✗ FAIL'}")

if __name__ == "__main__":
    _driver()
```

## Algorithm Explanation

### Approach: Frequency Counting + Adjacent Number Check

1. **Count Frequencies**: 
   - Build a frequency map/dictionary to count occurrences of each number
   - This takes O(n) time and O(k) space where k is the number of unique elements

2. **Check Adjacent Numbers**: 
   - For each unique number `num` in our frequency map
   - Check if `num + 1` also exists in the frequency map
   - We only check `num + 1` (not `num - 1`) to avoid counting the same pair twice

3. **Calculate Maximum Length**: 
   - If both `num` and `num + 1` exist, their combined frequency gives us the length of the longest harmonious subsequence containing only these two values
   - Track the maximum length across all valid pairs

4. **Return Result**: 
   - Return the maximum length found, or 0 if no harmonious subsequence exists

### Why This Works

- A harmonious subsequence can contain **at most 2 distinct values** that differ by exactly 1
- Since we want a subsequence (not subarray), **order doesn't matter**
- By counting frequencies, we can directly calculate the maximum possible length for any valid pair
- We only need to check consecutive integers since the difference must be exactly 1

## Complexity Analysis

### Time Complexity: O(n)
- **O(n)** to build the frequency map by iterating through all elements
- **O(k)** to iterate through unique elements where k ≤ n
- Overall: **O(n)**

### Space Complexity: O(k)
- **O(k)** for the frequency map where k is the number of unique elements
- In worst case where all elements are unique: **O(n)**

## Key Insights

1. **Harmonious Property**: Max - Min = 1 means only 2 distinct values allowed
2. **Subsequence vs Subarray**: Order doesn't matter, so we can count frequencies
3. **Optimization**: Only check `num + 1` to avoid duplicate counting
4. **Edge Cases**: Arrays with all same elements return 0 (no harmonious subsequence possible)

## Common Mistakes to Avoid

1. **Don't confuse subsequence with subarray** - order doesn't need to be preserved
2. **Don't check both `num + 1` and `num - 1`** - this counts the same pair twice
3. **Handle edge case** where no harmonious subsequence exists (return 0)
4. **Remember the difference must be exactly 1**, not "at most 1"
