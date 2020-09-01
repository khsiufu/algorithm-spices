=======
Hard
=======


41. First Missing Positive
------------------------------------------------------

`41. First Missing Positive`_

.. code:: python

   class Solution:
       def firstMissingPositive(self, nums: List[int]) -> int:
           # 思路是把1放在数组第一个位置nums[0]，2放在第二个位置nums[1]，即需要把nums[i]放在nums[nums[i] - 1]上，遍历整个数组
           # 如果 nums[i] != i + 1, 而 nums[i] 为整数且不大于n，另外 nums[i] 不等于 nums[nums[i] - 1] 的话，将两者位置调换
           for i in range(len(nums)):
               while 0 <= nums[i] - 1 < len(nums) and nums[nums[i] - 1] != nums[i]:
                   tmp = nums[i] - 1
                   nums[i], nums[tmp] = nums[tmp], nums[i]

           for i in range(len(nums)):
               if nums[i] != i + 1:
                   return i + 1
           return len(nums) + 1

.. _41. First Missing Positive: https://leetcode.com/problems/first-missing-positive/
