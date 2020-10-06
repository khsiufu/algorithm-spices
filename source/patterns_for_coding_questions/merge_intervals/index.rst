Merge Intervals (medium)
----------------------------------
.. code:: python

   '''
   Example 1:
   Intervals: [[1,4], [2,5], [7,9]]
   Output: [[1,5], [7,9]]
   Explanation: Since the first two intervals [1,4] and [2,5] overlap, we merged them into one [1,5].
   Example 2:
   Intervals: [[6,7], [2,4], [5,9]]
   Output: [[2,4], [5,9]]
   Explanation: Since the intervals [6,7] and [5,9] overlap, we merged them into one [5,9].
   Example 3:
   Intervals: [[1,4], [2,6], [3,5]]
   Output: [[1,6]]
   Explanation: Since all the given intervals overlap, we merged them into one.
   '''

   # mycode
   def merge(intervals):
       if not intervals:
           return []
       # sort
       intervals.sort()
       res = []
       for interval in intervals:
           # 空 or 迭代的数组起点 > 答案最后一个数组尾巴，就进行插入
           if not res or interval[0] > res[-1][1]:
               res.append(interval)
           # 否则，合并尾巴
           else:
               res[-1][1] = max(res[-1][1], interval[1])
       return res


   def main():
       print(merge([[1, 4], [2, 5], [7, 9]]))
       print(merge([[6, 7], [2, 4], [5, 9]]))
       print(merge([[1, 4], [2, 6], [3, 5]]))


   main()

   # answer
   class Interval:
       def __init__(self, start, end):
           self.start = start
           self.end = end

       def print_interval(self):
           print("[" + str(self.start) + ", " + str(self.end) + "]", end='')


   def merge(intervals):
       if len(intervals) < 2:
           return intervals

       # sort the intervals on the start time
       intervals.sort(key=lambda x: x.start)

       mergedIntervals = []
       start = intervals[0].start
       end = intervals[0].end
       for i in range(1, len(intervals)):
           interval = intervals[i]
           if interval.start <= end:  # overlapping intervals, adjust the 'end'
               end = max(interval.end, end)
           else:  # non-overlapping interval, add the previous internval and reset
               mergedIntervals.append(Interval(start, end))
               start = interval.start
               end = interval.end

       # add the last interval
       mergedIntervals.append(Interval(start, end))
       return mergedIntervals


   def main():
       print("Merged intervals: ", end='')
       for i in merge([Interval(1, 4), Interval(2, 5), Interval(7, 9)]):
           i.print_interval()
       print()

       print("Merged intervals: ", end='')
       for i in merge([Interval(6, 7), Interval(2, 4), Interval(5, 9)]):
           i.print_interval()
       print()

       print("Merged intervals: ", end='')
       for i in merge([Interval(1, 4), Interval(2, 6), Interval(3, 5)]):
           i.print_interval()
       print()


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(N * logN), where ‘N’ is the total number of intervals.
   We are iterating the intervals only once which will take O(N), in the beginning though,
   since we need to sort the intervals, our algorithm will take O(N * logN).
   Space complexity
   The space complexity of the above algorithm will be O(N) as we need to return a list containing all the merged intervals.
   We will also need O(N) space for sorting.
   For Java, depending on its version, Collection.sort() either uses Merge sort or Timsort, and both these algorithms need O(N) space.
   Overall, our algorithm has a space complexity of O(N).
   '''

Insert Interval (medium)
----------------------------------
.. code:: python

   '''
   Problem Statement
   Given a list of non-overlapping intervals sorted by their start time, insert a given interval at the correct position and merge all necessary intervals to produce a list that has only mutually exclusive intervals.
   Example 1:
   Input: Intervals=[[1,3], [5,7], [8,12]], New Interval=[4,6]
   Output: [[1,3], [4,7], [8,12]]
   Explanation: After insertion, since [4,6] overlaps with [5,7], we merged them into one [4,7].
   Example 2:
   Input: Intervals=[[1,3], [5,7], [8,12]], New Interval=[4,10]
   Output: [[1,3], [4,12]]
   Explanation: After insertion, since [4,10] overlaps with [5,7] & [8,12], we merged them into [4,12].
   Example 3:
   Input: Intervals=[[2,3],[5,7]], New Interval=[1,4]
   Output: [[1,4], [5,7]]
   Explanation: After insertion, since [1,4] overlaps with [2,3], we merged them into one [1,4].
   '''


   # mycode
   def insert(intervals, new_interval):
       i = 0
       while i < len(intervals) and intervals[i][0] < new_interval[0]:
           i += 1

       intervals.insert(i, new_interval)

       res = []
       for interval in intervals:
           if not res or interval[0] > res[-1][1]:
               res.append(interval)
           else:
               res[-1][1] = max(res[-1][1], interval[1])
       return res


   def main():
       print("Intervals after inserting the new interval: " +
             str(insert([[1, 3], [5, 7], [8, 12]], [4, 6])))
       print("Intervals after inserting the new interval: " +
             str(insert([[1, 3], [5, 7], [8, 12]], [4, 10])))
       print("Intervals after inserting the new interval: " +
             str(insert([[2, 3], [5, 7]], [1, 4])))


   main()


   # answer
   def insert(intervals, new_interval):
       merged = []
       i, start, end = 0, 0, 1

       # skip (and add to output) all intervals that come before the 'new_interval'
       while i < len(intervals) and intervals[i][end] < new_interval[start]:
           merged.append(intervals[i])
           i += 1

       # merge all intervals that overlap with 'new_interval'
       while i < len(intervals) and intervals[i][start] <= new_interval[end]:
           new_interval[start] = min(intervals[i][start], new_interval[start])
           new_interval[end] = max(intervals[i][end], new_interval[end])
           i += 1

       # insert the new_interval
       merged.append(new_interval)

       # add all the remaining intervals to the output
       while i < len(intervals):
           merged.append(intervals[i])
           i += 1
       return merged


   def main():
       print("Intervals after inserting the new interval: " +
             str(insert([[1, 3], [5, 7], [8, 12]], [4, 6])))
       print("Intervals after inserting the new interval: " +
             str(insert([[1, 3], [5, 7], [8, 12]], [4, 10])))
       print("Intervals after inserting the new interval: " +
             str(insert([[2, 3], [5, 7]], [1, 4])))


   main()


   '''
   Time complexity
   As we are iterating through all the intervals only once, the time complexity of the above algorithm is O(N),
   where ‘N’ is the total number of intervals.
   Space complexity
   The space complexity of the above algorithm will be O(N) as we need to return a list containing all the merged intervals.
   '''

Intervals Intersection (medium)
----------------------------------
.. code:: python

   '''
   Problem Statement
   Given two lists of intervals, find the intersection of these two lists. Each list consists of disjoint intervals sorted on their start time.
   Example 1:
   Input: arr1=[[1, 3], [5, 6], [7, 9]], arr2=[[2, 3], [5, 7]]
   Output: [2, 3], [5, 6], [7, 7]
   Explanation: The output list contains the common intervals between the two lists.
   Example 2:
   Input: arr1=[[1, 3], [5, 7], [9, 12]], arr2=[[5, 10]]
   Output: [5, 7], [9, 10]
   Explanation: The output list contains the common intervals between the two lists.
   '''


   # mycode
   def merge(intervals_a, intervals_b):
       i, j = 0, 0
       res = []
       while i < len(intervals_a) and j < len(intervals_b):
           a_start, a_end = intervals_a[i]
           b_start, b_end = intervals_b[j]
           if a_start <= b_end and b_start <= a_end:  # Criss-cross lock
               res.append([max(a_start, b_start), min(a_end, b_end)])  # Squeezing

           if a_end <= b_end:  # Exhausted this range in A
               i += 1  # Point to next range in A
           else:  # Exhausted this range in B
               j += 1  # Point to next range in B
       return res


   def main():
       print("Intervals Intersection: " +
             str(merge([[1, 3], [5, 6], [7, 9]], [[2, 3], [5, 7]])))
       print("Intervals Intersection: " +
             str(merge([[1, 3], [5, 7], [9, 12]], [[5, 10]])))


   main()


   # answer
   def merge(intervals_a, intervals_b):
       result = []
       i, j, start, end = 0, 0, 0, 1

       while i < len(intervals_a) and j < len(intervals_b):
           # check if intervals overlap and intervals_a[i]'s start time lies within the other intervals_b[j]
           a_overlaps_b = intervals_a[i][start] >= intervals_b[j][start] and \
                          intervals_a[i][start] <= intervals_b[j][end]

           # check if intervals overlap and intervals_a[j]'s start time lies within the other intervals_b[i]
           b_overlaps_a = intervals_b[j][start] >= intervals_a[i][start] and \
                          intervals_b[j][start] <= intervals_a[i][end]

           # store the the intersection part
           if (a_overlaps_b or b_overlaps_a):
               result.append([
                   max(intervals_a[i][start], intervals_b[j][start]),
                   min(intervals_a[i][end], intervals_b[j][end])
               ])

           # move next from the interval which is finishing first
           if intervals_a[i][end] < intervals_b[j][end]:
               i += 1
           else:
               j += 1

       return result


   def main():
       print("Intervals Intersection: " +
             str(merge([[1, 3], [5, 6], [7, 9]], [[2, 3], [5, 7]])))
       print("Intervals Intersection: " +
             str(merge([[1, 3], [5, 7], [9, 12]], [[5, 10]])))


   main()


   '''
   Time complexity
   As we are iterating through both the lists once, the time complexity of the above algorithm is O(N + M),
   where ‘N’ and ‘M’ are the total number of intervals in the input arrays respectively.
   Space complexity
   Ignoring the space needed for the result list, the algorithm runs in constant space O(1).
   '''

Conflicting Appointments (medium)
----------------------------------
.. code:: python

   '''
   Problem Statement
   Given an array of intervals representing ‘N’ appointments, find out if a person can attend all the appointments.

   Example 1:

   Appointments: [[1,4], [2,5], [7,9]]
   Output: false
   Explanation: Since [1,4] and [2,5] overlap, a person cannot attend both of these appointments.

   Example 2:

   Appointments: [[6,7], [2,4], [8,12]]
   Output: true
   Explanation: None of the appointments overlap, therefore a person can attend all of them.

   Example 3:

   Appointments: [[4,5], [2,3], [3,6]]
   Output: false
   Explanation: Since [4,5] and [3,6] overlap, a person cannot attend both of these appointments.
   '''


   # mycode
   def can_attend_all_appointments(intervals):
       intervals.sort(key=lambda x: x[0])
       for i in range(1, len(intervals)):
           if intervals[i][0] < intervals[i - 1][1]:
               return False
       return True


   def main():
       print("Can attend all appointments: " +
             str(can_attend_all_appointments([[1, 4], [2, 5], [7, 9]])))
       print("Can attend all appointments: " +
             str(can_attend_all_appointments([[6, 7], [2, 4], [8, 12]])))
       print("Can attend all appointments: " +
             str(can_attend_all_appointments([[4, 5], [2, 3], [3, 6]])))


   main()


   # answer
   def can_attend_all_appointments(intervals):
       intervals.sort(key=lambda x: x[0])
       start, end = 0, 1
       for i in range(1, len(intervals)):
           if intervals[i][start] < intervals[i - 1][end]:
               # please note the comparison above, it is "<" and not "<="
               # while merging we needed "<=" comparison, as we will be merging the two
               # intervals having condition "intervals[i][start] == intervals[i - 1][end]" but
               # such intervals don't represent conflicting appointments as one starts right
               # after the other
               return False
       return True


   def main():
       print("Can attend all appointments: " +
             str(can_attend_all_appointments([[1, 4], [2, 5], [7, 9]])))
       print("Can attend all appointments: " +
             str(can_attend_all_appointments([[6, 7], [2, 4], [8, 12]])))
       print("Can attend all appointments: " +
             str(can_attend_all_appointments([[4, 5], [2, 3], [3, 6]])))


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(N*logN), where ‘N’ is the total number of appointments.
   Though we are iterating the intervals only once, our algorithm will take O(N * logN) since we need to sort them in the beginning.
   Space complexity
   The space complexity of the above algorithm will be O(N), which we need for sorting.
   For Python, Arrays.sort() uses Timsort, which needs O(N) space.
   '''

