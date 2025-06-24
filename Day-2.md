## Date: 2025-06-24
Problem: Find All K-Distant Indices in an Array
Difficulty: Easy
Source: LeetCode
Link: https://leetcode.com/problems/find-all-k-distant-indices-in-an-array

```
from typing import List

class Solution:
    def findKDistantIndices(self, nums: List[int], key: int, k: int) -> List[int]:

```

 
 ## Finds all k-distant indices in the array.
        
        A k-distant index is an index i where there exists at least one index j
        such that |i - j| <= k and nums[j] == key.

        Args:
            nums: The input array of integers.
            key: The value to find in the array.
            k: The maximum allowed distance between indices.

        Returns:
            A sorted list of all k-distant indices.
            
        Approach:
            1. First find all indices where nums[j] == key
            2. For each such j, mark all indices i where |i-j| <= k
            3. Use a set to avoid duplicates
            4. Return the sorted result



```            
        result = set()
        key_indices = [i for i, val in enumerate(nums) if val == key]

        for j in key_indices:
            # Add all indices within k distance of j
            start = max(0, j - k)
            end = min(len(nums), j + k + 1)
            for i in range(start, end):
                result.add(i)

        return sorted(result)


def test_solution():
    sol = Solution()

```
    

    
    # Test Case 1
    nums1 = [3, 4, 9, 1, 3, 9, 5]
    key1 = 9
    k1 = 1
    assert sol.findKDistantIndices(nums1, key1, k1) == [1, 2, 3, 4, 5, 6]
    
    # Test Case 2
    nums2 = [2, 2, 2, 2, 2]
    key2 = 2
    k2 = 2
    assert sol.findKDistantIndices(nums2, key2, k2) == [0, 1, 2, 3, 4]
    
    # Additional Test Case
    nums3 = [1, 2, 3, 4, 5]
    key3 = 3
    k3 = 2
    assert sol.findKDistantIndices(nums3, key3, k3) == [0, 1, 2, 3, 4]
    
    print("All test cases pass")


```

if __name__ == "__main__":
    test_solution()

```
