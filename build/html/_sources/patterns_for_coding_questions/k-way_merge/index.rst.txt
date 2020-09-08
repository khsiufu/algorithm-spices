Merge K Sorted Lists (medium)
-----------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given an array of ‘K’ sorted LinkedLists, merge them into one sorted list.
   Example 1:
   Input: L1=[2, 6, 8], L2=[3, 6, 7], L3=[1, 3, 4]
   Output: [1, 2, 3, 3, 4, 6, 6, 7, 8]
   Example 2:
   Input: L1=[5, 8, 9], L2=[1, 7]
   Output: [1, 5, 7, 8, 9]
   '''

   # mycode
   from __future__ import print_function
   from heapq import *


   class ListNode:
       def __init__(self, value):
           self.value = value
           self.next = None

       def __lt__(self, other):
           return self.value < other.value


   def merge_lists(lists):
       # TODO: Write your code here
       heap = []
       for root in lists:
           if root is not None:
               heappush(heap, root)

       head, tail = None, None
       while heap:
           node = heappop(heap)
           if head is None:
               head, tail = node, node
           else:
               tail.next = node
               tail = tail.next
           if node.next is not None:
               heappush(heap, node.next)
       return head


   def main():
       l1 = ListNode(2)
       l1.next = ListNode(6)
       l1.next.next = ListNode(8)

       l2 = ListNode(3)
       l2.next = ListNode(6)
       l2.next.next = ListNode(7)

       l3 = ListNode(1)
       l3.next = ListNode(3)
       l3.next.next = ListNode(4)

       result = merge_lists([l1, l2, l3])
       print("Here are the elements form the merged list: ", end='')
       while result != None:
           print(str(result.value) + " ", end='')
           result = result.next


   main()

   # answer
   from __future__ import print_function
   from heapq import *


   class ListNode:
       def __init__(self, value):
           self.value = value
           self.next = None

       # used for the min-heap
       def __lt__(self, other):
           return self.value < other.value


   def merge_lists(lists):
       minHeap = []

       # put the root of each list in the min heap
       for root in lists:
           if root is not None:
               heappush(minHeap, root)

       # take the smallest(top) element form the min-heap and add it to the result
       # if the top element has a next element add it to the heap
       resultHead, resultTail = None, None
       while minHeap:
           node = heappop(minHeap)
           if resultHead is None:
               resultHead = resultTail = node
           else:
               resultTail.next = node
               resultTail = resultTail.next

           if node.next is not None:
               heappush(minHeap, node.next)

       return resultHead


   def main():
       l1 = ListNode(2)
       l1.next = ListNode(6)
       l1.next.next = ListNode(8)

       l2 = ListNode(3)
       l2.next = ListNode(6)
       l2.next.next = ListNode(7)

       l3 = ListNode(1)
       l3.next = ListNode(3)
       l3.next.next = ListNode(4)

       result = merge_lists([l1, l2, l3])
       print("Here are the elements form the merged list: ", end='')
       while result is not None:
           print(str(result.value) + " ", end='')
           result = result.next


   main()


   '''
   Time complexity
   Since we’ll be going through all the elements of all arrays and will be removing/adding one element to the heap in each step,
   the time complexity of the above algorithm will be O(N*logK), where ‘N’ is the total number of elements in all the ‘K’ input arrays.
   Space complexity
   The space complexity will be O(K) because, at any time, our min-heap will be storing one number from all the ‘K’ input arrays.
   '''

Kth Smallest Number in M Sorted Lists (Medium)
-----------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given ‘M’ sorted arrays, find the K’th smallest number among all the arrays.
   Example 1:
   Input: L1=[2, 6, 8], L2=[3, 6, 7], L3=[1, 3, 4], K=5
   Output: 4
   Explanation: The 5th smallest number among all the arrays is 4, this can be verified from the merged
   list of all the arrays: [1, 2, 3, 3, 4, 6, 6, 7, 8]
   Example 2:
   Input: L1=[5, 8, 9], L2=[1, 7], K=3
   Output: 7
   Explanation: The 3rd smallest number among all the arrays is 7.
   '''

   # mycode
   from heapq import *


   def find_Kth_smallest(lists, k):
       number = -1
       # TODO: Write your code here
       result = []
       for i in range(len(lists)):
           heappush(result, (lists[i][0], 0, lists[i]))

       count = 0
       while result:
           number, i, cur_list = heappop(result)
           count += 1
           if count == k:
               return number

           if i + 1 < len(cur_list):
               heappush(result, (cur_list[i + 1], i + 1, cur_list))


   def main():
       print("Kth smallest number is: " +
             str(find_Kth_smallest([[2, 6, 8], [3, 6, 7], [1, 3, 4]], 5)))


   main()

   # answer
   from heapq import *


   def find_Kth_smallest(lists, k):
       minHeap = []

       # put the 1st element of each list in the min heap
       for i in range(len(lists)):
           heappush(minHeap, (lists[i][0], 0, lists[i]))

       # take the smallest(top) element form the min heap, if the running count is equal to k return the number
       numberCount, number = 0, 0
       while minHeap:
           number, i, list = heappop(minHeap)
           numberCount += 1
           if numberCount == k:
               break
           # if the array of the top element has more elements, add the next element to the heap
           if len(list) > i + 1:
               heappush(minHeap, (list[i + 1], i + 1, list))

       return number


   def main():
       print("Kth smallest number is: " +
             str(find_Kth_smallest([[2, 6, 8], [3, 6, 7], [1, 3, 4]], 5)))


   main()


   '''
   Time complexity
   Since we’ll be going through at most ‘K’ elements among all the arrays,
   and we will remove/add one element in the heap in each step,
   the time complexity of the above algorithm will be O(K*logM) where ‘M’ is the total number of input arrays.
   Space complexity
   The space complexity will be O(M) because, at any time,
   our min-heap will be storing one number from all the ‘M’ input arrays.
   '''


   '''
   Similar Problems
   Problem 1: Given ‘M’ sorted arrays, find the median number among all arrays.
   Solution: This problem is similar to our parent problem with K=Median.
   So if there are ‘N’ total numbers in all the arrays we need to find the K’th minimum number where K=N/2K.
   Problem 2: Given a list of ‘K’ sorted arrays, merge them into one sorted list.
   Solution: This problem is similar to Merge K Sorted Lists except that
   the input is a list of arrays compared to LinkedLists.
   To handle this, we can use a similar approach as discussed in our parent problem
   by keeping a track of the array and the element indices.
   '''

