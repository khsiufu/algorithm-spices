=========================
Combinations
=========================


思路：使用一个常量记录位置，避免重复

.. code:: python

   def C(n, m, idx, cur):
       if len(cur) == m:
           print(cur)
           return
       for i in range(idx, n):
           cur.append(i + 1)
           C(n, m, i + 1, cur)
           cur.pop()

   n, m = 5, 3
   C(n, m, 0, [])

参考题目： LeetCode 77. Combinations

::

   Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.
   Example:
   Input: n = 4, k = 2
   Output:
   [
     [2,4],
     [3,4],
     [2,3],
     [1,2],
     [1,3],
     [1,4],
   ]

code 1

.. code:: python

   def dfs(nums, k, idx, path, res):
       if k == 0:
           res.append(path)
           return
       for i in range(idx, len(nums)):
           dfs(nums, k - 1, i + 1, path + [nums[i]], res)
       return res

   res = []
   print(dfs([1, 2, 3, 4], 2, 0, [], res))

code 2

.. code:: python

   class Solution:
       def __init__(self):
           self.output = []

       def combine(self, n, k, pos=0, temp=None):
           temp = temp or []

           if len(temp) == k:
               self.output.append(temp[:])
               return

           for i in range(pos, n):
               temp.append(i + 1)
               self.combine(n, k, i + 1, temp)
               temp.pop()

           return self.output
