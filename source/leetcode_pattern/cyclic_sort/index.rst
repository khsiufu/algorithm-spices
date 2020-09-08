Cyclic Sort (easy)
----------------------------------
.. code:: python

   '''
   Problem Statement
   We are given an array containing ‘n’ objects. Each object, when created, was assigned a unique number from 1 to ‘n’ based on their creation sequence.
   This means that the object with sequence number ‘3’ was created just before the object with sequence number ‘4’.
   Write a function to sort the objects in-place on their creation sequence number in O(n) and without any extra space.
   For simplicity, let’s assume we are passed an integer array containing only the sequence numbers, though each number is actually an object.
   Example 1:
   Input: [3, 1, 5, 4, 2]
   Output: [1, 2, 3, 4, 5]
   Example 2:
   Input: [2, 6, 4, 3, 1, 5]
   Output: [1, 2, 3, 4, 5, 6]
   Example 3:
   Input: [1, 5, 6, 4, 3, 2]
   Output: [1, 2, 3, 4, 5, 6]
   '''


   # mycode
   def cyclic_sort(nums):
       # TODO: Write your code here
       i = 0
       while i < len(nums):
           j = nums[i] - 1
           if i != j:
               nums[i], nums[j] = nums[j], nums[i]
           else:
               i += 1
       return nums


   # answer
   def cyclic_sort(nums):
       i = 0
       while i < len(nums):
           j = nums[i] - 1
           if nums[i] != nums[j]:
               nums[i], nums[j] = nums[j], nums[i]  # swap
           else:
               i += 1
       return nums


   def main():
       print(cyclic_sort([3, 1, 5, 4, 2]))
       print(cyclic_sort([2, 6, 4, 3, 1, 5]))
       print(cyclic_sort([1, 5, 6, 4, 3, 2]))


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(n).
   Although we are not incrementing the index i when swapping the numbers, this will result in more than ‘n’ iterations of the loop,
   but in the worst-case scenario, the while loop will swap a total of ‘n-1’ numbers and once a number is at its correct index,
   we will move on to the next number by incrementing i. So overall, our algorithm will take O(n) + O(n-1) which is asymptotically equivalent to O(n).
   Space complexity
   The algorithm runs in constant space O(1).
   '''

Find the Missing Number (easy)
----------------------------------
.. code:: python

   '''
   Problem Statement
   We are given an array containing ‘n’ distinct numbers taken from the range 0 to ‘n’.
   Since the array has only ‘n’ numbers out of the total ‘n+1’ numbers, find the missing number.
   Example 1:
   Input: [4, 0, 3, 1]
   Output: 2
   Example 2:
   Input: [8, 3, 5, 2, 4, 6, 0, 1]
   Output: 7
   '''


   # mycode
   def find_missing_number(nums):
       # TODO: Write your code here
       for i in range(len(nums)):
           if abs(nums[i]) < len(nums):
               nums[abs(nums[i])] = -nums[abs(nums[i])]

       for i in range(len(nums)):
           if nums[i] > 0:
               return i
       return len(nums)


   # answer
   def find_missing_number(nums):
       i, n = 0, len(nums)
       while i < n:
           j = nums[i]
           if nums[i] < n and nums[i] != nums[j]:
               nums[i], nums[j] = nums[j], nums[i]  # swap
           else:
               i += 1

       # find the first number missing from its index, that will be our required number
       for i in range(n):
           if nums[i] != i:
               return i

       return n


   def main():
       print(find_missing_number([4, 0, 3, 1]))
       print(find_missing_number([8, 3, 5, 2, 4, 6, 0, 1]))


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(n).
   In the while loop, although we are not incrementing the index i when swapping the numbers,
   this will result in more than ‘n’ iterations of the loop,
   but in the worst-case scenario, the while loop will swap a total of ‘n-1’ numbers and once a number is at its correct index,
   we will move on to the next number by incrementing i.
   In the end, we iterate the input array again to find the first number missing from its index,
   so overall, our algorithm will take O(n) + O(n-1) + O(n)  which is asymptotically equivalent to O(n).
   Space complexity
   The algorithm runs in constant space O(1).
   '''

