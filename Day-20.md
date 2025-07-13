# Maximum Matching of Players With Trainers

**Author:** Harikrishnan120A  
**Date:** 2025-07-13

## Problem Statement

You are given a 0-indexed integer array `players`, where `players[i]` represents the ability of the ith player. You are also given a 0-indexed integer array `trainers`, where `trainers[j]` represents the training capacity of the jth trainer.

The ith player can match with the jth trainer if the player's ability is less than or equal to the trainer's training capacity. Additionally, the ith player can be matched with at most one trainer, and the jth trainer can be matched with at most one player.

Return the maximum number of matchings between players and trainers that satisfy these conditions.

### Examples

**Example 1:**
Input: players = [4,7,9], trainers = [8,2,5,8]
Output: 2
Explanation:
One of the ways we can form two matchings is as follows:

players[0] can be matched with trainers[0] since 4 <= 8.

players[1] can be matched with trainers[3] since 7 <= 8.
It can be proven that 2 is the maximum number of matchings that can be formed.

text

**Example 2:**
Input: players = [1,1,1], trainers = [10]
Output: 1
Explanation:
The trainer can be matched with any of the 3 players.
Each player can only be matched with one trainer, so the maximum answer is 1.

text

### Constraints
- `1 <= players.length, trainers.length <= 10^5`
- `1 <= players[i], trainers[j] <= 10^9`

## Approach
1. **Sort Both Arrays**: Start by sorting both the `players` and `trainers` arrays. This allows us to use a greedy approach to match the smallest available trainer to the smallest player that they can train, ensuring we maximize the number of matches.
2. **Two Pointers Technique**: Use two pointers, one for the `players` array (`i`) and one for the `trainers` array (`j`). Traverse both arrays:
   - If the current player's ability is less than or equal to the current trainer's capacity, increment both pointers (this means a match is found).
   - Otherwise, increment only the trainer pointer to check the next trainer (since the current player cannot be matched with any trainer smaller than the current one, given the arrays are sorted).
3. **Count Matches**: The number of matches found using this approach will be the maximum possible.

## Solution Code

```python
class Solution:
    def matchPlayersAndTrainers(self, players, trainers):
        players.sort()
        trainers.sort()
        i = j = count = 0
        while i < len(players) and j < len(trainers):
            if players[i] <= trainers[j]:
                count += 1
                i += 1
                j += 1
            else:
                j += 1
        return count

# Driver code
if __name__ == "__main__":
    sol = Solution()
    players1 = [4, 7, 9]
    trainers1 = [8, 2, 5, 8]
    print(sol.matchPlayersAndTrainers(players1, trainers1))  # Output: 2

    players2 = [1, 1, 1]
    trainers2 = [10]
    print(sol.matchPlayersAndTrainers(players2, trainers2))  # Output: 1
Explanation
Sorting: By sorting both the players and trainers arrays, we ensure that we can process them in ascending order. This allows us to use a greedy method where we always try to match the smallest available trainer that can handle the current player.

Two Pointers: The pointers i (for players) and j (for trainers) start at the beginning of their respective arrays. For each player, we check if the current trainer can train them. If yes, we move both pointers forward and increment the match count. If not, we move the trainer pointer forward to check the next trainer. This ensures that we do not miss any potential matches and efficiently find the maximum number of matches in O(n log n + m log m) time due to the sorting steps, followed by an O(n + m) traversal, where n and m are the lengths of the players and trainers arrays, respectively.

This approach efficiently maximizes the number of matches by always considering the smallest possible pairings first, leveraging the sorted order to avoid unnecessary checks and ensuring optimal performance.

text
