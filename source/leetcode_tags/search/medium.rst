=======
Medium
=======


17. Letter Combinations of a Phone Number
------------------------------------------------------------

`17. Letter Combinations of a Phone Number`_

.. code:: python

   # Time: O(3^N * 4^M), Space: O(n)
   # N: (2, 3, 4, 5, 6, 8), M: (7, 9)
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


22. Generate Parentheses
------------------------------------------------------------

`22. Generate Parentheses`_

.. code:: python

   class Solution:
       def generateParenthesis(self, n: int) -> List[str]:
           res = []
           self.helper(n, n, [], res)
           return res

       def helper(self, left_count, right_count, path, res):
           if left_count < 0 or right_count < 0:
               return
           if left_count > right_count:
               return
           if left_count == 0 and right_count == 0:
               res.append(''.join(path))
               return
           self.helper(left_count - 1, right_count, path + ['('], res)
           self.helper(left_count, right_count - 1, path + [')'], res)

.. _22. Generate Parentheses: https://leetcode.com/problems/generate-parentheses/


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

   # Time: O(n!), Space: O(n)
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


47. Permutations II
------------------------------------------------------------

`47. Permutations II`_

.. code:: python

   class Solution:
       def permuteUnique(self, nums: List[int]) -> List[List[int]]:
           if not nums:
               return
           nums.sort()
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
               if i > 0 and nums[i] == nums[i - 1] and not used[i - 1]:
                   continue
               used[i] = True
               path.append(nums[i])
               self.dfs(nums, path, res, used)
               path.pop()
               used[i] = False

   """
   class Solution:
    def permuteUnique(self, nums: List[int]) -> List[List[int]]:
        res = []
        nums.sort()
        self.dfs(nums, [], res)
        return res

    def dfs(self, nums, path, res):
        if not nums:
            res.append(path)
        for i in range(len(nums)):
            if i > 0 and nums[i] == nums[i-1]:
                continue
            self.dfs(nums[:i] + nums[i+1:], path + [nums[i]], res)
   """

.. _47. Permutations II: https://leetcode.com/problems/permutations-ii/


77. Combinations
------------------------------------------------------------

`77. Combinations`_

.. code:: python

   # Time: O(C(n, k)), Space: O(k)
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


200. Number of Islands
------------------------------------------------------------

`200. Number of Islands`_

.. code:: python

   # Time: O(m*n)
   class Solution:
       def numIslands(self, grid: List[List[str]]) -> int:
           if not grid: return 0
           m, n = len(grid), len(grid[0])
           res = 0
           for y in range(m):
               for x in range(n):
                   res += int(grid[y][x]) - 0
                   self.dfs(grid, x, y, m, n)
           return res


       def dfs(self, grid, x, y, m, n):
           if x < 0 or y < 0 or x >= n or y >= m or grid[y][x] == '0':
               return
           grid[y][x] = '0'
           self.dfs(grid, x + 1, y, m, n)
           self.dfs(grid, x - 1, y, m, n)
           self.dfs(grid, x, y + 1, m, n)
           self.dfs(grid, x, y - 1, m, n)

.. _200. Number of Islands: https://leetcode.com/problems/number-of-islands/


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


994. Rotting Oranges
------------------------------------------------------------

`994. Rotting Oranges`_

.. code:: python

   class Solution:
       def orangesRotting(self, grid: List[List[int]]) -> int:
           row, col = len(grid), len(grid[0])
           dirs = [(-1, 0), (0, 1), (1, 0), (0, -1)]
           fresh_set = set()
           rotten = collections.deque()
           step = 0
           for x in range(row):
               for y in range(col):
                   if grid[x][y] == 1:
                       fresh_set.add((x, y))
                   elif grid[x][y] == 2:
                       rotten.append([x, y, step])
           while rotten:
               x, y, step = rotten.popleft()
               for dx, dy in dirs:
                   if 0 <= x + dx < row and 0 <= y + dy < col and grid[x + dx][y + dy] == 1:
                       grid[x + dx][y + dy] = 2
                       fresh_set.remove((x + dx, y + dy))
                       rotten.append([x + dx, y + dy, step + 1])
           return step if not fresh_set else -1

.. _994. Rotting Oranges: https://leetcode.com/problems/rotting-oranges/
