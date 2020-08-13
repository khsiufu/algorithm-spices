=======
Hard
=======


42. Trapping Rain Water
-----------------------------------------------------------

`42. Trapping Rain Water`_

.. code:: python

   class Solution:
       def trap(self, height: List[int]) -> int:
           if not height or len(height) < 3:
               return 0
           res = 0
           left, right = 0, len(height) - 1
           l_max, r_max = height[left], height[right]
           while left < right:
               l_max, r_max = max(height[left], l_max), max(height[right], r_max)
               if l_max <= r_max:
                   res += l_max - height[left]
                   left += 1
               else:
                   res += r_max - height[right]
                   right -= 1
           return res

.. _42. Trapping Rain Water: https://leetcode.com/problems/trapping-rain-water/
