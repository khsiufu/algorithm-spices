=========================
Tree Traversal
=========================


-  preorder
-  inorder
-  postorder


.. code:: python

   class TreeNode(object):
       def __init__(self, x):
           self.val = x
           self.left = None
           self.right = None

   def make_tree(lst):
       node = None
       if not lst:
           return
       if lst[0] is not None:
           node = TreeNode(lst.pop(0))
           node.left = make_tree(lst)
           node.right = make_tree(lst)
       else:
           lst.pop(0)
       return node

   def inorder(root, res):
       if not root:
           return
       inorder(root.left, res)
       res.append(root.val)
       inorder(root.right, res)

   """
   def preorder(root, res):
       if not root:
           return
       res.append(root.val)
       preorder(root.left, res)
       preorder(root.right, res)

   def postorder(root, res):
       if not root:
           return
       postorder(root.left, res)
       postorder(root.right, res)
       res.append(root.val)
   """

   def main():
       lst = [1, None, 2, 3]
       root = make_tree(lst)
       res = []
       inorder(root, res)
       print(res)


   if __name__ == '__main__':
       main()
