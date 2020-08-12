=======
Easy
=======


26. Remove Duplicates from Sorted Array
------------------------------------------------------

`26. Remove Duplicates from Sorted Array`_

.. code:: python

   class Solution:
       def removeDuplicates(self, nums: List[int]) -> int:
           s = 0
           for i in range(1, len(nums)):
               if nums[s] != nums[i]:
                   s += 1
                   nums[s] = nums[i]
           return s + 1

.. _26. Remove Duplicates from Sorted Array: https://leetcode.com/problems/remove-duplicates-from-sorted-array/


66. Plus One
------------------------------------------------------

`66. Plus One`_

.. code:: python

   class Solution:
       def plusOne(self, digits: List[int]) -> List[int]:
           return [int(a) for a in (str(int(''.join(map(str, digits))) + 1))]

.. _66. Plus One: https://leetcode.com/problems/plus-one/


118. Pascal’s Triangle
------------------------------------------------------

`118. Pascal’s Triangle`_

.. code:: python

   class Solution:
       def generate(self, numRows: int) -> List[List[int]]:
           res = []
           for i in range(numRows):
               res.append([])
               for j in range(i + 1):
                   if j in (0, i):
                       res[i].append(1)
                   else:
                       res[i].append(res[i-1][j-1] + res[i-1][j])
           return res

.. _118. Pascal’s Triangle: https://leetcode.com/problems/pascals-triangle/


448. Find All Numbers Disappeared in an Array
------------------------------------------------------

`448. Find All Numbers Disappeared in an Array`_

.. code:: python

   class Solution:
       def findDisappearedNumbers(self, nums: List[int]) -> List[int]:
           a = set([i for i in range(1, len(nums) + 1)])
           b = set(nums)
           return list(a - b)

.. _448. Find All Numbers Disappeared in an Array: https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/

