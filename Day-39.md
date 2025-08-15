# 🧮 Power of Four

**Date:** 2025-08-15  
**Difficulty:** Easy            
**Author:** Harikrishnan120A

---

## 📜 Problem Statement

Given an integer `n`, return `true` if it is a power of four. Otherwise, return `false`.
An integer `n` is a power of four if there exists an integer `x` such that: n == 4^x

---

## 📊 Examples

### Example 1             
**Input:**          
n = 16            
**Output:**          
true          

### Example 2
**Input:**           
n = 5           
**Output:**           
false               

### Example 3
**Input:**             
n = 1               
**Output:**              
true

---

## 🔒 Constraints

- `-2^31 <= n <= 2^31 - 1`

---

## 💡 Approach
1. A number that is a power of four must be **positive**.             
2. Keep dividing `n` by 4 while it is divisible by 4.          
3. If at the end the number becomes 1, it was a power of four.           

---

## 💻 Python Solution
```python
class Solution:
    def isPowerOfFour(self, n):
        if n <= 0:
            return False
        
        while n % 4 == 0:
            n //= 4
        
        return n == 1
```

## ⏱ Complexity Analysis

**Time Complexity:** O(log₄ n) – we repeatedly divide by 4 until we reach 1.      
**Space Complexity:** O(1) – no extra space used.      

## ✅ Summary

- Works for all integers within the given range.           
- Handles negative numbers and zero correctly.         
- Pure mathematical approach, no extra libraries required.
