# Apply Operations to an Array

## Problem Description

You are given a 0-indexed array `nums` of size `n` consisting of non-negative integers.

You need to apply `n - 1` operations to this array where, in the `i`th operation (0-indexed), you will apply the following on the `i`th element of nums:

- If `nums[i] == nums[i + 1]`, then multiply `nums[i]` by 2 and set `nums[i + 1]` to 0
- Otherwise, you skip this operation

After performing all the operations, shift all the 0's to the end of the array.

**Note:** The operations are applied sequentially, not all at once.

## Examples

### Example 1:
```
Input: nums = [1,2,2,1,1,0]
Output: [1,4,2,0,0,0]

Explanation:
- i = 0: nums[0] and nums[1] are not equal, so we skip this operation.
- i = 1: nums[1] and nums[2] are equal, we multiply nums[1] by 2 and change nums[2] to 0. 
  Array becomes [1,4,0,1,1,0].
- i = 2: nums[2] and nums[3] are not equal, so we skip this operation.
- i = 3: nums[3] and nums[4] are equal, we multiply nums[3] by 2 and change nums[4] to 0. 
  Array becomes [1,4,0,2,0,0].
- i = 4: nums[4] and nums[5] are equal, we multiply nums[4] by 2 and change nums[5] to 0. 
  Array becomes [1,4,0,2,0,0].
After shifting 0's to the end: [1,4,2,0,0,0]
```

### Example 2:
```
Input: nums = [0,1]
Output: [1,0]
Explanation: No operation can be applied, we just shift the 0 to the end.
```

## Constraints
- `2 <= nums.length <= 2000`
- `0 <= nums[i] <= 1000`

## Solution

```python
class Solution:
    def applyOperations(self, nums):
        """
        Apply operations to array and shift zeros to end.
        
        Time Complexity: O(n)
        Space Complexity: O(1)
        """
        n = len(nums)
        
        # Apply n-1 operations sequentially
        for i in range(n - 1):
            if nums[i] == nums[i + 1]:
                nums[i] *= 2
                nums[i + 1] = 0
        
        # Shift all zeros to the end using two pointers
        write_pos = 0
        
        # Move all non-zero elements to the front
        for read_pos in range(n):
            if nums[read_pos] != 0:
                nums[write_pos] = nums[read_pos]
                write_pos += 1
        
        # Fill remaining positions with zeros
        while write_pos < n:
            nums[write_pos] = 0
            write_pos += 1
        
        return nums

# Test the solution
if __name__ == "__main__":
    solution = Solution()
    
    # Test case 1
    nums1 = [1,2,2,1,1,0]
    result1 = solution.applyOperations(nums1[:])  # Use copy to preserve original
    print("Test 1:")
    print("Input: " + str([1,2,2,1,1,0]))
    print("Output: " + str(result1))
    print("Expected: [1,4,2,0,0,0]")
    print("✓ Passed" if result1 == [1,4,2,0,0,0] else "✗ Failed")
    print()
    
    # Test case 2
    nums2 = [0,1]
    result2 = solution.applyOperations(nums2[:])  # Use copy to preserve original
    print("Test 2:")
    print("Input: " + str([0,1]))
    print("Output: " + str(result2))
    print("Expected: [1,0]")
    print("✓ Passed" if result2 == [1,0] else "✗ Failed")
```

## Algorithm Explanation

### Step 1: Apply Operations
- Iterate through indices 0 to n-2
- For each index i, check if `nums[i] == nums[i+1]`
- If equal: multiply `nums[i]` by 2 and set `nums[i+1]` to 0
- If not equal: skip to next index

### Step 2: Shift Zeros to End
- Use two pointers technique for in-place shifting
- `write_pos`: points to the position where next non-zero element should be placed
- `read_pos`: scans through the array
- Copy all non-zero elements to the front, then fill remaining positions with zeros

## Complexity Analysis
- **Time Complexity:** O(n) - Single pass for operations + single pass for shifting
- **Space Complexity:** O(1) - In-place modifications only

## Key Insights
1. Operations must be applied sequentially, not simultaneously
2. When we modify elements at positions i and i+1, it affects subsequent operations
3. Two-pointer technique efficiently moves zeros to end without extra space

---
*Solution by [@Harikrishnan120A](https://github.com/Harikrishnan120A)*  
*Date: 2025-07-10*
