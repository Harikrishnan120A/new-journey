# Longest Binary Subsequence Less Than or Equal to K

**Difficulty:** Medium  
**Date Solved:** 2025-06-26  
**Author:** Harikrishnan120A

## Problem Description

You are given a binary string `s` and a positive integer `k`.

Return the length of the longest subsequence of `s` that makes up a binary number less than or equal to `k`.

**Note:**
- The subsequence can contain leading zeroes.
- The empty string is considered to be equal to 0.
- A subsequence is a string that can be derived from another string by deleting some or no characters without changing the order of the remaining characters.

## Examples

### Example 1:
```
Input: s = "1001010", k = 5
Output: 5
Explanation: The longest subsequence of s that makes up a binary number less than or equal to 5 is "00010", as this number is equal to 2 in decimal.
Note that "00100" and "00101" are also possible, which are equal to 4 and 5 in decimal, respectively.
The length of this subsequence is 5, so 5 is returned.
```

### Example 2:
```
Input: s = "00101001", k = 1
Output: 6
Explanation: "000001" is the longest subsequence of s that makes up a binary number less than or equal to 1, as this number is equal to 1 in decimal.
The length of this subsequence is 6, so 6 is returned.
```

## Constraints

- `1 <= s.length <= 1000`
- `s[i]` is either `'0'` or `'1'`
- `1 <= k <= 10^9`

## Solution

```python
class Solution(object):
    def longestSubsequence(self, s, k):
        n = len(s)
        count_zeros = s.count('0')
        ones_included = 0
        value = 0
        pow2 = 1
        for i in range(n - 1, -1, -1):
            if s[i] == '1':
                if value + pow2 <= k:
                    value += pow2
                    ones_included += 1
            pow2 <<= 1
            if pow2 > k:
                break
        return count_zeros + ones_included
```

## Approach

1. **Include all zeros**: All `'0'` characters can be safely included since they don't increase the binary value and leading zeros are allowed.

2. **Greedy selection of ones**: Traverse the string from right to left (least significant to most significant bit) and include `'1'` characters only if they don't make the total value exceed `k`.

3. **Early termination**: Stop checking further when the positional value exceeds `k`, as any additional `'1'` would make the number too large.

## Complexity Analysis

- **Time Complexity:** O(n) where n is the length of the string
- **Space Complexity:** O(1) using only constant extra space

## Key Insights

- Leading zeros don't affect the binary value, so all zeros can be included
- Processing from right to left ensures we prioritize less significant bits first
- The greedy approach works because including a less significant `'1'` is always better than a more significant one when both fit within the limit

---

*Solved on June 26, 2025*
