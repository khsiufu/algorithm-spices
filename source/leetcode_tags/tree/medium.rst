=======
Medium
=======


94. Binary Tree Inorder Traversal
------------------------------------------------------------

`94. Binary Tree Inorder Traversal`_

.. code:: python

   class Solution:
       def inorderTraversal(self, root: TreeNode) -> List[int]:
           res = []
           self.helper(root, res)
           return res


       def helper(self, root, res):
           if not root:
               return
           self.helper(root.left, res)
           res.append(root.val)
           self.helper(root.right, res)

.. _94. Binary Tree Inorder Traversal: https://leetcode.com/problems/binary-tree-inorder-traversal/


102. Binary Tree Level Order Traversal
------------------------------------------------------------

`102. Binary Tree Level Order Traversal`_

.. code:: python

   class Solution:
       """
       # DFS
       def levelOrder(self, root: TreeNode) -> List[List[int]]:
           res = []
           self.dfs(root, 0, res)
           return res

       def dfs(self, root, level, res):
           if not root:
               return
           if len(res) <= level:
               res.append([])
           res[level].append(root.val)
           self.dfs(root.left, level + 1, res)
           self.dfs(root.right, level + 1, res)
       """

       # BFS + Queue
       def levelOrder(self, root: TreeNode) -> List[List[int]]:
           res, queue = [], [(root, 0)]
           while queue:
               node, level = queue.pop(0)
               if node:
                   if len(res) <= level:
                       res.append([])
                   res[level].append(node.val)
                   queue.append((node.left, level + 1))
                   queue.append((node.right, level + 1))
           return res

.. _102. Binary Tree Level Order Traversal: https://leetcode.com/problems/binary-tree-level-order-traversal/


103. Binary Tree Zigzag Level Order Traversal
------------------------------------------------------------

`103. Binary Tree Zigzag Level Order Traversal`_

.. code:: python

   class Solution:
       def zigzagLevelOrder(self, root: TreeNode) -> List[List[int]]:
           res = []
           self.dfs(root, 0, res)
           return res

       def dfs(self, root, level, res):
           if not root:
               return
           if len(res) <= level:
               res.append([])
           if level % 2 == 0:
               res[level].append(root.val)
           else:
               res[level].insert(0, root.val)
           self.dfs(root.left, level + 1, res)
           self.dfs(root.right, level + 1, res)
       """
       def zigzagLevelOrder(self, root: TreeNode) -> List[List[int]]:
           res, queue = [], [(root, 0)]
           while queue:
               curr, level = queue.pop(0)
               if curr:
                   if len(res) <= level:
                       res.append([])
                   if level % 2 == 0:
                       res[level].append(curr.val)
                   else:
                       res[level].insert(0, curr.val)
                   queue.append((curr.left, level + 1))
                   queue.append((curr.right, level + 1))
           return res
       """

.. _103. Binary Tree Zigzag Level Order Traversal: https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/


105. Construct Binary Tree from Preorder and Inorder Traversal
-----------------------------------------------------------------

`105. Construct Binary Tree from Preorder and Inorder Traversal`_

.. code:: python

   class Solution:
       def buildTree(self, preorder: List[int], inorder: List[int]) -> TreeNode:
           if not preorder or not inorder:
               return None
           return self.helper(preorder, 0, len(preorder) - 1, inorder, 0, len(inorder) - 1)

       def helper(self, preorder, p_left, p_right, inorder, i_left, i_right):
           if p_left > p_right:
               return None
           if p_left == p_right:
               return TreeNode(preorder[p_left])
           idx = inorder.index(preorder[p_left])
           left_len = idx - i_left
           root = TreeNode(preorder[p_left])
           root.left = self.helper(preorder, p_left + 1, p_left + left_len, inorder, i_left, idx - 1)
           root.right = self.helper(preorder, p_left + left_len + 1, p_right, inorder, idx + 1, i_right)
           return root

.. _105. Construct Binary Tree from Preorder and Inorder Traversal: https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/


106. Construct Binary Tree from Inorder and Postorder Traversal
-----------------------------------------------------------------

`106. Construct Binary Tree from Inorder and Postorder Traversal`_

.. code:: python

   class Solution:
       def buildTree(self, inorder: List[int], postorder: List[int]) -> TreeNode:
           if not inorder or not postorder:
               return None
           return self.helper(inorder, 0, len(inorder) - 1, postorder, 0, len(postorder) - 1)

       def helper(self, inorder, i_left, i_right, postorder, p_left, p_right):
           if i_left > i_right:
               return None
           if i_left == i_right:
               return TreeNode(postorder[p_right])
           idx = inorder.index(postorder[p_right])
           left_len = idx - i_left
           root = TreeNode(postorder[p_right])
           root.left = self.helper(inorder, i_left, idx - 1, postorder, p_left, p_left + left_len - 1)
           root.right = self.helper(inorder, idx + 1, i_right, postorder, p_left + left_len , p_right - 1)
           return root

.. _106. Construct Binary Tree from Inorder and Postorder Traversal: https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/


113. Path Sum II
-----------------------------------------------------------------

`113. Path Sum II`_

.. code:: python

   class Solution:
       def pathSum(self, root: TreeNode, sum: int) -> List[List[int]]:
           if not root:
               return []
           res = []
           self.dfs(root, sum, [], res)
           return res

       def dfs(self, root, sum, path, res):
           if not root.left and not root.right and sum == root.val:
               path.append(root.val)
               res.append(path)
           if root.left:
               self.dfs(root.left, sum - root.val, path + [root.val], res)
           if root.right:
               self.dfs(root.right, sum - root.val, path + [root.val], res)

.. _113. Path Sum II: https://leetcode.com/problems/path-sum-ii/


114. Flatten Binary Tree to Linked List
------------------------------------------------------

`114. Flatten Binary Tree to Linked List`_

.. code:: python

   class Solution:
       def flatten(self, root: TreeNode) -> None:
           if not root:
               return None
           self.flatten(root.left)
           self.flatten(root.right)

           if not root.left:
               return None

           node = root.left
           while node.right:
               node = node.right

           node.right = root.right
           root.right = root.left
           root.left = None

.. _114. Flatten Binary Tree to Linked List: https://leetcode.com/problems/flatten-binary-tree-to-linked-list/


144. Binary Tree Preorder Traversal
-----------------------------------------------------------------

`144. Binary Tree Preorder Traversal`_

.. code:: python

   class Solution:
       def preorderTraversal(self, root: TreeNode) -> List[int]:
           res = []
           self.dfs(root, res)
           return res

       def dfs(self, root, res):
           if not root:
               return
           res.append(root.val)
           self.dfs(root.left, res)
           self.dfs(root.right, res)

.. _144. Binary Tree Preorder Traversal: https://leetcode.com/problems/binary-tree-preorder-traversal/


199. Binary Tree Right Side View
-----------------------------------------------------------------

`199. Binary Tree Right Side View`_

.. code:: python

   class Solution:
       def rightSideView(self, root: TreeNode) -> List[int]:
           res = []
           self.dfs(root, 0, res)
           return [x[0] for x in res]

       def dfs(self, root, level, res):
           if not root:
               return
           if len(res) <= level:
               res.append([])
           res[level].append(root.val)
           self.dfs(root.right, level + 1, res)
           self.dfs(root.left, level + 1, res)

.. _199. Binary Tree Right Side View: https://leetcode.com/problems/binary-tree-right-side-view/
