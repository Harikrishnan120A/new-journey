# K-th Character in String Game I

**Problem:** Find the K-th Character in String Game I  
**Difficulty:** Easy  
**Date:** 2025-07-03 08:45:52 (UTC)  
**Author:** Harikrishnan120A

## Problem Description

Alice and Bob are playing a game. Initially, Alice has a string word = "a".

You are given a positive integer k.

Now Bob will ask Alice to perform the following operation forever:

Generate a new string by changing each character in word to its next character in the English alphabet, and append it to the original word.

For example, performing the operation on "c" generates "cd" and performing the operation on "zb" generates "zbac".

Return the value of the kth character in word, after enough operations have been done for word to have at least k characters.

Note that the character 'z' can be changed to 'a' in the operation.

## Examples

### Example 1:
```
Input: k = 5
Output: "b"

Explanation:
Initially, word = "a". We need to do the operation three times:
- Generated string is "b", word becomes "ab".
- Generated string is "bc", word becomes "abbc".
- Generated string is "bccd", word becomes "abbcbccd".
```

### Example 2:
```
Input: k = 10
Output: "c"
```

## Constraints
- 1 <= k <= 500

## Solution

```python
class Solution:
    def kthCharacter(self, k):
        word = "a"
        
        # Keep generating until we have at least k characters
        while len(word) < k:
            # Generate new string by changing each character to its next character
            new_part = ""
            for char in word:
                if char == 'z':
                    new_part += 'a'  # 'z' wraps around to 'a'
                else:
                    new_part += chr(ord(char) + 1)  # next character in alphabet
            
            # Append the new part to the original word
            word += new_part
        
        # Return the k-th character (1-indexed, so we use k-1)
        return word[k-1]
```

## Algorithm Explanation

1. **Initialize:** Start with `word = "a"`
2. **Generate:** In each iteration:
   - Create a new string by converting each character to its next character in the alphabet
   - Handle wraparound: 'z' becomes 'a'
   - Append this new string to the original word
3. **Continue** until the word has at least k characters
4. **Return** the k-th character (using 0-based indexing)

## Time and Space Complexity

- **Time Complexity:** O(k) - We generate characters until we reach at least k characters
- **Space Complexity:** O(k) - We store the string which grows to at least k characters

## Test Cases

```python
def test_solution():
    solution = Solution()
    
    # Test case 1
    assert solution.kthCharacter(5) == "b"
    
    # Test case 2
    assert solution.kthCharacter(10) == "c"
    
    print("All test cases passed!")

test_solution()
```

---

**Created by:** [Harikrishnan120A](https://github.com/Harikrishnan120A)  
**Date:** July 3, 2025
