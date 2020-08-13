=======
Hard
=======


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
