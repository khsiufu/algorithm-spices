Order-agnostic Binary Search (easy)
-------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given a sorted array of numbers, find if a given number ‘key’ is present in the array. Though we know that the array is sorted, we don’t know if it’s sorted in ascending or descending order. You should assume that the array can have duplicates.
   Write a function to return the index of the ‘key’ if it is present in the array, otherwise return -1.
   Example 1:
   Input: [4, 6, 10], key = 10
   Output: 2
   Example 2:
   Input: [1, 2, 3, 4, 5, 6, 7], key = 5
   Output: 4
   Example 3:
   Input: [10, 6, 4], key = 10
   Output: 0
   Example 4:
   Input: [10, 6, 4], key = 4
   Output: 2
   '''


   # mycode
   def binary_search(arr, key):
       # TODO: Write your code here
       if arr[0] == arr[-1]:
           return 0

       if arr[0] < arr[-1]:
           start = 0
           end = len(arr) - 1

           while start <= end:
               index = (start + end) // 2
               if arr[index] < key:
                   start = index + 1
               elif arr[index] > key:
                   end = index - 1
               else:
                   return index

       if arr[0] > arr[-1]:
           start = 0
           end = len(arr) - 1

           while start <= end:
               index = (start + end) // 2
               if arr[index] > key:
                   start = index + 1
               elif arr[index] < key:
                   end = index - 1
               else:
                   return index

       return -1


   def main():
       print(binary_search([4, 6, 10], 10))
       print(binary_search([1, 2, 3, 4, 5, 6, 7], 5))
       print(binary_search([10, 6, 4], 10))
       print(binary_search([10, 6, 4], 4))


   main()


   # answer
   def binary_search(arr, key):
       start, end = 0, len(arr) - 1
       isAscending = arr[start] < arr[end]
       while start <= end:
           # calculate the middle of the current range
           mid = start + (end - start) // 2

           if key == arr[mid]:
               return mid

           if isAscending:  # ascending order
               if key < arr[mid]:
                   end = mid - 1  # the 'key' can be in the first half
               else:  # key > arr[mid]
                   start = mid + 1  # the 'key' can be in the second half
           else:  # descending order
               if key > arr[mid]:
                   end = mid - 1  # the 'key' can be in the first half
               else:  # key < arr[mid]
                   start = mid + 1  # the 'key' can be in the second half

       return -1  # element not found


   def main():
       print(binary_search([4, 6, 10], 10))
       print(binary_search([1, 2, 3, 4, 5, 6, 7], 5))
       print(binary_search([10, 6, 4], 10))
       print(binary_search([10, 6, 4], 4))


   main()


   '''
   Time complexity
   Since, we are reducing the search range by half at every step,
   this means that the time complexity of our algorithm will be O(logN) where ‘N’ is the total elements in the given array.
   Space complexity
   The algorithm runs in constant space O(1).
   '''

Ceiling of a Number (medium)
-------------------------------------------
.. code:: python

   '''
   Problem Statement #
   Given an array of numbers sorted in an ascending order, find the ceiling of a given number ‘key’. The ceiling of the ‘key’ will be the smallest element in the given array greater than or equal to the ‘key’.
   Write a function to return the index of the ceiling of the ‘key’. If there isn’t any ceiling return -1.
   Example 1:
   Input: [4, 6, 10], key = 6
   Output: 1
   Explanation: The smallest number greater than or equal to '6' is '6' having index '1'.
   Example 2:
   Input: [1, 3, 8, 10, 15], key = 12
   Output: 4
   Explanation: The smallest number greater than or equal to '12' is '15' having index '4'.
   Example 3:
   Input: [4, 6, 10], key = 17
   Output: -1
   Explanation: There is no number greater than or equal to '17' in the given array.
   Example 4:
   Input: [4, 6, 10], key = -1
   Output: 0
   Explanation: The smallest number greater than or equal to '-1' is '4' having index '0'.
   '''


   # mycode
   def search_ceiling_of_a_number(arr, key):
       # TODO: Write your code here
       start, end = 0, len(arr) - 1

       if key > arr[end]:
           return -1
       if key <= arr[0]:
           return 0

       while start <= end:
           mid = (start + end) // 2

           if arr[mid] == key:
               return mid

           if arr[mid] < key:
               start = mid + 1
           elif arr[mid] > key:
               end = mid - 1
       return start


   def main():
       print(search_ceiling_of_a_number([4, 6, 10], 6))
       print(search_ceiling_of_a_number([1, 3, 8, 10, 15], 12))
       print(search_ceiling_of_a_number([4, 6, 10], 17))
       print(search_ceiling_of_a_number([4, 6, 10], -1))


   main()


   # answer
   def search_ceiling_of_a_number(arr, key):
       n = len(arr)
       if key > arr[n - 1]:  # if the 'key' is bigger than the biggest element
           return -1

       start, end = 0, n - 1
       while start <= end:
           mid = start + (end - start) // 2
           if key < arr[mid]:
               end = mid - 1
           elif key > arr[mid]:
               start = mid + 1
           else:  # found the key
               return mid

       # since the loop is running until 'start <= end', so at the end of the while loop, 'start == end+1'
       # we are not able to find the element in the given array, so the next big number will be arr[start]
       return start


   def main():
       print(search_ceiling_of_a_number([4, 6, 10], 6))
       print(search_ceiling_of_a_number([1, 3, 8, 10, 15], 12))
       print(search_ceiling_of_a_number([4, 6, 10], 17))
       print(search_ceiling_of_a_number([4, 6, 10], -1))


   main()


   '''
   Time complexity
   Since we are reducing the search range by half at every step,
   this means that the time complexity of our algorithm will be O(logN) where ‘N’ is the total elements in the given array.
   Space complexity
   The algorithm runs in constant space O(1).
   '''


   '''
   Similar Problems
   Problem 1
   Given an array of numbers sorted in ascending order, find the floor of a given number ‘key’. The floor of the ‘key’ will be the biggest element in the given array smaller than or equal to the ‘key’
   Write a function to return the index of the floor of the ‘key’. If there isn’t a floor, return -1.
   Example 1:
   Input: [4, 6, 10], key = 6
   Output: 1
   Explanation: The biggest number smaller than or equal to '6' is '6' having index '1'.
   Example 2:
   Input: [1, 3, 8, 10, 15], key = 12
   Output: 3
   Explanation: The biggest number smaller than or equal to '12' is '10' having index '3'.
   Example 3:
   Input: [4, 6, 10], key = 17
   Output: 2
   Explanation: The biggest number smaller than or equal to '17' is '10' having index '2'.
   Example 4:
   Input: [4, 6, 10], key = -1
   Output: -1
   Explanation: There is no number smaller than or equal to '-1' in the given array.
   '''


   def search_floor_of_a_number(arr, key):
       if key < arr[0]:  # if the 'key' is smaller than the smallest element
           return -1

       start, end = 0, len(arr) - 1
       while start <= end:
           mid = start + (end - start) // 2
           if key < arr[mid]:
               end = mid - 1
           elif key > arr[mid]:
               start = mid + 1
           else:  # found the key
               return mid

       # since the loop is running until 'start <= end', so at the end of the while loop, 'start == end+1'
       # we are not able to find the element in the given array, so the next smaller number will be arr[end]
       return end


   def main():
       print(search_floor_of_a_number([4, 6, 10], 6))
       print(search_floor_of_a_number([1, 3, 8, 10, 15], 12))
       print(search_floor_of_a_number([4, 6, 10], 17))
       print(search_floor_of_a_number([4, 6, 10], -1))


   main()

Next Letter (medium)
-------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given an array of lowercase letters sorted in ascending order,
   find the smallest letter in the given array greater than a given ‘key’.
   Assume the given array is a circular list, which means that the last letter is assumed to be connected with the first letter.
   This also means that the smallest letter in the given array is greater than the last letter of the array and is also the first letter of the array.
   Write a function to return the next letter of the given ‘key’.
   Example 1:
   Input: ['a', 'c', 'f', 'h'], key = 'f'
   Output: 'h'
   Explanation: The smallest letter greater than 'f' is 'h' in the given array.
   Example 2:
   Input: ['a', 'c', 'f', 'h'], key = 'b'
   Output: 'c'
   Explanation: The smallest letter greater than 'b' is 'c'.
   Example 3:
   Input: ['a', 'c', 'f', 'h'], key = 'm'
   Output: 'a'
   Explanation: As the array is assumed to be circular, the smallest letter greater than 'm' is 'a'.
   Example 4:
   Input: ['a', 'c', 'f', 'h'], key = 'h'
   Output: 'a'
   Explanation: As the array is assumed to be circular, the smallest letter greater than 'h' is 'a'.
   '''


   # mycode
   def search_next_letter(letters, key):
       # TODO: Write your code here
       if key < letters[0] or key >= letters[-1]:
           return letters[0]

       start, end = 0, len(letters) - 1
       while start <= end:
           mid = (start + end) // 2
           if letters[mid] < key:
               start = mid + 1
           elif letters[mid] > key:
               end = mid - 1
           else:
               return letters[mid + 1 % len(letters)]
       return letters[start]


   def main():
       print(search_next_letter(['a', 'c', 'f', 'h'], 'f'))
       print(search_next_letter(['a', 'c', 'f', 'h'], 'b'))
       print(search_next_letter(['a', 'c', 'f', 'h'], 'm'))


   main()


   # answer
   def search_next_letter(letters, key):
       n = len(letters)
       if key < letters[0] or key > letters[n - 1]:
           return letters[0]

       start, end = 0, n - 1
       while start <= end:
           mid = start + (end - start) // 2
           if key < letters[mid]:
               end = mid - 1
           else:  # key >= letters[mid]:
               start = mid + 1

       # since the loop is running until 'start <= end', so at the end of the while loop, 'start == end+1'
       return letters[start % n]


   def main():
       print(search_next_letter(['a', 'c', 'f', 'h'], 'f'))
       print(search_next_letter(['a', 'c', 'f', 'h'], 'b'))
       print(search_next_letter(['a', 'c', 'f', 'h'], 'm'))


   main()


   '''
   Time complexity
   Since, we are reducing the search range by half at every step,
   this means that the time complexity of our algorithm will be O(logN)O
   where ‘N’ is the total elements in the given array.
   Space complexity
   The algorithm runs in constant space O(1).
   '''

