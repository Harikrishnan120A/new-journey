# Finding Pairs With a Certain Sum

**Difficulty:** Medium  
**Topics:** Array, Hash Table, Design  

## Problem Description

You are given two integer arrays `nums1` and `nums2`. You are tasked to implement a data structure that supports queries of two types:

1. Add a positive integer to an element of a given index in the array `nums2`.
2. Count the number of pairs `(i, j)` such that `nums1[i] + nums2[j]` equals a given value (0 ≤ i < nums1.length and 0 ≤ j < nums2.length).

Implement the `FindSumPairs` class:

- `FindSumPairs(int[] nums1, int[] nums2)` Initializes the FindSumPairs object with two integer arrays nums1 and nums2.
- `void add(int index, int val)` Adds val to nums2[index], i.e., apply nums2[index] += val.
- `int count(int tot)` Returns the number of pairs (i, j) such that nums1[i] + nums2[j] == tot.

## Example

```
Input
["FindSumPairs", "count", "add", "count", "count", "add", "add", "count"]
[[[1, 1, 2, 2, 2, 3], [1, 4, 5, 2, 5, 4]], [7], [3, 2], [8], [4], [0, 1], [1, 1], [7]]

Output
[null, 8, null, 2, 1, null, null, 11]

Explanation
FindSumPairs findSumPairs = new FindSumPairs([1, 1, 2, 2, 2, 3], [1, 4, 5, 2, 5, 4]);
findSumPairs.count(7);  // return 8; pairs (2,2), (3,2), (4,2), (2,4), (3,4), (4,4) make 2 + 5 and pairs (5,1), (5,5) make 3 + 4
findSumPairs.add(3, 2); // now nums2 = [1,4,5,4,5,4]
findSumPairs.count(8);  // return 2; pairs (5,2), (5,4) make 3 + 5
findSumPairs.count(4);  // return 1; pair (5,0) makes 3 + 1
findSumPairs.add(0, 1); // now nums2 = [2,4,5,4,5,4]
findSumPairs.add(1, 1); // now nums2 = [2,5,5,4,5,4]
findSumPairs.count(7);  // return 11; pairs (2,1), (2,2), (2,4), (3,1), (3,2), (3,4), (4,1), (4,2), (4,4) make 2 + 5 and pairs (5,3), (5,5) make 3 + 4
```

## Constraints

- 1 ≤ nums1.length ≤ 1000
- 1 ≤ nums2.length ≤ 10⁵
- 1 ≤ nums1[i] ≤ 10⁹
- 1 ≤ nums2[i] ≤ 10⁵
- 0 ≤ index < nums2.length
- 1 ≤ val ≤ 10⁵
- 1 ≤ tot ≤ 10⁹
- At most 1000 calls are made to add and count each.

## Solution Approach

### Key Insights:
1. **nums1** is read-only, so we can preprocess it
2. **nums2** gets modified, so we need to track its frequency efficiently
3. For counting pairs with sum `tot`, we need `nums1[i] + nums2[j] = tot`, which means `nums2[j] = tot - nums1[i]`

### Algorithm:
- Use a frequency map to track counts of elements in `nums2`
- For `add()`: Update the frequency map when modifying `nums2`
- For `count()`: For each element in `nums1`, find the required complement in `nums2` using the frequency map

## Implementation

### Python Solution

```python
from collections import Counter

class FindSumPairs:
    def __init__(self, nums1, nums2):
        self.nums1 = nums1
        self.nums2 = nums2
        # Keep frequency count of nums2 for efficient lookups
        self.nums2_count = Counter(nums2)
    
    def add(self, index, val):
        # Remove old value from counter
        old_val = self.nums2[index]
        self.nums2_count[old_val] -= 1
        if self.nums2_count[old_val] == 0:
            del self.nums2_count[old_val]
        
        # Update nums2 and add new value to counter
        self.nums2[index] += val
        new_val = self.nums2[index]
        self.nums2_count[new_val] = self.nums2_count.get(new_val, 0) + 1
    
    def count(self, tot):
        pairs = 0
        # For each element in nums1, find how many elements in nums2 
        # can pair with it to make the target sum
        for num1 in self.nums1:
            needed = tot - num1
            if needed in self.nums2_count:
                pairs += self.nums2_count[needed]
        return pairs
```

### Java Solution

```java
import java.util.*;

class FindSumPairs {
    private int[] nums1;
    private int[] nums2;
    private Map<Integer, Integer> nums2Count;
    
    public FindSumPairs(int[] nums1, int[] nums2) {
        this.nums1 = nums1;
        this.nums2 = nums2;
        this.nums2Count = new HashMap<>();
        
        // Build frequency map for nums2
        for (int num : nums2) {
            nums2Count.put(num, nums2Count.getOrDefault(num, 0) + 1);
        }
    }
    
    public void add(int index, int val) {
        int oldVal = nums2[index];
        
        // Remove old value from count
        nums2Count.put(oldVal, nums2Count.get(oldVal) - 1);
        if (nums2Count.get(oldVal) == 0) {
            nums2Count.remove(oldVal);
        }
        
        // Update nums2 and add new value to count
        nums2[index] += val;
        int newVal = nums2[index];
        nums2Count.put(newVal, nums2Count.getOrDefault(newVal, 0) + 1);
    }
    
    public int count(int tot) {
        int pairs = 0;
        for (int num1 : nums1) {
            int needed = tot - num1;
            pairs += nums2Count.getOrDefault(needed, 0);
        }
        return pairs;
    }
}
```

## Complexity Analysis

- **Time Complexity:**
  - `add()`: O(1) average case
  - `count()`: O(n) where n is length of nums1
  - Initialization: O(m) where m is length of nums2

- **Space Complexity:** O(m) where m is length of nums2

## How It Works

1. **Initialization**: Store `nums1` as-is and create a frequency counter for `nums2`
2. **Add operation**: 
   - Decrease count of old value in frequency map
   - Update the array element
   - Increase count of new value in frequency map
3. **Count operation**: 
   - For each element in `nums1`, calculate what value we need from `nums2`
   - Sum up the frequencies of all needed values from the frequency map

## Why This Approach Works

- Since `nums1` doesn't change, we can iterate through it for each count query
- Using a frequency map for `nums2` allows O(1) lookups and updates
- This is more efficient than checking all pairs (which would be O(n×m) for each count)
- The frequency map automatically handles duplicate values in `nums2`

---

**Author:** Harikrishnan120A  
**Date:** July 6, 2025
