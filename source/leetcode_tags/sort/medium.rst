=======
Medium
=======


56. Merge Intervals
------------------------------------------------------------

`56. Merge Intervals`_

.. code:: python

   class Solution:
       def merge(self, intervals: List[List[int]]) -> List[List[int]]:
           if not intervals:
               return []
           # sort
           intervals.sort()
           res = []

           for interval in intervals:
               # 空 or 迭代的数组起点 > 答案最后一个数组尾巴，就进行插入
               if not res or interval[0] > res[-1][1]:
                   res.append(interval)
               # 否则，合并尾巴
               else:
                   res[-1][1] = max(res[-1][1], interval[1])
           return res

.. _56. Merge Intervals: https://leetcode.com/problems/merge-intervals/


179. Largest Number
------------------------------------------------------------

`179. Largest Number`_

.. code:: python

   class Solution:
       def largestNumber(self, nums: List[int]) -> str:
           # use quick sort, in-place
           self.quickSort(nums, 0, len(nums) - 1)
           return str(int("".join(map(str, nums))))

       def quickSort(self, nums, l, r):
           if l >= r:
               return
           pos = self.partition(nums, l, r)
           self.quickSort(nums, l, pos - 1)
           self.quickSort(nums, pos + 1, r)

       def partition(self, nums, l, r):
           low = l
           while l < r:
               if self.compare(nums[l], nums[r]):
                   nums[l], nums[low] = nums[low], nums[l]
                   low += 1
               l += 1
           nums[low], nums[r] = nums[r], nums[low]
           return low

       def compare(self, n1, n2):
           return str(n1) + str(n2) > str(n2) + str(n1)

.. _179. Largest Number: https://leetcode.com/problems/largest-number/