Find all Missing Numbers (easy)
----------------------------------
.. code:: python

   '''
   Problem Statement
   We are given an unsorted array containing numbers taken from the range 1 to ‘n’.
   The array can have duplicates, which means some numbers will be missing. Find all those missing numbers.
   Example 1:
   Input: [2, 3, 1, 8, 2, 3, 5, 1]
   Output: 4, 6, 7
   Explanation: The array should have all numbers from 1 to 8, due to duplicates 4, 6, and 7 are missing.
   Example 2:
   Input: [2, 4, 1, 2]
   Output: 3
   Example 3:
   Input: [2, 3, 2, 1]
   Output: 4
   '''


   # mycode
   def find_missing_numbers(nums):
       missingNumbers = []
       # TODO: Write your code here
       i = 0
       while i < len(nums):
           j = nums[i] - 1
           if i != j and j != nums[j] - 1:
               nums[i], nums[j] = nums[j], nums[i]
           else:
               i += 1
       for i in range(len(nums)):
           if i != nums[i] - 1:
               missingNumbers.append(i + 1)
       return missingNumbers


   '''
   Be careful about i != j and nums[i] != nums[j]
   when there are duplicates in index i, then using i!=j as condition, while will keep looping
   using nums[i] != nums[j] can avoid this problem, because duplicates means there exists nums[i] = nums[j]
   2 4 1 2
   i=0
   4 2 1 2
   2 2 1 4
   i=1
   2 2 1 4
   i=2
   1 2 2 4
   i=3
   1 2 2 4
   '''


   # mycode2
   def find_missing_numbers(nums):
       missingNumbers = []
       # TODO: Write your code here
       for i in range(len(nums)):
           j = abs(nums[i]) - 1
           if nums[j] >= 0:
               nums[j] = -nums[j]

       for i in range(len(nums)):
           if nums[i] > 0:
               missingNumbers.append(i + 1)
       return missingNumbers


   # answer
   def find_missing_numbers(nums):
       i = 0
       while i < len(nums):
           j = nums[i] - 1
           if nums[i] != nums[j]:
               nums[i], nums[j] = nums[j], nums[i]  # swap
           else:
               i += 1

       missingNumbers = []

       for i in range(len(nums)):
           if nums[i] != i + 1:
               missingNumbers.append(i + 1)

       return missingNumbers


   def main():
       print(find_missing_numbers([2, 3, 1, 8, 2, 3, 5, 1]))
       print(find_missing_numbers([2, 4, 1, 2]))
       print(find_missing_numbers([2, 3, 2, 1]))


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(n).
   Space complexity
   Ignoring the space required for the output array, the algorithm runs in constant space O(1).
   '''

Find the Duplicate Number (easy)
----------------------------------
.. code:: python

   '''
   Problem Statement
   We are given an unsorted array containing ‘n+1’ numbers taken from the range 1 to ‘n’.
   The array has only one duplicate but it can be repeated multiple times.
   Find that duplicate number without using any extra space. You are, however, allowed to modify the input array.
   Example 1:
   Input: [1, 4, 4, 3, 2]
   Output: 4
   Example 2:
   Input: [2, 1, 3, 3, 5, 4]
   Output: 3
   Example 3:
   Input: [2, 4, 1, 4, 4]
   Output: 4
   '''


   # mycode
   def find_duplicate(nums):
       # TODO: Write your code here
       for i in range(len(nums)):
           j = abs(nums[i]) - 1
           if nums[j] > 0:
               nums[j] = -nums[j]
           else:
               return j + 1
       return -1


   # mycode2
   def find_duplicate(nums):
       # TODO: Write your code here
       i = 0
       while i < len(nums):
           j = nums[i] - 1

           if nums[i] != nums[j]:
               nums[i], nums[j] = nums[j], nums[i]
           elif nums[i] == nums[j] and i != j:
               return nums[i]
           else:
               i += 1

       return -1


   # answer
   def find_duplicate(nums):
       i = 0
       while i < len(nums):
           if nums[i] != i + 1:
               j = nums[i] - 1
               if nums[i] != nums[j]:
                   nums[i], nums[j] = nums[j], nums[i]  # swap
               else:  # we have found the duplicate
                   return nums[i]
           else:
               i += 1

       return -1


   def main():
       print(find_duplicate([1, 4, 4, 3, 2]))
       print(find_duplicate([2, 1, 3, 3, 5, 4]))
       print(find_duplicate([2, 4, 1, 4, 4]))


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(n).
   Space complexity
   The algorithm runs in constant space O(1) but modifies the input array.
   '''


   '''
   Similar Problems
   Problem 1: Can we solve the above problem in O(1) space and without modifying the input array?
   Solution: While doing the cyclic sort, we realized that the array will have a cycle due to the duplicate number and that the start of the cycle will always point to the duplicate number.
   This means that we can use the fast & the slow pointer method to find the duplicate number or the start of the cycle similar to Start of LinkedList Cycle.
   The time complexity of the above algorithm is O(n) and the space complexity is O(1).
   '''


   def find_duplicate(arr):
       slow, fast = arr[0], arr[arr[0]]
       while slow != fast:
           slow = arr[slow]
           fast = arr[arr[fast]]

       # find cycle length
       current = arr[arr[slow]]
       cycleLength = 1
       while current != arr[slow]:
           current = arr[current]
           cycleLength += 1

       return find_start(arr, cycleLength)


   def find_start(arr, cycleLength):
       pointer1, pointer2 = arr[0], arr[0]
       # move pointer2 ahead 'cycleLength' steps
       while cycleLength > 0:
           pointer2 = arr[pointer2]
           cycleLength -= 1

       # increment both pointers until they meet at the start of the cycle
       while pointer1 != pointer2:
           pointer1 = arr[pointer1]
           pointer2 = arr[pointer2]

       return pointer1


   def main():
       print(find_duplicate([1, 4, 4, 3, 2]))
       print(find_duplicate([2, 1, 3, 3, 5, 4]))
       print(find_duplicate([2, 4, 1, 4, 4]))


   main()

