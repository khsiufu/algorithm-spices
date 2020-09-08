Top 'K' Numbers (easy)
------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given an unsorted array of numbers, find the ‘K’ largest numbers in it.
   Note: For a detailed discussion about different approaches to solve this problem, take a look at Kth Smallest Number.
   Example 1:
   Input: [3, 1, 5, 12, 2, 11], K = 3
   Output: [5, 12, 11]
   Example 2:
   Input: [5, 12, 11, -1, 12], K = 3
   Output: [12, 11, 12]
   '''

   # mycode
   from heapq import *


   def find_k_largest_numbers(nums, k):
       result = []
       # TODO: Write your code here

       for num in nums:
           if len(result) < k:
               heappush(result, num)
           else:
               if num > result[0]:
                   heappop(result)
                   heappush(result, num)

       return result


   def main():

       print("Here are the top K numbers: " +
             str(find_k_largest_numbers([3, 1, 5, 12, 2, 11], 3)))

       print("Here are the top K numbers: " +
             str(find_k_largest_numbers([5, 12, 11, -1, 12], 3)))


   main()

   # answer
   from heapq import *


   def find_k_largest_numbers(nums, k):
       minHeap = []
       # put first 'K' numbers in the min heap
       for i in range(k):
           heappush(minHeap, nums[i])

       # go through the remaining numbers of the array, if the number from the array is bigger than the
       # top(smallest) number of the min-heap, remove the top number from heap and add the number from array
       for i in range(k, len(nums)):
           if nums[i] > minHeap[0]:
               heappop(minHeap)
               heappush(minHeap, nums[i])

       # the heap has the top 'K' numbers, return them in a list
       return list(minHeap)


   def main():

       print("Here are the top K numbers: " +
             str(find_k_largest_numbers([3, 1, 5, 12, 2, 11], 3)))

       print("Here are the top K numbers: " +
             str(find_k_largest_numbers([5, 12, 11, -1, 12], 3)))


   main()


   '''
   Time complexity
   As discussed above, the time complexity of this algorithm is O(K*logK+(N-K)*logK), which is asymptotically equal to O(N*logK)
   Space complexity
   The space complexity will be O(K) since we need to store the top ‘K’ numbers in the heap.
   '''

Kth Smallest Number (easy)
------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given an unsorted array of numbers, find Kth smallest number in it.
   Please note that it is the Kth smallest number in the sorted order, not the Kth distinct element.
   Note: For a detailed discussion about different approaches to solve this problem, take a look at Kth Smallest Number.
   Example 1:
   Input: [1, 5, 12, 2, 11, 5], K = 3
   Output: 5
   Explanation: The 3rd smallest number is '5', as the first two smaller numbers are [1, 2].
   Example 2:
   Input: [1, 5, 12, 2, 11, 5], K = 4
   Output: 5
   Explanation: The 4th smallest number is '5', as the first three small numbers are [1, 2, 5].
   Example 3:
   Input: [5, 12, 11, -1, 12], K = 3
   Output: 11
   Explanation: The 3rd smallest number is '11', as the first two small numbers are [5, -1].
   '''

   # mycode
   from heapq import *


   def find_Kth_smallest_number(nums, k):
       # TODO: Write your code here
       result = []
       for num in nums:
           heappush(result, num)
       return result[k - 1]


   def main():

       print("Kth smallest number is: " +
             str(find_Kth_smallest_number([1, 5, 12, 2, 11, 5], 3)))

       # since there are two 5s in the input array, our 3rd and 4th smallest numbers should be a '5'
       print("Kth smallest number is: " +
             str(find_Kth_smallest_number([1, 5, 12, 2, 11, 5], 4)))

       print("Kth smallest number is: " +
             str(find_Kth_smallest_number([5, 12, 11, -1, 12], 3)))


   main()

   # answer
   from heapq import *


   def find_Kth_smallest_number(nums, k):
       maxHeap = []
       # put first k numbers in the max heap
       for i in range(k):
           heappush(maxHeap, -nums[i])

       # go through the remaining numbers of the array, if the number from the array is smaller than the
       # top(biggest) number of the heap, remove the top number from heap and add the number from array
       for i in range(k, len(nums)):
           if -nums[i] > maxHeap[0]:
               heappop(maxHeap)
               heappush(maxHeap, -nums[i])

       # the root of the heap has the Kth smallest number
       return -maxHeap[0]


   def main():

       print("Kth smallest number is: " +
             str(find_Kth_smallest_number([1, 5, 12, 2, 11, 5], 3)))

       # since there are two 5s in the input array, our 3rd and 4th smallest numbers should be a '5'
       print("Kth smallest number is: " +
             str(find_Kth_smallest_number([1, 5, 12, 2, 11, 5], 4)))

       print("Kth smallest number is: " +
             str(find_Kth_smallest_number([5, 12, 11, -1, 12], 3)))


   main()


   '''
   Time complexity
   The time complexity of this algorithm is O(K*logK+(N-K)*logK), which is asymptotically equal to O(N*logK)
   Space complexity
   The space complexity will be O(K) because we need to store ‘K’ smallest numbers in the heap.
   An Alternate Approach
   Alternatively, we can use a Min Heap to find the Kth smallest number.
   We can insert all the numbers in the min-heap and then extract the top ‘K’ numbers from the heap to find the Kth smallest number.
   Initializing the min-heap with all numbers will take O(N) and extracting ‘K’ numbers will take O(KlogN).
   Overall, the time complexity of this algorithm will be O(N+KlogN) and the space complexity will be O(N).
   '''

