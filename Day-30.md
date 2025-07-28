# Count Number of Maximum Bitwise-OR Subsets

**Author**: Harikrishnan120A  
**Date**: 2025-07-28  
**Difficulty**: Medium  
**Tags**: Backtracking, Bit Manipulation

---

## 🧩 Problem Description

Given an integer array `nums`, find the number of non-empty subsets such that the **bitwise OR** of all elements in the subset is equal to the **maximum possible bitwise OR** of any subset of `nums`.

### Example 1:

Input: nums = [3,1]
Output: 2
Explanation: The maximum OR is 3. The subsets that give OR = 3 are [3], [3,1].

shell
Copy
Edit

### Example 2:

Input: nums = [2,2,2]
Output: 7
Explanation: All non-empty subsets have OR = 2.

yaml
Copy
Edit


---

## 💡 Approach

1. **Find the maximum OR** that any subset can achieve by OR-ing all elements.
2. **Use backtracking** to explore all possible subsets.
3. For each subset, if its OR value matches the maximum, increment a counter.
4. To support environments without `nonlocal` (like Python 2), we use a list to store the count.

---

## ✅ Python Code (Compatible with Python 2 and 3)

```python
class Solution:
    def countMaxOrSubsets(self, nums):
        max_or = 0
        for num in nums:
            max_or |= num

        count = [0]  # Use list to simulate nonlocal variable

        def backtrack(index, current_or):
            if index == len(nums):
                if current_or == max_or:
                    count[0] += 1
                return
            # Include current number
            backtrack(index + 1, current_or | nums[index])
            # Exclude current number
            backtrack(index + 1, current_or)

        backtrack(0, 0)
        return count[0]
```

## 🧪 Sample Runs

sol = Solution()
print(sol.countMaxOrSubsets([3, 1]))       # Output: 2
print(sol.countMaxOrSubsets([2, 2, 2]))    # Output: 7
print(sol.countMaxOrSubsets([1, 2, 3]))    # Output: 6

## 📦 Time & Space Complexity

**Time Complexity:** O(2^n) — All subsets are explored.

**Space Complexity:** O(n) — Maximum recursion depth.


