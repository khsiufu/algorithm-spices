=======
Medium
=======


33. Search in Rotated Sorted Array
------------------------------------------------------------

`33. Search in Rotated Sorted Array`_

.. code:: python

   class Solution:
       def search(self, nums: List[int], target: int) -> int:
           l, r = 0, len(nums) - 1
           while l <= r:
               mid = l + (r - l) // 2
               if nums[mid] == target:
                   return mid
               elif nums[l] <= nums[mid]:
                   if nums[l] <= target < nums[mid]:
                       r = mid - 1
                   else:
                       l = mid + 1
               elif nums[mid] <= nums[r]:
                   if nums[mid] < target <= nums[r]:
                       l = mid + 1
                   else:
                       r = mid - 1
           return -1

.. _33. Search in Rotated Sorted Array: https://leetcode.com/problems/search-in-rotated-sorted-array/


34. Find First and Last Position of Element in Sorted Array
------------------------------------------------------------

`34. Find First and Last Position of Element in Sorted Array`_

.. code:: python

   class Solution:
       def searchRange(self, nums: List[int], target: int) -> List[int]:
           if not nums:
               return [-1, -1]
           l, r = 0, len(nums)
           while l < r:
               mid = l + (r - l) // 2
               if nums[mid] >= target:
                   r = mid
               else:
                   l = mid + 1
           # tmp
           start = l
           l, r = 0, len(nums)
           while l < r:
               mid = l + (r - l) // 2
               if nums[mid] > target:
                   r = mid
               else:
                   l = mid + 1
           end = l
           return [-1, -1] if start == end else [start, end - 1]

.. _34. Find First and Last Position of Element in Sorted Array: https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/


74. Search a 2D Matrix
------------------------------------------------------------

`74. Search a 2D Matrix`_

.. code:: python

   class Solution:
       def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
           if not matrix or target is None:
               return False

           row, col = len(matrix), len(matrix[0])
           low, high = 0, row * col - 1

           while low <= high:
               mid = low + (high - low) // 2
               num = matrix[mid // col][mid % col]

               if num == target:
                   return True
               elif num < target:
                   low = mid + 1
               else:
                   high = mid - 1
           return False

.. _74. Search a 2D Matrix: https://leetcode.com/problems/search-a-2d-matrix/


240. Search a 2D Matrix II
------------------------------------------------------------

`240. Search a 2D Matrix II`_

.. code:: python

   class Solution:
       def searchMatrix(self, matrix, target):
           if not matrix or not target:
               return False
           rows, cols = len(matrix), len(matrix[0])
           row, col = rows - 1, 0
           while row >= 0 and col <= cols - 1:
               if matrix[row][col] == target:
                   return True
               elif matrix[row][col] > target:
                   row -= 1
               else:
                   col += 1
           return False

.. _240. Search a 2D Matrix II: https://leetcode.com/problems/search-a-2d-matrix-ii/
