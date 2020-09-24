Pair with Target Sum (easy)
-----------------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given an array of sorted numbers and a target sum, find a pair in the array whose sum is equal to the given target.
   Write a function to return the indices of the two numbers (i.e. the pair) such that they add up to the given target.
   Example 1:
   Input: [1, 2, 3, 4, 6], target=6
   Output: [1, 3]
   Explanation: The numbers at index 1 and 3 add up to 6: 2+4=6
   Example 2:
   Input: [2, 5, 9, 11], target=11
   Output: [0, 2]
   Explanation: The numbers at index 0 and 2 add up to 11: 2+9=11
   '''


   # mycode
   def pair_with_targetsum(arr, target_sum):
       l, r = 0, len(arr) - 1

       while l < r:
           s = arr[l] + arr[r]
           if s == target_sum:
               return [l, r]
           elif s < target_sum:
               l += 1
           else:
               r -= 1
       return [-1, -1]


   # answer
   def pair_with_targetsum(arr, target_sum):
       left, right = 0, len(arr) - 1
       while (left < right):
           current_sum = arr[left] + arr[right]
           if current_sum == target_sum:
               return [left, right]

           if target_sum > current_sum:
               left += 1  # we need a pair with a bigger sum
           else:
               right -= 1  # we need a pair with a smaller sum
       return [-1, -1]


   def main():
       print(pair_with_targetsum([1, 2, 3, 4, 6], 6))
       print(pair_with_targetsum([2, 5, 9, 11], 11))


   main()


   '''
   Time Complexity
   The time complexity of the above algorithm will be O(N),
   where ‘N’ is the total number of elements in the given array.
   Space Complexity
   The algorithm runs in constant space O(1).
   An Alternate approach
   Instead of using a two-pointer or a binary search approach,
   we can utilize a HashTable to search for the required pair.
   We can iterate through the array one number at a time.
   Let’s say during our iteration we are at number ‘X’,
   so we need to find ‘Y’ such that “X + Y == TargetX+Y==Target”.
   We will do two things here:
   Search for ‘Y’ (which is equivalent to “Target - XTarget−X”) in the HashTable.
   If it is there, we have found the required pair.
   Otherwise, insert “X” in the HashTable, so that we can search it for the later numbers.
   Here is what our algorithm will look like:
   '''


   def pair_with_targetsum(arr, target_sum):
       nums = {}  # to store numbers and their indices
       for i, num in enumerate(arr):
           if target_sum - num in nums:
               return [nums[target_sum - num], i]
           else:
               nums[arr[i]] = i
       return [-1, -1]


   def main():
       print(pair_with_targetsum([1, 2, 3, 4, 6], 6))
       print(pair_with_targetsum([2, 5, 9, 11], 11))


   main()


   '''
   Time Complexity
   The time complexity of the above algorithm will be O(N),
   where ‘N’ is the total number of elements in the given array.
   Space Complexity
   The space complexity will also be O(N), as, in the worst case, we will be pushing ‘N’ numbers in the HashTable.
   '''

Remove Duplicates (easy)
-----------------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given an array of sorted numbers, remove all duplicates from it. You should not use any extra space; after removing the duplicates in-place return the new length of the array.
   Example 1:
   Input: [2, 3, 3, 3, 6, 9, 9]
   Output: 4
   Explanation: The first four elements after removing the duplicates will be [2, 3, 6, 9].
   Example 2:
   Input: [2, 2, 2, 11]
   Output: 2
   Explanation: The first two elements after removing the duplicates will be [2, 11].
   '''


   # mycode
   def remove_duplicates(arr):
       s = 1
       for i in range(1, len(arr)):
           if arr[i] != arr[i - 1]:
               arr[s] = arr[i]
               s += 1
       return s


   # answer
   def remove_duplicates(arr):
       # index of the next non-duplicate element
       next_non_duplicate = 1

       i = 1
       while (i < len(arr)):
           if arr[next_non_duplicate - 1] != arr[i]:
               arr[next_non_duplicate] = arr[i]
               next_non_duplicate += 1
           i += 1

       return next_non_duplicate


   def main():
       print(remove_duplicates([2, 3, 3, 3, 6, 9, 9]))
       print(remove_duplicates([2, 2, 2, 11]))


   main()


   '''
   Time Complexity
   The time complexity of the above algorithm will be O(N),
   where ‘N’ is the total number of elements in the given array.
   Space Complexity
   The algorithm runs in constant space O(1).
   '''


   '''
   Similar Questions #
   Problem 1: Given an unsorted array of numbers and a target ‘key’, remove all instances of ‘key’ in-place and return the new length of the array.
   Example 1:
   Input: [3, 2, 3, 6, 3, 10, 9, 3], Key=3
   Output: 4
   Explanation: The first four elements after removing every 'Key' will be [2, 6, 10, 9].
   Example 2:
   Input: [2, 11, 2, 2, 1], Key=2
   Output: 2
   Explanation: The first two elements after removing every 'Key' will be [11, 1].
   '''


   def remove_element(arr, key):
       nextElement = 0  # index of the next element which is not 'key'
       for i in range(len(arr)):
           if arr[i] != key:
               arr[nextElement] = arr[i]
               nextElement += 1

       return nextElement


   def main():
       print("Array new length: " + str(remove_element([3, 2, 3, 6, 3, 10, 9, 3], 3)))
       print("Array new length: " + str(remove_element([2, 11, 2, 2, 1], 2)))


   main()


   '''
   Time and Space Complexity:
   The time complexity of the above algorithm will be O(N), where ‘N’ is the total number of elements in the given array.
   The algorithm runs in constant space O(1).
   '''

