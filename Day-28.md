# Find Missing and Repeated Values in Grid

**Author**: Harikrishnan120A    
**Date**: 2023-11-15

## Problem Statement
Given a 0-indexed 2D integer matrix `grid` of size `n * n` with values in the range `[1, n²]`, each integer appears exactly once except one which appears twice and another which is missing. The task is to find the repeating and missing numbers.

## Approach
1. **Flatten the Grid**: Convert the 2D grid into a 1D list to simplify processing.
2. **Frequency Tracking**: Use a dictionary to count occurrences of each number in the flattened list.
3. **Identify Repeating and Missing Numbers**:
   - The repeating number will be the one with a frequency of 2.
   - The missing number will be the one in the range `[1, n²]` that does not appear in the grid.
4. **Return Result**: Compile the results into an array where the first element is the repeating number and the second is the missing number.

## Solution Code
```python
class Solution:
    def findMissingAndRepeatedValues(self, grid):
        n = len(grid)
        max_num = n * n
        frequency = {}
        
        # Flatten the grid and count frequencies
        for row in grid:
            for num in row:
                frequency[num] = frequency.get(num, 0) + 1
        
        a = None
        b = None
        
        # Find the repeated number (a)
        for num in frequency:
            if frequency[num] == 2:
                a = num
                break
        
        # Find the missing number (b)
        for num in range(1, max_num + 1):
            if num not in frequency:
                b = num
                break
        
        return [a, b]
```

## Explanation
1. **Class Definition**: The `Solution` class encapsulates the method `findMissingAndRepeatedValues`.
2. **Method Definition**: The method processes the grid to find the repeating and missing numbers.
3. **Frequency Dictionary**: Tracks occurrences of each number in the grid.
4. **Finding Numbers**:
   - The repeating number is identified by checking for a frequency of 2.
   - The missing number is found by checking the absence of a number in the range `[1, n²]`.
5. **Result**: Returns a list with the repeating and missing numbers.

This solution efficiently processes the grid with a time complexity of O(n²), making it optimal for the given constraints.
