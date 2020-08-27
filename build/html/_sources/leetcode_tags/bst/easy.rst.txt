=======
Easy
=======


235. Lowest Common Ancestor of a Binary Search Tree
------------------------------------------------------------

`235. Lowest Common Ancestor of a Binary Search Tree`_

.. code:: python

   class Solution:
       def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
           if not root:
               return None
           if (root.val - p.val) * (root.val - q.val) <= 0:
               return root
           elif root.val > p.val and root.val > q.val:
               return self.lowestCommonAncestor(root.left, p, q)
           else:
               return self.lowestCommonAncestor(root.right, p, q)

.. _235. Lowest Common Ancestor of a Binary Search Tree: https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/


700. Search in a Binary Search Tree
------------------------------------------------------------

`700. Search in a Binary Search Tree`_

.. code:: python

   class Solution:
       def searchBST(self, root: TreeNode, val: int) -> TreeNode:
           if not root:
               return
           if root.val == val:
               return root
           elif root.val < val:
               return self.searchBST(root.right, val)
           else:
               return self.searchBST(root.left, val)

.. _700. Search in a Binary Search Tree: https://leetcode.com/problems/search-in-a-binary-search-tree/