'K' Closest Points to the Origin (easy)
------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given an array of points in the a 2D2D plane, find ‘K’ closest points to the origin.
   Example 1:
   Input: points = [[1,2],[1,3]], K = 1
   Output: [[1,2]]
   Explanation: The Euclidean distance between (1, 2) and the origin is sqrt(5).
   The Euclidean distance between (1, 3) and the origin is sqrt(10).
   Since sqrt(5) < sqrt(10), therefore (1, 2) is closer to the origin.
   Example 2:
   Input: point = [[1, 3], [3, 4], [2, -1]], K = 2
   Output: [[1, 3], [2, -1]]
   '''

   import math
   from heapq import *


   class Point:
       def __init__(self, x, y):
           self.x = x
           self.y = y

       def print_point(self):
           print("[" + str(self.x) + ", " + str(self.y) + "] ", end='')
           print(self.x**2 + self.y**2)

       def __lt__(self, other):

           return (self.x**2 + self.y**2) > (other.x**2 + other.y**2)


   def find_closest_points(points, k):
       result = []
       # TODO: Write your code here
       for point in points:
           if len(result) < k:
               heappush(result, point)
           else:
               if (point.x**2 + point.y**2) < (result[0].x**2 + result[0].y**2):
                   heappop(result)
                   heappush(result, point)

       return result


   def main():

       result = find_closest_points([Point(1, 3), Point(3, 4), Point(2, -1)], 2)
       print("Here are the k points closest the origin: ", end='')
       for point in result:
           point.print_point()


   main()

   # answer
   from __future__ import print_function
   from heapq import *


   class Point:
       def __init__(self, x, y):
           self.x = x
           self.y = y

       # used for max-heap
       def __lt__(self, other):
           return self.distance_from_origin() > other.distance_from_origin()

       def distance_from_origin(self):
           # ignoring sqrt to calculate the distance
           return (self.x * self.x) + (self.y * self.y)

       def print_point(self):
           print("[" + str(self.x) + ", " + str(self.y) + "] ", end='')


   def find_closest_points(points, k):
       maxHeap = []
       # put first 'k' points in the max heap
       for i in range(k):
           heappush(maxHeap, points[i])

       # go through the remaining points of the input array, if a point is closer to the origin than the top point
       # of the max-heap, remove the top point from heap and add the point from the input array
       for i in range(k, len(points)):
           if points[i].distance_from_origin() < maxHeap[0].distance_from_origin():
               heappop(maxHeap)
               heappush(maxHeap, points[i])

       # the heap has 'k' points closest to the origin, return them in a list
       return list(maxHeap)


   def main():

       result = find_closest_points([Point(1, 3), Point(3, 4), Point(2, -1)], 2)
       print("Here are the k points closest the origin: ", end='')
       for point in result:
           point.print_point()


   main()


   '''
   Time complexity
   The time complexity of this algorithm is (N*logK) as we iterating all points and pushing them into the heap.
   Space complexity
   The space complexity will be O(K) because we need to store ‘K’ point in the heap.
   '''

Connect Ropes (easy)
------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given ‘N’ ropes with different lengths, we need to connect these ropes into one big rope with minimum cost.
   The cost of connecting two ropes is equal to the sum of their lengths.
   Example 1:
   Input: [1, 3, 11, 5]
   Output: 33
   Explanation: First connect 1+3(=4), then 4+5(=9), and then 9+11(=20). So the total cost is 33 (4+9+20)
   Example 2:
   Input: [3, 4, 5, 6]
   Output: 36
   Explanation: First connect 3+4(=7), then 5+6(=11), 7+11(=18). Total cost is 36 (7+11+18)
   Example 3:
   Input: [1, 3, 11, 5, 2]
   Output: 42
   Explanation: First connect 1+2(=3), then 3+3(=6), 6+5(=11), 11+11(=22). Total cost is 42 (3+6+11+22)
   '''

   # mycode
   from heapq import *


   def minimum_cost_to_connect_ropes(ropeLengths):
       result = []
       # TODO: Write your code here
       for i in ropeLengths:
           heappush(result, i)

       lenghth = 0
       while len(result) > 1:
           temp = heappop(result) + heappop(result)
           lenghth += temp
           heappush(result, temp)
       return lenghth


   def main():

       print("Minimum cost to connect ropes: " +
             str(minimum_cost_to_connect_ropes([1, 3, 11, 5])))
       print("Minimum cost to connect ropes: " +
             str(minimum_cost_to_connect_ropes([3, 4, 5, 6])))
       print("Minimum cost to connect ropes: " +
             str(minimum_cost_to_connect_ropes([1, 3, 11, 5, 2])))


   main()

   # answer
   from heapq import *


   def minimum_cost_to_connect_ropes(ropeLengths):
       minHeap = []
       # add all ropes to the min heap
       for i in ropeLengths:
           heappush(minHeap, i)

       # go through the values of the heap, in each step take top (lowest) rope lengths from the min heap
       # connect them and push the result back to the min heap.
       # keep doing this until the heap is left with only one rope
       result, temp = 0, 0
       while len(minHeap) > 1:
           temp = heappop(minHeap) + heappop(minHeap)
           result += temp
           heappush(minHeap, temp)

       return result


   def main():

       print("Minimum cost to connect ropes: " +
             str(minimum_cost_to_connect_ropes([1, 3, 11, 5])))
       print("Minimum cost to connect ropes: " +
             str(minimum_cost_to_connect_ropes([3, 4, 5, 6])))
       print("Minimum cost to connect ropes: " +
             str(minimum_cost_to_connect_ropes([1, 3, 11, 5, 2])))


   main()


   '''
   Time complexity
   Given ‘N’ ropes, we need O(N*logN)to insert all the ropes in the heap.
   In each step, while processing the heap, we take out two elements from the heap and insert one.
   This means we will have a total of ‘N’ steps, having a total time complexity of O(N*logN).
   Space complexity #
   The space complexity will be O(N) because we need to store all the ropes in the heap.
   '''

