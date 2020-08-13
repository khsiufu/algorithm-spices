=======
Medium
=======


98. Validate Binary Search Tree
------------------------------------------------------------

`98. Validate Binary Search Tree`_

.. code:: python

   class Solution:
       def isValidBST(self, root: TreeNode) -> bool:
           return self.helper(root, float('-inf'), float('inf'))

       def helper(self, root, lower, upper):
           if not root:
               return True
           return root.val > lower and root.val < upper \
               and self.helper(root.left, lower, root.val) \
               and self.helper(root.right, root.val, upper)

.. _98. Validate Binary Search Tree: https://leetcode.com/problems/validate-binary-search-tree/


109. Convert Sorted List to Binary Search Tree
------------------------------------------------------------

`109. Convert Sorted List to Binary Search Tree`_

.. code:: python

   class Solution:
       def sortedListToBST(self, head: ListNode) -> TreeNode:
           lst = []
           while head:
               lst.append(head.val)
               head = head.next
           return self.helper(lst, 0, len(lst) - 1)

       def helper(self, lst, start, end):
           if start > end:
               return None
           if start == end:
               return TreeNode(lst[start])
           mid = (start + end) >> 1
           root = TreeNode(lst[mid])
           root.left = self.helper(lst, start, mid - 1)
           root.right = self.helper(lst, mid + 1, end)
           return root

.. _109. Convert Sorted List to Binary Search Tree: https://leetcode.com/problems/convert-sorted-list-to-binary-search-tree/


1038. Binary Search Tree to Greater Sum Tree
------------------------------------------------------------

`1038. Binary Search Tree to Greater Sum Tree`_

.. code:: python

   class Solution:
       def bstToGst(self, root: TreeNode) -> TreeNode:
           self.sum = 0
           self.helper(root)
           return root

       def helper(self, node):
           if not node:
               return
           self.helper(node.right)
           node.val += self.sum
           self.sum = node.val
           self.helper(node.left)

.. _1038. Binary Search Tree to Greater Sum Tree: https://leetcode.com/problems/binary-search-tree-to-greater-sum-tree/
