# Valid Word Checker

**Author**: Harikrishnan120A  
**Date**: 2025-07-15

## Problem Statement
A word is considered valid if:
- It contains a minimum of 3 characters.
- It contains only digits (0-9) and English letters (uppercase and lowercase).
- It includes at least one vowel.
- It includes at least one consonant.

Given a string `word`, return `True` if the word is valid, otherwise return `False`.

## Approach
1. **Check Length**: Ensure the word has at least 3 characters.
2. **Check Valid Characters**: Verify all characters are digits or English letters.
3. **Check Vowel and Consonant Presence**: Confirm the word contains at least one vowel and one consonant.

## Solution Code
~~~python
class Solution:
    def isValid(self, word: str) -> bool:
        if len(word) < 3:
            return False
        
        vowels = {'a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'}
        has_vowel = False
        has_consonant = False
        valid_chars = set('abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789')
        
        for char in word:
            if char not in valid_chars:
                return False
            
            if char in vowels:
                has_vowel = True
            elif char.isalpha():
                has_consonant = True
        
        return has_vowel and has_consonant

~~~

## Explanation

1. **Length Check:** The function first checks if the word length is less than 3, returning False if true.

2. **Character Validation:** Each character is checked to ensure it's a digit or English letter. Invalid characters cause the function to return False.

3. **Vowel and Consonant Check:** The function checks for at least one vowel and one consonant. Vowels are identified from a predefined set, and consonants are any alphabetic characters not in this set. The function returns True only if both conditions are met.
