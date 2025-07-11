# Meeting Rooms III Solution
**Author:** Harikrishnan120A  
**Date:** 2024-07-11

## Problem Statement
Given `n` rooms and a list of meetings with start and end times, allocate meetings to rooms following specific rules and return the room number that held the most meetings.

## Approach
1. **Sort meetings** by start time
2. Use **min-heaps** to manage:
   - Available rooms (by room number)
   - Occupied rooms (by end time)
3. Process each meeting:
   - Free rooms that have ended
   - Assign to lowest available room
   - Delay if no rooms available
4. Track meeting counts per room
5. Return room with highest count (smallest number if tie)

## Solution Code
```python
import heapq

class Solution:
    def mostBooked(self, n, meetings):
        meetings.sort()
        available = list(range(n))
        heapq.heapify(available)
        occupied = []  # (end_time, room)
        count = [0] * n
        
        for start, end in meetings:
            # Free up ended rooms
            while occupied and occupied[0][0] <= start:
                time, room = heapq.heappop(occupied)
                heapq.heappush(available, room)
            
            if available:
                room = heapq.heappop(available)
                heapq.heappush(occupied, (end, room))
                count[room] += 1
            else:
                # Delay meeting
                time, room = heapq.heappop(occupied)
                new_end = time + (end - start)
                heapq.heappush(occupied, (new_end, room))
                count[room] += 1
        
        max_count = max(count)
        return count.index(max_count)
