=======
Hard
=======


99. Recover Binary Search Tree
------------------------------------------------------------

`99. Recover Binary Search Tree`_

.. code:: python

   class Solution:
       def recoverTree(self, root: TreeNode) -> None:
           """
           二叉搜索树的中序遍历（元素有递增的）
           test case inOrder: [3, 2, 1]
           正常BST: [1, 2, 3]
           这里我们有个规律发现这两个节点:
           第一个节点，是第一个按照中序遍历时候前一个节点大于后一个节点，我们选取前一个节点，这里指节点3;
           第二个节点，是在第一个节点找到之后，后面出现前一个节点大于后一个节点，我们选择后一个节点，这里指节点1;
           """
           self.prev = TreeNode(float('-inf'))
           self.first, self.second = None, None
           self.inorder(root)
           self.first.val, self.second.val = self.second.val, self.first.val

       def inorder(self, root):
           if not root:
               return
           self.inorder(root.left)
           if not self.first and self.prev.val > root.val:
               self.first, self.second = self.prev, root
           if self.first and self.prev.val > root.val:
               self.second = root
           self.prev = root
           self.inorder(root.right)

.. _99. Recover Binary Search Tree: https://leetcode.com/problems/recover-binary-search-tree/
