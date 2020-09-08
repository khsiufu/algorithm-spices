Find the Median of a Number Stream (medium)
--------------------------------------------
.. code:: python

   '''
   Problem Statement
   Design a class to calculate the median of a number stream. The class should have the following two methods:
   insertNum(int num): stores the number in the class
   findMedian(): returns the median of all numbers inserted in the class
   If the count of numbers inserted in the class is even, the median will be the average of the middle two numbers.
   Example 1:
   1. insertNum(3)
   2. insertNum(1)
   3. findMedian() -> output: 2
   4. insertNum(5)
   5. findMedian() -> output: 3
   6. insertNum(4)
   7. findMedian() -> output: 3.5
   '''

   # mycode
   from heapq import *


   class MedianOfAStream:

       minHeap = []
       maxHeap = []

       def insert_num(self, num):
           # TODO: Write your code here
           if not self.minHeap or num <= -self.minHeap[0]:
               heappush(self.minHeap, -num)
           else:
               heappush(self.maxHeap, num)

           if len(self.minHeap) > len(self.maxHeap) + 1:
               heappush(self.maxHeap, -heappop(self.minHeap))
           elif len(self.minHeap) < len(self.maxHeap):
               heappush(self.minHeap, -heappop(self.maxHeap))

       def find_median(self):
           # TODO: Write your code here
           if len(self.maxHeap) == len(self.minHeap):
               return (self.maxHeap[0] - self.minHeap[0]) / 2
           else:
               return -self.minHeap[0]


   def main():
       medianOfAStream = MedianOfAStream()
       medianOfAStream.insert_num(3)
       medianOfAStream.insert_num(1)
       print("The median is: " + str(medianOfAStream.find_median()))
       medianOfAStream.insert_num(5)
       print("The median is: " + str(medianOfAStream.find_median()))
       medianOfAStream.insert_num(4)
       print("The median is: " + str(medianOfAStream.find_median()))


   main()

   # answer
   from heapq import *


   class MedianOfAStream:

       maxHeap = []  # containing first half of numbers
       minHeap = []  # containing second half of numbers

       def insert_num(self, num):
           if not self.maxHeap or -self.maxHeap[0] >= num:
               heappush(self.maxHeap, -num)
           else:
               heappush(self.minHeap, num)

           # either both the heaps will have equal number of elements or max-heap will have one
           # more element than the min-heap
           if len(self.maxHeap) > len(self.minHeap) + 1:
               heappush(self.minHeap, -heappop(self.maxHeap))
           elif len(self.maxHeap) < len(self.minHeap):
               heappush(self.maxHeap, -heappop(self.minHeap))

       def find_median(self):
           if len(self.maxHeap) == len(self.minHeap):
               # we have even number of elements, take the average of middle two elements
               return -self.maxHeap[0] / 2.0 + self.minHeap[0] / 2.0

           # because max-heap will have one more element than the min-heap
           return -self.maxHeap[0] / 1.0


   def main():
       medianOfAStream = MedianOfAStream()
       medianOfAStream.insert_num(3)
       medianOfAStream.insert_num(1)
       print("The median is: " + str(medianOfAStream.find_median()))
       medianOfAStream.insert_num(5)
       print("The median is: " + str(medianOfAStream.find_median()))
       medianOfAStream.insert_num(4)
       print("The median is: " + str(medianOfAStream.find_median()))


   main()


   '''
   Time complexity
   The time complexity of the insertNum() will be O(logN) due to the insertion in the heap.
   The time complexity of the findMedian() will be O(1) as we can find the median from the top elements of the heaps.
   Space complexity
   The space complexity will be O(N) because, as at any time, we will be storing all the numbers.
   '''

