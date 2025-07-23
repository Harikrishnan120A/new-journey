# Maximum Score From Removing Substrings

**Author:** Harikrishnan120A

**Date:** July 23, 2025  
**Language:** Python  
**Difficulty:** Medium  

## Problem Description
You are given a string `s` and two integers `x` and `y`. You can perform two types of operations any number of times:
1. Remove substring "ab" and gain `x` points.
2. Remove substring "ba" and gain `y` points.

Return the maximum points you can gain after applying the above operations on `s`.

## Solutions

### Python 3 Solution (with type hints)
```python
class Solution:
    def maximumGain(self, s: str, x: int, y: int) -> int:
        def calculate_score(s, first, second, first_score, second_score):
            stack = []
            total = 0
            # Process the first pattern
            for char in s:
                if stack and stack[-1] == first and char == second:
                    stack.pop()
                    total += first_score
                else:
                    stack.append(char)
            # Process the remaining string for the second pattern
            s_remaining = ''.join(stack)
            stack = []
            for char in s_remaining:
                if stack and stack[-1] == second and char == first:
                    stack.pop()
                    total += second_score
                else:
                    stack.append(char)
            return total
        
        # We need to check both scenarios: ab first or ba first and return the max
        scenario1 = calculate_score(s, 'a', 'b', x, y)
        scenario2 = calculate_score(s, 'b', 'a', y, x)
        return max(scenario1, scenario2)
```

## Example Usage

```
sol = Solution()
print(sol.maximumGain("cdbcbbaaabab", 4, 5))  # Output: 19
print(sol.maximumGain("aabbaaxybbaabb", 5, 4))  # Output: 20
```

## Approach

**The solution uses a greedy approach with stack processing:**

First pass removes all occurrences of the higher-value substring ("ab" if x > y, else "ba")

Second pass processes the remaining string for the other substring

Returns the maximum score from both scenarios

## Complexity Analysis

**Time Complexity:** O(n), where n is the length of the string s

**Space Complexity:** O(n), for the stack storage
