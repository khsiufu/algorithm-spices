=======
Hard
=======


123. Best Time to Buy and Sell Stock III
------------------------------------------------------------

`123. Best Time to Buy and Sell Stock III`_

.. code:: python

   # Time: O(n), Space: O(1)
   class Solution:
       def maxProfit(self, prices: List[int]) -> int:
           one_buy = two_buy = sys.maxsize
           one_profit = two_profit = 0
           for p in prices:
               one_buy = min(one_buy, p)
               one_profit = max(one_profit, p - one_buy)
               two_buy = min(two_buy, p - one_profit)
               two_profit = max(two_profit, p - two_buy)
           return two_profit

.. _123. Best Time to Buy and Sell Stock III: https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/