Number Range (medium)
-------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given an array of numbers sorted in ascending order, find the range of a given number ‘key’. The range of the ‘key’ will be the first and last position of the ‘key’ in the array.
   Write a function to return the range of the ‘key’. If the ‘key’ is not present return [-1, -1].
   Example 1:
   Input: [4, 6, 6, 6, 9], key = 6
   Output: [1, 3]
   Example 2:
   Input: [1, 3, 8, 10, 15], key = 10
   Output: [3, 3]
   Example 3:
   Input: [1, 3, 8, 10, 15], key = 12
   Output: [-1, -1]
   '''


   # mycode
   def find_range(arr, key):
       result = [-1, -1]
       # TODO: Write your code here
       result[0] = binary_search(arr, key, False)
       if result[0] != -1:
           result[1] = binary_search(arr, key, True)
       return result


   def binary_search(arr, key, findMax):
       start, end = 0, len(arr) - 1

       keyIndex = -1
       while start <= end:
           mid = (start + end) // 2

           if arr[mid] < key:
               start = mid + 1
           elif arr[mid] > key:
               end = mid - 1
           else:
               keyIndex = mid
               if findMax:
                   start = mid + 1
               else:
                   end = mid - 1

       return keyIndex


   def main():
       print(find_range([4, 6, 6, 6, 9], 6))
       print(find_range([1, 3, 8, 10, 15], 10))
       print(find_range([1, 3, 8, 10, 15], 12))


   main()


   # answer
   def find_range(arr, key):
       result = [-1, -1]
       result[0] = binary_search(arr, key, False)
       if result[
               0] != -1:  # no need to search, if 'key' is not present in the input array
           result[1] = binary_search(arr, key, True)
       return result


   # modified Binary Search
   def binary_search(arr, key, findMaxIndex):
       keyIndex = -1
       start, end = 0, len(arr) - 1
       while start <= end:
           mid = start + (end - start) // 2
           if key < arr[mid]:
               end = mid - 1
           elif key > arr[mid]:
               start = mid + 1
           else:  # key == arr[mid]
               keyIndex = mid
               if findMaxIndex:
                   start = mid + 1  # search ahead to find the last index of 'key'
               else:
                   end = mid - 1  # search behind to find the first index of 'key'

       return keyIndex


   def main():
       print(find_range([4, 6, 6, 6, 9], 6))
       print(find_range([1, 3, 8, 10, 15], 10))
       print(find_range([1, 3, 8, 10, 15], 12))


   main()


   '''
   Time complexity
   Since, we are reducing the search range by half at every step, this means that the time complexity of our algorithm
   will be O(logN) where ‘N’ is the total elements in the given array.
   Space complexity
   The algorithm runs in constant space O(1).
   '''

Search in a Sorted Infinite Array (medium)
-------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given an infinite sorted array (or an array with unknown size),
   find if a given number ‘key’ is present in the array.
   Write a function to return the index of the ‘key’ if it is present in the array, otherwise return -1.
   Since it is not possible to define an array with infinite (unknown) size,
    you will be provided with an interface ArrayReader to read elements of the array.
    ArrayReader.get(index) will return the number at index;
    if the array’s size is smaller than the index, it will return Integer.MAX_VALUE.
   Example 1:
   Input: [4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30], key = 16
   Output: 6
   Explanation: The key is present at index '6' in the array.
   Example 2:
   Input: [4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30], key = 11
   Output: -1
   Explanation: The key is not present in the array.
   Example 3:
   Input: [1, 3, 8, 10, 15], key = 15
   Output: 4
   Explanation: The key is present at index '4' in the array.
   Example 4:
   Input: [1, 3, 8, 10, 15], key = 200
   Output: -1
   Explanation: The key is not present in the array.
   '''

   # mycode
   import math


   class ArrayReader:
       def __init__(self, arr):
           self.arr = arr

       def get(self, index):
           if index >= len(self.arr):
               return math.inf
           return self.arr[index]


   def search_in_infinite_array(reader, key):
       # TODO: Write your code here
       n = len(reader.arr)
       start, end = 0, n - 1
       while start <= end:
           mid = (start + end) // 2
           if reader.arr[mid] < key:
               start = mid + 1
           elif reader.arr[mid] > key:
               end = mid - 1
           else:
               return mid
       return -1


   def main():
       reader = ArrayReader([4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30])
       print(search_in_infinite_array(reader, 16))
       print(search_in_infinite_array(reader, 11))
       reader = ArrayReader([1, 3, 8, 10, 15])
       print(search_in_infinite_array(reader, 15))
       print(search_in_infinite_array(reader, 200))


   main()

   # answer
   import math


   class ArrayReader:
       def __init__(self, arr):
           self.arr = arr

       def get(self, index):
           if index >= len(self.arr):
               return math.inf
           return self.arr[index]


   def search_in_infinite_array(reader, key):
       # find the proper bounds first
       start, end = 0, 1
       while reader.get(end) < key:
           newStart = end + 1
           end += (end - start + 1) * 2
           # increase to double the bounds size
           start = newStart

       return binary_search(reader, key, start, end)


   def binary_search(reader, key, start, end):
       while start <= end:
           mid = start + (end - start) // 2
           if key < reader.get(mid):
               end = mid - 1
           elif key > reader.get(mid):
               start = mid + 1
           else:  # found the key
               return mid

       return -1


   def main():
       reader = ArrayReader([4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30])
       print(search_in_infinite_array(reader, 16))
       print(search_in_infinite_array(reader, 11))
       reader = ArrayReader([1, 3, 8, 10, 15])
       print(search_in_infinite_array(reader, 15))
       print(search_in_infinite_array(reader, 200))


   main()


   '''
   Time complexity
   There are two parts of the algorithm. In the first part,
   we keep increasing the bound’s size exponentially (double it every time) while searching for the proper bounds.
   Therefore, this step will take O(logN) assuming that the array will have maximum ‘N’ numbers.
   In the second step, we perform the binary search which will take O(logN),
   so the overall time complexity of our algorithm will be O(logN + logN)
   which is asymptotically equivalent to O(logN).
   Space complexity
   The algorithm runs in constant space O(1).
   '''