Problem Challenge 1 - Minimum Meeting Rooms (hard)
---------------------------------------------------
.. code:: python

   '''
   Solution Review: Problem Challenge 1 - Minimum Meeting Rooms (hard)
   Given a list of intervals representing the start and end time of ‘N’ meetings,
   find the minimum number of rooms required to hold all the meetings.
   Example 1:
   Meetings: [[1,4], [2,5], [7,9]]

   Output: 2
   Explanation: Since [1,4] and [2,5] overlap, we need two rooms to hold these two meetings. [7,9] can
   occur in any of the two rooms later.

   Example 2:
   Meetings: [[6,7], [2,4], [8,12]]

   Output: 1
   Explanation: None of the meetings overlap, therefore we only need one room to hold all meetings.

   Example 3:
   Meetings: [[1,4], [2,3], [3,6]]

   Output:2
   Explanation: Since [1,4] overlaps with the other two meetings [2,3] and [3,6], we need two rooms to
   hold all the meetings.

   Example 4:
   Meetings: [[4,5], [2,3], [2,4], [3,5]]

   Output: 2
   Explanation: We will need one room for [2,3] and [3,5], and another room for [2,4] and [4,5].
   Here is a visual representation of Example 4:
   '''

   # mycode
   from heapq import *


   class Meeting:
       def __init__(self, start, end):
           self.start = start
           self.end = end

       def __lt__(self, other):
           return self.end < other.end


   def min_meeting_rooms(meetings):
       meetings.sort(key=lambda x: x.start)
       conflict = []
       min_rooms = 0
       for meeting in meetings:
           while len(conflict) > 0 and meeting.start >= conflict[0].end:
               heappop(conflict)
           heappush(conflict, meeting)
           min_rooms = max(len(conflict), min_rooms)
       return min_rooms


   def main():
       print("Minimum meeting rooms required: " + str(
           min_meeting_rooms(
               [Meeting(4, 5),
                Meeting(2, 3),
                Meeting(2, 4),
                Meeting(3, 5)])))
       print(
           "Minimum meeting rooms required: " +
           str(min_meeting_rooms([Meeting(
               1, 4), Meeting(2, 5), Meeting(7, 9)])))
       print(
           "Minimum meeting rooms required: " +
           str(min_meeting_rooms([Meeting(
               6, 7), Meeting(2, 4), Meeting(8, 12)])))
       print(
           "Minimum meeting rooms required: " +
           str(min_meeting_rooms([Meeting(
               1, 4), Meeting(2, 3), Meeting(3, 6)])))
       print("Minimum meeting rooms required: " + str(
           min_meeting_rooms(
               [Meeting(4, 5),
                Meeting(2, 3),
                Meeting(2, 4),
                Meeting(3, 5)])))


   main()

   #answer
   from heapq import *


   class Meeting:
       def __init__(self, start, end):
           self.start = start
           self.end = end

       def __lt__(self, other):
           # min heap based on meeting.end
           return self.end < other.end


   def min_meeting_rooms(meetings):
       # sort the meetings by start time
       meetings.sort(key=lambda x: x.start)

       minRooms = 0
       minHeap = []
       for meeting in meetings:
           # remove all the meetings that have ended
           while (len(minHeap) > 0 and meeting.start >= minHeap[0].end):
               heappop(minHeap)
           # add the current meeting into min_heap
           heappush(minHeap, meeting)
           # all active meetings are in the min_heap, so we need rooms for all of them.
           minRooms = max(minRooms, len(minHeap))
       return minRooms


   def main():
       print("Minimum meeting rooms required: " + str(
           min_meeting_rooms(
               [Meeting(4, 5),
                Meeting(2, 3),
                Meeting(2, 4),
                Meeting(3, 5)])))
       print(
           "Minimum meeting rooms required: " +
           str(min_meeting_rooms([Meeting(
               1, 4), Meeting(2, 5), Meeting(7, 9)])))
       print(
           "Minimum meeting rooms required: " +
           str(min_meeting_rooms([Meeting(
               6, 7), Meeting(2, 4), Meeting(8, 12)])))
       print(
           "Minimum meeting rooms required: " +
           str(min_meeting_rooms([Meeting(
               1, 4), Meeting(2, 3), Meeting(3, 6)])))
       print("Minimum meeting rooms required: " + str(
           min_meeting_rooms(
               [Meeting(4, 5),
                Meeting(2, 3),
                Meeting(2, 4),
                Meeting(3, 5)])))


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(N*logN), where ‘N’ is the total number of meetings. T
   his is due to the sorting that we did in the beginning.
   Also, while iterating the meetings we might need to poll/offer meeting to the priority queue.
   Each of these operations can take O(logN).
   Overall our algorithm will take O(NlogN).
   Space complexity
   The space complexity of the above algorithm will be O(N) which is required for sorting.
   Also, in the worst case scenario, we’ll have to insert all the meetings into the Min Heap (when all meetings overlap) which will also take O(N) space.
   The overall space complexity of our algorithm is O(N).
   '''

Problem Challenge 2 - Maximum CPU Load (hard)
----------------------------------------------
.. code:: python

   '''
   Problem Challenge 2
   Maximum CPU Load (hard)
   We are given a list of Jobs. Each job has a Start time, an End time, and a CPU load when it is running.
   Our goal is to find the maximum CPU load at any time if all the jobs are running on the same machine.
   Example 1:
   Jobs: [[1,4,3], [2,5,4], [7,9,6]]
   Output: 7
   Explanation: Since [1,4,3] and [2,5,4] overlap, their maximum CPU load (3+4=7) will be when both the
   jobs are running at the same time i.e., during the time interval (2,4).
   Example 2:
   Jobs: [[6,7,10], [2,4,11], [8,12,15]]
   Output: 15
   Explanation: None of the jobs overlap, therefore we will take the maximum load of any job which is 15.
   Example 3:
   Jobs: [[1,4,2], [2,4,1], [3,6,5]]
   Output: 8
   Explanation: Maximum CPU load will be 8 as all jobs overlap during the time interval [3,4].
   '''

   # mycode
   from heapq import *


   class job:
       def __init__(self, start, end, cpu_load):
           self.start = start
           self.end = end
           self.cpu_load = cpu_load

       def __lt__(self, other):
           self.end < other.end


   def find_max_cpu_load(jobs):
       jobs.sort(key=lambda x: x.start)

       sum_cpu_load, temp = 0, 0
       conflict = []

       for job in jobs:

           while len(conflict) > 0 and job.start >= conflict[0].end:
               temp -= conflict[0].cpu_load
               heappop(conflict)
           heappush(conflict, job)
           temp += job.cpu_load
           sum_cpu_load = max(sum_cpu_load, temp)

       return sum_cpu_load


   def main():
       print("Maximum CPU load at any time: " +
             str(find_max_cpu_load([job(
                 1, 4, 3), job(2, 5, 4), job(7, 9, 6)])))
       print("Maximum CPU load at any time: " +
             str(find_max_cpu_load([job(6, 7, 10),
                                    job(2, 4, 11),
                                    job(8, 12, 15)])))
       print("Maximum CPU load at any time: " +
             str(find_max_cpu_load([job(
                 1, 4, 2), job(2, 4, 1), job(3, 6, 5)])))


   main()

   # answer
   from heapq import *


   class job:
       def __init__(self, start, end, cpu_load):
           self.start = start
           self.end = end
           self.cpu_load = cpu_load

       def __lt__(self, other):
           # min heap based on job.end
           return self.end < other.end


   def find_max_cpu_load(jobs):
       # sort the jobs by start time
       jobs.sort(key=lambda x: x.start)
       max_cpu_load, current_cpu_load = 0, 0
       min_heap = []

       for j in jobs:
           # remove all the jobs that have ended
           while (len(min_heap) > 0 and j.start >= min_heap[0].end):
               current_cpu_load -= min_heap[0].cpu_load
               heappop(min_heap)
           # add the current job into min_heap
           heappush(min_heap, j)
           current_cpu_load += j.cpu_load
           max_cpu_load = max(max_cpu_load, current_cpu_load)
       return max_cpu_load


   def main():
       print("Maximum CPU load at any time: " +
             str(find_max_cpu_load([job(
                 1, 4, 3), job(2, 5, 4), job(7, 9, 6)])))
       print("Maximum CPU load at any time: " +
             str(find_max_cpu_load([job(6, 7, 10),
                                    job(2, 4, 11),
                                    job(8, 12, 15)])))
       print("Maximum CPU load at any time: " +
             str(find_max_cpu_load([job(
                 1, 4, 2), job(2, 4, 1), job(3, 6, 5)])))


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(N*logN), where ‘N’ is the total number of jobs.
   This is due to the sorting that we did in the beginning.
   Also, while iterating the jobs, we might need to poll/offer jobs to the priority queue.
   Each of these operations can take O(logN). Overall our algorithm will take O(NlogN).
   Space complexity
   The space complexity of the above algorithm will be O(N), which is required for sorting.
   Also, in the worst case, we have to insert all the jobs into the priority queue (when all jobs overlap) which will also take O(N) space.
   The overall space complexity of our algorithm is O(N).
   '''

