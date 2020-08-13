=======
Medium
=======


17. Letter Combinations of a Phone Number
------------------------------------------------------------

`17. Letter Combinations of a Phone Number`_

.. code:: python

   class Solution:
       def letterCombinations(self, digits: str) -> List[str]:
           if not digits:
               return []
           dct = {'2': 'abc', '3': 'def', '4': 'ghi', '5': 'jkl',
                  '6': 'mno', '7': 'pqrs', '8': 'tuv', '9': 'wxyz'}
           res = []
           self.dfs(digits, dct, 0, '', res)
           return res

       def dfs(self, digits, dct, index, path, res):
           if len(path) == len(digits):
               res.append(path)
               return
           for i in range(index, len(digits)):
               for j in dct[digits[i]]:
                   self.dfs(digits, dct, i + 1, path + j, res)

.. _17. Letter Combinations of a Phone Number: https://leetcode.com/problems/letter-combinations-of-a-phone-number/


39. Combination Sum
------------------------------------------------------------

`39. Combination Sum`_

.. code:: python

   class Solution:
       def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
           res = []
           candidates.sort()
           self.dfs(candidates, target, 0, [], res)
           return res

       def dfs(self, nums, target, idx, path, res):
           if target < 0:
               return
           if target == 0:
               res.append(path)
               return
           for i in range(idx, len(nums)):
               self.dfs(nums, target - nums[i], i, path + [nums[i]], res)

.. _39. Combination Sum: https://leetcode.com/problems/combination-sum/


40. Combination Sum II
------------------------------------------------------------

`40. Combination Sum II`_

.. code:: python

   class Solution:
       def combinationSum2(self, candidates: List[int], target: int) -> List[List[int]]:
           res = []
           candidates.sort()
           self.dfs(candidates, target, 0, [], res)
           return res

       def dfs(self, lst, target, index, path, res):
           if target < 0:
               return
           if target == 0:
               res.append(path)
               return res
           for i in range(index, len(lst)):
               if i > index and lst[i] == lst[i-1]:
                   continue
               self.dfs(lst, target - lst[i], i + 1, path + [lst[i]], res)

.. _40. Combination Sum II: https://leetcode.com/problems/combination-sum-ii/


46. Permutations
------------------------------------------------------------

`46. Permutations`_

.. code:: python

   class Solution:
       def permute(self, nums: List[int]) -> List[List[int]]:
           if not nums:
               return []
           res, used = [], [False] * len(nums)
           self.dfs(nums, [], res, used)
           return res

       def dfs(self, nums, path, res, used):
           if len(path) == len(nums):
               res.append(path[:])
               return
           for i in range(len(nums)):
               if used[i]:
                   continue
               used[i] = True
               path.append(nums[i])
               self.dfs(nums, path, res, used)
               path.pop()
               used[i] = False


   """
   # use python characteristic
   class Solution:
       def permute(self, nums: List[int]) -> List[List[int]]:
           if not nums:
               return []
           res = []
           self.dfs(nums, [], res)
           return res

       def dfs(self, nums, path, res):
           if not nums:
               res.append(path)
               return
           for i in range(len(nums)):
               self.dfs(nums[:i] + nums[i+1:], path + [nums[i]], res)
   """

.. _46. Permutations: https://leetcode.com/problems/permutations/


77. Combinations
------------------------------------------------------------

`77. Combinations`_

.. code:: python

   class Solution:
       def combine(self, n: int, k: int) -> List[List[int]]:
           res = []
           self.dfs(range(1, n + 1), k, 0, [], res)
           return res


       def dfs(self, nums, k, idx, path, res):
           if k == 0:
               res.append(path[:])
               return
           for i in range(idx, len(nums)):
               path.append(nums[i])
               self.dfs(nums, k - 1, i + 1, path, res)
               path.pop()

.. _77. Combinations: https://leetcode.com/problems/combinations/


79. Word Search
------------------------------------------------------------

`79. Word Search`_

.. code:: python

   class Solution:
       def exist(self, board: List[List[str]], word: str) -> bool:
           if not board:
               return False
           for i in range(len(board)):
               for j in range(len(board[0])):
                   if self.dfs(board, i, j, word):
                       return True
           return False

       def dfs(self, board, i, j, word):
           if len(word) == 0:
               return True
           if i < 0 or i >= len(board) or j < 0 or j >= len(board[0]) or word[0] != board[i][j]:
               return False
           tmp = board[i][j]
           board[i][j] = '#'
           res = self.dfs(board, i + 1, j, word[1:]) or \
               self.dfs(board, i - 1, j, word[1:]) or \
               self.dfs(board, i, j + 1, word[1:]) or \
               self.dfs(board, i, j - 1, word[1:])
           board[i][j] = tmp
           return res

.. _79. Word Search: https://leetcode.com/problems/word-search/


216. Combination Sum III
------------------------------------------------------------

`216. Combination Sum III`_

.. code:: python

   class Solution:
       def combinationSum3(self, k: int, n: int) -> List[List[int]]:
           res = []
           self.dfs(range(1, 10), k, n, 0, [], res)
           return res

       def dfs(self, nums, k, n, index, path, res):
           if k < 0 or n < 0:
               return
           if k == 0 and n == 0:
               res.append(path)
               return
           for i in range(index, len(nums)):
               self.dfs(nums, k - 1, n - nums[i], i + 1, path + [nums[i]], res)

.. _216. Combination Sum III: https://leetcode.com/problems/combination-sum-iii/


542. 01 Matrix
------------------------------------------------------------

`542. 01 Matrix`_

.. code:: python

   class Solution:
       def updateMatrix(self, matrix: List[List[int]]) -> List[List[int]]:
           # BFS helper
           def bfs(node):
               from collections import deque
               q = deque()
               i, j = node
               q.append(((i, j), 0))  # d (dist to a zero) = 0 initially
               visited = set()
               dirs = [(1, 0), (-1, 0), (0, 1), (0, -1)]
               while q:
                   for i in range(len(q)):
                       coor, d = q.popleft()
                       x, y = coor
                       # if a zero nei is found
                       if matrix[x][y] == 0:
                           return d
                       visited.add(coor)
                       # investiagte neighbours
                       for dir in dirs:
                           newX, newY = x + dir[0], y + dir[1]
                           # within bounds:
                           if newX >= 0 and newX <= len(matrix) - 1 and \
                                   newY >= 0 and newY <= len(matrix[0]) - 1:
                               # not seen:
                               if (newX, newY) not in visited:
                                   q.append(((newX, newY), d + 1))
               return -1

           # main logic #
           '''
           steps:
               - itertate over matrix to find cells = 1
               - pass cells equaling 1 to a bfs to find the closest 0 to them
               - update matrix
           '''
           for i in range(len(matrix)):
               for j in range(len(matrix[0])):
                   if matrix[i][j] == 1:
                       d = bfs((i, j))  # d = closest dist to a 0
                       matrix[i][j] = d  # update M with d
           return matrix

.. _542. 01 Matrix: https://leetcode.com/problems/01-matrix/