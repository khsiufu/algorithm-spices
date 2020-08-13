=======
Easy
=======


53. Maximum Subarray
------------------------------------------------------------

`53. Maximum Subarray`_

.. code:: python

   class Solution:
       def maxSubArray(self, nums: List[int]) -> int:
           # nums: [-2, 1, -3, 4, -1, 2, 1, -5, 4]
           #   dp: [-2, 1, -2, 4,  3, 5, 6, 1,  5]
           dp = [0 for _ in range(len(nums))]
           res = dp[0] = nums[0]
           for i in range(1, len(nums)):
               dp[i] = max(nums[i], dp[i - 1] + nums[i])
               res = max(dp[i], res)
           return res

.. _53. Maximum Subarray: https://leetcode.com/problems/maximum-subarray/


70. Climbing Stairs
------------------------------------------------------------

`70. Climbing Stairs`_

.. code:: python

   class Solution:
       def climbStairs(self, n: int) -> int:
           if n == 1:
               return 1

           one, two = 1, 2
           for i in range(2, n):
               one, two = two, one + two
           return two

.. _70. Climbing Stairs: https://leetcode.com/problems/climbing-stairs/


121. Best Time to Buy and Sell Stock
------------------------------------------------------------

`121. Best Time to Buy and Sell Stock`_

.. code:: python

   class Solution:
       def maxProfit(self, prices: List[int]) -> int:
           if not prices:
               return 0
           minPri, maxPro = prices[0], 0
           for i in range(1, len(prices)):
               minPri = min(minPri, prices[i])
               maxPro = max(maxPro, prices[i] - minPri)
           return maxPro

.. _121. Best Time to Buy and Sell Stock: https://leetcode.com/problems/best-time-to-buy-and-sell-stock/


198. House Robber
------------------------------------------------------------

`198. House Robber`_

.. code:: python

   # Time: O(n), Space: O(1)
   class Solution:
       def rob(self, nums: List[int]) -> int:
           if not nums:
               return 0

           size = len(nums)
           if size == 1:
               return nums[0]

           first, second = nums[0], max(nums[0], nums[1])
           for i in range(2, size):
               first, second = second, max(first + nums[i], second)

           return second

.. _198. House Robber: https://leetcode.com/problems/house-robber/
