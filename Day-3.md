# Kth Smallest Product of Two Sorted Arrays

## 📋 Problem Description
Given two sorted 0-indexed integer arrays `nums1` and `nums2`, and an integer `k`, return the kth (1-based) smallest product of `nums1[i] * nums2[j]` where `0 <= i < nums1.length` and `0 <= j < nums2.length`.


### Example 
**Input:**

python
nums1 = [2,5], nums2 = [3,4], k = 2
Output:

text
8
Explanation:
The 2 smallest products are:

nums1[0] * nums2[0] = 2 * 3 = 6

nums1[0] * nums2[1] = 2 * 4 = 8
The 2nd smallest product is 8.



🔒 Constraints
1 <= nums1.length, nums2.length <= 5 * 10^4

-10^5 <= nums1[i], nums2[j] <= 10^5

1 <= k <= nums1.length * nums2.length

Both arrays are sorted in non-decreasing order

🧠 Approach
We use binary search to efficiently find the kth smallest product without generating all possible products:

Binary Search Setup
Initialize search range between minimum and maximum possible products

Counting Function
For a given mid value, count products ≤ mid by:

Special handling for zeros

For positive numbers: find elements in nums2 where product ≤ mid

For negative numbers: reverse inequality due to sign change

Search Adjustment
Narrow search space based on count comparison with k


~~~

class Solution:
    def kthSmallestProduct(self, nums1: List[int], nums2: List[int], k: int) -> int:
        def count_leq(target: int) -> int:
            count = 0
            for num in nums1:
                if num == 0:
                    if target >= 0:
                        count += len(nums2)
                elif num > 0:
                    max_val = target // num
                    if target % num < 0:
                        max_val -= 1
                    idx = bisect.bisect_right(nums2, max_val)
                    count += idx
                else:
                    min_val = target // num
                    if target % num != 0:
                        min_val += 1
                    idx = bisect.bisect_left(nums2, min_val)
                    count += len(nums2) - idx
            return count

        left, right = -10**10 - 1, 10**10 + 1
        while left < right:
            mid = (left + right) // 2
            if count_leq(mid) < k:
                left = mid + 1
            else:
                right = mid
        return left
⏱ Complexity Analysis
Time Complexity: O(n log m + log(max_product - min_product))

~~~


##Space Complexity: O(1)


✨ Key Features

🚀 Efficient binary search avoids O(n×m) complexity

🔍 Proper handling of positive/negative/zero values

📝 Type hints for better code clarity

🧩 Modular counting function



##🏗 Repository Structure


text
kth-smallest-product/
├── README.md           # This documentation
├── solution.py         # Implementation code
└── tests/              # Test cases
    └── test_solution.py

    

##🚀 Example Usage


python
sol = Solution()
print(sol.kthSmallestProduct([2,5], [3,4], 2))        # Output: 8
print(sol.kthSmallestProduct([-4,-2,0,3], [2,4], 6))  # Output: 0
print(sol.kthSmallestProduct([-2,-1,0,1,2], [-3,-1,2,4,5], 3))  # Output: -6

📅 Date
June 25, 2025