Squaring a Sorted Array (easy)
-----------------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given a sorted array, create a new array containing squares of all the number of the input array in the sorted order.
   Example 1:
   Input: [-2, -1, 0, 2, 3]
   Output: [0, 1, 4, 4, 9]
   Example 2:
   Input: [-3, -1, 0, 1, 2]
   Output: [0 1 1 4 9]
   '''


   # mycode
   def make_squares(arr):
       res = [0] * len(arr)
       l, r = 0, len(arr) - 1
       k = len(arr) - 1
       while l <= r:
           if arr[l] ** 2 >= arr[r] ** 2:
               res[k] = arr[l] ** 2
               l += 1
               k -= 1
           else:
               res[k] = arr[r] ** 2
               r -= 1
               k -= 1
       return res


   # answer
   def make_squares(arr):
       n = len(arr)
       squares = [0 for x in range(n)]
       highestSquareIdx = n - 1
       left, right = 0, n - 1
       while left <= right:
           leftSquare = arr[left] * arr[left]
           rightSquare = arr[right] * arr[right]
           if leftSquare > rightSquare:
               squares[highestSquareIdx] = leftSquare
               left += 1
           else:
               squares[highestSquareIdx] = rightSquare
               right -= 1
           highestSquareIdx -= 1

       return squares


   def main():

       print("Squares: " + str(make_squares([-2, -1, 0, 2, 3])))
       print("Squares: " + str(make_squares([-3, -1, 0, 1, 2])))


   main()


   '''
   Time complexity
   The time complexity of the above algorithm will be O(N) as we are iterating the input array only once.
   Space complexity
   The space complexity of the above algorithm will also be O(N); this space will be used for the output array.
   '''

Triplet Sum to Zero (medium)
-----------------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given an array of unsorted numbers, find all unique triplets in it that add up to zero.
   Example 1:
   Input: [-3, 0, 1, 2, -1, 1, -2]
   Output: [-3, 1, 2], [-2, 0, 2], [-2, 1, 1], [-1, 0, 1]
   Explanation: There are four unique triplets whose sum is equal to zero.
   Example 2:
   Input: [-5, 2, -1, -2, 3]
   Output: [[-5, 2, 3], [-2, -1, 3]]
   Explanation: There are two unique triplets whose sum is equal to zero.
   '''


   # mycode
   def search_triplets(arr):
       triplets = []
       arr.sort()
       # TODO: Write your code here
       for i in range(len(arr)):
           if i > 0 and arr[i] == arr[i - 1]:
               continue
           search_pair(arr, -arr[i], i + 1, triplets)

       return triplets


   def search_pair(arr, target_sum, left, triplets):
       right = len(arr) - 1
       while left < right:
           if arr[left] + arr[right] == target_sum:
               triplets.append([-target_sum, arr[left], arr[right]])
               left += 1
               right -= 1

               while left < right and arr[left] == arr[left - 1]:
                   left += 1
               while left < right and arr[right] == arr[right + 1]:
                   right -= 1

           elif arr[left] + arr[right] > target_sum:
               right -= 1
           else:
               left += 1


   # answer
   def search_triplets(arr):
       arr.sort()
       triplets = []
       for i in range(len(arr)):
           if i > 0 and arr[i] == arr[i - 1]:  # skip same element to avoid duplicate triplets
               continue
           search_pair(arr, -arr[i], i + 1, triplets)

       return triplets


   def search_pair(arr, target_sum, left, triplets):
       right = len(arr) - 1
       while (left < right):
           current_sum = arr[left] + arr[right]
           if current_sum == target_sum:  # found the triplet
               triplets.append([-target_sum, arr[left], arr[right]])
               left += 1
               right -= 1
               while left < right and arr[left] == arr[left - 1]:
                   left += 1  # skip same element to avoid duplicate triplets
               while left < right and arr[right] == arr[right + 1]:
                   right -= 1  # skip same element to avoid duplicate triplets
           elif target_sum > current_sum:
               left += 1  # we need a pair with a bigger sum
           else:
               right -= 1  # we need a pair with a smaller sum


   def main():
       print(search_triplets([-3, 0, 1, 2, -1, 1, -2]))
       print(search_triplets([-5, 2, -1, -2, 3]))


   main()


   '''
   Time complexity
   Sorting the array will take O(N * logN).
   The searchPair() function will take O(N).
   As we are calling searchPair() for every number in the input array,
   this means that overall searchTriplets() will take O(N * logN + N^2), which is asymptotically equivalent to O(N^2).
   Space complexity
   Ignoring the space required for the output array,
   the space complexity of the above algorithm will be O(N) which is required for sorting.
   '''

