
# Number of Equivalent Domino Pairs


Leetcode Problem

**Difficulty:** Easy

**Date:** 2025-07-16

**Author:** Harikrishnan120A

**Topics:** Hashing, Array


## 🧩 Problem Description
Given a list of dominoes, dominoes[i] = [a, b], two dominoes are considered equivalent if either:

a == c and b == d, or

a == d and b == c

That is, one domino can be rotated to be equal to another.

Return the number of pairs (i, j) for which 0 <= i < j < dominoes.length and dominoes[i] is equivalent to dominoes[j].

## 🔍 Example
Example 1
text
Copy
Edit
Input:  dominoes = [[1,2],[2,1],[3,4],[5,6]]
Output: 1
Explanation: [1,2] and [2,1] are equivalent.
Example 2
text
Copy
Edit
Input:  dominoes = [[1,2],[1,2],[1,1],[1,2],[2,2]]
Output: 3
Explanation:
There are 3 pairs of [1,2] dominoes:
- (0,1), (0,3), (1,3)
🧠 Approach
To determine equivalency between two dominoes [a, b] and [c, d], they are considered the same if {a, b} == {c, d} (as sets), but since the order of elements in sets doesn't matter and we want a fixed format for hashing, we sort each domino such that we always store (min(a,b), max(a,b)).

## Steps:
Use a dictionary (defaultdict) to count the frequency of each normalized domino (using sorted tuple (min(a,b), max(a,b))).

For each domino form seen f times, the number of equivalent pairs is f * (f - 1) // 2 (combinatorics: choosing 2 out of f).


## ✅ Python Code


~~~python


from collections import defaultdict

class Solution:
    def numEquivDominoPairs(self, dominoes):
        count = defaultdict(int)
        res = 0
        for a, b in dominoes:
            key = tuple(sorted((a, b)))  # normalize
            res += count[key]
            count[key] += 1
        return res


~~~


## ⏱️ Time & Space Complexity
Time Complexity: O(n), where n is the number of dominoes

Space Complexity: O(n), for the hash map storing domino pair counts

## 📌 Constraints
1 <= dominoes.length <= 40,000

Each domino has exactly two integers: dominoes[i].length == 2

1 <= dominoes[i][j] <= 9

## 🔁 Related Topics

Hash

Table

Combinatorics

Arrays
