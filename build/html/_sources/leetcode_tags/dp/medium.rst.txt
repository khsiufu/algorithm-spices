=======
Medium
=======


5. Longest Palindromic Substring
------------------------------------------------------------

`5. Longest Palindromic Substring`_

.. code:: python

   class Solution:
       # DP, Time: O(n^2), Space: O(n^2)
       # 参考：https://leetcode-cn.com/problems/longest-palindromic-substring/solution/zhong-xin-kuo-san-dong-tai-gui-hua-by-liweiwei1419/
       def longestPalindrome(self, s: str) -> str:
           size = len(s)
           if size < 2:
               return s

           dp = [[False for _ in range(size)] for _ in range(size)]

           max_len = 1
           start = 0

           for i in range(size):
               dp[i][i] = True

           for j in range(1, size):
               for i in range(0, j):
                   if s[i] == s[j]:
                       if j - i < 3:
                           dp[i][j] = True
                       else:
                           dp[i][j] = dp[i + 1][j - 1]
                   else:
                       dp[i][j] = False

                   if dp[i][j]:
                       cur_len = j - i + 1
                       if cur_len > max_len:
                           max_len = cur_len
                           start = i
           return s[start:start + max_len]

       """
       def longestPalindrome(self, s: str) -> str:
           res = ""
           for i in range(len(s)):
               # odd case
               tmp = self.helper(s, i, i)
               if len(tmp) > len(res):
                   res = tmp
               # even case
               tmp = self.helper(s, i, i + 1)
               if len(tmp) > len(res):
                   res = tmp
           return res

       def helper(self, s, l, r):
           while l >= 0 and r < len(s) and s[l] == s[r]:
               l -= 1
               r += 1
           return s[l + 1: r]
       """

.. _5. Longest Palindromic Substring: https://leetcode.com/problems/longest-palindromic-substring/


62. Unique Paths
------------------------------------------------------------

`62. Unique Paths`_

.. code:: python

   class Solution:
       def uniquePaths(self, m: int, n: int) -> int:
           if not m or not n:
               return 0
           dp = [[1 for _ in range(m)] for _ in range(n)]
           for row in range(1, n):
               for col in range(1, m):
                   dp[row][col] = dp[row - 1][col] + dp[row][col - 1]
           return dp[-1][-1]

.. _62. Unique Paths: https://leetcode.com/problems/unique-paths/


64. Minimum Path Sum
------------------------------------------------------------

`64. Minimum Path Sum`_

.. code:: python

   class Solution:
       def minPathSum(self, grid: List[List[int]]) -> int:
           if not grid:
               return 0
           row, col = len(grid), len(grid[0])
           dp = [[0 for _ in range(col)] for _ in range(row)]
           dp[0][0] = grid[0][0]
           for i in range(1, row):
               dp[i][0] = dp[i-1][0] + grid[i][0]
           for i in range(1, col):
               dp[0][i] = dp[0][i-1] + grid[0][i]
           for i in range(1, row):
               for j in range(1, col):
                   dp[i][j] = min(dp[i-1][j], dp[i][j-1]) + grid[i][j]
           return dp[-1][-1]

.. _64. Minimum Path Sum: https://leetcode.com/problems/minimum-path-sum/


91. Decode Ways
------------------------------------------------------------

`91. Decode Ways`_

.. code:: python

   # DP, Time: O(n), Space: O(n)
   class Solution:
       def numDecodings(self, s: str) -> int:
           if not s:
               return 0
           size = len(s)
           dp = [1] + [0] * size
           for i in range(1, size + 1):
               if s[i - 1] != '0':
                   dp[i] += dp[i - 1]
               if i >= 2 and 10 <= int(s[i - 2: i]) <= 26:
                   dp[i] += dp[i - 2]
           return dp[-1]

.. _91. Decode Ways: https://leetcode.com/problems/decode-ways/


95. Unique Binary Search Trees II
------------------------------------------------------------

`95. Unique Binary Search Trees II`_

.. code:: python

   class Solution:
       def generateTrees(self, n: int) -> List[TreeNode]:
           def generate(l, r):   # split between [l, r)
               if l == r:
                   return [None]
               nodes = []
               for i in range(l, r):
                   for lchild in generate(l, i):
                       for rchild in generate(i+1, r):
                           node = TreeNode(i+1)   # +1 to convert the index to the actual value
                           node.left = lchild
                           node.right = rchild
                           nodes.append(node)
               return nodes
           return generate(0, n) if n else []

.. _95. Unique Binary Search Trees II: https://leetcode.com/problems/unique-binary-search-trees-ii/


96. Unique Binary Search Trees
------------------------------------------------------------

`96. Unique Binary Search Trees`_

.. code:: python

   class Solution:
       def numTrees(self, n: int) -> int:
           res = [0] * (n + 1)
           res[0] = 1
           for i in range(1, n + 1):
               for j in range(i):
                   res[i] += res[j] * res[i-1-j]
           return res[n]

.. _96. Unique Binary Search Trees: https://leetcode.com/problems/unique-binary-search-trees/


120. Triangle
------------------------------------------------------------

`120. Triangle`_