Triplet Sum Close to Target (medium)
-----------------------------------------------------
.. code:: python

   '''
   Triplet Sum Close to Target (medium)
   Problem Statement
   Given an array of unsorted numbers and a target number, find a triplet in the array whose sum is as close to the target number as possible, return the sum of the triplet.
   If there are more than one such triplet, return the sum of the triplet with the smallest sum.
   Example 1:
   Input: [-2, 0, 1, 2], target=2
   Output: 1
   Explanation: The triplet [-2, 1, 2] has the closest sum to the target.
   Example 2:
   Input: [-3, -1, 1, 2], target=1
   Output: 0
   Explanation: The triplet [-3, 1, 2] has the closest sum to the target.
   Example 3:
   Input: [1, 0, 1, 1], target=100
   Output: 3
   Explanation: The triplet [1, 1, 1] has the closest sum to the target.
   '''


   # mycode
   import math


   def triplet_sum_close_to_target(arr, target_sum):

       # TODO: Write your code here
       arr.sort()
       min_sum, err_min = 0, math.inf

       for i in range(len(arr)):
           j, k = i + 1, len(arr) - 1
           while j < k:
               err = abs(arr[i] + arr[j] + arr[k] - target_sum)
               if err < err_min:
                   err_min = err
                   min_sum = arr[i] + arr[j] + arr[k]
               elif err == err_min:
                   min_sum = min(min_sum, arr[i] + arr[j] + arr[k])

               if arr[i] + arr[j] + arr[k] < target_sum:
                   j += 1
               elif arr[i] + arr[j] + arr[k] > target_sum:
                   k -= 1

       return min_sum


   # answer
   import math


   def triplet_sum_close_to_target(arr, target_sum):
       arr.sort()
       smallest_difference = math.inf
       for i in range(len(arr) - 2):
           left = i + 1
           right = len(arr) - 1
           while (left < right):
               target_diff = target_sum - arr[i] - arr[left] - arr[right]
               if target_diff == 0:  # we've found a triplet with an exact sum
                   return target_sum - target_diff  # return sum of all the numbers

               # the second part of the following 'if' is to handle the smallest sum when we have more than one solution
               if abs(target_diff) < abs(smallest_difference) or (
                       abs(target_diff) == abs(smallest_difference)
                       and target_diff > smallest_difference):
                   smallest_difference = target_diff  # save the closest and the biggest difference

               if target_diff > 0:
                   left += 1  # we need a triplet with a bigger sum
               else:
                   right -= 1  # we need a triplet with a smaller sum

       return target_sum - smallest_difference


   def main():
       print(triplet_sum_close_to_target([-2, 0, 1, 2], 2))
       print(triplet_sum_close_to_target([-3, -1, 1, 2], 1))
       print(triplet_sum_close_to_target([1, 0, 1, 1], 100))


   main()


   '''
   Time complexity
   Sorting the array will take O(N* logN)O(N∗logN). Overall searchTriplet() will take O(N * logN + N^2),
   which is asymptotically equivalent to O(N^2).
   Space complexity
   The space complexity of the above algorithm will be O(N) which is required for sorting.
   '''