Top 'K' Frequent Numbers (medium)
------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given an unsorted array of numbers, find the top ‘K’ frequently occurring numbers in it.
   Example 1:
   Input: [1, 3, 5, 12, 11, 12, 11], K = 2
   Output: [12, 11]
   Explanation: Both '11' and '12' apeared twice.
   Example 2:
   Input: [5, 12, 11, 3, 11], K = 2
   Output: [11, 5] or [11, 12] or [11, 3]
   Explanation: Only '11' appeared twice, all other numbers appeared once.
   '''

   # mycode
   from heapq import *


   def find_k_frequent_numbers(nums, k):
       topNumbers = []
       result = []
       # TODO: Write your code here
       mapping = {}
       for num in nums:
           if num not in mapping:
               mapping[num] = 1
           else:
               mapping[num] += 1

       for num, freq in mapping.items():
           if len(result) < k:
               heappush(result, (freq, num))
           else:
               if freq > result[0][0]:
                   heappop(result)
                   heappush(result, (freq, num))

       for i in range(len(result) - 1, -1, -1):
           topNumbers.append(result[i][1])
       return topNumbers


   def main():

       print("Here are the K frequent numbers: " +
             str(find_k_frequent_numbers([1, 3, 5, 12, 11, 12, 11], 2)))

       print("Here are the K frequent numbers: " +
             str(find_k_frequent_numbers([5, 12, 11, 3, 11], 2)))


   main()

   # answer
   from heapq import *


   def find_k_frequent_numbers(nums, k):

       # find the frequency of each number
       numFrequencyMap = {}
       for num in nums:
           numFrequencyMap[num] = numFrequencyMap.get(num, 0) + 1

       minHeap = []

       # go through all numbers of the numFrequencyMap and push them in the minHeap, which will have
       # top k frequent numbers. If the heap size is more than k, we remove the smallest(top) number
       for num, frequency in numFrequencyMap.items():
           heappush(minHeap, (frequency, num))
           if len(minHeap) > k:
               heappop(minHeap)

       # create a list of top k numbers
       topNumbers = []
       while minHeap:
           topNumbers.append(heappop(minHeap)[1])

       return topNumbers


   def main():

       print("Here are the K frequent numbers: " +
             str(find_k_frequent_numbers([1, 3, 5, 12, 11, 12, 11], 2)))

       print("Here are the K frequent numbers: " +
             str(find_k_frequent_numbers([5, 12, 11, 3, 11], 2)))


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(N+N*logK).
   Space complexity
   The space complexity will be O(N). Even though we are storing only ‘K’ numbers in the heap.
   For the frequency map, however, we need to store all the ‘N’ numbers.
   '''

Frequency Sort (medium)
------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given a string, sort it based on the decreasing frequency of its characters.
   Example 1:
   Input: "Programming"
   Output: "rrggmmPiano"
   Explanation: 'r', 'g', and 'm' appeared twice, so they need to appear before any other character.
   Example 2:
   Input: "abcbab"
   Output: "bbbaac"
   Explanation: 'b' appeared three times, 'a' appeared twice, and 'c' appeared only once.
   '''

   # mycode
   from heapq import *


   def sort_character_by_frequency(str):
       # TODO: Write your code here
       mapping = {}
       for i in str:
           mapping[i] = mapping.get(i, 0) + 1

       temp = []
       for i, freq in mapping.items():
           heappush(temp, (-freq, i))

       result = ""
       while temp:
           freq, i = heappop(temp)
           result += i * (-freq)
       return result


   def main():

       print("String after sorting characters by frequency: " +
             sort_character_by_frequency("Programming"))
       print("String after sorting characters by frequency: " +
             sort_character_by_frequency("abcbab"))


   main()

   # answer
   from heapq import *


   def sort_character_by_frequency(str):

       # find the frequency of each character
       charFrequencyMap = {}
       for char in str:
           charFrequencyMap[char] = charFrequencyMap.get(char, 0) + 1

       maxHeap = []
       # add all characters to the max heap
       for char, frequency in charFrequencyMap.items():
           heappush(maxHeap, (-frequency, char))

       # build a string, appending the most occurring characters first
       sortedString = []
       while maxHeap:
           frequency, char = heappop(maxHeap)
           for _ in range(-frequency):
               sortedString.append(char)

       return ''.join(sortedString)


   def main():

       print("String after sorting characters by frequency: " +
             sort_character_by_frequency("Programming"))
       print("String after sorting characters by frequency: " +
             sort_character_by_frequency("abcbab"))


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(D*logD) where ‘D’ is the number of distinct characters in the input string.
   This means, in the worst case, when all characters are unique the time complexity of the algorithm will be O(N*logN)
   where ‘N’ is the total number of characters in the string.
   Space complexity
   The space complexity will be O(N), as in the worst case, we need to store all the ‘N’ characters in the HashMap.
   '''

