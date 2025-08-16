# Maximum 69 Number

**Date:** 2025-08-15  
**Difficulty:** Easy  
**Author:** Harikrishnan120A


## Problem
You are given a positive integer `num` consisting only of digits `6` and `9`.  
Return the maximum number you can get by changing **at most one digit** (6 → 9 or 9 → 6).

### Example 1
Input: num = 9669
Output: 9969

### Example 2
Input: num = 9996
Output: 9999

### Example 3
Input: num = 9999
Output: 9999

---

## Constraints
- 1 <= num <= 10^4  
- num consists of only digits `6` and `9`.

---

## Solution (Python)

```python
class Solution:
    def maximum69Number(self, num):
        num_list = list(str(num))
        for i in range(len(num_list)):
            if num_list[i] == '6':
                num_list[i] = '9'
                break
        return int("".join(num_list))
```
## Explanation

-Convert the number to a list of characters.                 
-Traverse the list and change the first 6 to a 9.                        
-Break after the first change since only one digit can be modified.                   
-Convert the list back into an integer and return the result.                

## Complexity

**Time:** O(d) — where d is the number of digits (≤ 4 here).             
**Space:** O(d) — for storing the digit list.
