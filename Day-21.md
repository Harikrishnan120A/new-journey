# Convert Binary Number in a Linked List to Integer

**Author:** Harikrishnan120A

**Date:** July 14, 2025

## Problem Statement
Given the `head` of a singly-linked list where each node contains a binary digit (0 or 1), return the decimal value of the binary number it represents. The most significant bit is at the head of the linked list.

### Examples
1. **Input:** `head = [1,0,1]`  
   **Output:** `5`  
   **Explanation:** `(101)₂ = (5)₁₀`

2. **Input:** `head = [0]`  
   **Output:** `0`

## Approach
1. **Traverse the Linked List:** Start from the head node and move to the end, collecting binary digits.
2. **Convert Binary to Decimal:** Use the positional values of each bit (powers of 2) to compute the decimal value.
3. **Calculate Decimal Value:** Initialize a result variable to 0. For each bit, update the result by shifting left (multiplying by 2) and adding the current bit's value.

## Solution Code
```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def getDecimalValue(self, head):
        decimal_value = 0
        current = head
        while current is not None:
            decimal_value = decimal_value * 2 + current.val
            current = current.next
        return decimal_value
```

## Explanation
- **Initialization:** `decimal_value` starts at 0 to accumulate the result.
- **Traversal:** Loop through each node in the linked list:
  - **Update Decimal Value:** Multiply the current value by 2 (shift left) and add the node's value (0 or 1).
- **Termination:** Return the accumulated `decimal_value` after processing all nodes.

### Example Walkthrough
For the linked list `1 -> 0 -> 1`:
1. **First Node (1):** `decimal_value = 0 * 2 + 1 = 1`
2. **Second Node (0):** `decimal_value = 1 * 2 + 0 = 2`
3. **Third Node (1):** `decimal_value = 2 * 2 + 1 = 5`
4. **Result:** `5`

**Time Complexity:** O(n)  
**Space Complexity:** O(1)
