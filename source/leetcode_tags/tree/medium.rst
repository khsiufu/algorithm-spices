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

.. code:: go

   func inorderTraversal(root *TreeNode) []int {
       res := []int{}
       dfs(root, &res)
       return res
   }

   func dfs(node *TreeNode, res *[]int) {
       if node == nil {
           return
       }
       dfs(node.Left, res)
       *res = append(*res, node.Val)
       dfs(node.Right, res)
   }

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

.. code:: go

   func levelOrder(root *TreeNode) [][]int {
       res := [][]int{}
       dfs(root, 0, &res)
       return res
   }

   func dfs(node *TreeNode, level int, res *[][]int) {
       if node == nil {
           return
       }
       if len(*res) <= level {
           *res = append(*res, []int{})
       }
       (*res)[level] = append((*res)[level], node.Val)
       dfs(node.Left, level + 1, res)
       dfs(node.Right, level + 1, res)
   }

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

.. code:: go

   func bfs(s *[][]int, level int, root *TreeNode)  {
       if root == nil {
           return
       }

       if len(*s) == level {
           *s = append(*s, []int{})
       }

       if level % 2 == 1 {
           (*s)[level] = append([]int{root.Val}, (*s)[level]...)
       } else {
           (*s)[level] = append((*s)[level], root.Val)
       }
       for _, v := range []*TreeNode{root.Left, root.Right} {
           bfs(s, level + 1, v)
       }
   }

   func zigzagLevelOrder(root *TreeNode) [][]int {
       if root == nil {
           return [][]int{}
       }
       var s [][]int
       bfs(&s, 0, root)
       return s
   }

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

.. code:: go

   func buildTree(preorder []int, inorder []int) *TreeNode {
       if len(preorder) == 0 || len(inorder) == 0 {
           return nil
       }
       i := find(preorder[0], inorder)
       left := buildTree(preorder[1:i+1], inorder[:i])
       right := buildTree(preorder[i+1:], inorder[i+1:])
       return &TreeNode{
           Val: preorder[0],
           Left: left,
           Right: right,
       }
   }

   func find(target int, nums []int) int {
       for i, x := range nums {
           if x == target {
               return i
           }
       }
       return -1
   }

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

.. code:: go

   func buildTree(inorder []int, postorder []int) *TreeNode {
       if len(inorder) == 0 || len(postorder) == 0 {
           return nil
       }
       j := len(postorder)-1
       i := find(postorder[j], inorder)
       left := buildTree(inorder[:i], postorder[:i])
       right := buildTree(inorder[i+1:], postorder[i:j])
       return &TreeNode{
           Val: postorder[j],
           Left: left,
           Right: right,
       }
   }

   func find(target int, nums []int) int {
       for i, x := range nums {
           if x == target {
               return i
           }
       }
       return -1
   }

.. _106. Construct Binary Tree from Inorder and Postorder Traversal: https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/
