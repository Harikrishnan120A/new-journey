# Pascal's Triangle

**Author:** Harikrishnan120A  
**Date:** 2025-08-01  

---

## 📝 Problem Description

Given an integer `numRows`, return the first `numRows` of Pascal's triangle.

In Pascal's triangle, each number is the sum of the two numbers directly above it.

---

## 📥 Input

- `numRows` (integer): Number of rows to generate in Pascal's Triangle  
- Constraint: `1 <= numRows <= 30`

---

## 📤 Output

- A list of lists containing the first `numRows` of Pascal's Triangle.

---

## 💡 Example

### Example 1:
**Input:**
numRows = 5

**Output:**
[[1],
[1,1],
[1,2,1],
[1,3,3,1],
[1,4,6,4,1]]

### Example 2:
**Input:**
numRows = 1

**Output:**
[[1]]

---

## 🧠 Approach

- Start with the first row as `[1]`.
- For each subsequent row:
  - Begin and end with `1`.
  - Each inner value is the sum of the two numbers directly above it from the previous row.
- Append each row to the result.

---

## ✅ Python Solution

```python
class Solution:
    def generate(self, numRows):
        triangle = []

        for row_num in range(numRows):
            row = [1] * (row_num + 1)
            for j in range(1, row_num):
                row[j] = triangle[row_num - 1][j - 1] + triangle[row_num - 1][j]
            triangle.append(row)

        return triangle

# Example usage:
sol = Solution()
print(sol.generate(5))
```

## 📌 Notes
This version avoids type annotations for full compatibility.

Works in any standard Python environment without additional imports.