.. code:: python

   class Solution:
       def minimumTotal(self, triangle: List[List[int]]) -> int:
           if not triangle:
               return 0
           res = triangle[-1]
           for i in range(len(triangle) - 2, -1, -1):
               for j in range(len(triangle[i])):
                   res[j] = min(res[j], res[j+1]) + triangle[i][j]
           return res[0]

.. _120. Triangle: https://leetcode.com/problems/triangle/


213. House Robber II
------------------------------------------------------------

`213. House Robber II`_

.. code:: python

   # Time: O(n), Space: O(1)
   class Solution:
       def rob(self, nums: List[int]) -> int:
           if not nums:
               return 0
           if len(nums) == 1:
               return nums[0]
           return max(self.helper(nums[:-1]), self.helper(nums[1:]))

       def helper(self, nums):
           if not nums:
               return 0
           if len(nums) == 1:
               return nums[0]
           a, b = nums[0], max(nums[:2])
           for i in range(2, len(nums)):
               a, b = b, max(b, a + nums[i])
           return b

.. _213. House Robber II: https://leetcode.com/problems/house-robber-ii/


279. Perfect Squares
------------------------------------------------------------

`279. Perfect Squares`_

.. code:: python

   # Time: O(n * n ^ 0.5), Space: O(n)
   class Solution:
       def numSquares(self, n: int) -> int:
           dp = [i for i in range(n + 1)]
           for i in range(2, n + 1):
               for j in range(1, int(i ** 0.5) + 1):
                   dp[i] = min(dp[i], dp[i - j * j] + 1)
           return dp[-1]

.. _279. Perfect Squares: https://leetcode.com/problems/perfect-squares/


300. Longest Increasing Subsequence
------------------------------------------------------------

`300. Longest Increasing Subsequence`_

.. code:: python

   # Time: O(n^2), Space: O(n)
   class Solution:
       def lengthOfLIS(self, nums: List[int]) -> int:
           if not nums:
               return 0
           dp = [1] * len(nums)
           for i in range(len(nums)):
               for j in range(i):
                   # 如果要求非严格递增，将此行 '<' 改为 '<=' 即可。
                    if nums[j] < nums[i]:
                       dp[i] = max(dp[i], dp[j] + 1)
           return max(dp)

.. _300. Longest Increasing Subsequence: https://leetcode.com/problems/longest-increasing-subsequence/


322. Coin Change
------------------------------------------------------------

`322. Coin Change`_

.. code:: python

   class Solution:
       def coinChange(self, coins: List[int], amount: int) -> int:
           dp = [float('inf')] * (amount + 1)
           dp[0] = 0

           for coin in coins:
               for x in range(coin, amount + 1):
                   dp[x] = min(dp[x], dp[x - coin] + 1)
           return dp[amount] if dp[amount] != float('inf') else -1

.. _322. Coin Change: https://leetcode.com/problems/coin-change/


494. Target Sum
------------------------------------------------------------

`494. Target Sum`_

.. code:: python

   class Solution:
       def findTargetSumWays(self, nums: List[int], S: int) -> int:
           ## RC ##
           ## APPROACH : DP ##
           ## INTUITION : THINK LIKE SUBSET SUM PROBLEM (tushor roy DP solution) Leetcode 416. Partition equal subset sum ##
           # but here  1. our target can range from -totalSum to +totalSum
           #           2. and we dont include True directly from above sequence, coz it is not subsequence we are looking for. so here consider if and only if previous value exists
           # [1,1,1,1,1]
           # 3
           # [
           #   [0, 0, 0, 0, 1, 0, 1, 0, 0, 0, 0],
           #   [0, 0, 0, 1, 0, 2, 0, 1, 0, 0, 0],
           #   [0, 0, 1, 0, 3, 0, 3, 0, 1, 0, 0],
           #   [0, 1, 0, 4, 0, 6, 0, 4, 0, 1, 0],
           #   [1, 0, 5, 0, 10, 0, 10, 0, 5, 0, 1]
           # ]

           ## TIME COMPLEXITY : O(N^2) ##
           ## SPACE COMPLEXITY : O(N^2) ##

           totalSum = sum(nums)
           if(S not in range(-1 * totalSum, totalSum + 1) ): return 0
           dp = [ [ 0 for j in range( totalSum*2 + 1 ) ] for i in range(len(nums))]

           ## BASE CASE ## FIRST ROW ##
           dp[0][totalSum + nums[0]] += 1
           dp[0][totalSum - nums[0]] += 1

           for i in range(1, len(nums)):
               for j in range( totalSum*2 + 1 ):

                   if( j - nums[i] >= 0 and dp[i-1][j-nums[i]] > 0 ):          # left side
                       dp[i][j] += dp[i-1][j-nums[i]]

                   if( j + nums[i] <= totalSum*2 and dp[i-1][j+nums[i]] > 0 ): # right side
                       dp[i][j] += dp[i-1][j+nums[i]]

           return dp[-1][totalSum + S]

           ## APPROACH : BACKTRACKING + MEMOIZATION ##
           def dfs(curr, nums):
               key = (curr, tuple(nums))
               if key in cache: return cache[key]
               if not nums: return 1 if curr == S else 0
               res = dfs(curr - nums[0], nums[1:]) + dfs(curr + nums[0], nums[1:])
               cache[key] = res
               return res
           cache = {}
           return dfs(0, nums)

.. _494. Target Sum: https://leetcode.com/problems/target-sum/
