=========================
Permutations
=========================


思路：使用数组记住使用过数字

.. code:: python

   def P(n, m, cur, used):
       if len(cur) == m:
           print(cur)
           return
       for i in range(n):
           if used[i]:
               continue
           used[i] = True
           cur.append(i + 1)
           P(n, m, cur, used)
           cur.pop()
           used[i] = False

   n, m  = 5, 3
   P(n, m, [], [False] * n)

参考题目： LeetCode 46. Permutations

::

   Given a collection of distinct integers, return all possible permutations.
   Example:
   Input: [1,2,3]
   Output:
   [
     [1,2,3],
     [1,3,2],
     [2,1,3],
     [2,3,1],
     [3,1,2],
     [3,2,1]
   ]

code 1

.. code:: python

   def dfs(nums, path, res):
       if not nums:
           res.append(path)
           return
       for i in range(len(nums)):
           dfs(nums[:i] + nums[i+1:], path + [nums[i]], res)
       return res

   res = []
   print(dfs([1, 2, 3], [], res))

code 2

.. code:: python

   class Solution:
       def permute(self, nums: List[int]) -> List[List[int]]:
           if not nums:
               return []
           res, used = [], [False] * len(nums)
           self.helper(nums, used, [], res)
           return res

       def helper(self, nums, used, path, res):
           if len(path) == len(nums):
               res.append(path[:])
               return
           for i in range(len(nums)):
               if used[i]:
                   continue
               used[i] = True
               path.append(nums[i])
               self.helper(nums, used, path, res)
               path.pop()
               used[i] = False
