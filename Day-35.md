# 🧠 Fruit Into Baskets

Author: Harikrishnan120A          
Date: August 4, 2025           
Difficulty: Medium             
Tags: Sliding Window, HashMap           

## ✅ Problem Description

We need to pick the maximum number of fruits in a contiguous subarray where we can carry only two types of fruits at most, using two baskets.
This is a classic sliding window problem where we expand the window to the right and contract it from the left if the number of fruit types exceeds two.

## 🚀 Code Solution (Python)

```
class Solution:
    def totalFruit(self, fruits):
        basket = {}
        left = 0
        max_fruits = 0

        for right in range(len(fruits)):
            fruit = fruits[right]
            basket[fruit] = basket.get(fruit, 0) + 1

            while len(basket) > 2:
                left_fruit = fruits[left]
                basket[left_fruit] -= 1
                if basket[left_fruit] == 0:
                    del basket[left_fruit]
                left += 1

            max_fruits = max(max_fruits, right - left + 1)

        return max_fruits

```

## 📈 Example Execution

Example 1:

fruits = [1, 2, 1]       
**Output:** 3 (Pick all trees)

Example 2:

fruits = [0, 1, 2, 2]      
**Output:** 3 (Pick [1,2,2])

Example 3:

fruits = [1, 2, 3, 2, 2]     
**Output:** 4 (Pick [2,3,2,2])


## 🧠 Time and Space Complexity

**Time Complexity:** O(n) — Each fruit is processed at most twice (once added, once removed).               

**Space Complexity:** O(1) — At most 2 keys in the basket dictionary.