Find all Duplicate Numbers (easy)
----------------------------------
.. code:: python

   '''
   Problem Statement
   We are given an unsorted array containing ‘n’ numbers taken from the range 1 to ‘n’.
   The array has some duplicates, find all the duplicate numbers without using any extra space.
   Example 1:
   Input: [3, 4, 4, 5, 5]
   Output: [4, 5]
   Example 2:
   Input: [5, 4, 7, 2, 3, 5, 3]
   Output: [3, 5]
   '''


   # mycode
   def find_all_duplicates(nums):
       duplicateNumbers = []
       # TODO: Write your code here
       for i in range(len(nums)):
           j = abs(nums[i]) - 1
           if nums[j] > 0:
               nums[j] = -nums[j]
           else:
               duplicateNumbers.append(j + 1)
       return duplicateNumbers


   # answer
   def find_all_duplicates(nums):
       i = 0
       while i < len(nums):
           j = nums[i] - 1
           if nums[i] != nums[j]:
               nums[i], nums[j] = nums[j], nums[i]  # swap
           else:
               i += 1

       duplicateNumbers = []
       for i in range(len(nums)):
           if nums[i] != i + 1:
               duplicateNumbers.append(nums[i])

       return duplicateNumbers


   def main():
       print(find_all_duplicates([3, 4, 4, 5, 5]))
       print(find_all_duplicates([5, 4, 7, 2, 3, 5, 3]))


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(n).
   Space complexity
   Ignoring the space required for storing the duplicates, the algorithm runs in constant space O(1).
   '''

Problem Challenge 1 - Find the Corrupt Pair (easy)
---------------------------------------------------
.. code:: python

   '''
   Problem Challenge 1
   Find the Corrupt Pair (easy)
   We are given an unsorted array containing ‘n’ numbers taken from the range 1 to ‘n’. The array originally contained all the numbers from 1 to ‘n’, but due to a data error, one of the numbers got duplicated which also resulted in one number going missing. Find both these numbers.
   Example 1:
   Input: [3, 1, 2, 5, 2]
   Output: [2, 4]
   Explanation: '2' is duplicated and '4' is missing.
   Example 2:
   Input: [3, 1, 2, 3, 6, 4]
   Output: [3, 5]
   Explanation: '3' is duplicated and '5' is missing.
   '''


   # mycode
   def find_corrupt_numbers(nums):
       # TODO: Write your code here
       duplicate, missing = 0, 0
       i = 0

       while i < len(nums):
           j = nums[i] - 1
           if i != j:
               if nums[i] != nums[j]:
                   nums[i], nums[j] = nums[j], nums[i]
               else:
                   duplicate = nums[i]
                   i += 1
           else:
               i += 1

       for i in range(len(nums)):
           if nums[i] - 1 != i:
               missing = i + 1
       return [duplicate, missing]


   # answer
   def find_corrupt_numbers(nums):
       i = 0
       while i < len(nums):
           j = nums[i] - 1
           if nums[i] != nums[j]:
               nums[i], nums[j] = nums[j], nums[i]  # swap
           else:
               i += 1

       for i in range(len(nums)):
           if nums[i] != i + 1:
               return [nums[i], i + 1]

       return [-1, -1]


   def main():
       print(find_corrupt_numbers([3, 1, 2, 5, 2]))
       print(find_corrupt_numbers([3, 1, 2, 3, 6, 4]))


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(n).
   Space complexity
   The algorithm runs in constant space O(1).
   '''

