# Find the Original Typed String I

## Problem Description

Alice is attempting to type a specific string on her computer. However, she tends to be clumsy and may press a key for too long, resulting in a character being typed multiple times.

Although Alice tried to focus on her typing, she is aware that she may still have done this at most once.

You are given a string `word`, which represents the final output displayed on Alice's screen.

Return the total number of possible original strings that Alice might have intended to type.

## Examples

### Example 1:
```
Input: word = "abbcccc"
Output: 5
```
**Explanation:** The possible strings are: "abbcccc", "abbccc", "abbcc", "abbc", and "abcccc".

### Example 2:
```
Input: word = "abcd"
Output: 1
```
**Explanation:** The only possible string is "abcd".

### Example 3:
```
Input: word = "aaaa"
Output: 4
```
**Explanation:** The possible strings are: "aaaa", "aaa", "aa", and "a".

## Constraints

- `1 <= word.length <= 100`
- `word` consists only of lowercase English letters.

## Solution

### Approach

The key insight is that Alice can make a mistake **at most once** by holding a key too long. This means:

1. **No mistake case**: The typed string is exactly what Alice intended
2. **One mistake case**: Exactly one group of consecutive identical characters was typed more than intended

For each group of consecutive identical characters of length `k > 1`, Alice could have intended to type `1, 2, ..., k-1` of those characters, giving us `k-1` additional possibilities.

### Algorithm

1. Scan through the string to identify all groups of consecutive identical characters
2. For each group of size `k > 1`, add `k-1` to the total possibilities
3. Add 1 for the "no mistake" case
4. Return the total count

### Implementation

```python
class Solution:
    def possibleStringCount(self, word):
        """
        Find the number of possible original strings Alice intended to type.
        
        Args:
            word: The final string displayed on screen
        
        Returns:
            Number of possible original strings
        """
        n = len(word)
        if n == 1:
            return 1
        
        # Count consecutive character groups
        groups = []
        i = 0
        
        while i < n:
            char = word[i]
            count = 1
            
            # Count consecutive identical characters
            while i + count < n and word[i + count] == char:
                count += 1
            
            if count > 1:  # Only consider groups with more than 1 character
                groups.append(count)
            
            i += count
        
        # Calculate total possibilities
        total = 1  # Case where no mistake was made
        
        # For each group of consecutive characters, add possibilities
        # where that group was the result of holding a key too long
        for group_size in groups:
            # Can reduce the group to any size from 1 to group_size-1
            total += (group_size - 1)
        
        return total
```

### Example Walkthrough

For `word = "abbcccc"`:

1. **Find consecutive groups**: 
   - "bb" (length 2)
   - "cccc" (length 4)

2. **Calculate possibilities**:
   - No mistake: "abbcccc" (1 possibility)
   - Mistake with "bb": "abcccc" (1 possibility)
   - Mistake with "cccc": "abbccc", "abbcc", "abbc" (3 possibilities)
   - **Total**: 1 + 1 + 3 = 5

## Complexity Analysis

- **Time Complexity**: O(n) where n is the length of the word
- **Space Complexity**: O(g) where g is the number of consecutive character groups (at most n/2)

## Test Cases

```python
def test_solution():
    solution = Solution()
    
    test_cases = [
        ("abbcccc", 5),
        ("abcd", 1),
        ("aaaa", 4),
        ("a", 1),
        ("aabbcc", 4)  # Additional test case
    ]
    
    for word, expected in test_cases:
        result = solution.possibleStringCount(word)
        status = "PASS" if result == expected else "FAIL"
        print(f"Input: '{word}' -> Output: {result}, Expected: {expected}, Status: {status}")

if __name__ == "__main__":
    test_solution()
```

## Tags

- **Difficulty**: Easy
- **Topics**: String, Simulation, Counting
- **Companies**: Premium content

---

**Author**: [Harikrishnan120A](https://github.com/Harikrishnan120A)  
**Date**: July 1, 2025
