# Fruits Into Baskets II 🧺🍎

**Author:** Harikrishnan120A  
**Date:** 2025-08-05  
**Difficulty:** Easy  
**Topic:** Greedy, Arrays

---

## 🧩 Problem Statement

You are given two arrays of integers, `fruits` and `baskets`, each of length `n`, where:
- `fruits[i]` represents the quantity of the ith type of fruit,
- `baskets[j]` represents the capacity of the jth basket.

From left to right, place the fruits according to these rules:
1. Each fruit type must be placed in the **leftmost available** basket with a capacity **greater than or equal** to the quantity of that fruit type.
2. Each basket can hold **only one type** of fruit.
3. If a fruit type **cannot be placed**, it remains unplaced.

Return the **number of unplaced fruit types**.


```class Solution:

  def numOfUnplacedFruits(self, fruits, baskets):
        n = len(fruits)
        used = [False] * n  # Track used baskets
        unplaced = 0

        for i in range(n):
            placed = False
            for j in range(n):
                if not used[j] and baskets[j] >= fruits[i]:
                    used[j] = True
                    placed = True
                    break
            if not placed:
                unplaced += 1

        return unplaced

# Sample Test
print(Solution().numOfUnplacedFruits([4, 2, 5], [3, 5, 4]))  # Output: 1
print(Solution().numOfUnplacedFruits([3, 6, 1], [6, 4, 7]))  # Output: 0

```

## 💡 Constraints

- `n == fruits.length == baskets.length`
- `1 <= n <= 100`
- `1 <= fruits[i], baskets[i] <= 1000`



## 🧪 Test Cases

print(Solution().unplacedFruits([4,2,5], [3,5,4]))  # Output: 1
print(Solution().unplacedFruits([3,6,1], [6,4,7]))  # Output: 0

## 🏁 Time & Space 

**Time Complexity:** O(n²) — for each fruit, we check up to n baskets.               
**Space Complexity:** O(n) — for the used list.