Problem Challenge 3 - Employee Free Time (hard)
-------------------------------------------------
.. code:: python

   '''
   Problem Challenge 3
   Employee Free Time (hard)
   For ‘K’ employees, we are given a list of intervals representing the working hours of each employee.
   Our goal is to find out if there is a free interval that is common to all employees.
   You can assume that each list of employee working hours is sorted on the start time.
   Example 1:
   Input: Employee Working Hours=[[[1,3], [5,6]], [[2,3], [6,8]]]
   Output: [3,5]
   Explanation: Both the employess are free between [3,5].
   Example 2:
   Input: Employee Working Hours=[[[1,3], [9,12]], [[2,4]], [[6,8]]]
   Output: [4,6], [8,9]
   Explanation: All employess are free between [4,6] and [8,9].
   Example 3:
   Input: Employee Working Hours=[[[1,3]], [[2,4]], [[3,5], [7,9]]]
   Output: [5,7]
   Explanation: All employess are free between [5,7].
   '''

   # mycode
   def find_employee_free_time(schedule):
       temp, res = [], []

       for intervals in schedule:
           for i in intervals:
               temp.append(i)

       temp.sort(key=lambda x: x[0])

       for i in range(1, len(temp)):
           if temp[i][0] > temp[i - 1][1]:
               res.append([temp[i - 1][1], temp[i][0]])
       return res


   def main():
       print(find_employee_free_time([[[1, 3], [5, 6]], [[2, 3], [6, 8]]]))
       print(find_employee_free_time([[[1, 3], [9, 12]], [[2, 4], [6, 8]]]))
       print(find_employee_free_time([[[1, 3], [2, 4]], [[3, 5], [7, 9]]]))


   main()

   # answer
   from __future__ import print_function
   from heapq import *


   class Interval:
       def __init__(self, start, end):
           self.start = start
           self.end = end

       def print_interval(self):
           print("[" + str(self.start) + ", " + str(self.end) + "]", end='')


   class EmployeeInterval:
       def __init__(self, interval, employeeIndex, intervalIndex):
           self.interval = interval  # interval representing employee's working hours
           # index of the list containing working hours of this employee
           self.employeeIndex = employeeIndex
           self.intervalIndex = intervalIndex  # index of the interval in the employee list

       def __lt__(self, other):
           # min heap based on meeting.end
           return self.interval.start < other.interval.start


   def find_employee_free_time(schedule):
       if schedule is None:
           return []

       n = len(schedule)
       result, minHeap = [], []

       # insert the first interval of each employee to the queue
       for i in range(n):
           heappush(minHeap, EmployeeInterval(schedule[i][0], i, 0))

       previousInterval = minHeap[0].interval
       while minHeap:
           queueTop = heappop(minHeap)
           # if previousInterval is not overlapping with the next interval, insert a free interval
           if previousInterval.end < queueTop.interval.start:
               result.append(
                   Interval(previousInterval.end, queueTop.interval.start))
               previousInterval = queueTop.interval
           else:  # overlapping intervals, update the previousInterval if needed
               if previousInterval.end < queueTop.interval.end:
                   previousInterval = queueTop.interval

           # if there are more intervals available for the same employee, add their next interval
           employeeSchedule = schedule[queueTop.employeeIndex]
           if len(employeeSchedule) > queueTop.intervalIndex + 1:
               heappush(
                   minHeap,
                   EmployeeInterval(employeeSchedule[queueTop.intervalIndex + 1],
                                    queueTop.employeeIndex,
                                    queueTop.intervalIndex + 1))

       return result


   def main():

       input = [[Interval(1, 3), Interval(5, 6)],
                [Interval(2, 3), Interval(6, 8)]]
       print("Free intervals: ", end='')
       for interval in find_employee_free_time(input):
           interval.print_interval()
       print()

       input = [[Interval(1, 3), Interval(9, 12)], [Interval(2, 4)],
                [Interval(6, 8)]]
       print("Free intervals: ", end='')
       for interval in find_employee_free_time(input):
           interval.print_interval()
       print()

       input = [[Interval(1, 3)], [Interval(2, 4)],
                [Interval(3, 5), Interval(7, 9)]]
       print("Free intervals: ", end='')
       for interval in find_employee_free_time(input):
           interval.print_interval()
       print()


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(N*logK), where ‘N’ is the total number of intervals and ‘K’ is the total number of employees.
   This is due to the fact that we are iterating through the intervals only once (which will take O(N),
   and every time we process an interval, we remove (and can insert) one interval in the Min Heap, (which will take O(logK)O(logK)).
   At any time the heap will not have more than ‘K’ elements.
   Space complexity
   The space complexity of the above algorithm will be O(K) as at any time the heap will not have more than ‘K’ elements.
   '''