Sliding Window Median (hard)
--------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given an array of numbers and a number ‘k’, find the median of all the ‘k’ sized sub-arrays (or windows) of the array.
   Example 1:
   Input: nums=[1, 2, -1, 3, 5], k = 2
   Output: [1.5, 0.5, 1.0, 4.0]
   Explanation: Lets consider all windows of size ‘2’:
   [1, 2, -1, 3, 5] -> median is 1.5
   [1, 2, -1, 3, 5] -> median is 0.5
   [1, 2, -1, 3, 5] -> median is 1.0
   [1, 2, -1, 3, 5] -> median is 4.0
   Example 2:
   Input: nums=[1, 2, -1, 3, 5], k = 3
   Output: [1.0, 2.0, 3.0]
   Explanation: Lets consider all windows of size ‘3’:
   [1, 2, -1, 3, 5] -> median is 1.0
   [1, 2, -1, 3, 5] -> median is 2.0
   [1, 2, -1, 3, 5] -> median is 3.0
   '''

   # mycode
   from heapq import *


   class SlidingWindowMedian:
       def find_sliding_window_median(self, nums, k):
           def rebalance(minHeap, maxHeap):
               if len(maxHeap) > len(minHeap) + 1:
                   heappush(minHeap, -heappop(maxHeap))
               elif len(maxHeap) < len(minHeap):
                   heappush(maxHeap, -heappop(minHeap))

           def remove(value, heap):
               index = heap.index(value)

               if len(heap) == 1:
                   heap = []
               elif index == len(heap) - 1:
                   heap = heap[:len(heap) - 1]
               else:
                   heap = heap[:index] + heap[index + 1:]
               return heap

           result = []
           # TODO: Write your code here
           result = [0.0] * (len(nums) - k + 1)
           minHeap, maxHeap = [], []

           for i in range(len(nums)):
               if not maxHeap or nums[i] <= -maxHeap[0]:
                   heappush(maxHeap, -nums[i])
               else:
                   heappush(minHeap, nums[i])

               rebalance(minHeap, maxHeap)

               # print(minHeap, maxHeap)

               if i - k + 1 >= 0:
                   if len(maxHeap) == len(minHeap):
                       result[i - k + 1] = (minHeap[0] - maxHeap[0]) / 2
                   else:
                       result[i - k + 1] = -maxHeap[0]

                   removeElement = nums[i - k + 1]

                   if removeElement >= minHeap[0]:
                       minHeap = remove(removeElement, minHeap)
                   else:
                       maxHeap = remove(-removeElement, maxHeap)

               rebalance(minHeap, maxHeap)

           return result


   def main():

       slidingWindowMedian = SlidingWindowMedian()
       result = slidingWindowMedian.find_sliding_window_median([1, 2, -1, 3, 5],
                                                               2)
       print("Sliding window medians are: " + str(result))

       slidingWindowMedian = SlidingWindowMedian()
       result = slidingWindowMedian.find_sliding_window_median([1, 2, -1, 3, 5],
                                                               3)
       print("Sliding window medians are: " + str(result))


   main()

   # answer
   from heapq import *
   import heapq


   class SlidingWindowMedian:
       def __init__(self):
           self.maxHeap, self.minHeap = [], []

       def find_sliding_window_median(self, nums, k):
           result = [0.0 for x in range(len(nums) - k + 1)]
           for i in range(0, len(nums)):
               if not self.maxHeap or nums[i] <= -self.maxHeap[0]:
                   heappush(self.maxHeap, -nums[i])
               else:
                   heappush(self.minHeap, nums[i])

               self.rebalance_heaps()

               if i - k + 1 >= 0:  # if we have at least 'k' elements in the sliding window
                   # add the median to the the result array
                   if len(self.maxHeap) == len(self.minHeap):
                       # we have even number of elements, take the average of middle two elements
                       result[i - k + 1] = -self.maxHeap[0] / \
                                           2.0 + self.minHeap[0] / 2.0
                   else:  # because max-heap will have one more element than the min-heap
                       result[i - k + 1] = -self.maxHeap[0] / 1.0

                   # remove the the element going out of the sliding window
                   elementToBeRemoved = nums[i - k + 1]
                   if elementToBeRemoved <= -self.maxHeap[0]:
                       self.remove(self.maxHeap, -elementToBeRemoved)
                   else:
                       self.remove(self.minHeap, elementToBeRemoved)

                   self.rebalance_heaps()

           return result

       # removes an element from the heap keeping the heap property
       def remove(self, heap, element):
           ind = heap.index(element)  # find the element
           # move the element to the end and delete it
           heap[ind] = heap[-1]
           del heap[-1]
           # we can use heapify to readjust the elements but that would be O(N),
           # instead, we will adjust only one element which will O(logN)
           if ind < len(heap):
               heapq._siftup(heap, ind)
               heapq._siftdown(heap, 0, ind)

       def rebalance_heaps(self):
           # either both the heaps will have equal number of elements or max-heap will have
           # one more element than the min-heap
           if len(self.maxHeap) > len(self.minHeap) + 1:
               heappush(self.minHeap, -heappop(self.maxHeap))
           elif len(self.maxHeap) < len(self.minHeap):
               heappush(self.maxHeap, -heappop(self.minHeap))


   def main():

       slidingWindowMedian = SlidingWindowMedian()
       result = slidingWindowMedian.find_sliding_window_median([1, 2, -1, 3, 5],
                                                               2)
       print("Sliding window medians are: " + str(result))

       slidingWindowMedian = SlidingWindowMedian()
       result = slidingWindowMedian.find_sliding_window_median([1, 2, -1, 3, 5],
                                                               3)
       print("Sliding window medians are: " + str(result))


   main()


   '''
   Time complexity
   The time complexity of our algorithm is O(N*K) where ‘N’ is the total number of elements in the input array and ‘K’ is the size of the sliding window.
   This is due to the fact that we are going through all the ‘N’ numbers and, while doing so, we are doing two things:
   1. Inserting/removing numbers from heaps of size ‘K’. This will take O(logK)
   2. Removing the element going out of the sliding window. This will take O(K) as we will be searching this element in an array of size ‘K’ (i.e., a heap).
   Space complexity
   Ignoring the space needed for the output array, the space complexity will be O(K) because, at any time, we will be storing all the numbers within the sliding window.
   '''

Maximize Capital (hard)
--------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given a set of investment projects with their respective profits, we need to find the most profitable projects. We are given an initial capital and are allowed to invest only in a fixed number of projects. Our goal is to choose projects that give us the maximum profit.
   We can start an investment project only when we have the required capital. Once a project is selected, we can assume that its profit has become our capital.
   Example 1:
   Input: Project Capitals=[0,1,2], Project Profits=[1,2,3], Initial Capital=1, Number of Projects=2
   Output: 6
   Explanation:
   With initial capital of ‘1’, we will start the second project which will give us profit of ‘2’. Once we selected our first project, our total capital will become 3 (profit + initial capital).
   With ‘3’ capital, we will select the third project, which will give us ‘3’ profit.
   After the completion of the two projects, our total capital will be 6 (1+2+3).
   Example 2:
   Input: Project Capitals=[0,1,2,3], Project Profits=[1,2,3,5], Initial Capital=0, Number of Projects=3
   Output: 8
   Explanation:
   With ‘0’ capital, we can only select the first project, bringing out capital to 1.
   Next, we will select the second project, which will bring our capital to 3.
   Next, we will select the fourth project, giving us a profit of 5.
   After selecting the three projects, our total capital will be 8 (1+2+5).
   '''

   # mycode
   from heapq import *


   def find_maximum_capital(capital, profits, numberOfProjects, initialCapital):
       # TODO: Write your code here
       capitalList = []
       profitList = []

       for i in range(len(capital)):
           heappush(capitalList, (capital[i], i))

       availableCapital = initialCapital
       for i in range(numberOfProjects):
           while capitalList and capitalList[0][0] <= availableCapital:
               capital, i = heappop(capitalList)
               heappush(profitList, -profits[i])

           if not profitList:
               break

           availableCapital -= heappop(profitList)

       return availableCapital


   def main():

       print("Maximum capital: " +
             str(find_maximum_capital([0, 1, 2], [1, 2, 3], 2, 1)))
       print("Maximum capital: " +
             str(find_maximum_capital([0, 1, 2, 3], [1, 2, 3, 5], 3, 0)))


   main()

   # answer
   from heapq import *


   def find_maximum_capital(capital, profits, numberOfProjects, initialCapital):
       minCapitalHeap = []
       maxProfitHeap = []

       # insert all project capitals to a min-heap
       for i in range(0, len(profits)):
           heappush(minCapitalHeap, (capital[i], i))

       # let's try to find a total of 'numberOfProjects' best projects
       availableCapital = initialCapital
       for _ in range(numberOfProjects):
           # find all projects that can be selected within the available capital and insert them in a max-heap
           while minCapitalHeap and minCapitalHeap[0][0] <= availableCapital:
               capital, i = heappop(minCapitalHeap)
               heappush(maxProfitHeap, (-profits[i], i))

           # terminate if we are not able to find any project that can be completed within the available capital
           if not maxProfitHeap:
               break

           # select the project with the maximum profit
           availableCapital += -heappop(maxProfitHeap)[0]

       return availableCapital


   def main():

       print("Maximum capital: " +
             str(find_maximum_capital([0, 1, 2], [1, 2, 3], 2, 1)))
       print("Maximum capital: " +
             str(find_maximum_capital([0, 1, 2, 3], [1, 2, 3, 5], 3, 0)))


   main()


   '''
   Time complexity
   Since, at the most, all the projects will be pushed to both the heaps once,
   the time complexity of our algorithm is O(NlogN + KlogN),
   where ‘N’ is the total number of projects and ‘K’ is the number of projects we are selecting.
   Space complexity
   The space complexity will be O(N) because we will be storing all the projects in the heaps.
   '''

