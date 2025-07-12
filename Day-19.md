# 🏆 The Earliest and Latest Rounds Where Players Compete

**Author:** Harikrishnan.A  
**Date:** 📅 2025-07-12  
**Repository:** [Harikrishnan120A](https://github.com/Harikrishnan120A)

---

## 📘 Problem Description

There is a tournament where `n` players are participating. The players stand in a row and are numbered from `1` to `n`. In every round:

- The **1st player** plays against the **last player**
- The **2nd** plays against the **second-last**, and so on.
- If there’s an **odd** number of players, the **middle player** automatically advances.

After each round:
- The **winners are reordered** based on their **original player numbers** (ascending order).

There are two special players:
- `firstPlayer` and `secondPlayer`  
- They are unbeatable: they always **win** until they face each other.

Your task is to return:
- The **earliest** and **latest** round in which `firstPlayer` and `secondPlayer` can compete.

---

## 🔒 Constraints

- `2 <= n <= 28`
- `1 <= firstPlayer < secondPlayer <= n`

---

## 🧠 Approach

1. Simulate the tournament using recursion with memoization.
2. Use a DFS (depth-first search) to try all possible outcomes of matches **not involving** the unbeatable players.
3. When the unbeatable players face each other, we record the **round number**.
4. Keep track of both:
   - The **earliest** round they can meet (best-case)
   - The **latest** round they can meet (worst-case)

We use a `memo` dictionary to avoid recalculating for the same group of players.

---

## 🔍 Example 

**sol = Solution()
**print(sol.earliestAndLatest(11, 2, 4))  # Output: [3, 4]
**print(sol.earliestAndLatest(5, 1, 5))   # Output: [1, 1]


~~~python

class Solution:
    def earliestAndLatest(self, n, firstPlayer, secondPlayer):
        def dfs(players_tuple, round_num):
            players = list(players_tuple)
            i, j = 0, len(players) - 1

            while i < j:
                if (players[i], players[j]) == (firstPlayer, secondPlayer) or (players[i], players[j]) == (secondPlayer, firstPlayer):
                    return round_num, round_num
                i += 1
                j -= 1

            res = [float('inf'), float('-inf')]

            def backtrack(i, j, nxt):
                if i >= j:
                    if i == j:
                        nxt.append(players[i])
                    nxt_sorted = tuple(sorted(nxt))
                    if nxt_sorted in memo:
                        a, b = memo[nxt_sorted]
                    else:
                        a, b = dfs(nxt_sorted, round_num + 1)
                        memo[nxt_sorted] = (a, b)
                    res[0] = min(res[0], a)
                    res[1] = max(res[1], b)
                    return

                a, b = players[i], players[j]
                if a in (firstPlayer, secondPlayer) or b in (firstPlayer, secondPlayer):
                    winner = a if a in (firstPlayer, secondPlayer) else b
                    backtrack(i + 1, j - 1, nxt + [winner])
                else:
                    backtrack(i + 1, j - 1, nxt + [a])
                    backtrack(i + 1, j - 1, nxt + [b])

            backtrack(0, len(players) - 1, [])
            return res

        memo = {}
        return list(dfs(tuple(range(1, n + 1)), 1))

~~~


