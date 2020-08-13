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


27. Remove Element
------------------------------------------------------

`27. Remove Element`_

.. code:: python

   class Solution:
       def removeElement(self, nums: List[int], val: int) -> int:
           if not len(nums):
               return 0
           count = 0
           for i in range(len(nums)):
               if nums[i] != val:
                   nums[count] = nums[i]
                   count += 1
           return count

.. _27. Remove Element: https://leetcode.com/problems/remove-element/


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


189. Rotate Array
------------------------------------------------------

`189. Rotate Array`_

.. code:: python

   class Solution:
       def rotate(self, nums: List[int], k: int) -> None:
           k = k % len(nums)
           self.reverse(nums, 0, len(nums) - k - 1)
           self.reverse(nums, len(nums) - k, len(nums) - 1)
           self.reverse(nums, 0, len(nums) - 1)

       def reverse(self, nums, s, e):
           while s < e:
               nums[s], nums[e] = nums[e], nums[s]
               s += 1
               e -= 1

.. _189. Rotate Array: https://leetcode.com/problems/rotate-array/


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