Kth Largest Number in a Stream (medium)
------------------------------------------
.. code:: python

   '''
   Problem Statement
   Design a class to efficiently find the Kth largest element in a stream of numbers.
   The class should have the following two things:
   The constructor of the class should accept an integer array containing initial numbers from the stream and an integer ‘K’.
   The class should expose a function add(int num) which will store the given number and return the Kth largest number.
   Example 1:
   Input: [3, 1, 5, 12, 2, 11], K = 4
   1. Calling add(6) should return '5'.
   2. Calling add(13) should return '6'.
   2. Calling add(4) should still return '6'.
   '''

   # mycode
   from heapq import *


   class KthLargestNumberInStream:
       def __init__(self, nums, k):
           # TODO: Write your code here
           self.k = k
           self.result = []

           for num in nums:
               heappush(self.result, num)
               if len(self.result) > self.k:
                   heappop(self.result)

       def add(self, num):
           # TODO: Write your code here
           heappush(self.result, num)
           if len(self.result) > self.k:
               heappop(self.result)
           return self.result[0]


   def main():

       kthLargestNumber = KthLargestNumberInStream([3, 1, 5, 12, 2, 11], 4)
       print("4th largest number is: " + str(kthLargestNumber.add(6)))
       print("4th largest number is: " + str(kthLargestNumber.add(13)))
       print("4th largest number is: " + str(kthLargestNumber.add(4)))


   main()

   # answer
   from heapq import *


   class KthLargestNumberInStream:
       minHeap = []

       def __init__(self, nums, k):
           self.k = k
           # add the numbers in the min heap
           for num in nums:
               self.add(num)

       def add(self, num):
           # add the new number in the min heap
           heappush(self.minHeap, num)

           # if heap has more than 'k' numbers, remove one number
           if len(self.minHeap) > self.k:
               heappop(self.minHeap)

           # return the 'Kth largest number
           return self.minHeap[0]


   def main():

       kthLargestNumber = KthLargestNumberInStream([3, 1, 5, 12, 2, 11], 4)
       print("4th largest number is: " + str(kthLargestNumber.add(6)))
       print("4th largest number is: " + str(kthLargestNumber.add(13)))
       print("4th largest number is: " + str(kthLargestNumber.add(4)))


   main()


   '''
   Time complexity
   The time complexity of the add() function will be O(logK) since we are inserting the new number in the heap.
   Space complexity
   The space complexity will be O(K) for storing numbers in the heap.
   '''