Kth Smallest Number in a Sorted Matrix (Hard)
-----------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given ‘M’ sorted arrays, find the K’th smallest number among all the arrays.
   Example 1:
   Input: L1=[2, 6, 8], L2=[3, 6, 7], L3=[1, 3, 4], K=5
   Output: 4
   Explanation: The 5th smallest number among all the arrays is 4, this can be verified from the merged
   list of all the arrays: [1, 2, 3, 3, 4, 6, 6, 7, 8]
   Example 2:
   Input: L1=[5, 8, 9], L2=[1, 7], K=3
   Output: 7
   Explanation: The 3rd smallest number among all the arrays is 7.
   '''

   # mycode
   from heapq import *


   def find_Kth_smallest(lists, k):
       number = -1
       # TODO: Write your code here
       result = []
       for i in range(len(lists)):
           heappush(result, (lists[i][0], 0, lists[i]))

       count = 0
       while result:
           number, i, cur_list = heappop(result)
           count += 1
           if count == k:
               return number

           if i + 1 < len(cur_list):
               heappush(result, (cur_list[i + 1], i + 1, cur_list))


   def main():
       print("Kth smallest number is: " +
             str(find_Kth_smallest([[2, 6, 8], [3, 6, 7], [1, 3, 4]], 5)))


   main()

   # answer
   from heapq import *


   def find_Kth_smallest(lists, k):
       minHeap = []

       # put the 1st element of each list in the min heap
       for i in range(len(lists)):
           heappush(minHeap, (lists[i][0], 0, lists[i]))

       # take the smallest(top) element form the min heap, if the running count is equal to k return the number
       numberCount, number = 0, 0
       while minHeap:
           number, i, list = heappop(minHeap)
           numberCount += 1
           if numberCount == k:
               break
           # if the array of the top element has more elements, add the next element to the heap
           if len(list) > i + 1:
               heappush(minHeap, (list[i + 1], i + 1, list))

       return number


   def main():
       print("Kth smallest number is: " +
             str(find_Kth_smallest([[2, 6, 8], [3, 6, 7], [1, 3, 4]], 5)))


   main()


   '''
   Time complexity
   Since we’ll be going through at most ‘K’ elements among all the arrays,
   and we will remove/add one element in the heap in each step,
   the time complexity of the above algorithm will be O(K*logM) where ‘M’ is the total number of input arrays.
   Space complexity
   The space complexity will be O(M) because, at any time,
   our min-heap will be storing one number from all the ‘M’ input arrays.
   '''


   '''
   Similar Problems
   Problem 1: Given ‘M’ sorted arrays, find the median number among all arrays.
   Solution: This problem is similar to our parent problem with K=Median.
   So if there are ‘N’ total numbers in all the arrays we need to find the K’th minimum number where K=N/2K.
   Problem 2: Given a list of ‘K’ sorted arrays, merge them into one sorted list.
   Solution: This problem is similar to Merge K Sorted Lists except that
   the input is a list of arrays compared to LinkedLists.
   To handle this, we can use a similar approach as discussed in our parent problem
   by keeping a track of the array and the element indices.
   '''
               row -= 1
           else:
               # as matrix[row][col] is less than or equal to the mid, let's keep track of the
               # biggest number less than or equal to the mid
               smaller = max(smaller, matrix[row][col])
               count += row + 1
               col += 1

       return count, smaller, larger


   def main():
       print("Kth smallest number is: " +
             str(find_Kth_smallest([[1, 4], [2, 5]], 2)))

       print("Kth smallest number is: " + str(find_Kth_smallest([[-5]], 1)))

       print("Kth smallest number is: " +
             str(find_Kth_smallest([[2, 6, 8], [3, 7, 10], [5, 8, 11]], 5)))

       print("Kth smallest number is: " +
             str(find_Kth_smallest([[1, 5, 9], [10, 11, 13], [12, 13, 15]], 8)))


   main()


   '''
   Time complexity
   The Binary Search could take O(log(max-min)) iterations where ‘max’ is the largest and ‘min’ is the smallest element in the matrix and in each iteration we take O(N)O(N) for counting, therefore, the overall time complexity of the algorithm will be O(N*log(max-min))O(N∗log(max−min)).
   Space complexity
   The algorithm runs in constant space O(1).
   '''

Smallest Number Range (Hard)
-----------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given ‘M’ sorted arrays, find the smallest range that includes at least one number from each of the ‘M’ lists.
   Example 1:
   Input: L1=[1, 5, 8], L2=[4, 12], L3=[7, 8, 10]
   Output: [4, 7]
   Explanation: The range [4, 7] includes 5 from L1, 4 from L2 and 7 from L3.
   Example 2:
   Input: L1=[1, 9], L2=[4, 12], L3=[7, 10, 16]
   Output: [9, 12]
   Explanation: The range [9, 12] includes 9 from L1, 12 from L2 and 10 from L3.
   '''

   # mycode
   from heapq import *
   import math


   def find_smallest_range(lists):
       # TODO: Write your code here
       heap = []
       start, end = -math.inf, math.inf
       current_max = -math.inf
       for i in lists:
           heappush(heap, (i[0], 0, i))
           current_max = max(i[0], current_max)

       while len(heap) == len(lists):
           number, i, current_list = heappop(heap)

           if current_max - number < end - start:
               start = number
               end = current_max

           if i + 1 < len(current_list):
               heappush(heap, (current_list[i + 1], i + 1, current_list))
               current_max = max(current_max, current_list[i + 1])

       return [start, end]


   def main():
       print("Smallest range is: " +
             str(find_smallest_range([[1, 5, 8], [4, 12], [7, 8, 10]])))


   main()

   # answer
   from heapq import *
   import math


   def find_smallest_range(lists):
       minHeap = []
       rangeStart, rangeEnd = 0, math.inf
       currentMaxNumber = -math.inf

       # put the 1st element of each array in the max heap
       for arr in lists:
           heappush(minHeap, (arr[0], 0, arr))
           currentMaxNumber = max(currentMaxNumber, arr[0])

       # take the smallest(top) element form the min heap, if it gives us smaller range, update the ranges
       # if the array of the top element has more elements, insert the next element in the heap
       while len(minHeap) == len(lists):
           num, i, arr = heappop(minHeap)
           if rangeEnd - rangeStart > currentMaxNumber - num:
               rangeStart = num
               rangeEnd = currentMaxNumber

           if len(arr) > i + 1:
               # insert the next element in the heap
               heappush(minHeap, (arr[i + 1], i + 1, arr))
               currentMaxNumber = max(currentMaxNumber, arr[i + 1])

       return [rangeStart, rangeEnd]


   def main():
       print("Smallest range is: " +
             str(find_smallest_range([[1, 5, 8], [4, 12], [7, 8, 10]])))


   main()


   '''
   Time complexity
   Since, at most, we’ll be going through all the elements of all the arrays and will remove/add one element in the heap in each step, t
   he time complexity of the above algorithm will be O(N*logM) where ‘N’ is the total number of elements in all the ‘M’ input arrays.
   Space complexity
   The space complexity will be O(M) because, at any time, our min-heap will be store one number from all the ‘M’ input arrays.
   '''

