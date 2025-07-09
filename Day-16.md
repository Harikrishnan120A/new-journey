# Reschedule Meetings for Maximum Free Time

**Difficulty:** Medium  
**Topics:** Array, Sliding Window, Greedy  
**Companies:** Premium Problem

## Problem Description

You are given an integer `eventTime` denoting the duration of an event, where the event occurs from time t = 0 to time t = eventTime.

You are also given two integer arrays `startTime` and `endTime`, each of length n. These represent the start and end time of n non-overlapping meetings, where the ith meeting occurs during the time [startTime[i], endTime[i]].

You can reschedule at most k meetings by moving their start time while maintaining the same duration, to maximize the longest continuous period of free time during the event.

The relative order of all the meetings should stay the same and they should remain non-overlapping.

Return the maximum amount of free time possible after rearranging the meetings.

Note that the meetings can not be rescheduled to a time outside the event.

## Examples

### Example 1:
```
Input: eventTime = 5, k = 1, startTime = [1,3], endTime = [2,5]
Output: 2
Explanation: Reschedule the meeting at [1, 2] to [2, 3], leaving no meetings during the time [0, 2].
```

### Example 2:
```
Input: eventTime = 10, k = 1, startTime = [0,2,9], endTime = [1,4,10]
Output: 6
Explanation: Reschedule the meeting at [2, 4] to [1, 3], leaving no meetings during the time [3, 9].
```

### Example 3:
```
Input: eventTime = 5, k = 2, startTime = [0,1,2,3,4], endTime = [1,2,3,4,5]
Output: 0
Explanation: There is no time during the event not occupied by meetings.
```

## Constraints
- 1 <= eventTime <= 10^9
- n == startTime.length == endTime.length
- 2 <= n <= 10^5
- 1 <= k <= n
- 0 <= startTime[i] < endTime[i] <= eventTime
- endTime[i] <= startTime[i + 1] where i lies in the range [0, n - 2]

## Solution Approach

### Key Insights:
1. **Gap Analysis**: We need to identify gaps between meetings that can be merged
2. **Sliding Window**: When we reschedule k consecutive meetings, we can merge k+1 gaps
3. **Optimization**: Use sliding window technique to avoid recalculating sums

### Algorithm:
1. Calculate all gaps between meetings (including before first and after last meeting)
2. Use sliding window to find the optimal sequence of k+1 consecutive gaps to merge
3. Return the maximum merged gap possible

## Implementation

```python
class Solution:
    def maxFreeTime(self, eventTime, k, startTime, endTime):
        """
        Reschedule at most k meetings to maximize continuous free time.
        Optimized version using sliding window technique.
        
        Time Complexity: O(n)
        Space Complexity: O(n)
        """
        n = len(startTime)
        
        # Calculate gaps between meetings
        gaps = []
        
        # Gap before first meeting
        gaps.append(startTime[0])
        
        # Gaps between consecutive meetings
        for i in range(n - 1):
            gaps.append(startTime[i + 1] - endTime[i])
        
        # Gap after last meeting
        gaps.append(eventTime - endTime[-1])
        
        # If k >= n, we can reschedule all meetings
        if k >= n:
            total_meeting_time = sum(endTime[i] - startTime[i] for i in range(n))
            return eventTime - total_meeting_time
        
        # Use sliding window to find maximum sum of k+1 consecutive gaps
        max_free_time = 0
        
        # Calculate initial window sum (first k+1 gaps)
        window_sum = sum(gaps[:k + 1])
        max_free_time = window_sum
        
        # Slide the window
        for i in range(1, n - k + 1):
            # Remove the leftmost gap and add the new rightmost gap
            window_sum = window_sum - gaps[i - 1] + gaps[i + k]
            max_free_time = max(max_free_time, window_sum)
        
        return max_free_time
```

## Complexity Analysis

- **Time Complexity:** O(n) where n is the number of meetings
  - O(n) to calculate gaps
  - O(n) for sliding window traversal
- **Space Complexity:** O(n) for storing the gaps array

## Test Cases

```python
def test_solution():
    solution = Solution()
    
    # Test Case 1
    assert solution.maxFreeTime(5, 1, [1, 3], [2, 5]) == 2
    
    # Test Case 2
    assert solution.maxFreeTime(10, 1, [0, 2, 9], [1, 4, 10]) == 6
    
    # Test Case 3
    assert solution.maxFreeTime(5, 2, [0, 1, 2, 3, 4], [1, 2, 3, 4, 5]) == 0
    
    print("All tests passed!")

test_solution()
```

## Detailed Explanation

### Gap Calculation:
For meetings at times [start₀, end₀], [start₁, end₁], ..., [startₙ₋₁, endₙ₋₁]:

```
gaps = [
    start₀,                    // gap before first meeting
    start₁ - end₀,            // gap between meeting 0 and 1
    start₂ - end₁,            // gap between meeting 1 and 2
    ...
    startₙ₋₁ - endₙ₋₂,        // gap between meeting n-2 and n-1
    eventTime - endₙ₋₁        // gap after last meeting
]
```

### Sliding Window Optimization:
Instead of recalculating sum for each window:
- Initial window: `sum(gaps[0:k+1])`
- For window starting at i: `previous_sum - gaps[i-1] + gaps[i+k]`

This reduces complexity from O(n×k) to O(n).

### Example Walkthrough (Example 2):
```
eventTime = 10, k = 1
startTime = [0, 2, 9], endTime = [1, 4, 10]

gaps = [0, 1, 5, 0]
       ^  ^  ^  ^
       |  |  |  +-- after last meeting: 10-10 = 0
       |  |  +-- between [4] and [9]: 9-4 = 5
       |  +-- between [1] and [2]: 2-1 = 1
       +-- before first meeting: 0-0 = 0

For k=1, we need windows of size k+1=2:
- Window [0,1]: gaps[0] + gaps[1] = 0 + 1 = 1
- Window [1,2]: gaps[1] + gaps[2] = 1 + 5 = 6  ← Maximum
- Window [2,3]: gaps[2] + gaps[3] = 5 + 0 = 5

Answer: 6
```

## Edge Cases Handled
1. **k ≥ n**: Can reschedule all meetings, return total free time
2. **Single meeting**: Algorithm works correctly
3. **No gaps**: Returns 0 as expected
4. **Large inputs**: Optimized sliding window prevents TLE

---

**Author:** [@Harikrishnan120A](https://github.com/Harikrishnan120A)  
**Date:** July 9, 2025
