# Maximum Number of Events That Can Be Attended

## Problem Description

You are given an array of events where `events[i] = [startDayi, endDayi]`. Every event i starts at `startDayi` and ends at `endDayi`.

You can attend an event i at any day d where `startTimei <= d <= endTimei`. You can only attend one event at any time d.

Return the maximum number of events you can attend.

## Examples

### Example 1:
```
Input: events = [[1,2],[2,3],[3,4]]
Output: 3
Explanation: You can attend all the three events.
One way to attend them all is as shown.
Attend the first event on day 1.
Attend the second event on day 2.
Attend the third event on day 3.
```

### Example 2:
```
Input: events = [[1,2],[2,3],[3,4],[1,2]]
Output: 4
```

## Constraints

- `1 <= events.length <= 10^5`
- `events[i].length == 2`
- `1 <= startDayi <= endDayi <= 10^5`

## Solution Approach

This problem can be solved using a **greedy algorithm**. The key insight is to always prioritize events that end earlier, as this leaves maximum flexibility for attending future events.

### Algorithm Steps:

1. **Sort events by end day**: Events that end sooner get higher priority
2. **Greedy selection**: For each event, try to attend it on the earliest available day within its range
3. **Track used days**: Ensure we don't double-book any day

## Implementation

### Basic Solution (O(n²) time complexity)

```python
class Solution:
    def maxEvents(self, events):
        """
        Find maximum number of events that can be attended.
        
        Args:
            events: List of [startDay, endDay] pairs
        
        Returns:
            Maximum number of events that can be attended
        """
        # Sort events by end day (greedy approach)
        events.sort(key=lambda x: x[1])
        
        attended = 0
        used_days = set()
        
        for start, end in events:
            # Try to attend on the earliest available day within the event's range
            for day in range(start, end + 1):
                if day not in used_days:
                    used_days.add(day)
                    attended += 1
                    break
        
        return attended
```

### Optimized Solution (O(n log n) time complexity)

```python
import heapq

class Solution:
    def maxEvents(self, events):
        """
        Optimized solution using priority queue for better performance
        """
        # Sort events by start day
        events.sort()
        
        # Priority queue to store end days of available events
        available_events = []
        
        event_idx = 0
        attended = 0
        day = 1
        
        # Continue until no more events to process
        while event_idx < len(events) or available_events:
            # Add all events that start on current day
            while event_idx < len(events) and events[event_idx][0] <= day:
                heapq.heappush(available_events, events[event_idx][1])
                event_idx += 1
            
            # Remove events that have already ended
            while available_events and available_events[0] < day:
                heapq.heappop(available_events)
            
            # Attend the event that ends earliest (if any available)
            if available_events:
                heapq.heappop(available_events)
                attended += 1
            
            day += 1
        
        return attended
```

## Algorithm Walkthrough

### Example 1: `events = [[1,2],[2,3],[3,4]]`

1. After sorting by end day: `[[1,2],[2,3],[3,4]]` (already sorted)
2. Event [1,2]: Can attend on day 1 → attend on day 1, mark day 1 as used
3. Event [2,3]: Can attend on day 2 (day 1 is used) → attend on day 2, mark day 2 as used  
4. Event [3,4]: Can attend on day 3 (days 1,2 are used) → attend on day 3, mark day 3 as used
5. **Result: 3 events attended**

### Example 2: `events = [[1,2],[2,3],[3,4],[1,2]]`

1. After sorting by end day: `[[1,2],[1,2],[2,3],[3,4]]`
2. First [1,2]: Attend on day 1
3. Second [1,2]: Attend on day 2 (day 1 used)
4. Event [2,3]: Attend on day 3 (days 1,2 used)
5. Event [3,4]: Attend on day 4 (days 1,2,3 used)
6. **Result: 4 events attended**

## Complexity Analysis

### Basic Solution:
- **Time Complexity**: O(n²) in worst case, where n is the number of events
- **Space Complexity**: O(n) for storing used days

### Optimized Solution:
- **Time Complexity**: O(n log n) for sorting and heap operations
- **Space Complexity**: O(n) for the priority queue

## Key Insights

1. **Greedy Strategy**: Always prioritize events that end earlier
2. **Flexibility Preservation**: By attending events that end sooner, we preserve maximum options for future events
3. **Optimal Substructure**: The problem has optimal substructure - making the locally optimal choice leads to a globally optimal solution

## Test Cases

```python
def test_solution():
    solution = Solution()
    
    # Test case 1
    events1 = [[1,2],[2,3],[3,4]]
    assert solution.maxEvents(events1) == 3
    
    # Test case 2
    events2 = [[1,2],[2,3],[3,4],[1,2]]
    assert solution.maxEvents(events2) == 4
    
    # Additional test case
    events3 = [[1,4],[4,4],[2,2],[3,4],[1,1]]
    assert solution.maxEvents(events3) == 4
    
    print("All test cases passed!")

test_solution()
```

## Related Problems

- Activity Selection Problem
- Interval Scheduling Maximization
- Meeting Rooms II

---

**Author**: Harikrishnan120A  
**Date**: 2025-07-07  
**Difficulty**: Medium  
**Topics**: Greedy Algorithm, Priority Queue, Sorting
