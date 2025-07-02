# Original Typed String II

## Problem Description

**Difficulty:** Hard  
**Type:** Dynamic Programming, String Processing  
**Companies:** Premium Content

Alice is attempting to type a specific string on her computer. However, she tends to be clumsy and may press a key for too long, resulting in a character being typed multiple times.

You are given a string `word`, which represents the final output displayed on Alice's screen. You are also given a positive integer `k`.

Return the total number of possible original strings that Alice might have intended to type, if she was trying to type a string of size at least `k`.

Since the answer may be very large, return it modulo `10^9 + 7`.

## Examples

### Example 1
```
Input: word = "aabbccdd", k = 7
Output: 5
Explanation: The possible strings are: "aabbccdd", "aabbccd", "aabbcdd", "aabccdd", and "abbccdd".
```

### Example 2
```
Input: word = "aabbccdd", k = 8
Output: 1
Explanation: The only possible string is "aabbccdd".
```

### Example 3
```
Input: word = "aaabbb", k = 3
Output: 8
```

## Constraints

- `1 <= word.length <= 5 * 10^5`
- `word` consists only of lowercase English letters
- `1 <= k <= 2000`

## Solution Approach

This problem requires dynamic programming to count valid combinations. The key insights are:

1. **Group consecutive characters:** Identify groups of consecutive identical characters
2. **Base case optimization:** If `k ≤ number of groups`, all combinations are valid since each group contributes at least 1 character
3. **DP for counting:** Use dynamic programming to count invalid combinations (length < k) and subtract from total
4. **Optimization techniques:** Use prefix sums to avoid nested loops and reduce time complexity

## Algorithm Steps

1. Parse the input string to find consecutive character groups
2. If `k ≤ number of groups`, return the product of all group sizes
3. Use DP to count combinations that result in strings shorter than k
4. Subtract invalid combinations from total possible combinations

## Code Implementation

### Python

```python
class Solution(object):
    def possibleStringCount(self, word, k):
        MOD = 1000000007
        
        # Find groups of consecutive same characters
        groups = []
        i = 0
        while i < len(word):
            j = i
            while j < len(word) and word[j] == word[i]:
                j = j + 1
            groups.append(j - i)
            i = j
        
        num_groups = len(groups)
        
        # If k <= number of groups, all combinations are valid
        if k <= num_groups:
            result = 1
            for group_len in groups:
                result = (result * group_len) % MOD
            return result
        
        # Special optimization for single group case
        if num_groups == 1:
            group_size = groups[0]
            if k > group_size:
                return 0
            else:
                return group_size - k + 1
        
        # For multiple groups, use optimized DP
        # We need to count ways to get < k total characters
        
        # Use space-optimized DP
        prev_dp = [0] * k
        prev_dp[0] = 1
        
        for group_size in groups:
            curr_dp = [0] * k
            
            # Use prefix sums for optimization
            prefix_sum = [0] * (k + 1)
            for j in range(k):
                prefix_sum[j + 1] = (prefix_sum[j] + prev_dp[j]) % MOD
            
            for j in range(k):
                # We can use 1 to min(group_size, j+1) characters
                max_use = min(group_size, j + 1)
                if max_use >= 1:
                    # Sum of prev_dp[j-max_use] to prev_dp[j-1]
                    start_idx = max(0, j - max_use)
                    end_idx = j
                    curr_dp[j] = (prefix_sum[end_idx] - prefix_sum[start_idx] + MOD) % MOD
            
            prev_dp = curr_dp
        
        # Calculate total and subtract invalid
        total_combinations = 1
        for group_len in groups:
            total_combinations = (total_combinations * group_len) % MOD
        
        invalid_combinations = sum(prev_dp) % MOD
        result = (total_combinations - invalid_combinations + MOD) % MOD
        return result
```

## Complexity Analysis

- **Time Complexity:** `O(num_groups × k)` where `num_groups` is the number of consecutive character groups
- **Space Complexity:** `O(k)` for the DP arrays

## Key Optimizations

1. Early termination for cases where `k ≤ number of groups`
2. Special handling for single group scenarios
3. Prefix sum technique to avoid nested loops in DP transitions
4. Space optimization by maintaining only the current and previous DP states

## Test Cases

The solution handles various edge cases including:

- Very long strings with repeated characters
- Small values of k relative to string length
- Single character group scenarios
- Large constraint inputs (up to 5×10^5 characters)

---

**Author:** Harikrishnan120A  
**Date:** July 2, 2025
