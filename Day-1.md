# Two Sum Solution

**Last Updated:** June 25, 2023  
**Difficulty:** Easy  
**Category:** Array/Hash Table  

## Problem Description
Given an array of integers `nums` and an integer `target`, return the indices of the two numbers that add up to the target.

### Key Points:
- Each input has exactly one solution
- You cannot use the same element twice
- Return the answer in any order

## Example
```python
Input: nums = [2, 7, 11, 15], target = 9
Output: [0, 1]
Explanation: nums[0] + nums[1] = 2 + 7 = 9

```
## Optimal Solution Approach


Hash Map (Dictionary) Method


Initialize an empty dictionary to store numbers and their indices

Iterate through the array with index and value

Calculate complement (target - current number)

Check if complement exists in dictionary:

If found: Return indices

If not: Store current number and index

Complexity Analysis
Metric	Value	Explanation
Time	O(n)	Single pass through the array
Space	O(n)	Stores up to n elements in dictionary

``` python
def two_sum(nums, target):
    """
    Finds indices of two numbers that add up to target.
    
    Args:
        nums: List of integers
        target: Target sum
        
    Returns:
        List of two indices
    """
    num_map = {}
    for index, num in enumerate(nums):
        complement = target - num
        if complement in num_map:
            return [num_map[complement], index]
        num_map[num] = index
    return []  # As per problem statement, this line is unreachable

# Example Usage
if __name__ == "__main__":
    nums = [2, 7, 11, 15]
    target = 9
    print(two_sum(nums, target))  # Output: [0, 1]
