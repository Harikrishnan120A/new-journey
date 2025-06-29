# Number of Subsequences That Satisfy the Given Sum Condition

**Difficulty:** Medium  
**Topics:** Array, Two Pointers, Sorting, Binary Search

## Problem Description

You are given an array of integers `nums` and an integer `target`.

Return the number of non-empty subsequences of `nums` such that the sum of the minimum and maximum element on it is less or equal to `target`. Since the answer may be too large, return it modulo 10^9 + 7.

### Examples

**Example 1:**
```
Input: nums = [3,5,6,7], target = 9
Output: 4
Explanation: There are 4 subsequences that satisfy the condition.
[3] -> Min value + max value <= target (3 + 3 <= 9)
[3,5] -> (3 + 5 <= 9)
[3,5,6] -> (3 + 6 <= 9)
[3,6] -> (3 + 6 <= 9)
```

**Example 2:**
```
Input: nums = [3,3,6,8], target = 10
Output: 6
Explanation: There are 6 subsequences that satisfy the condition. (nums can have repeated numbers).
[3] , [3] , [3,3], [3,6] , [3,6] , [3,3,6]
```

**Example 3:**
```
Input: nums = [2,3,3,4,6,7], target = 12
Output: 61
Explanation: There are 63 non-empty subsequences, two of them do not satisfy the condition ([6,7], [7]).
Number of valid subsequences (63 - 2 = 61).
```

### Constraints

- `1 <= nums.length <= 10^5`
- `1 <= nums[i] <= 10^6`
- `1 <= target <= 10^6`

## Solution

### Approach

The key insight is that after sorting the array, for any subsequence, the minimum element will be the leftmost element and the maximum element will be the rightmost element.

**Algorithm:**
1. Sort the array
2. Use two pointers (left and right)
3. If `nums[left] + nums[right] <= target`, all subsequences starting with `nums[left]` and ending at or before `nums[right]` are valid
4. The count of such subsequences is `2^(right - left)`
5. Use modulo arithmetic to handle large numbers

### Code

```python
class Solution:
    def numSubseq(self, nums, target):
        MOD = 10**9 + 7
        nums.sort()
        left, right = 0, len(nums) - 1
        result = 0
        
        # Precompute powers of 2 to avoid repeated calculation
        powers = [1] * len(nums)
        for i in range(1, len(nums)):
            powers[i] = (powers[i-1] * 2) % MOD
        
        while left <= right:
            if nums[left] + nums[right] <= target:
                # All subsequences starting with nums[left] and ending 
                # at or before nums[right] are valid
                result = (result + powers[right - left]) % MOD
                left += 1
            else:
                # Sum too large, reduce the maximum
                right -= 1
        
        return result
```

### Complexity Analysis

- **Time Complexity:** O(n log n) where n is the length of nums
  - O(n log n) for sorting
  - O(n) for the two-pointer traversal
- **Space Complexity:** O(n) for the powers array

### Example Walkthrough

For `nums = [3,5,6,7], target = 9`:

1. After sorting: `[3,5,6,7]`
2. left=0, right=3: `3+7=10 > 9`, move right to 2
3. left=0, right=2: `3+6=9 ≤ 9`, add `2^(2-0)=4`, move left to 1
4. left=1, right=2: `5+6=11 > 9`, move right to 1
5. left=1, right=1: `5+5=10 > 9`, move right to 0
6. left > right, stop
7. Result: 4 ✓

## Author

**Harikrishnan120A**  
*Date: 2025-06-29*

---

### Tags
`#leetcode` `#medium` `#array` `#two-pointers` `#sorting` `#subsequence` `#modular-arithmetic`