Triplets with Smaller Sum (medium)
-----------------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given an array arr of unsorted numbers and a target sum, count all triplets in it such that arr[i] + arr[j] + arr[k] < target where i, j, and k are three different indices. Write a function to return the count of such triplets.
   Example 1:
   Input: [-1, 0, 2, 3], target=3
   Output: 2
   Explanation: There are two triplets whose sum is less than the target: [-1, 0, 3], [-1, 0, 2]
   Example 2:
   Input: [-1, 4, 2, 1, 3], target=5
   Output: 4
   Explanation: There are four triplets whose sum is less than the target:
      [-1, 1, 4], [-1, 1, 3], [-1, 1, 2], [-1, 2, 3]
   '''


   # mycode
   def triplet_with_smaller_sum(arr, target):
       count = 0
       # TODO: Write your code here
       arr.sort()

       for i in range(len(arr)):
           j, k = i + 1, len(arr) - 1
           while j < k:
               if arr[i] + arr[j] + arr[k] < target:
                   count += (k - j)
                   j += 1
               else:
                   k -= 1

       return count


   # answer
   def triplet_with_smaller_sum(arr, target):
       arr.sort()
       count = 0
       for i in range(len(arr) - 2):
           count += search_pair(arr, target - arr[i], i)
       return count


   def search_pair(arr, target_sum, first):
       count = 0
       left, right = first + 1, len(arr) - 1
       while (left < right):
           if arr[left] + arr[right] < target_sum:  # found the triplet
               # since arr[right] >= arr[left], therefore, we can replace arr[right] by any number between
               # left and right to get a sum less than the target sum
               count += right - left
               left += 1
           else:
               right -= 1  # we need a pair with a smaller sum
       return count


   def main():
       print(triplet_with_smaller_sum([-1, 0, 2, 3], 3))
       print(triplet_with_smaller_sum([-1, 4, 2, 1, 3], 5))


   main()


   '''
   Time complexity
   Sorting the array will take O(N * logN). The searchPair() will take O(N).
   So, overall searchTriplets() will take O(N * logN + N^2), which is asymptotically equivalent to O(N^2).
   Space complexity
   Ignoring the space required for the output array,
   the space complexity of the above algorithm will be O(N) which is required for sorting if we are not using an in-place sorting algorithm.
   '''

Subarrays with Product Less than a Target (medium)
-----------------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given an array with positive numbers and a target number,
   find all of its contiguous subarrays whose product is less than the target number.
   Example 1:
   Input: [2, 5, 3, 10], target=30
   Output: [2], [5], [2, 5], [3], [5, 3], [10]
   Explanation: There are six contiguous subarrays whose product is less than the target.
   Example 2:
   Input: [8, 2, 6, 5], target=50
   Output: [8], [2], [8, 2], [6], [2, 6], [5], [6, 5]
   Explanation: There are seven contiguous subarrays whose product is less than the target.
   '''


   # mycode
   def find_subarrays(arr, target):
       result = []
       product = 1
       win_start = 0

       for win_end in range(len(arr)):

           product *= arr[win_end]
           print(product)

           while product >= target and win_start < len(arr):
               product /= arr[win_start]
               win_start += 1

           if product < target:
               temp_i = []
               for i in range(win_end, win_start - 1, -1):
                   temp_i.append(arr[i])
                   temp = temp_i.copy()
                   result.append(temp)

       return result


   # answer
   from collections import deque


   def find_subarrays(arr, target):
       result = []
       product = 1
       left = 0
       for right in range(len(arr)):
           product *= arr[right]
           while (product >= target and left < len(arr)):
               product /= arr[left]
               left += 1
           # since the product of all numbers from left to right is less than the target therefore,
           # all subarrays from lef to right will have a product less than the target too; to avoid
           # duplicates, we will start with a subarray containing only arr[right] and then extend it
           temp_list = deque()
           for i in range(right, left - 1, -1):
               temp_list.appendleft(arr[i])
               result.append(list(temp_list))
       return result


   def main():
       print(find_subarrays([2, 5, 3, 10], 30))
       print(find_subarrays([8, 2, 6, 5], 50))


   main()


   '''
   Time complexity
   The main for-loop managing the sliding window takes O(N)but creating subarrays can take up to O(N^2) in the worst case.
   Therefore overall, our algorithm will take O(N^3).
   Space complexity
   Ignoring the space required for the output list, the algorithm runs in O(N) space which is used for the temp list.
   At the most, we need a space of O(n^2) for all the output lists.
   '''

