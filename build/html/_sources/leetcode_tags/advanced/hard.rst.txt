=======
Hard
=======


`84. Largest Rectangle in Histogram`_
------------------------------------------------------

`84. Largest Rectangle in Histogram`_

.. code:: python

   class Solution:
       def largestRectangleArea(self, heights: List[int]) -> int:
           heights.append(0)
           stack = [-1]
           ans = 0
           for i in range(len(heights)):
               while heights[i] < heights[stack[-1]]:
                   h = heights[stack.pop()]
                   w = i - stack[-1] - 1
                   ans = max(ans, h * w)
               stack.append(i)
           heights.pop()
           return ans

.. _84. Largest Rectangle in Histogram: https://leetcode.com/problems/largest-rectangle-in-histogram/
