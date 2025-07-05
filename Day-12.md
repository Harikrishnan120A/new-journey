# Find Lucky Integer in an Array

## Problem Description
**Difficulty:** Easy  
**Topics:** Array, Hash Table, Counting

Given an array of integers `arr`, a lucky integer is an integer that has a frequency in the array equal to its value.

Return the largest lucky integer in the array. If there is no lucky integer return -1.

## Examples

### Example 1:
```
Input: arr = [2,2,3,4]
Output: 2
Explanation: The only lucky number in the array is 2 because frequency[2] == 2.
```

### Example 2:
```
Input: arr = [1,2,2,3,3,3]
Output: 3
Explanation: 1, 2 and 3 are all lucky numbers, return the largest of them.
```

### Example 3:
```
Input: arr = [2,2,2,3,3]
Output: -1
Explanation: There are no lucky numbers in the array.
```

## Constraints
- `1 <= arr.length <= 500`
- `1 <= arr[i] <= 500`

## Solution Approach

1. **Count Frequencies:** Create a frequency map of all numbers in the array
2. **Find Lucky Numbers:** Check which numbers have frequency equal to their value
3. **Return Maximum:** Return the largest lucky number, or -1 if none exists

### Algorithm Steps
1. Initialize a dictionary to count frequencies
2. Iterate through the array and count each number's frequency
3. Iterate through the frequency map to find lucky numbers
4. Track the maximum lucky number found
5. Return the result

## Code Implementation

### Python

```python
class Solution(object):
    def findLucky(self, arr):
        """
        Find the largest lucky integer in an array.
        A lucky integer is an integer that has a frequency equal to its value.
        
        Args:
            arr: List of integers
        
        Returns:
            int: The largest lucky integer, or -1 if no lucky integer exists
        """
        # Step 1: Count frequency of each number
        frequency = {}
        for num in arr:
            if num in frequency:
                frequency[num] += 1
            else:
                frequency[num] = 1
        
        # Step 2: Find the largest lucky integer
        max_lucky = -1
        for num in frequency:
            if num == frequency[num]:  # Lucky integer condition
                if num > max_lucky:
                    max_lucky = num
        
        return max_lucky
```

## Example Walkthrough

### Input: [2, 2, 3, 4]

**Frequency Count:**
```
{2: 2, 3: 1, 4: 1}
```

**Lucky Check:**
- 2 == 2 ✅ (lucky)
- 3 != 1 ❌ (not lucky)
- 4 != 1 ❌ (not lucky)

**Result:** 2

### Input: [1, 2, 2, 3, 3, 3]

**Frequency Count:**
```
{1: 1, 2: 2, 3: 3}
```

**Lucky Check:**
- 1 == 1 ✅ (lucky)
- 2 == 2 ✅ (lucky)
- 3 == 3 ✅ (lucky)

**Lucky Numbers:** [1, 2, 3]  
**Result:** max([1, 2, 3]) = 3

## Complexity Analysis

**Time Complexity:** O(n) where n is the length of the array
- One pass to count frequencies: O(n)
- One pass through frequency map: O(k) where k ≤ n
- Overall: O(n)

**Space Complexity:** O(k) where k is the number of unique elements
- Space for frequency dictionary: O(k)
- In worst case k = n, so O(n)

## Test Cases

```python
def test_solution():
    solution = Solution()
    
    # Test Case 1
    assert solution.findLucky([2, 2, 3, 4]) == 2
    
    # Test Case 2
    assert solution.findLucky([1, 2, 2, 3, 3, 3]) == 3
    
    # Test Case 3
    assert solution.findLucky([2, 2, 2, 3, 3]) == -1
    
    # Edge Cases
    assert solution.findLucky([1]) == 1
    assert solution.findLucky([5, 5, 5, 5, 5]) == 5
    assert solution.findLucky([4, 4, 4, 4]) == -1
    
    print("All test cases passed!")
```

## Alternative Solutions

### Using Collections.Counter

```python
from collections import Counter

class Solution(object):
    def findLucky(self, arr):
        freq = Counter(arr)
        lucky_numbers = [num for num, count in freq.items() if num == count]
        return max(lucky_numbers) if lucky_numbers else -1
```

### One-Pass Optimized

```python
class Solution(object):
    def findLucky(self, arr):
        frequency = {}
        
        # Count frequencies
        for num in arr:
            frequency[num] = frequency.get(num, 0) + 1
        
        # Find maximum lucky number
        max_lucky = -1
        for num in frequency:
            if num == frequency[num] and num > max_lucky:
                max_lucky = num
        
        return max_lucky
```

## Related Problems
- Find All Lucky Numbers in a Matrix
- Majority Element
- Find the Duplicate Number

---

**Author:** Harikrishnan120A  
**Date:** 2025-07-05  
**Language:** Python  
**Difficulty:** Easy