Dutch National Flag Problem (medium)
-----------------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given an array containing 0s, 1s and 2s, sort the array in-place. You should treat numbers of the array as objects,
   hence, we can’t count 0s, 1s, and 2s to recreate the array.
   The flag of the Netherlands consists of three colors: red, white and blue;
   and since our input array also consists of three different numbers that is why it is called Dutch National Flag problem.
   Example 1:
   Input: [1, 0, 2, 1, 0]
   Output: [0 0 1 1 2]
   Example 2:
   Input: [2, 2, 0, 1, 2, 0]
   Output: [0 0 1 2 2 2 ]
   '''


   # mycode
   def dutch_flag_sort(arr):
       # TODO: Write your code here
       left, i = 0, 0
       right = len(arr) - 1

       while i <= right:
           if arr[i] == 0:
               arr[i], arr[left] = arr[left], arr[i]
               left += 1
               i += 1
           elif arr[i] == 2:
               arr[i], arr[right] = arr[right], arr[i]
               right -= 1
           else:
               i += 1

       return


   '''
   Time complexity
   The time complexity of the above algorithm will be O(N) as we are iterating the input array only once.
   Space complexity #
   The algorithm runs in constant space O(1).
   '''

Problem Challenge 1 - Quadruple Sum to Target (medium)
-------------------------------------------------------
.. code:: python

   '''
   Problem Challenge 1
   Quadruple Sum to Target (medium)
   Given an array of unsorted numbers and a target number, find all unique quadruplets in it, whose sum is equal to the target number.
   Example 1:
   Input: [4, 1, 2, -1, 1, -3], target=1
   Output: [-3, -1, 1, 4], [-3, 1, 1, 2]
   Explanation: Both the quadruplets add up to the target.
   Example 2:
   Input: [2, 0, -1, 1, -2, 2], target=2
   Output: [-2, 0, 2, 2], [-1, 0, 1, 2]
   Explanation: Both the quadruplets add up to the target.
   '''


   # mycode
   def search_quadruplets(arr, target):
       quadruplets = []
       # TODO: Write your code here

       arr.sort()

       for i in range(len(arr) - 3):
           if i > 0 and arr[i] == arr[i - 1]:
               continue
           for j in range(i + 1, len(arr) - 2):
               if j > i and arr[j] == arr[j - 1]:
                   continue
               search_pair(arr, i, j, target, quadruplets)

       return quadruplets


   def search_pair(arr, i, j, target, quadruplets):
       left = j + 1
       right = len(arr) - 1

       sub_target = target - arr[i] - arr[j]

       while left < right:
           if arr[left] + arr[right] == sub_target:
               quadruplets.append([arr[i], arr[j], arr[left], arr[right]])
               left += 1
               right -= 1

               while left < right and arr[left] == arr[left - 1]:
                   left += 1

               while left < right and arr[right] == arr[right + 1]:
                   right -= 1
           elif arr[left] + arr[right] < sub_target:
               left += 1
           else:
               right -= 1


   # answer
   def search_quadruplets(arr, target):
       arr.sort()
       quadruplets = []
       for i in range(0, len(arr) - 3):
           # skip same element to avoid duplicate quadruplets
           if i > 0 and arr[i] == arr[i - 1]:
               continue
           for j in range(i + 1, len(arr) - 2):
               # skip same element to avoid duplicate quadruplets
               if j > i + 1 and arr[j] == arr[j - 1]:
                   continue
               search_pairs(arr, target, i, j, quadruplets)
       return quadruplets


   def search_pairs(arr, target_sum, first, second, quadruplets):
       left = second + 1
       right = len(arr) - 1
       while (left < right):
           sum = arr[first] + arr[second] + arr[left] + arr[right]
           if sum == target_sum:  # found the quadruplet
               quadruplets.append(
                   [arr[first], arr[second], arr[left], arr[right]])
               left += 1
               right -= 1
               while (left < right and arr[left] == arr[left - 1]):
                   left += 1  # skip same element to avoid duplicate quadruplets
               while (left < right and arr[right] == arr[right + 1]):
                   right -= 1  # skip same element to avoid duplicate quadruplets
           elif sum < target_sum:
               left += 1  # we need a pair with a bigger sum
           else:
               right -= 1  # we need a pair with a smaller sum


   def main():
       print(search_quadruplets([4, 1, 2, -1, 1, -3], 1))
       print(search_quadruplets([2, 0, -1, 1, -2, 2], 2))


   main()


   '''
   Time complexity
   Sorting the array will take O(N*logN). Overall searchQuadruplets() will take O(N * logN + N^3), which is asymptotically equivalent to O(N^3).
   Space complexity
   The space complexity of the above algorithm will be O(N) which is required for sorting.
   '''

Problem Challenge 2 - Comparing Strings containing Backspaces (medium)
-----------------------------------------------------------------------
.. code:: python

   '''
   Problem Challenge 2
   Comparing Strings containing Backspaces (medium)
   Given two strings containing backspaces (identified by the character ‘#’), check if the two strings are equal.
   Example 1:
   Input: str1="xy#z", str2="xzz#"
   Output: true
   Explanation: After applying backspaces the strings become "xz" and "xz" respectively.
   Example 2:
   Input: str1="xy#z", str2="xyz#"
   Output: false
   Explanation: After applying backspaces the strings become "xz" and "xy" respectively.
   Example 3:
   Input: str1="xp#", str2="xyz##"
   Output: true
   Explanation: After applying backspaces the strings become "x" and "x" respectively.
   In "xyz##", the first '#' removes the character 'z' and the second '#' removes the character 'y'.
   Example 4:
   Input: str1="xywrrmp", str2="xywrrmu#p"
   Output: true
   Explanation: After applying backspaces the strings become "xywrrmp" and "xywrrmp" respectively.
   '''


   # mycode
   def backspace_compare(str1, str2):
       # TODO: Write your code here
       if clean(str1) == clean(str2):
           return True
       return False


   def clean(str):
       i = len(str) - 1
       while i >= 0:
           count = 0

           while i >= 0 and str[i] == '#':
               count += 1
               i -= 1

           if count > 0 and i + count == len(str) - 1:
               str = str[:i - count + 1]
               i = i - count

           elif count > 0 and i - count + 1 == 0:
               str = str[i + count + 1:]
               i = -1

           elif count > 0:
               str = str[:i - count + 1] + str[i + count + 1:]
               i = i - count - 1
               print(str)
           else:
               i = i - 1

           print(str, count, i)
       return str


   # answer
   def backspace_compare(str1, str2):
       # use two pointer approach to compare the strings
       index1 = len(str1) - 1
       index2 = len(str2) - 1
       while (index1 >= 0 or index2 >= 0):
           i1 = get_next_valid_char_index(str1, index1)
           i2 = get_next_valid_char_index(str2, index2)
           if i1 < 0 and i2 < 0:  # reached the end of both the strings
               return True
           if i1 < 0 or i2 < 0:  # reached the end of one of the strings
               return False
           if str1[i1] != str2[i2]:  # check if the characters are equal
               return False

           index1 = i1 - 1
           index2 = i2 - 1

       return True


   def get_next_valid_char_index(str, index):
       backspace_count = 0
       while (index >= 0):
           if str[index] == '#':  # found a backspace character
               backspace_count += 1
           elif backspace_count > 0:  # a non-backspace character
               backspace_count -= 1
           else:
               break

           index -= 1  # skip a backspace or a valid character

       return index


   def main():
       print(backspace_compare("xy#z", "xzz#"))
       print(backspace_compare("xy#z", "xyz#"))
       print(backspace_compare("xp#", "xyz##"))
       print(backspace_compare("xywrrmp", "xywrrmu#p"))


   main()


   '''
   Time complexity
   The time complexity of the above algorithm will be O(M+N) where ‘M’ and ‘N’ are the lengths of the two input strings respectively.
   Space complexity
   The algorithm runs in constant space O(1).
   '''

Problem Challenge 3 - Minimum Window Sort (medium)
---------------------------------------------------
.. code:: python

   '''
   Problem Challenge 3
   Minimum Window Sort (medium)
   Given an array, find the length of the smallest subarray in it which when sorted will sort the whole array.
   Example 1:
   Input: [1, 2, 5, 3, 7, 10, 9, 12]
   Output: 5
   Explanation: We need to sort only the subarray [5, 3, 7, 10, 9] to make the whole array sorted
   Example 2:
   Input: [1, 3, 2, 0, -1, 7, 10]
   Output: 5
   Explanation: We need to sort only the subarray [1, 3, 2, 0, -1] to make the whole array sorted
   Example 3:
   Input: [1, 2, 3]
   Output: 0
   Explanation: The array is already sorted
   Example 4:
   Input: [3, 2, 1]
   Output: 3
   Explanation: The whole array needs to be sorted.
   '''

   # mycode
   import math


   def shortest_window_sort(arr):
       # TODO: Write your code here

       left, right = 1, len(arr) - 1
       max_num, min_num = -math.inf, math.inf

       while left < len(arr) - 1 and arr[left] < arr[left + 1]:
           left += 1

       while right > 0 and arr[right] > arr[right - 1]:
           right -= 1

       for i in range(left, right + 1):
           max_num = max(max_num, arr[i])
           min_num = min(min_num, arr[i])

       for i in range(left, -1, -1):
           if arr[i] >= min_num:
               left = i

       for i in range(right, len(arr)):
           if arr[i] <= max_num:
               right = i

       if right == 0:
           return 0

       return right - left + 1


   # answer
   import math


   def shortest_window_sort(arr):
       low, high = 0, len(arr) - 1
       # find the first number out of sorting order from the beginning
       while (low < len(arr) - 1 and arr[low] <= arr[low + 1]):
           low += 1

       if low == len(arr) - 1:  # if the array is sorted
           return 0

       # find the first number out of sorting order from the end
       while (high > 0 and arr[high] >= arr[high - 1]):
           high -= 1

       # find the maximum and minimum of the subarray
       subarray_max = -math.inf
       subarray_min = math.inf
       for k in range(low, high + 1):
           subarray_max = max(subarray_max, arr[k])
           subarray_min = min(subarray_min, arr[k])

       # extend the subarray to include any number which is bigger than the minimum of the subarray
       while (low > 0 and arr[low - 1] > subarray_min):
           low -= 1
       # extend the subarray to include any number which is smaller than the maximum of the subarray
       while (high < len(arr) - 1 and arr[high + 1] < subarray_max):
           high += 1

       return high - low + 1


   def main():
       print(shortest_window_sort([1, 2, 5, 3, 7, 10, 9, 12]))
       print(shortest_window_sort([1, 3, 2, 0, -1, 7, 10]))
       print(shortest_window_sort([1, 2, 3]))
       print(shortest_window_sort([3, 2, 1]))


   main()


   '''
   Time complexity
   The time complexity of the above algorithm will be O(N)O(N).
   Space complexity
   The algorithm runs in constant space O(1)O(1).
   '''