Minimum Difference Element (medium)
-------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given an array of numbers sorted in ascending order,
   find the element in the array that has the minimum difference with the given ‘key’.
   Example 1:
   Input: [4, 6, 10], key = 7
   Output: 6
   Explanation: The difference between the key '7' and '6' is minimum than any other number in the array
   Example 2:
   Input: [4, 6, 10], key = 4
   Output: 4
   Example 3:
   Input: [1, 3, 8, 10, 15], key = 12
   Output: 10
   Example 4:
   Input: [4, 6, 10], key = 17
   Output: 10
   '''

   # mycode
   def search_min_diff_element(arr, key):
       # TODO: Write your code here
       if key <= arr[0]:
           return arr[0]
       if key >= arr[-1]:
           return arr[-1]

       start, end = 0, len(arr) - 1
       while start <= end:
           mid = (start + end) // 2

           if arr[mid] < key:
               start = mid + 1
           elif arr[mid] > key:
               end = mid - 1
           else:
               return arr[mid]

       if abs(arr[start] - key) >= abs(arr[end] - key):
           return arr[end]
       else:
           return arr[start]


   def main():
       print(search_min_diff_element([4, 6, 10], 7))
       print(search_min_diff_element([4, 6, 10], 4))
       print(search_min_diff_element([1, 3, 8, 10, 15], 12))
       print(search_min_diff_element([4, 6, 10], 17))


   main()


   # answer
   def search_min_diff_element(arr, key):
       if key < arr[0]:
           return arr[0]
       n = len(arr)
       if key > arr[n - 1]:
           return arr[n - 1]

       start, end = 0, n - 1
       while start <= end:
           mid = start + (end - start) // 2
           if key < arr[mid]:
               end = mid - 1
           elif key > arr[mid]:
               start = mid + 1
           else:
               return arr[mid]

       # at the end of the while loop, 'start == end+1'
       # we are not able to find the element in the given array
       # return the element which is closest to the 'key'
       if (arr[start] - key) < (key - arr[end]):
           return arr[start]
       return arr[end]


   def main():
       print(search_min_diff_element([4, 6, 10], 7))
       print(search_min_diff_element([4, 6, 10], 4))
       print(search_min_diff_element([1, 3, 8, 10, 15], 12))
       print(search_min_diff_element([4, 6, 10], 17))


   main()


   '''
   Time complexity
   Since, we are reducing the search range by half at every step,
   this means the time complexity of our algorithm will be O(logN)
   where ‘N’ is the total elements in the given array.
   Space complexity
   The algorithm runs in constant space O(1).
   '''

Bitonic Array Maximum (easy)
-------------------------------------------
.. code:: python

   '''
   Problem Statement
   Find the maximum value in a given Bitonic array. An array is considered bitonic if it is monotonically increasing and then monotonically decreasing. Monotonically increasing or decreasing means that for any index i in the array arr[i] != arr[i+1].
   Example 1:
   Input: [1, 3, 8, 12, 4, 2]
   Output: 12
   Explanation: The maximum number in the input bitonic array is '12'.
   Example 2:
   Input: [3, 8, 3, 1]
   Output: 8
   Example 3:
   Input: [1, 3, 8, 12]
   Output: 12
   Example 4:
   Input: [10, 9, 8]
   Output: 10
   '''


   # mycode
   def find_max_in_bitonic_array(arr):
       # TODO: Write your code here
       start, end = 0, len(arr) - 1
       while start <= end:
           mid = (start + end) // 2
           if mid == len(arr) - 1:
               return arr[mid]
           if mid < len(arr) - 1 and arr[mid] < arr[mid + 1]:
               start = mid + 1
           else:
               if mid - 1 >= 0 and arr[mid] > arr[mid - 1]:
                   return arr[mid]
               elif mid == 0:
                   return arr[mid]
               else:
                   end = mid - 1


   def main():
       print(find_max_in_bitonic_array([1, 3, 8, 12, 4, 2]))
       print(find_max_in_bitonic_array([3, 8, 3, 1]))
       print(find_max_in_bitonic_array([1, 3, 8, 12]))
       print(find_max_in_bitonic_array([10, 9, 8]))


   main()


   # answer
   def find_max_in_bitonic_array(arr):
       start, end = 0, len(arr) - 1
       while start < end:
           mid = start + (end - start) // 2
           if arr[mid] > arr[mid + 1]:
               end = mid
           else:
               start = mid + 1

       # at the end of the while loop, 'start == end'
       return arr[start]


   def main():
       print(find_max_in_bitonic_array([1, 3, 8, 12, 4, 2]))
       print(find_max_in_bitonic_array([3, 8, 3, 1]))
       print(find_max_in_bitonic_array([1, 3, 8, 12]))
       print(find_max_in_bitonic_array([10, 9, 8]))


   main()


   '''
   Time complexity
   Since we are reducing the search range by half at every step,
   this means that the time complexity of our algorithm will be O(logN)
   where ‘N’ is the total elements in the given array.
   Space complexity
   The algorithm runs in constant space O(1).
   '''

Problem Challenge 1 - Search Bitonic Array (medium)
----------------------------------------------------
.. code:: python

   '''
   Problem Challenge 1
   Search Bitonic Array (medium)
   Given a Bitonic array, find if a given ‘key’ is present in it.
   An array is considered bitonic if it is monotonically increasing and then monotonically decreasing.
   Monotonically increasing or decreasing means that for any index i in the array arr[i] != arr[i+1].
   Write a function to return the index of the ‘key’. If the ‘key’ is not present, return -1.
   Example 1:
   Input: [1, 3, 8, 4, 3], key=4
   Output: 3
   Example 2:
   Input: [3, 8, 3, 1], key=8
   Output: 1
   Example 3:
   Input: [1, 3, 8, 12], key=12
   Output: 3
   Example 4:
   Input: [10, 9, 8], key=10
   Output: 0
   '''


   # mycode
   def search_bitonic_array(arr, key):
       # TODO: Write your code here
       maxIndex = search_maximum(arr)
       if key > arr[maxIndex]:
           return -1
       start, end = 0, maxIndex

       while start <= end:
           mid = (start + end) // 2
           if arr[mid] < key:
               start = mid + 1
           elif arr[mid] > key:
               end = mid - 1
           else:
               return mid

       start, end = maxIndex, len(arr) - 1
       while start <= end:
           mid = (start + end) // 2
           if arr[mid] < key:
               end = mid - 1
           elif arr[mid] > key:
               start = mid + 1
           else:
               return mid

       return -1


   def search_maximum(arr):
       start, end = 0, len(arr) - 1
       while start < end:
           mid = (start + end) // 2
           if arr[mid] < arr[mid + 1]:
               start = mid + 1
           else:
               end = mid

       return start


   def main():
       print(search_bitonic_array([1, 3, 8, 4, 3], 4))
       print(search_bitonic_array([3, 8, 3, 1], 8))
       print(search_bitonic_array([1, 3, 8, 12], 12))
       print(search_bitonic_array([10, 9, 8], 10))


   main()


   # answer
   def search_bitonic_array(arr, key):
       maxIndex = find_max(arr)
       keyIndex = binary_search(arr, key, 0, maxIndex)
       if keyIndex != -1:
           return keyIndex
       return binary_search(arr, key, maxIndex + 1, len(arr) - 1)


   # find index of the maximum value in a bitonic array
   def find_max(arr):
       start, end = 0, len(arr) - 1
       while start < end:
           mid = start + (end - start) // 2
           if arr[mid] > arr[mid + 1]:
               end = mid
           else:
               start = mid + 1

       # at the end of the while loop, 'start == end'
       return start


   # order-agnostic binary search
   def binary_search(arr, key, start, end):
       while start <= end:
           mid = int(start + (end - start) / 2)

           if key == arr[mid]:
               return mid

           if arr[start] < arr[end]:  # ascending order
               if key < arr[mid]:
                   end = mid - 1
               else:  # key > arr[mid]
                   start = mid + 1
           else:  # descending order
               if key > arr[mid]:
                   end = mid - 1
               else:  # key < arr[mid]
                   start = mid + 1

       return -1  # element is not found


   def main():
       print(search_bitonic_array([1, 3, 8, 4, 3], 4))
       print(search_bitonic_array([3, 8, 3, 1], 8))
       print(search_bitonic_array([1, 3, 8, 12], 12))
       print(search_bitonic_array([10, 9, 8], 10))


   main()


   '''
   Time complexity
   Since we are reducing the search range by half at every step,
   this means that the time complexity of our algorithm will be O(logN)
   where ‘N’ is the total elements in the given array.
   Space complexity
   The algorithm runs in constant space O(1).
   '''

Problem Challenge 2 - Search in Rotated Array (medium)
-------------------------------------------------------
.. code:: python

   '''
   Problem Challenge 2
   Search in Rotated Array (medium)
   Given an array of numbers which is sorted in ascending order and also rotated by some arbitrary number,
   find if a given ‘key’ is present in it.
   Write a function to return the index of the ‘key’ in the rotated array. If the ‘key’ is not present, return -1.
   You can assume that the given array does not have any duplicates.
   Example 1:
   Input: [10, 15, 1, 3, 8], key = 15
   Output: 1
   Explanation: '15' is present in the array at index '1'.
   Example 2:
   Input: [4, 5, 7, 9, 10, -1, 2], key = 10
   Output: 4
   Explanation: '10' is present in the array at index '4'.
   '''


   # mycode
   def search_rotated_array(arr, key):
       # TODO: Write your code here
       start, end = 0, len(arr) - 1
       while start <= end:
           mid = (start + end) // 2
           if arr[mid] == key:
               return mid

           if arr[start] <= arr[mid]:
               if arr[start] <= key and arr[mid] > key:
                   end = mid - 1
               else:
                   start = mid + 1
           else:
               if key > arr[end] or key < arr[mid]:
                   end = mid - 1
               else:
                   start = mid + 1
       return -1


   def main():
       print(search_rotated_array([10, 15, 1, 3, 8], 15))
       print(search_rotated_array([4, 5, 7, 9, 10, -1, 2], 10))


   main()


   # answer
   def search_rotated_array(arr, key):
       start, end = 0, len(arr) - 1
       while start <= end:
           mid = start + (end - start) // 2
           if arr[mid] == key:
               return mid

           if arr[start] <= arr[mid]:  # left side is sorted in ascending order
               if key >= arr[start] and key < arr[mid]:
                   end = mid - 1
               else:  # key > arr[mid]
                   start = mid + 1
           else:  # right side is sorted in ascending order
               if key > arr[mid] and key <= arr[end]:
                   start = mid + 1
               else:
                   end = mid - 1

       # we are not able to find the element in the given array
       return -1


   def main():
       print(search_rotated_array([10, 15, 1, 3, 8], 15))
       print(search_rotated_array([4, 5, 7, 9, 10, -1, 2], 10))


   main()


   '''
   Time complexity
   Since we are reducing the search range by half at every step,
   this means that the time complexity of our algorithm will be O(logN)
   where ‘N’ is the total elements in the given array.
   Space complexity
   The algorithm runs in constant space O(1).
   '''


   '''
   Similar Problems
   Problem 1
   How do we search in a sorted and rotated array that also has duplicates?
   The code above will fail in the following example!
   Example 1:
   Input: [3, 7, 3, 3, 3], key = 7
   Output: 1
   Explanation: '7' is present in the array at index '1'.
   Solution
   The only problematic scenario is when the numbers at indices start, middle, and end are the same, as in this case,
   we can’t decide which part of the array is sorted.
   In such a case, the best we can do is to skip one number from both ends: start = start + 1 & end = end - 1.
   '''


   def search_rotated_with_duplicates(arr, key):
       start, end = 0, len(arr) - 1
       while start <= end:
           mid = start + (end - start) // 2
           if arr[mid] == key:
               return mid

           # the only difference from the previous solution,
           # if numbers at indexes start, mid, and end are same, we can't choose a side
           # the best we can do, is to skip one number from both ends as key != arr[mid]
           if arr[start] == arr[mid] and arr[end] == arr[mid]:
               start += 1
               end -= 1
           elif arr[start] <= arr[mid]:  # left side is sorted in ascending order
               if key >= arr[start] and key < arr[mid]:
                   end = mid - 1
               else:  # key > arr[mid]
                   start = mid + 1

           else:  # right side is sorted in ascending order
               if key > arr[mid] and key <= arr[end]:
                   start = mid + 1
               else:
                   end = mid - 1

       # we are not able to find the element in the given array
       return -1


   def main():
       print(search_rotated_with_duplicates([3, 7, 3, 3, 3], 7))


   main()

Problem Challenge 3 - Rotation Count (medium)
----------------------------------------------
.. code:: python

   '''
   Problem Challenge 3
   Rotation Count (medium)
   Given an array of numbers which is sorted in ascending order and is rotated ‘k’ times around a pivot, find ‘k’.
   You can assume that the array does not have any duplicates.
   Example 1:
   Input: [10, 15, 1, 3, 8]
   Output: 2
   Explanation: The array has been rotated 2 times.
   Example 2:
   Input: [4, 5, 7, 9, 10, -1, 2]
   Output: 5
   Explanation: The array has been rotated 5 times.
   Example 3:
   Input: [1, 3, 8, 10]
   Output: 0
   Explanation: The array has been not been rotated.
   '''


   # mycode
   def count_rotations(arr):
       # TODO: Write your code here
       start, end = 0, len(arr) - 1
       while start <= end:
           mid = (start + end) // 2

           if mid > start and arr[mid - 1] > arr[mid]:
               return mid
           if mid < start and arr[mid] > arr[mid + 1]:
               return mid + 1

           if arr[start] < arr[mid]:
               start = mid + 1
           else:
               end = mid - 1

       return 0


   def main():
       print(count_rotations([10, 15, 1, 3, 8]))
       print(count_rotations([4, 5, 7, 9, 10, -1, 2]))
       print(count_rotations([1, 3, 8, 10]))


   main()


   # answer
   def count_rotations(arr):
       start, end = 0, len(arr) - 1
       while start < end:
           mid = start + (end - start) // 2

           # if mid is greater than the next element
           if mid < end and arr[mid] > arr[mid + 1]:
               return mid + 1

           # if mid is smaller than the previous element
           if mid > start and arr[mid - 1] > arr[mid]:
               return mid

           if arr[start] < arr[
                   mid]:  # left side is sorted, so the pivot is on right side
               start = mid + 1
           else:  # right side is sorted, so the pivot is on the left side
               end = mid - 1

       return 0  # the array has not been rotated


   def main():
       print(count_rotations([10, 15, 1, 3, 8]))
       print(count_rotations([4, 5, 7, 9, 10, -1, 2]))
       print(count_rotations([1, 3, 8, 10]))


   main()


   '''
   Time complexity
   This algorithm will run in O(logN) most of the times,
   but since we only skip two numbers in case of duplicates instead of the half of the numbers,
   therefore the worst case time complexity will become O(N).
   Space complexity
   The algorithm runs in constant space O(1).
   '''