Problem Challenge 2 - Find the Smallest Missing Positive Number (medium)
--------------------------------------------------------------------------
.. code:: python

   '''
   Problem Challenge 2
   Find the Smallest Missing Positive Number (medium)
   Given an unsorted array containing numbers, find the smallest missing positive number in it.
   Example 1:
   Input: [-3, 1, 5, 4, 2]
   Output: 3
   Explanation: The smallest missing positive number is '3'
   Example 2:
   Input: [3, -2, 0, 1, 2]
   Output: 4
   Example 3:
   Input: [3, 2, 5, 1]
   Output: 4
   '''


   # mycode
   def find_first_missing_positive(nums):
       # TODO: Write your code here
       i = 0
       while i < len(nums):
           j = nums[i] - 1
           if j >= 0 and j < len(nums):
               if nums[i] != nums[j]:
                   nums[i], nums[j] = nums[j], nums[i]
               else:
                   i += 1
           else:
               i += 1

       for i in range(len(nums)):
           if nums[i] - 1 != i:
               return i + 1


   # answer
   def find_first_missing_positive(nums):
       i, n = 0, len(nums)
       while i < n:
           j = nums[i] - 1
           if nums[i] > 0 and nums[i] <= n and nums[i] != nums[j]:
               nums[i], nums[j] = nums[j], nums[i]  # swap
           else:
               i += 1

       for i in range(n):
           if nums[i] != i + 1:
               return i + 1

       return nums.length + 1


   def main():
       print(find_first_missing_positive([-3, 1, 5, 4, 2]))
       print(find_first_missing_positive([3, -2, 0, 1, 2]))
       print(find_first_missing_positive([3, 2, 5, 1]))


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(n).
   Space complexity
   The algorithm runs in constant space O(1).
   '''

Problem Challenge 3 - Find the First K Missing Positive Numbers (hard)
------------------------------------------------------------------------
.. code:: python

   '''
   Problem Challenge 3
   Find the First K Missing Positive Numbers (hard)
   Given an unsorted array containing numbers and a number ‘k’, find the first ‘k’ missing positive numbers in the array.
   Example 1:
   Input: [3, -1, 4, 5, 5], k=3
   Output: [1, 2, 6]
   Explanation: The smallest missing positive numbers are 1, 2 and 6.
   Example 2:
   Input: [2, 3, 4], k=3
   Output: [1, 5, 6]
   Explanation: The smallest missing positive numbers are 1, 5 and 6.
   Example 3:
   Input: [-2, -3, 4], k=2
   Output: [1, 2]
   Explanation: The smallest missing positive numbers are 1 and 2.
   '''


   # mycode
   def find_first_k_missing_positive(nums, k):
       missingNumbers = []
       # TODO: Write your code here
       i = 0
       while i < len(nums):
           j = nums[i] - 1
           if j >= 0 and j < len(nums) and nums[i] != nums[j]:
               nums[i], nums[j] = nums[j], nums[i]
           else:
               i += 1

       i = 0
       while i < len(nums):
           if nums[i] - 1 != i:
               missingNumbers.append(i + 1)
           i += 1

       i = 1
       if k <= len(missingNumbers):
           missingNumbers = missingNumbers[:k]
       else:
           while len(missingNumbers) < k:
               if max(missingNumbers) + 1 < max(
                       nums) and max(missingNumbers) + 1 not in nums:
                   missingNumbers.append(max(missingNumbers) + 1)
               else:
                   missingNumbers.append(max(nums) + i)
                   i += 1

       return missingNumbers


   # answer
   def find_first_k_missing_positive(nums, k):
       n = len(nums)
       i = 0
       while i < len(nums):
           j = nums[i] - 1
           if nums[i] > 0 and nums[i] <= n and nums[i] != nums[j]:
               nums[i], nums[j] = nums[j], nums[i]  # swap
           else:
               i += 1

       missingNumbers = []
       extraNumbers = set()
       for i in range(n):
           if len(missingNumbers) < k:
               if nums[i] != i + 1:
                   missingNumbers.append(i + 1)
                   extraNumbers.add(nums[i])

       # add the remaining missing numbers
       i = 1
       while len(missingNumbers) < k:
           candidateNumber = i + n
           # ignore if the array contains the candidate number
           if candidateNumber not in extraNumbers:
               missingNumbers.append(candidateNumber)
           i += 1

       return missingNumbers


   def main():
       print(find_first_k_missing_positive([3, -1, 4, 5, 5], 3))
       print(find_first_k_missing_positive([2, 3, 4], 3))
       print(find_first_k_missing_positive([-2, -3, 4], 2))


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(n + k), as the last two for loops will run for O(n) and O(k) times respectively.
   Space complexity
   The algorithm needs O(k) space to store the extraNumbers.
   '''
