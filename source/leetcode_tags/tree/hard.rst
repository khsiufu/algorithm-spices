=======
Hard
=======


124. Binary Tree Maximum Path Sum
-----------------------------------------------------------------

`124. Binary Tree Maximum Path Sum`_

.. code:: python

   class Solution:
       def maxPathSum(self, root: TreeNode) -> int:
           self.res = float('-inf')
           self.dfs(root)
           return self.res

       def dfs(self, root):
           if not root:
               return 0
           l = max(0, self.dfs(root.left))
           r = max(0, self.dfs(root.right))
           self.res = max(self.res, l + r + root.val)
           return max(l, r) + root.val

.. _124. Binary Tree Maximum Path Sum: https://leetcode.com/problems/binary-tree-maximum-path-sum/


145. Binary Tree Postorder Traversal
-----------------------------------------------------------------

`145. Binary Tree Postorder Traversal`_

.. code:: python

   class Solution:
       def postorderTraversal(self, root: TreeNode) -> List[int]:
           res = []
           self.dfs(root, res)
           return res

       def dfs(self, root, res):
           if not root:
               return
           self.dfs(root.left, res)
           self.dfs(root.right, res)
           res.append(root.val)

.. _145. Binary Tree Postorder Traversal: https://leetcode.com/problems/binary-tree-postorder-traversal/