Problem Challenge 1 - K Pairs with Largest Sums (Hard)
-------------------------------------------------------
.. code:: python

   '''
   Problem Challenge 1
   K Pairs with Largest Sums (Hard)
   Given two sorted arrays in descending order, find ‘K’ pairs with the largest sum where each pair consists of numbers from both the arrays.
   Example 1:
   Input: L1=[9, 8, 2], L2=[6, 3, 1], K=3
   Output: [9, 3], [9, 6], [8, 6]
   Explanation: These 3 pairs have the largest sum. No other pair has a sum larger than any of these.
   Example 2:
   Input: L1=[5, 2, 1], L2=[2, -1], K=3
   Output: [5, 2], [5, -1], [2, 2]
   '''

   # mycode
   from heapq import *


   def find_k_largest_pairs(nums1, nums2, k):
       result = []
       # TODO: Write your code here
       heap = []

       for i in range(min(k, len(nums1))):
           for j in range(min(k, len(nums2))):
               if len(heap) < k:
                   heappush(heap, (nums1[i] + nums2[j], [nums1[i], nums2[j]]))
               else:
                   if nums1[i] + nums2[j] > heap[0][0]:
                       heappop(heap)
                       heappush(heap, (nums1[i] + nums2[j], [nums1[i], nums2[j]]))

       while heap:
           _, ans = heappop(heap)
           result.append(ans)

       return result


   def main():
       print("Pairs with largest sum are: " +
             str(find_k_largest_pairs([9, 8, 2], [6, 3, 1], 3)))


   main()

   # answer
   from __future__ import print_function
   from heapq import *


   def find_k_largest_pairs(nums1, nums2, k):
       minHeap = []
       for i in range(0, min(k, len(nums1))):
           for j in range(min(k, len(nums2))):
               if len(minHeap) < k:
                   heappush(minHeap, (nums1[i] + nums2[j], i, j))
               else:
                   # if the sum of the two numbers from the two arrays is smaller than the smallest(top)
                   # element of the heap, we can 'break' here. Since the arrays are sorted in the
                   # descending order, we'll not be able to find a pair with a higher sum moving forward
                   if nums1[i] + nums2[j] < minHeap[0][0]:
                       break
                   else:  # we have a pair with a larger sum, remove top and insert this pair in the heap
                       heappop(minHeap)
                       heappush(minHeap, (nums1[i] + nums2[j], i, j))

       result = []
       for (num, i, j) in minHeap:
           result.append([nums1[i], nums2[j]])

       return result


   def main():
       print("Pairs with largest sum are: " +
             str(find_k_largest_pairs([9, 8, 2], [6, 3, 1], 3)))


   main()


   '''
   Time complexity
   Since, at most, we’ll be going through all the elements of both arrays and we will add/remove one element in the heap in each step,
   the time complexity of the above algorithm will be O(N*M*logK) where ‘N’ and ‘M’ are the total number of elements in both arrays, respectively.
   If we assume that both arrays have at least ‘K’ elements then the time complexity can be simplified to O(K^2logK),
   because we are not iterating more than ‘K’ elements in both arrays.
   Space complexity
   The space complexity will be O(K) because, at any time, our Min Heap will be storing ‘K’ largest pairs.
   '''
