=======
Medium
=======


29. Divide Two Integers
------------------------------------------------------------

`29. Divide Two Integers`_

.. code:: python

   class Solution:
       def divide(self, dividend: int, divisor: int) -> int:
           int_max, int_min = (1 << 31) - 1, -1 << 31
           sign = 1
           if 0 in [dividend, divisor]:
               return 0
           elif dividend < 0 < divisor or divisor < 0 < dividend:
               sign = -1
               dividend, divisor = abs(dividend), abs(divisor)
           else:
               dividend, divisor = abs(dividend), abs(divisor)
           res = 0
           while dividend >= divisor:
               tmp, val = divisor, 1
               while dividend >= tmp:
                   res += val
                   dividend -= tmp
                   tmp += tmp
                   val += val
           if sign == 1:
               return min(int_max, res)
           else:
               return max(int_min, 0 - res)

.. _29. Divide Two Integers: https://leetcode.com/problems/divide-two-integers/


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


50. Pow(x, n)
------------------------------------------------------------

`50. Pow(x, n)`_

.. code:: python

   class Solution:
       def myPow(self, x: float, n: int) -> float:
           if not n:
               return 1
           # 2^-2 = 1 / 2^2
           if n < 0:
               return 1 / self.myPow(x, -n)
           # odd case 2^3 = 2 * 2^2
           if n % 2:
               return x * self.myPow(x, n - 1)
           # even case 2^4 = 4 ^ 2^2
           return self.myPow(x * x, n // 2)

.. _50. Pow(x, n): https://leetcode.com/problems/powx-n/


69. Sqrt(x)
------------------------------------------------------------

`69. Sqrt(x)`_

.. code:: python

   class Solution:
       def mySqrt(self, x: int) -> int:
           l, r = 1, x
           while l <= r:
               mid = l + (r - l) // 2
               if mid * mid == x:
                   return mid
               elif mid * mid < x:
                   l = mid + 1
               else:
                   r = mid - 1
           return r

.. _69. Sqrt(x): https://leetcode.com/problems/sqrtx/


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


153. Find Minimum in Rotated Sorted Array
------------------------------------------------------------

`153. Find Minimum in Rotated Sorted Array`_

.. code:: python

   class Solution:
       def findMin(self, nums: List[int]) -> int:
           l, r = 0, len(nums) - 1
           while l < r:
               mid = l + (r - l) // 2
               if nums[mid] > nums[r]:
                   l = mid + 1
               else:
                   r = mid
           return nums[r]

.. _153. Find Minimum in Rotated Sorted Array: https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/


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


378. Kth Smallest Element in a Sorted Matrix
------------------------------------------------------------

`378. Kth Smallest Element in a Sorted Matrix`_

.. code:: python

   class Solution:
       def kthSmallest(self, matrix: List[List[int]], k: int) -> int:
           return sorted([elem for row in matrix for elem in row])[k - 1]

.. _378. Kth Smallest Element in a Sorted Matrix: https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/


875. Koko Eating Bananas
------------------------------------------------------------

`875. Koko Eating Bananas`_

.. code:: python

   class Solution:
       def minEatingSpeed(self, piles: List[int], H: int) -> int:
           l, r = 1, max(piles)
           while l < r:
               m = l + (r - l) // 2
               if sum((p + m - 1) // m for p in piles) > H:
                   l = m + 1
               else:
                   r = m
           return l

.. _875. Koko Eating Bananas: https://leetcode.com/problems/koko-eating-bananas/