'K' Closest Numbers (medium)
------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given a sorted number array and two integers ‘K’ and ‘X’, find ‘K’ closest numbers to ‘X’ in the array.
   Return the numbers in the sorted order. ‘X’ is not necessarily present in the array.
   Example 1:
   Input: [5, 6, 7, 8, 9], K = 3, X = 7
   Output: [6, 7, 8]
   Example 2:
   Input: [2, 4, 5, 6, 9], K = 3, X = 6
   Output: [4, 5, 6]
   Example 3:
   Input: [2, 4, 5, 6, 9], K = 3, X = 10
   Output: [5, 6, 9]
   '''

   # mycode
   from heapq import *


   def find_closest_elements(arr, K, X):
       result = []

       # TODO: Write your code here
       temp1, temp2 = [], []
       for i in arr:
           heappush(temp1, (abs(X - i), i))

       i = K
       while i > 0:
           heappush(temp2, heappop(temp1)[1])
           i -= 1

       while temp2:
           result.append(heappop(temp2))
       return result


   def main():
       print("'K' closest numbers to 'X' are: " +
             str(find_closest_elements([5, 6, 7, 8, 9], 3, 7)))
       print("'K' closest numbers to 'X' are: " +
             str(find_closest_elements([2, 4, 5, 6, 9], 3, 6)))
       print("'K' closest numbers to 'X' are: " +
             str(find_closest_elements([2, 4, 5, 6, 9], 3, 10)))


   main()

   # answer
   from heapq import *


   def find_closest_elements(arr, K, X):
       index = binary_search(arr, X)
       low, high = index - K, index + K

       low = max(low, 0)  # 'low' should not be less than zero
       # 'high' should not be greater the size of the array
       high = min(high, len(arr) - 1)

       minHeap = []
       # add all candidate elements to the min heap, sorted by their absolute difference from 'X'
       for i in range(low, high + 1):
           heappush(minHeap, (abs(arr[i] - X), arr[i]))

       # we need the top 'K' elements having smallest difference from 'X'
       result = []
       for _ in range(K):
           result.append(heappop(minHeap)[1])

       result.sort()
       return result


   def binary_search(arr, target):
       low, high = 0, len(arr) - 1
       while low <= high:
           mid = int(low + (high - low) / 2)
           if arr[mid] == target:
               return mid
           if arr[mid] < target:
               low = mid + 1
           else:
               high = mid - 1
       if low > 0:
           return low - 1
       return low


   def main():
       print("'K' closest numbers to 'X' are: " +
             str(find_closest_elements([5, 6, 7, 8, 9], 3, 7)))
       print("'K' closest numbers to 'X' are: " +
             str(find_closest_elements([2, 4, 5, 6, 9], 3, 6)))
       print("'K' closest numbers to 'X' are: " +
             str(find_closest_elements([2, 4, 5, 6, 9], 3, 10)))


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(logN + K*logK).
   We need O(logN) for Binary Search and O(K*logK) to insert the numbers in the Min Heap,
   as well as to sort the output array.
   Space complexity
   The space complexity will be O(K), as we need to put a maximum of 2K2K numbers in the heap.
   '''


   '''
   Alternate Solution using Two Pointers
   After finding the number closest to ‘X’ through Binary Search,
   we can use the Two Pointers approach to find the ‘K’ closest numbers.
   Let’s say the closest number is ‘Y’.
   We can have a left pointer to move back from ‘Y’ and a right pointer to move forward from ‘Y’.
   At any stage, whichever number pointed out by the left or the right pointer gives the smaller difference from ‘X’
   will be added to our result list.
   To keep the resultant list sorted we can use a Queue.
   So whenever we take the number pointed out by the left pointer,
   we will append it at the beginning of the list and whenever we take the number pointed out by the right pointer
   we will append it at the end of the list.
   Here is what our algorithm will look like:
   '''

   from collections import deque


   def find_closest_elements(arr, K, X):
       result = deque()
       index = binary_search(arr, X)
       leftPointer, rightPointer = index, index + 1
       n = len(arr)
       for i in range(K):
           if leftPointer >= 0 and rightPointer < n:
               diff1 = abs(X - arr[leftPointer])
               diff2 = abs(X - arr[rightPointer])
               if diff1 <= diff2:
                   result.appendleft(arr[leftPointer])
                   leftPointer -= 1
               else:
                   result.append(arr[rightPointer])
                   rightPointer += 1
           elif leftPointer >= 0:
               result.appendleft(arr[leftPointer])
               leftPointer -= 1
           elif rightPointer < n:
               result.append(arr[rightPointer])
               rightPointer += 1

       return result


   def binary_search(arr, target):
       low, high = 0, len(arr) - 1
       while low <= high:
           mid = int(low + (high - low) / 2)
           if arr[mid] == target:
               return mid
           if arr[mid] < target:
               low = mid + 1
           else:
               high = mid - 1
       if low > 0:
           return low - 1
       return low


   def main():
       print("'K' closest numbers to 'X' are: " +
             str(find_closest_elements([5, 6, 7, 8, 9], 3, 7)))
       print("'K' closest numbers to 'X' are: " +
             str(find_closest_elements([2, 4, 5, 6, 9], 3, 6)))
       print("'K' closest numbers to 'X' are: " +
             str(find_closest_elements([2, 4, 5, 6, 9], 3, 10)))


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(logN + K).
   We need O(logN) for Binary Search and O(K) for finding the ‘K’ closest numbers using the two pointers.
   Space complexity
   If we ignoring the space required for the output list, the algorithm runs in constant space O(1).
   '''

Maximum Distinct Elements (medium)
------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given an array of numbers and a number ‘K’, we need to remove ‘K’ numbers from the array such that we are left with maximum distinct numbers.
   Example 1:
   Input: [7, 3, 5, 8, 5, 3, 3], and K=2
   Output: 3
   Explanation: We can remove two occurrences of 3 to be left with 3 distinct numbers [7, 3, 8], we have
   to skip 5 because it is not distinct and occurred twice.
   Another solution could be to remove one instance of '5' and '3' each to be left with three
   distinct numbers [7, 5, 8], in this case, we have to skip 3 because it occurred twice.
   Example 2:
   Input: [3, 5, 12, 11, 12], and K=3
   Output: 2
   Explanation: We can remove one occurrence of 12, after which all numbers will become distinct. Then
   we can delete any two numbers which will leave us 2 distinct numbers in the result.
   Example 3:
   Input: [1, 2, 3, 3, 3, 3, 4, 4, 5, 5, 5], and K=2
   Output: 3
   Explanation: We can remove one occurrence of '4' to get three distinct numbers.
   '''

   # mycode
   from heapq import *


   def find_maximum_distinct_elements(nums, k):
       # TODO: Write your code here
       if len(nums) <= k:
           return 0
       mapping = {}
       for num in nums:
           mapping[num] = mapping.get(num, 0) + 1

       count = 0
       heap = []
       for num, freq in mapping.items():
           if freq == 1:
               count += 1
           else:
               heappush(heap, (freq, num))

       while k > 0 and heap:
           freq, num = heappop(heap)
           if freq - 1 == 1:
               count += 1
           else:
               heappush(heap, (freq - 1, num))
           k -= 1
       count -= k

       return count


   def main():

       print("Maximum distinct numbers after removing K numbers: " +
             str(find_maximum_distinct_elements([7, 3, 5, 8, 5, 3, 3], 2)))
       print("Maximum distinct numbers after removing K numbers: " +
             str(find_maximum_distinct_elements([3, 5, 12, 11, 12], 3)))
       print("Maximum distinct numbers after removing K numbers: " + str(
           find_maximum_distinct_elements([1, 2, 3, 3, 3, 3, 4, 4, 5, 5, 5], 2)))


   main()

   # answer
   from heapq import *


   def find_maximum_distinct_elements(nums, k):
       distinctElementsCount = 0
       if len(nums) <= k:
           return distinctElementsCount

       # find the frequency of each number
       numFrequencyMap = {}
       for i in nums:
           numFrequencyMap[i] = numFrequencyMap.get(i, 0) + 1

       minHeap = []
       # insert all numbers with frequency greater than '1' into the min-heap
       for num, frequency in numFrequencyMap.items():
           if frequency == 1:
               distinctElementsCount += 1
           else:
               heappush(minHeap, (frequency, num))

       # following a greedy approach, try removing the least frequent numbers first from the min-heap
       while k > 0 and minHeap:
           frequency, num = heappop(minHeap)
           # to make an element distinct, we need to remove all of its occurrences except one
           k -= frequency - 1
           if k >= 0:
               distinctElementsCount += 1

       # if k > 0, this means we have to remove some distinct numbers
       if k > 0:
           distinctElementsCount -= k

       return distinctElementsCount


   def main():

       print("Maximum distinct numbers after removing K numbers: " +
             str(find_maximum_distinct_elements([7, 3, 5, 8, 5, 3, 3], 2)))
       print("Maximum distinct numbers after removing K numbers: " +
             str(find_maximum_distinct_elements([3, 5, 12, 11, 12], 3)))
       print("Maximum distinct numbers after removing K numbers: " + str(
           find_maximum_distinct_elements([1, 2, 3, 3, 3, 3, 4, 4, 5, 5, 5], 2)))


   main()


   '''
   Time complexity
   Since we will insert all numbers in a HashMap and a Min Heap, this will take O(N*logN) where ‘N’ is the total input numbers.
   While extracting numbers from the heap, in the worst case, we will need to take out ‘K’ numbers.
   This will happen when we have at least ‘K’ numbers with a frequency of two.
   Since the heap can have a maximum of ‘N/2’ numbers, therefore,
   extracting an element from the heap will take O(logN) and extracting ‘K’ numbers will take O(KlogN).
   So overall, the time complexity of our algorithm will be O(N*logN + KlogN).
   We can optimize the above algorithm and only push ‘K’ elements in the heap,
   as in the worst case we will be extracting ‘K’ elements from the heap. This optimization will reduce the overall time complexity to O(N*logK + KlogK).
   Space complexity
   The space complexity will be O(N) as, in the worst case, we need to store all the ‘N’ characters in the HashMap.
   '''