Problem Challenge 1 - Next Interval (hard)
--------------------------------------------
.. code:: python

   '''
   Problem Challenge 1
   Next Interval (hard)
   Given an array of intervals, find the next interval of each interval. In a list of intervals,
   for an interval ‘i’ its next interval ‘j’ will have the smallest ‘start’ greater than or equal to the ‘end’ of ‘i’.
   Write a function to return an array containing indices of the next interval of each input interval.
   If there is no next interval of a given interval, return -1.
   It is given that none of the intervals have the same start point.
   Example 1:
   Input: Intervals [[2,3], [3,4], [5,6]]
   Output: [1, 2, -1]
   Explanation: The next interval of [2,3] is [3,4] having index ‘1’. Similarly, the next interval of [3,4] is [5,6] having index ‘2’. There is no next interval for [5,6] hence we have ‘-1’.
   Example 2:
   Input: Intervals [[3,4], [1,5], [4,6]]
   Output: [2, -1, -1]
   Explanation: The next interval of [3,4] is [4,6] which has index ‘2’. There is no next interval for [1,5] and [4,6].
   '''

   # mycode
   from heapq import *


   class Interval:
       def __init__(self, start, end):
           self.start = start
           self.end = end


   def find_next_interval(intervals):
       startList = []
       endList = []
       result = [-1] * len(intervals)

       for i in range(len(intervals)):
           heappush(startList, (intervals[i].start, i))
           heappush(endList, (intervals[i].end, i))

       while endList:
           endValue, endIndex = heappop(endList)

           while startList and startList[0][0] < endValue:
               heappop(startList)

           if startList:
               startValue, startIndex = heappop(startList)
               result[endIndex] = startIndex
               heappush(startList, (startValue, startIndex))

       return result


   def main():

       result = find_next_interval(
           [Interval(2, 3), Interval(3, 4),
            Interval(5, 6)])
       print("Next interval indices are: " + str(result))

       result = find_next_interval(
           [Interval(3, 4), Interval(1, 5),
            Interval(4, 6)])
       print("Next interval indices are: " + str(result))


   main()

   # answer
   from heapq import *


   class Interval:
       def __init__(self, start, end):
           self.start = start
           self.end = end


   def find_next_interval(intervals):
       n = len(intervals)

       # heaps for finding the maximum start and end
       maxStartHeap, maxEndHeap = [], []

       result = [0 for x in range(n)]
       for endIndex in range(n):
           heappush(maxStartHeap, (-intervals[endIndex].start, endIndex))
           heappush(maxEndHeap, (-intervals[endIndex].end, endIndex))

       # go through all the intervals to find each interval's next interval
       for _ in range(n):
           # let's find the next interval of the interval which has the highest 'end'
           topEnd, endIndex = heappop(maxEndHeap)
           result[endIndex] = -1  # defaults to - 1
           if -maxStartHeap[0][0] >= -topEnd:
               topStart, startIndex = heappop(maxStartHeap)
               # find the the interval that has the closest 'start'
               while maxStartHeap and -maxStartHeap[0][0] >= -topEnd:
                   topStart, startIndex = heappop(maxStartHeap)
               result[endIndex] = startIndex
               # put the interval back as it could be the next interval of other intervals
               heappush(maxStartHeap, (topStart, startIndex))

       return result


   def main():

       result = find_next_interval(
           [Interval(2, 3), Interval(3, 4),
            Interval(5, 6)])
       print("Next interval indices are: " + str(result))

       result = find_next_interval(
           [Interval(3, 4), Interval(1, 5),
            Interval(4, 6)])
       print("Next interval indices are: " + str(result))


   main()


   '''
   Time complexity
   The time complexity of our algorithm will be O(NlogN), where ‘N’ is the total number of intervals.
   Space complexity
   The space complexity will be O(N) because we will be storing all the intervals in the heaps.
   '''
