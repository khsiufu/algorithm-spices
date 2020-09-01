=======
Medium
=======


31. Next Permutation
------------------------------------------------------

`31. Next Permutation`_

.. code:: python

   class Solution:
       def nextPermutation(self, nums: List[int]) -> None:
           i = len(nums) - 2
           while i >= 0 and nums[i] >= nums[i+1]:
               i -= 1
           if i < 0: # 6 5 4 3 2 1
               nums.reverse()
               return
           j = len(nums) - 1
           while j >= 0 and nums[i] >= nums[j]:
               j -= 1
           nums[i], nums[j] = nums[j], nums[i]

           l, r = i + 1, len(nums) - 1
           while l < r:
               nums[l], nums[r] = nums[r], nums[l]
               l += 1
               r -= 1

.. _31. Next Permutation: https://leetcode.com/problems/next-permutation/


48. Rotate Image
------------------------------------------------------

`48. Rotate Image`_

.. code:: python

   class Solution:
       def rotate(self, matrix: List[List[int]]) -> None:
           matrix[:] = zip(*matrix[::-1])

.. _48. Rotate Image: https://leetcode.com/problems/rotate-image/


54. Spiral Matrix
------------------------------------------------------

`54. Spiral Matrix`_

.. code:: python

   class Solution:
       def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
           if not matrix:
               return []

           res = []
           left, right = 0, len(matrix[0]) - 1
           top, bottom = 0, len(matrix) - 1

           while left < right and top < bottom:
               for i in range(left, right):
                   res.append(matrix[top][i])
               for i in range(top, bottom):
                   res.append(matrix[i][right])
               for i in range(right, left, -1):
                   res.append(matrix[bottom][i])
               for i in range(bottom, top, -1):
                   res.append(matrix[i][left])

               # 上面做完一圈
               left += 1
               right -= 1
               top += 1
               bottom -= 1

           if left == right:
               # 剩下垂直，range右边临界要包含
               for i in range(top, bottom + 1):
                   res.append(matrix[i][left])
           elif top == bottom:
               # 剩下横向，range右边临界要包含
               for i in range(left, right + 1):
                   res.append(matrix[top][i])

           return res

.. _54. Spiral Matrix: https://leetcode.com/problems/spiral-matrix/


59. Spiral Matrix II
------------------------------------------------------

`59. Spiral Matrix II`_

.. code:: python

   class Solution:
       def generateMatrix(self, n):
           if not n:
               return []
           res = [[0 for _ in range(n)] for _ in range(n)]
           left, right, top, down, num = 0, n-1, 0, n-1, 1
           while left <= right and top <= down:
               for i in range(left, right+1):
                   res[top][i] = num
                   num += 1
               top += 1
               for i in range(top, down+1):
                   res[i][right] = num
                   num += 1
               right -= 1
               for i in range(right, left-1, -1):
                   res[down][i] = num
                   num += 1
               down -= 1
               for i in range(down, top-1, -1):
                   res[i][left] = num
                   num += 1
               left += 1
           return res

.. _59. Spiral Matrix II: https://leetcode.com/problems/spiral-matrix-ii/


73. Set Matrix Zeroes
------------------------------------------------------

`73. Set Matrix Zeroes`_

.. code:: python

   class Solution:
       def setZeroes(self, matrix: List[List[int]]) -> None:
           row, col = len(matrix), len(matrix[0])
           firstRowFlag, firstColFlag = False, False

           # 找第一行是否有0
           for j in range(col):
               if matrix[0][j] == 0:
                   firstRowFlag = True
                   break

           # 第一列是否有0
           for i in range(row):
               if matrix[i][0] == 0:
                   firstColFlag = True
                   break

           # 把第一行或者第一列作为 标志位
           for i in range(1, row):
               for j in range(1, col):
                   if matrix[i][j] == 0:
                       matrix[i][0] = matrix[0][j] = 0

           # set zero
           for i in range(1, row):
               for j in range(1, col):
                   if matrix[i][0] == 0 or matrix[0][j] == 0:
                       matrix[i][j] = 0

           if firstRowFlag:
               for j in range(col):
                   matrix[0][j] = 0
           if firstColFlag:
               for i in range(row):
                   matrix[i][0] = 0

.. _73. Set Matrix Zeroes: https://leetcode.com/problems/set-matrix-zeroes/


80. Remove Duplicates from Sorted Array II
------------------------------------------------------

`80. Remove Duplicates from Sorted Array II`_

.. code:: python

   class Solution(object):
       def removeDuplicates(self, nums):
           if len(nums) <= 2:
               return len(nums)
           count = 2
           for i in range(2, len(nums)):
               if nums[i] != nums[count-2]:
                   nums[count] = nums[i]
                   count += 1
           return count

.. _80. Remove Duplicates from Sorted Array II: https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/


442. Find All Duplicates in an Array
------------------------------------------------------

`442. Find All Duplicates in an Array`_

.. code:: python

   class Solution:
       def findDuplicates(self, nums: List[int]) -> List[int]:
           return [key for key, value in collections.Counter(nums).items() if value == 2]

.. _442. Find All Duplicates in an Array: https://leetcode.com/problems/find-all-duplicates-in-an-array/
