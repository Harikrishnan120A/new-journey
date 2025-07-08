# Maximum Number of Events That Can Be Attended II

## Problem Description

You are given an array of events where `events[i] = [startDayi, endDayi, valuei]`. The ith event starts at `startDayi` and ends at `endDayi`, and if you attend this event, you will receive a value of `valuei`. You are also given an integer `k` which represents the maximum number of events you can attend.

You can only attend one event at a time. If you choose to attend an event, you must attend the entire event. Note that the end day is inclusive: that is, you cannot attend two events where one of them starts and the other ends on the same day.

Return the maximum sum of values that you can receive by attending events.

## Examples

### Example 1:
```
Input: events = [[1,2,4],[3,4,3],[2,3,1]], k = 2
Output: 7
Explanation: Choose the green events, 0 and 1 (0-indexed) for a total value of 4 + 3 = 7.
```

### Example 2:
```
Input: events = [[1,2,4],[3,4,3],[2,3,10]], k = 2
Output: 10
Explanation: Choose event 2 for a total value of 10.
Notice that you cannot attend any other event as they overlap, and that you do not have to attend k events.
```

### Example 3:
```
Input: events = [[1,1,1],[2,2,2],[3,3,3],[4,4,4]], k = 3
Output: 9
Explanation: Although the events do not overlap, you can only attend 3 events. Pick the highest valued three.
```

## Constraints

- `1 <= k <= events.length`
- `1 <= k * events.length <= 10^6`
- `1 <= startDayi <= endDayi <= 10^9`
- `1 <= valuei <= 10^6`

## Solution Approach

This problem is solved using **Dynamic Programming with Binary Search**:

1. **Sort events by end time** - Process events in chronological order
2. **Use DP state**: `dp[i][j]` = maximum value using first `i` events and attending at most `j` events
3. **For each event**, choose between:
   - Skip it: `dp[i][j] = dp[i-1][j]`
   - Take it: `dp[i][j] = dp[prev][j-1] + value[i]` where `prev` is the latest non-conflicting event
4. **Use binary search** to efficiently find the latest non-conflicting event

## Implementation

```python
class Solution:
    def maxValue(self, events, k):
        # Sort events by end time
        events.sort(key=lambda x: x[1])
        n = len(events)
        
        # Find the latest event that ends before current event starts
        def findLatestNonConflicting(index):
            left, right = 0, index - 1
            result = -1
            
            while left <= right:
                mid = (left + right) // 2
                if events[mid][1] < events[index][0]:  # No conflict
                    result = mid
                    left = mid + 1
                else:
                    right = mid - 1
            
            return result
        
        # DP: dp[i][j] = max value using first i events with at most j events attended
        dp = [[0] * (k + 1) for _ in range(n + 1)]
        
        for i in range(1, n + 1):
            start, end, value = events[i - 1]
            
            for j in range(1, k + 1):
                # Option 1: Don't take current event
                dp[i][j] = dp[i - 1][j]
                
                # Option 2: Take current event
                prev = findLatestNonConflicting(i - 1)
                if prev == -1:
                    # No previous non-conflicting event
                    dp[i][j] = max(dp[i][j], value)
                else:
                    dp[i][j] = max(dp[i][j], dp[prev + 1][j - 1] + value)
        
        return dp[n][k]

# Test with the examples
def test_examples():
    solution = Solution()
    
    # Example 1
    events1 = [[1,2,4],[3,4,3],[2,3,1]]
    k1 = 2
    print("Example 1:", solution.maxValue(events1, k1))  # Expected: 7
    
    # Example 2
    events2 = [[1,2,4],[3,4,3],[2,3,10]]
    k2 = 2
    print("Example 2:", solution.maxValue(events2, k2))  # Expected: 10
    
    # Example 3
    events3 = [[1,1,1],[2,2,2],[3,3,3],[4,4,4]]
    k3 = 3
    print("Example 3:", solution.maxValue(events3, k3))  # Expected: 9

# Run the tests
if __name__ == "__main__":
    test_examples()
```

## Complexity Analysis

- **Time Complexity**: O(n * k * log n)
  - O(n log n) for sorting
  - O(n * k * log n) for DP with binary search
- **Space Complexity**: O(n * k) for the DP table

## How It Works

1. **Sort by end time**: Ensures we process events optimally
2. **Binary search**: Efficiently finds the latest event that doesn't conflict with the current one
3. **DP transition**: For each event and each count j, we choose the maximum between:
   - Not taking the current event: `dp[i-1][j]`
   - Taking the current event: `dp[latest_non_conflicting][j-1] + current_value`

## Visual Examples

![image1](image1)
*Example 1: Choose events 0 and 1 for maximum value of 7*

![image2](image2)
*Example 2: Choose only event 2 for maximum value of 10*

![image3](image3)
*Example 3: Choose events 1, 2, and 3 for maximum value of 9*

---

**Author**: Harikrishnan120A  
**Date**: 2025-07-08  
**Difficulty**: Hard  
**Topics**: Dynamic Programming, Binary Search, Greedy
