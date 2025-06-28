# Find Subsequence of Length K With the Largest Sum

**Difficulty:** Easy  
**Topics:** Array, Sorting, Heap (Priority Queue)  
**Companies:** Amazon, Google, Microsoft

## Problem Statement

You are given an integer array `nums` and an integer `k`. You want to find a subsequence of `nums` of length `k` that has the largest sum.

Return any such subsequence as an integer array of length `k`.

A subsequence is an array that can be derived from another array by deleting some or no elements without changing the order of the remaining elements.

### Examples

**Example 1:**
```
Input: nums = [2,1,3,3], k = 2
Output: [3,3]
Explanation: The subsequence has the largest sum of 3 + 3 = 6.
```

**Example 2:**
```
Input: nums = [-1,-2,3,4], k = 3
Output: [-1,3,4]
Explanation: The subsequence has the largest sum of -1 + 3 + 4 = 6.
```

**Example 3:**
```
Input: nums = [3,4,3,3], k = 2
Output: [3,4]
Explanation: The subsequence has the largest sum of 3 + 4 = 7. 
Another possible subsequence is [4, 3].
```

### Constraints

- `1 <= nums.length <= 1000`
- `-10^5 <= nums[i] <= 10^5`
- `1 <= k <= nums.length`

## Solution

### Approach

The key insight is that we need to:
1. Select the k largest elements from the array
2. Maintain their original relative order from the input array

### Algorithm

1. **Create indexed pairs**: Pair each number with its original index
2. **Sort strategically**: Sort by value (descending) to get largest elements first
3. **Select k elements**: Take the first k elements after sorting
4. **Restore order**: Sort the selected elements by their original indices
5. **Extract values**: Return just the values in their original relative order

### Implementation

```python
class Solution:
    def maxSubsequence(self, nums, k):
        """
        Find a subsequence of length k with the largest sum.
        
        Args:
            nums: List of integers
            k: Length of desired subsequence
        
        Returns:
            List of integers representing the subsequence
        """
        n = len(nums)
        
        # Create list of (value, index) pairs
        indexed_nums = [(nums[i], i) for i in range(n)]
        
        # Sort by value in descending order, then by index in ascending order
        # This ensures we pick the largest values, and if there are ties,
        # we prefer the ones that appear earlier
        indexed_nums.sort(key=lambda x: (-x[0], x[1]))
        
        # Take the k largest elements
        selected = indexed_nums[:k]
        
        # Sort by original index to maintain order
        selected.sort(key=lambda x: x[1])
        
        # Extract just the values
        result = [value for value, index in selected]
        
        return result
```

### Alternative Implementation (More Concise)

```python
class Solution:
    def maxSubsequence(self, nums, k):
        # Get indices of k largest elements
        indices = sorted(range(len(nums)), key=lambda i: nums[i], reverse=True)[:k]
        
        # Sort indices to maintain original order
        indices.sort()
        
        # Return elements in original order
        return [nums[i] for i in indices]
```

## Complexity Analysis

- **Time Complexity:** O(n log n) where n is the length of the input array
  - Sorting the indexed pairs takes O(n log n)
  - All other operations are O(n) or O(k)

- **Space Complexity:** O(n) 
  - For storing the indexed pairs and selected elements

## Test Cases

```python
def test_solution():
    solution = Solution()
    
    # Test Example 1
    assert solution.maxSubsequence([2,1,3,3], 2) == [3,3]
    
    # Test Example 2
    assert solution.maxSubsequence([-1,-2,3,4], 3) == [-1,3,4]
    
    # Test Example 3
    result = solution.maxSubsequence([3,4,3,3], 2)
    assert result in [[3,4], [4,3]]  # Both are valid answers
    
    # Edge case: k = 1
    assert solution.maxSubsequence([1,2,3], 1) == [3]
    
    # Edge case: all negative numbers
    assert solution.maxSubsequence([-5,-3,-1,-2], 2) == [-3,-1]
    
    print("All test cases passed!")

if __name__ == "__main__":
    test_solution()
```

## Key Points

- The solution maintains the relative order of elements as they appeared in the original array
- When there are duplicate values, the algorithm will prefer elements that appear earlier in the array
- The subsequence property is preserved (no reordering of the selected elements)
- Works correctly with negative numbers and handles all edge cases

## LeetCode Link

[Find Subsequence of Length K With the Largest Sum - LeetCode](https://leetcode.com/problems/find-subsequence-of-length-k-with-the-largest-sum/)

---

**Author:** [Harikrishnan120A](https://github.com/Harikrishnan120A)  
**Date:** June 28, 2025