Sum of Elements (medium)
------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given an array, find the sum of all numbers between the K1’th and K2’th smallest elements of that array.
   Example 1:
   Input: [1, 3, 12, 5, 15, 11], and K1=3, K2=6
   Output: 23
   Explanation: The 3rd smallest number is 5 and 6th smallest number 15. The sum of numbers coming
   between 5 and 15 is 23 (11+12).
   Example 2:
   Input: [3, 5, 8, 7], and K1=1, K2=4
   Output: 12
   Explanation: The sum of the numbers between the 1st smallest number (3) and the 4th smallest
   number (8) is 12 (5+7).
   '''

   # mycode
   from heapq import *


   def find_sum_of_elements(nums, k1, k2):
       # TODO: Write your code here
       temp = []
       for num in nums:
           heappush(temp, num)

       k, result = 0, 0
       while temp:
           k += 1
           num = heappop(temp)
           if k > k1 and k < k2:
               result += num

       return result


   def main():

       print("Sum of all numbers between k1 and k2 smallest numbers: " +
             str(find_sum_of_elements([1, 3, 12, 5, 15, 11], 3, 6)))
       print("Sum of all numbers between k1 and k2 smallest numbers: " +
             str(find_sum_of_elements([3, 5, 8, 7], 1, 4)))


   main()

   # answer
   from heapq import *


   def find_sum_of_elements(nums, k1, k2):
       minHeap = []
       # insert all numbers to the min heap
       for num in nums:
           heappush(minHeap, num)

       # remove k1 small numbers from the min heap
       for _ in range(k1):
           heappop(minHeap)

       elementSum = 0
       # sum next k2-k1-1 numbers
       for _ in range(k2 - k1 - 1):
           elementSum += heappop(minHeap)

       return elementSum


   def main():

       print("Sum of all numbers between k1 and k2 smallest numbers: " +
             str(find_sum_of_elements([1, 3, 12, 5, 15, 11], 3, 6)))
       print("Sum of all numbers between k1 and k2 smallest numbers: " +
             str(find_sum_of_elements([3, 5, 8, 7], 1, 4)))


   main()


   '''
   Time complexity
   Since we need to put all the numbers in a min-heap, the time complexity of the above algorithm will be O(N*logN)
   where ‘N’ is the total input numbers.
   Space complexity
   The space complexity will be O(N), as we need to store all the ‘N’ numbers in the heap.
   '''


   '''
   Alternate Solution
   We can iterate the array and use a max-heap to keep track of the top K2 numbers.
   We can, then, add the top K2-K1-1 numbers in the max-heap to find the sum of all numbers
   coming between the K1’th and K2’th smallest numbers. Here is what the algorithm will look like:
   '''

   from heapq import *


   def find_sum_of_elements(nums, k1, k2):
       maxHeap = []
       # keep smallest k2 numbers in the max heap
       for i in range(len(nums)):
           if i < k2 - 1:
               heappush(maxHeap, -nums[i])
           elif nums[i] < -maxHeap[0]:
               heappop(maxHeap
                       )  # as we are interested only in the smallest k2 numbers
               heappush(maxHeap, -nums[i])

       # get the sum of numbers between k1 and k2 indices
       # these numbers will be at the top of the max heap
       elementSum = 0
       for _ in range(k2 - k1 - 1):
           elementSum += -heappop(maxHeap)

       return elementSum


   def main():

       print("Sum of all numbers between k1 and k2 smallest numbers: " +
             str(find_sum_of_elements([1, 3, 12, 5, 15, 11], 3, 6)))
       print("Sum of all numbers between k1 and k2 smallest numbers: " +
             str(find_sum_of_elements([3, 5, 8, 7], 1, 4)))


   main()


   '''
   Time complexity
   Since we need to put only the top K2 numbers in the max-heap at any time,
   the time complexity of the above algorithm will be O(N*logK2).
   Space complexity
   The space complexity will be O(K2), as we need to store the smallest ‘K2’ numbers in the heap.
   '''

Rearrange String (hard)
------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given a string, find if its letters can be rearranged in such a way that no two same characters ome next to each other.
   Example 1:
   Input: "aappp"
   Output: "papap"
   Explanation: In "papap", none of the repeating characters come next to each other.
   Example 2:
   Input: "Programming"
   Output: "rgmrgmPiano" or "gmringmrPoa" or "gmrPagimnor", etc.
   Explanation: None of the repeating characters come next to each other.
   Example 3:
   Input: "aapa"
   Output: ""
   Explanation: In all arrangements of "aapa", atleast two 'a' will come together e.g., "apaa", "paaa".
   '''

   # mycode
   from heapq import *


   def rearrange_string(str):
       # TODO: Write your code here
       mapping = {}
       for i in str:
           mapping[i] = mapping.get(i, 0) + 1

       heap = []
       for i, freq in mapping.items():
           heappush(heap, (-freq, i))

       result = ''
       while heap:
           most_freq, most_i = heappop(heap)
           result += most_i
           if -most_freq > 1:
               heappush(heap, (most_freq + 1, most_i))
           if heap:
               sec_freq, sec_i = heappop(heap)
               if sec_i == most_i:
                   return ''
               else:
                   heappush(heap, (sec_freq, sec_i))
       return result


   def main():
       print("Rearranged string:  " + rearrange_string("aappp"))
       print("Rearranged string:  " + rearrange_string("Programming"))
       print("Rearranged string:  " + rearrange_string("aapa"))


   main()

   # answer
   from heapq import *


   def rearrange_string(str):
       charFrequencyMap = {}
       for char in str:
           charFrequencyMap[char] = charFrequencyMap.get(char, 0) + 1

       maxHeap = []
       # add all characters to the max heap
       for char, frequency in charFrequencyMap.items():
           heappush(maxHeap, (-frequency, char))

       previousChar, previousFrequency = None, 0
       resultString = []
       while maxHeap:
           frequency, char = heappop(maxHeap)
           # add the previous entry back in the heap if its frequency is greater than zero
           if previousChar and -previousFrequency > 0:
               heappush(maxHeap, (previousFrequency, previousChar))
           # append the current character to the result string and decrement its count
           resultString.append(char)
           previousChar = char
           previousFrequency = frequency + 1  # decrement the frequency

       # if we were successful in appending all the characters to the result string, return it
       return ''.join(resultString) if len(resultString) == len(str) else ""


   def main():
       print("Rearranged string:  " + rearrange_string("aappp"))
       print("Rearranged string:  " + rearrange_string("Programming"))
       print("Rearranged string:  " + rearrange_string("aapa"))


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(N*logN) where ‘N’ is the number of characters in the input string.
   Space complexity
   The space complexity will be O(N), as in the worst case, we need to store all the ‘N’ characters in the HashMap.
   '''

Problem Challenge 1 - Rearrange String K Distance Apart (hard)
---------------------------------------------------------------
.. code:: python

   '''
   Problem Challenge 1
   Rearrange String K Distance Apart (hard)
   Given a string and a number ‘K’, find if the string can be rearranged such that the same characters are at least ‘K’ distance apart from each other.
   Example 1:
   Input: "mmpp", K=2
   Output: "mpmp" or "pmpm"
   Explanation: All same characters are 2 distance apart.
   Example 2:
   Input: "Programming", K=3
   Output: "rgmPrgmiano" or "gmringmrPoa" or "gmrPagimnor" and a few more
   Explanation: All same characters are 3 distance apart.
   Example 3:
   Input: "aab", K=2
   Output: "aba"
   Explanation: All same characters are 2 distance apart.
   Example 4:
   Input: "aappa", K=3
   Output: ""
   Explanation: We cannot find an arrangement of the string where any two 'a' are 3 distance apart.
   '''

   from heapq import *
   from collections import deque


   def reorganize_string(str, k):
       # TODO: Write your code here
       mapping = {}

       for i in str:
           mapping[i] = mapping.get(i, 0) + 1

       heap = []
       for i, freq in mapping.items():
           heappush(heap, (-freq, i))

       result = ''
       queue = deque()

       while heap:
           freq, i = heappop(heap)
           result += i
           queue.append((freq + 1, i))

           if len(queue) >= k:
               freq, i = queue.popleft()
               if -freq > 0:
                   heappush(heap, (freq, i))

       return result if len(result) == len(str) else ''


   def main():
       print("Reorganized string: " + reorganize_string("mmpp", 2))
       print("Reorganized string: " + reorganize_string("Programming", 3))
       print("Reorganized string: " + reorganize_string("aab", 2))
       print("Reorganized string: " + reorganize_string("aapa", 3))


   main()

   # answer
   from heapq import *
   from collections import deque


   def reorganize_string(str, k):
       if k <= 1:
           return str

       charFrequencyMap = {}
       for char in str:
           charFrequencyMap[char] = charFrequencyMap.get(char, 0) + 1

       maxHeap = []
       # add all characters to the max heap
       for char, frequency in charFrequencyMap.items():
           heappush(maxHeap, (-frequency, char))

       queue = deque()
       resultString = []
       while maxHeap:
           frequency, char = heappop(maxHeap)
           # append the current character to the result string and decrement its count
           resultString.append(char)
           # decrement the frequency and append to the queue
           queue.append((char, frequency + 1))
           if len(queue) == k:
               char, frequency = queue.popleft()
               if -frequency > 0:
                   heappush(maxHeap, (frequency, char))

       # if we were successful in appending all the characters to the result string, return it
       return ''.join(resultString) if len(resultString) == len(str) else ""


   def main():
       print("Reorganized string: " + reorganize_string("Programming", 3))
       print("Reorganized string: " + reorganize_string("mmpp", 2))
       print("Reorganized string: " + reorganize_string("aab", 2))
       print("Reorganized string: " + reorganize_string("aapa", 3))


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(N*logN) where ‘N’ is the number of characters in the input string.
   Space complexity
   The space complexity will be O(N), as in the worst case, we need to store all the ‘N’ characters in the HashMap.
   '''

