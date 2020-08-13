=======
Medium
=======


209. Minimum Size Subarray Sum
------------------------------------------------------------

`209. Minimum Size Subarray Sum`_

.. code:: python

   class Solution:
       def minSubArrayLen(self, s: int, nums: List[int]) -> int:
           total = left = right = 0
           res = len(nums) + 1
           while right < len(nums):
               total += nums[right]
               while total >= s:
                   res = min(res, right - left + 1)
                   total -= nums[left]
                   left += 1
               right += 1
           return res if res <= len(nums) else 0

.. _209. Minimum Size Subarray Sum: https://leetcode.com/problems/minimum-size-subarray-sum/
