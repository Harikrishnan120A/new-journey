# Fancy String Solution

**Author**: Harikrishnan120A
**Date**: July 24, 2023

## Problem Statement
A fancy string is a string where no three consecutive characters are equal. Given a string `s`, delete the minimum possible number of characters to make it fancy.

## Solution Approach
The solution iterates through the string while maintaining a result list. For each character, it checks if adding it would create three consecutive identical characters. If not, the character is added to the result.

## Solution Code
```python
class Solution:
    def makeFancyString(self, s: str) -> str:
        if len(s) < 3:
            return s
        res = []
        for char in s:
            if len(res) >= 2 and res[-1] == char and res[-2] == char:
                continue
            res.append(char)
        return ''.join(res)
```

## Explanation

**Initial Check:** If the string length is less than 3, return it immediately as no modifications are needed.

**Result Construction:** We build the result string character by character Skip adding a character if it would create three consecutive identical characters

Otherwise, add the character to the result

**Efficiency:** The algorithm runs in O(n) time with O(n) space complexity, making it optimal for large inputs.

## Example Usage

```python

sol = Solution()
print(sol.makeFancyString("leeetcode"))  # Output: "leetcode"
print(sol.makeFancyString("aaabaaaa"))   # Output: "aabaa"
print(sol.makeFancyString("aab"))        # Output: "aab"
```