Problem Challenge 2 - Scheduling Tasks (hard)
-----------------------------------------------
.. code:: python

   '''
   Problem Challenge 2
   Scheduling Tasks (hard)
   You are given a list of tasks that need to be run, in any order, on a server. Each task will take one CPU interval to execute but once a task has finished, it has a cooling period during which it can’t be run again. If the cooling period for all tasks is ‘K’ intervals, find the minimum number of CPU intervals that the server needs to finish all tasks.
   If at any time the server can’t execute any task then it must stay idle.
   Example 1:
   Input: [a, a, a, b, c, c], K=2
   Output: 7
   Explanation: a -> c -> b -> a -> c -> idle -> a
   Example 2:
   Input: [a, b, a], K=3
   Output: 5
   Explanation: a -> b -> idle -> idle -> a
   '''

   # mycode
   from heapq import *
   from collections import deque


   def schedule_tasks(tasks, k):
       intervalCount = 0
       # TODO: Write your code here
       mapping = {}
       for i in tasks:
           mapping[i] = mapping.get(i, 0) + 1

       heap = []
       for i, freq in mapping.items():
           heappush(heap, (-freq, i))

       queue = deque()
       char = ''
       while heap:
           freq, i = heappop(heap)

           intervalCount += 1
           if i == char:
               print(k - len_queue)
               intervalCount += (k - len_queue)
           queue.append((freq, i))

           if len(queue) > k:
               freq, i = queue.popleft()
               if -freq > 1:
                   char = i
                   heappush(heap, (freq + 1, i))

           if heap == [] and queue != []:
               freq, i = queue.popleft()
               if -freq > 1:
                   char = i
                   heappush(heap, (freq + 1, i))

           len_queue = len(queue)

       return intervalCount


   def main():
       print("Minimum intervals needed to execute all tasks: " +
             str(schedule_tasks(['a', 'a', 'a', 'b', 'c', 'c'], 2)))
       print("Minimum intervals needed to execute all tasks: " +
             str(schedule_tasks(['a', 'b', 'a'], 3)))


   main()

   # answer
   from heapq import *


   def schedule_tasks(tasks, k):
       intervalCount = 0
       taskFrequencyMap = {}
       for char in tasks:
           taskFrequencyMap[char] = taskFrequencyMap.get(char, 0) + 1

       maxHeap = []
       # add all tasks to the max heap
       for char, frequency in taskFrequencyMap.items():
           heappush(maxHeap, (-frequency, char))

       while maxHeap:
           waitList = []
           n = k + 1  # try to execute as many as 'k+1' tasks from the max-heap
           while n > 0 and maxHeap:
               intervalCount += 1
               frequency, char = heappop(maxHeap)
               if -frequency > 1:
                   # decrement the frequency and add to the waitList
                   waitList.append((frequency + 1, char))
               n -= 1

           # put all the waiting list back on the heap
           for frequency, char in waitList:
               heappush(maxHeap, (frequency, char))

           if maxHeap:
               intervalCount += n  # we'll be having 'n' idle intervals for the next iteration

       return intervalCount


   def main():
       print("Minimum intervals needed to execute all tasks: " +
             str(schedule_tasks(['a', 'a', 'a', 'b', 'c', 'c'], 2)))
       print("Minimum intervals needed to execute all tasks: " +
             str(schedule_tasks(['a', 'b', 'a'], 3)))


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(N*logN) where ‘N’ is the number of tasks.
   Our while loop will iterate once for each occurrence of the task in the input (i.e. ‘N’) and
   in each iteration we will remove a task from the heap which will take O(logN) time.
   Hence the overall time complexity of our algorithm is O(N*logN).
   Space complexity
   The space complexity will be O(N), as in the worst case, we need to store all the ‘N’ tasks in the HashMap.
   '''

Problem Challenge 3 - Frequency Stack (hard)
---------------------------------------------
.. code:: python

   '''
   Problem Challenge 3
   Frequency Stack (hard)
   Design a class that simulates a Stack data structure, implementing the following two operations:
   push(int num): Pushes the number ‘num’ on the stack.
   pop(): Returns the most frequent number in the stack. If there is a tie, return the number which was pushed later.
   Example:
   After following push operations: push(1), push(2), push(3), push(2), push(1), push(2), push(5)

   1. pop() should return 2, as it is the most frequent number
   2. Next pop() should return 1
   3. Next pop() should return 2
   '''

   # mycode
   from heapq import *


   class FrequencyStack:
       def __init__(self):
           self.heap = []
           self.mapping = {}

       def push(self, num):
           # TODO: Write your code here
           self.mapping[num] = self.mapping.get(num, 0) + 1
           if num not in self.heap:
               heappush(self.heap, (-self.mapping[num], num))
           else:
               index = self.heap.index(num)
               if index == len(self.heap) - 1:
                   self.heap = self.heap[:index]
               else:
                   self.heap = self.heap[0:index] + self.heap[index + 1:]
               heappush(self.heap, (-mapping[num], num))

       def pop(self):
           freq, i = heappop(self.heap)
           if -freq > 1:
               heappush(self.heap, (-freq + 1, i))
           return i


   def main():
       frequencyStack = FrequencyStack()
       frequencyStack.push(1)
       frequencyStack.push(2)
       frequencyStack.push(3)
       frequencyStack.push(2)
       frequencyStack.push(1)
       frequencyStack.push(2)
       frequencyStack.push(5)
       print(frequencyStack.pop())
       print(frequencyStack.pop())
       print(frequencyStack.pop())


   main()

   # answer
   from heapq import *


   class Element:
       def __init__(self, number, frequency, sequenceNumber):
           self.number = number
           self.frequency = frequency
           self.sequenceNumber = sequenceNumber

       def __lt__(self, other):
           # higher frequency wins
           if self.frequency != other.frequency:
               return self.frequency > other.frequency
           # if both elements have same frequency, return the element that was pushed later
           return self.sequenceNumber > other.sequenceNumber


   class FrequencyStack:
       sequenceNumber = 0
       maxHeap = []
       frequencyMap = {}

       def push(self, num):
           self.frequencyMap[num] = self.frequencyMap.get(num, 0) + 1
           heappush(self.maxHeap,
                    Element(num, self.frequencyMap[num], self.sequenceNumber))
           self.sequenceNumber += 1

       def pop(self):
           num = heappop(self.maxHeap).number
           # decrement the frequency or remove if this is the last number
           if self.frequencyMap[num] > 1:
               self.frequencyMap[num] -= 1
           else:
               del self.frequencyMap[num]

           return num


   def main():
       frequencyStack = FrequencyStack()
       frequencyStack.push(1)
       frequencyStack.push(2)
       frequencyStack.push(3)
       frequencyStack.push(2)
       frequencyStack.push(1)
       frequencyStack.push(2)
       frequencyStack.push(5)
       print(frequencyStack.pop())
       print(frequencyStack.pop())
       print(frequencyStack.pop())


   main()


   '''
   Time complexity
   The time complexity of push() and pop() is O(logN) where ‘N’ is the current number of elements in the heap.
   Space complexity
   We will need O(N) space for the heap and the map, so the overall space complexity of the algorithm is O(N).
   '''
