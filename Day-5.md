# Longest Subsequence Repeated k Times

## Problem Description

**Difficulty:** Hard  
**Topics:** String, Dynamic Programming, Backtracking  

You are given a string `s` of length `n`, and an integer `k`. You are tasked to find the longest subsequence repeated k times in string s.

A subsequence is a string that can be derived from another string by deleting some or no characters without changing the order of the remaining characters.

A subsequence `seq` is repeated k times in the string `s` if `seq * k` is a subsequence of `s`, where `seq * k` represents a string constructed by concatenating `seq` k times.

For example, "bba" is repeated 2 times in the string "bababcba", because the string "bbabba", constructed by concatenating "bba" 2 times, is a subsequence of the string "bababcba".

Return the longest subsequence repeated k times in string s. If multiple such subsequences are found, return the lexicographically largest one. If there is no such subsequence, return an empty string.

## Examples

### Example 1:
![image1](image1)

**Input:** s = "letsleetcode", k = 2  
**Output:** "let"  
**Explanation:** There are two longest subsequences repeated 2 times: "let" and "ete".  
"let" is the lexicographically largest one.

### Example 2:
**Input:** s = "bb", k = 2  
**Output:** "b"  
**Explanation:** The longest subsequence repeated 2 times is "b".

### Example 3:
**Input:** s = "ab", k = 2  
**Output:** ""  
**Explanation:** There is no subsequence repeated 2 times. Empty string is returned.

## Constraints

- n == s.length
- 2 <= n, k <= 2000
- 2 <= n < k * 8
- s consists of lowercase English letters.

## Solution

```python
class Solution(object):
    def longestSubsequenceRepeatedK(self, s, k):
        """
        :type s: str
        :type k: int
        :rtype: str
        """
        from collections import Counter
        
        # Count frequency of each character
        char_count = Counter(s)
        
        # Only consider characters that appear at least k times
        valid_chars = [char for char in 'abcdefghijklmnopqrstuvwxyz' if char_count[char] >= k]
        
        def can_form_k_times(subseq):
            """Check if subsequence can be repeated k times in string s"""
            if not subseq:
                return True
            
            # We need to find k occurrences of the subsequence
            target = subseq * k
            
            # Use two pointers to check if target is a subsequence of s
            i = 0  # pointer for s
            j = 0  # pointer for target
            
            while i < len(s) and j < len(target):
                if s[i] == target[j]:
                    j += 1
                i += 1
            
            return j == len(target)
        
        # Use a list to store the best result (mutable for Python 2)
        best_result = [""]
        
        def backtrack(current_subseq):
            """Backtrack to find the longest valid subsequence"""
            if not can_form_k_times(current_subseq):
                return
            
            # Update best result
            if (len(current_subseq) > len(best_result[0]) or 
                (len(current_subseq) == len(best_result[0]) and current_subseq > best_result[0])):
                best_result[0] = current_subseq
            
            # Try extending with each valid character
            for char in valid_chars:
                # Only extend if we haven't exceeded the character limit
                new_count = current_subseq.count(char) + 1
                if new_count <= char_count[char] // k:
                    backtrack(current_subseq + char)
        
        # Start backtracking
        backtrack("")
        return best_result[0]
```

## Algorithm Explanation

### Approach: Backtracking with Pruning

1. **Character Frequency Analysis**: First, identify which characters can potentially be part of a valid subsequence. A character must appear at least k times to be part of a subsequence repeated k times.

2. **Character Usage Limit**: For each valid character, calculate the maximum number of times it can be used in the subsequence. If a character appears `count` times in the original string, it can be used at most `count // k` times in the subsequence.

3. **Backtracking**: Use backtracking to generate all possible subsequences from valid characters, with the constraint that each character is used at most its calculated limit.

4. **Subsequence Validation**: For each candidate subsequence, verify if it can be repeated k times as a subsequence of the original string using a two-pointer approach.

5. **Result Selection**: Among all valid subsequences, select the one with maximum length. In case of ties, select the lexicographically largest one.

### Key Optimizations

- **Early Pruning**: Only consider characters that appear at least k times
- **Usage Limiting**: Prevent generating invalid subsequences by limiting character usage
- **Efficient Validation**: Use two-pointer technique for subsequence checking

### Complexity Analysis

- **Time Complexity**: O(2^m × n) where m is the number of valid characters and n is the length of the string. In practice, this is much better due to pruning.
- **Space Complexity**: O(m + n) for the recursion stack and character counting.

## Test Cases

The solution handles all the given examples correctly:
- Example 1: Returns "let" (lexicographically larger than "ete")
- Example 2: Returns "b" 
- Example 3: Returns "" (no valid subsequence)

---

**Author:** Harikrishnan120A  
**Date:** 2025-06-27  
**Platform:** LeetCode
