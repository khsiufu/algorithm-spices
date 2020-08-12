=======
Medium
=======


`442. Find All Duplicates in an Array`_

.. code:: python

   class Solution:
       def findDuplicates(self, nums: List[int]) -> List[int]:
           return [key for key, value in collections.Counter(nums).items() if value == 2]

.. _442. Find All Duplicates in an Array: https://leetcode.com/problems/find-all-duplicates-in-an-array/


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
