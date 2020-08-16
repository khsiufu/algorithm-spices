=======
Easy
=======


100. Same Tree
------------------------------------------------------------

`100. Same Tree`_

.. code:: python

   class Solution:
       def isSameTree(self, p: TreeNode, q: TreeNode) -> bool:
           if not p and not q:
               return True
           if not p or not q:
               return False
           return p.val == q.val and self.isSameTree(p.left, q.left) and \
               self.isSameTree(p.right, q.right)

.. _100. Same Tree: https://leetcode.com/problems/same-tree/


101. Symmetric Tree
------------------------------------------------------------

`101. Symmetric Tree`_

.. code:: python

   class Solution:
       def isSymmetric(self, root: TreeNode) -> bool:
           if not root:
               return True
           return self.helper(root.left, root.right)

       def helper(self, left, right):
           if not left and not right:
               return True
           if not left or not right:
               return False
           if left.val != right.val:
               return False
           return self.helper(left.left, right.right) and self.helper(left.right, right.left)

.. _101. Symmetric Tree: https://leetcode.com/problems/symmetric-tree/


104. Maximum Depth of Binary Tree
------------------------------------------------------------

`104. Maximum Depth of Binary Tree`_

.. code:: python

   class Solution:
       def maxDepth(self, root: TreeNode) -> int:
           if not root:
               return 0
           return max(self.maxDepth(root.left), self.maxDepth(root.right)) + 1

.. _104. Maximum Depth of Binary Tree: https://leetcode.com/problems/maximum-depth-of-binary-tree/


107. Binary Tree Level Order Traversal II
------------------------------------------------------------

`107. Binary Tree Level Order Traversal II`_

.. code:: python

   class Solution:
       """
       def levelOrderBottom(self, root: TreeNode) -> List[List[int]]:
           # BFS + Queue
           queue, res = collections.deque([(root, 0)]), []
           while queue:
               node, level = queue.popleft()
               if node:
                   if len(res) < level + 1:
                       res.append([])
                   res[level].append(node.val)
                   queue.append((node.left, level + 1))
                   queue.append((node.right, level + 1))
           return res[::-1]
       """

       def levelOrderBottom(self, root: TreeNode) -> List[List[int]]:
           # DFS
           res = []
           self.dfs(root, 0, res)
           return res

       def dfs(self, root, level, res):
           if root:
               if len(res) < level + 1:
                   res.insert(0, [])
               res[-(level + 1)].append(root.val)
               self.dfs(root.left, level + 1, res)
               self.dfs(root.right, level + 1, res)

.. _107. Binary Tree Level Order Traversal II: https://leetcode.com/problems/binary-tree-level-order-traversal-ii/


110. Balanced Binary Tree
------------------------------------------------------------

`110. Balanced Binary Tree`_

.. code:: python

   class Solution:
       def isBalanced(self, root: TreeNode) -> bool:
           return self.helper(root)[1]

       def helper(self, root):
           if not root:
               return (0, True)
           l_depth, l_balanced = self.helper(root.left)
           r_depth, r_balanced = self.helper(root.right)
           return max(l_depth, r_depth) + 1, l_balanced and r_balanced and abs(l_depth - r_depth) <= 1

.. _110. Balanced Binary Tree: https://leetcode.com/problems/balanced-binary-tree/


108. Convert Sorted Array to Binary Search Tree
------------------------------------------------------------

`108. Convert Sorted Array to Binary Search Tree`_

.. code:: python

   class Solution:
       def sortedArrayToBST(self, nums: List[int]) -> TreeNode:
           l, r = 0, len(nums) - 1
           if l <= r:
               m = l + (r - l) // 2
               root = TreeNode(nums[m])
               root.left = self.sortedArrayToBST(nums[:m])
               root.right = self.sortedArrayToBST(nums[m+1:])
               return root

.. _108. Convert Sorted Array to Binary Search Tree: https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/


111. Minimum Depth of Binary Tree
-----------------------------------------------------------------

`111. Minimum Depth of Binary Tree`_

.. code:: python

   class Solution:
       def minDepth(self, root: TreeNode) -> int:
           if not root:
               return 0
           if None in [root.left, root.right]:
               return max(self.minDepth(root.left), self.minDepth(root.right)) + 1
           else:
               return min(self.minDepth(root.left), self.minDepth(root.right)) + 1

.. _111. Minimum Depth of Binary Tree: https://leetcode.com/problems/minimum-depth-of-binary-tree/


112. Path Sum
-----------------------------------------------------------------

`112. Path Sum`_

.. code:: python

   class Solution:
       def hasPathSum(self, root: TreeNode, sum: int) -> bool:
           if not root:
               return False
           if not root.left and not root.right:
               return sum == root.val
           return self.hasPathSum(root.left, sum - root.val) or \
               self.hasPathSum(root.right, sum - root.val)

.. _112. Path Sum: https://leetcode.com/problems/path-sum/
