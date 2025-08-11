# 📌 Range Product Queries of Powers

**Date:** 2025-08-11  
**Difficulty:** Medium  
**Author:** Harikrishnan120A  

---

## 📝 Problem Statement

Given a positive integer `n`, there exists a **0-indexed array** called `powers`, composed of the minimum number of powers of 2 that sum to `n`. The array is sorted in **non-decreasing order** and is unique.

You are also given a **0-indexed 2D integer array** `queries`, where each `queries[i] = [left, right]`.  
For each query, find the product of `powers[left]` to `powers[right]` (inclusive) and return the results modulo **1,000,000,007**.

---

### Example 1
Input: n = 15, queries = [[0,1],[2,2],[0,3]]
Output: [2,4,64]

**Explanation:**
n = 15 → binary 1111 → powers = [1, 2, 4, 8]
Query 1: 1 × 2 = 2
Query 2: 4
Query 3: 1 × 2 × 4 × 8 = 64

### Example 2
Input: n = 2, queries = [[0,0]]
Output: [2]

**Explanation:**
n = 2 → powers = [2]
Query: 2

---

## 💡 Approach

### Idea:
- The `powers` array is made of **distinct powers of 2** from `n`’s binary representation.
- Instead of multiplying directly, we can store the **exponents** of 2, use **prefix sums**, and compute:
  
  \[
  \text{product} = 2^{\text{sum of exponents in range}} \pmod{10^9+7}
  \]
  
- This avoids modular inverse and is faster.

### Complexity:
- **Time:** O(log n + Q)
- **Space:** O(log n)

---

## 💻 Code Implementation
```python
class Solution:
    def productQueries(self, n, queries):
        MOD = 10**9 + 7

        # Step 1: Extract exponents of set bits
        exps = []
        bit = 0
        temp = n
        while temp:
            if temp & 1:
                exps.append(bit)
            bit += 1
            temp >>= 1

        # Step 2: Prefix sum of exponents
        prefix = [0] * (len(exps) + 1)
        for i in range(len(exps)):
            prefix[i+1] = prefix[i] + exps[i]

        # Step 3: Answer queries using modular exponentiation
        ans = []
        for l, r in queries:
            s = prefix[r+1] - prefix[l]
            ans.append(pow(2, s, MOD))

        return ans
```

### Example Usage

if __name__ == "__main__":
    sol = Solution()
    print(sol.productQueries(15, [[0,1],[2,2],[0,3]]))  # [2, 4, 64]
    print(sol.productQueries(2, [[0,0]]))               # [2]


## 📊 Complexity Analysis

Step	Time Complexity	Space Complexity
Build exponents list	O(log n)	O(log n)
Prefix sum	O(log n)	O(log n)
Answer queries	O(Q)	O(1)
Total	O(log n + Q)	O(log n)

## ✅ Notes
Using exponents + pow(2, sum, MOD) avoids modular inverses.

Works for 1 ≤ n ≤ 10⁹ and up to 10⁵ queries efficiently.
