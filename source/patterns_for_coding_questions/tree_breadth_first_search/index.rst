Binary Tree Level Order Traversal (easy)
-----------------------------------------
.. code:: python

   '''
   Problem Statement
   Given a binary tree, populate an array to represent its level-by-level traversal.
   You should populate the values of all nodes of each level from left to right in separate sub-arrays.
   '''

   # mycode
   class TreeNode:
       def __init__(self, val):
           self.val = val
           self.left, self.right = None, None


   def traverse(root):
       from collections import deque

       queue, res = deque([(root, 0)]), []
       while queue:
           node, level = queue.popleft()
           if node:
               if len(res) < level + 1:
                   res.append([])
               res[level].append(node.val)
               queue.append((node.left, level + 1))
               queue.append((node.right, level + 1))
       return res


   def main():
       root = TreeNode(12)
       root.left = TreeNode(7)
       root.right = TreeNode(1)
       root.left.left = TreeNode(9)
       root.right.left = TreeNode(10)
       root.right.right = TreeNode(5)
       print("Level order traversal: " + str(traverse(root)))


   main()

   # answer
   from collections import deque


   class TreeNode:
       def __init__(self, val):
           self.val = val
           self.left, self.right = None, None


   def traverse(root):
       result = []
       if root is None:
           return result

       queue = deque()
       queue.append(root)
       while queue:
           levelSize = len(queue)
           currentLevel = []
           for _ in range(levelSize):
               currentNode = queue.popleft()
               # add the node to the current level
               currentLevel.append(currentNode.val)
               # insert the children of current node in the queue
               if currentNode.left:
                   queue.append(currentNode.left)
               if currentNode.right:
                   queue.append(currentNode.right)

           result.append(currentLevel)

       return result


   def main():
       root = TreeNode(12)
       root.left = TreeNode(7)
       root.right = TreeNode(1)
       root.left.left = TreeNode(9)
       root.right.left = TreeNode(10)
       root.right.right = TreeNode(5)
       print("Level order traversal: " + str(traverse(root)))


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(N), where ‘N’ is the total number of nodes in the tree.
   This is due to the fact that we traverse each node once.
   Space complexity
   The space complexity of the above algorithm will be O(N) as we need to return a list containing the level order traversal.
   We will also need O(N) space for the queue. Since we can have a maximum of N/2 nodes at any level (this could happen only at the lowest level),
   therefore we will need O(N) space to store them in the queue.
   '''

Reverse Level Order Traversal (easy)
-----------------------------------------
.. code:: python

   '''
   Problem Statement
   Given a binary tree, populate an array to represent its level-by-level traversal in reverse order, i.e., the lowest level comes first.
   You should populate the values of all nodes in each level from left to right in separate sub-arrays.
   '''

   # mycode
   class TreeNode:
       def __init__(self, val):
           self.val = val
           self.left, self.right = None, None


   def traverse(root):
       from collections import deque

       queue, res = deque([(root, 0)]), []
       while queue:
           node, level = queue.popleft()
           if node:
               if len(res) < level + 1:
                   res.append([])
               res[level].append(node.val)
               queue.append((node.left, level + 1))
               queue.append((node.right, level + 1))
       return res[::-1]


   def main():
       root = TreeNode(12)
       root.left = TreeNode(7)
       root.right = TreeNode(1)
       root.left.left = TreeNode(9)
       root.right.left = TreeNode(10)
       root.right.right = TreeNode(5)
       print("Reverse level order traversal: " + str(traverse(root)))


   main()

   # answer
   from collections import deque


   class TreeNode:
       def __init__(self, val):
           self.val = val
           self.left, self.right = None, None


   def traverse(root):
       result = deque()
       if root is None:
           return result

       queue = deque()
       queue.append(root)
       while queue:
           levelSize = len(queue)
           currentLevel = []
           for _ in range(levelSize):
               currentNode = queue.popleft()
               # add the node to the current level
               currentLevel.append(currentNode.val)
               # insert the children of current node in the queue
               if currentNode.left:
                   queue.append(currentNode.left)
               if currentNode.right:
                   queue.append(currentNode.right)

           result.appendleft(currentLevel)

       return result


   def main():
       root = TreeNode(12)
       root.left = TreeNode(7)
       root.right = TreeNode(1)
       root.left.left = TreeNode(9)
       root.right.left = TreeNode(10)
       root.right.right = TreeNode(5)
       print("Reverse level order traversal: " + str(traverse(root)))


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(N), where ‘N’ is the total number of nodes in the tree.
   This is due to the fact that we traverse each node once.
   Space complexity
   The space complexity of the above algorithm will be O(N) as we need to return a list containing the level order traversal.
   We will also need O(N) space for the queue. Since we can have a maximum of N/2 nodes at any level (this could happen only at the lowest level),
   therefore we will need O(N) space to store them in the queue.
   '''

Zigzag Traversal (medium)
-----------------------------------------
.. code:: python

   '''
   Problem Statement
   Given a binary tree, populate an array to represent its zigzag level order traversal.
   You should populate the values of all nodes of the first level from left to right,
   then right to left for the next level and keep alternating in the same manner for the following levels.
   '''

   # mycode
   class TreeNode:
       def __init__(self, val):
           self.val = val
           self.left, self.right = None, None


   def traverse(root):
       from collections import deque

       res, queue = [], deque([(root, 0)])
       while queue:
           node, level = queue.popleft()
           if node:
               if len(res) < level + 1:
                   res.append([])
               if level % 2 == 0:
                   res[level].append(node.val)
               else:
                   res[level].insert(0, node.val)
               queue.append((node.left, level + 1))
               queue.append((node.right, level + 1))
       return res


   def main():
       root = TreeNode(12)
       root.left = TreeNode(7)
       root.right = TreeNode(1)
       root.left.left = TreeNode(9)
       root.right.left = TreeNode(10)
       root.right.right = TreeNode(5)
       root.right.left.left = TreeNode(20)
       root.right.left.right = TreeNode(17)
       print("Zigzag traversal: " + str(traverse(root)))


   main()

   # answer
   from collections import deque


   class TreeNode:
       def __init__(self, val):
           self.val = val
           self.left, self.right = None, None


   def traverse(root):
       result = []
       if root is None:
           return result

       queue = deque()
       queue.append(root)
       leftToRight = True
       while queue:
           levelSize = len(queue)
           currentLevel = deque()
           for _ in range(levelSize):
               currentNode = queue.popleft()

               # add the node to the current level based on the traverse direction
               if leftToRight:
                   currentLevel.append(currentNode.val)
               else:
                   currentLevel.appendleft(currentNode.val)

               # insert the children of current node in the queue
               if currentNode.left:
                   queue.append(currentNode.left)
               if currentNode.right:
                   queue.append(currentNode.right)

           result.append(list(currentLevel))
           # reverse the traversal direction
           leftToRight = not leftToRight

       return result


   def main():
       root = TreeNode(12)
       root.left = TreeNode(7)
       root.right = TreeNode(1)
       root.left.left = TreeNode(9)
       root.right.left = TreeNode(10)
       root.right.right = TreeNode(5)
       root.right.left.left = TreeNode(20)
       root.right.left.right = TreeNode(17)
       print("Zigzag traversal: " + str(traverse(root)))


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(N), where ‘N’ is the total number of nodes in the tree.
   This is due to the fact that we traverse each node once.
   Space complexity
   The space complexity of the above algorithm will be O(N) as we need to return a list containing the level order traversal.
   We will also need O(N) space for the queue. Since we can have a maximum of N/2 nodes at any level (this could happen only at the lowest level),
   therefore we will need O(N) space to store them in the queue.
   '''

Level Averages in a Binary Tree (easy)
-----------------------------------------
.. code:: python

   '''
   Problem Statement
   Given a binary tree, populate an array to represent the averages of all of its levels.
   '''

   # mycode
   class TreeNode:
       def __init__(self, val):
           self.val = val
           self.left, self.right = None, None


   def find_level_averages(root):
       from collections import deque
       res, queue = [], deque([(root, 0)])
       while queue:
           node, level = queue.popleft()
           if node:
               if len(res) < level + 1:
                   res.append([])
               res[level].append(node.val)
               queue.append((node.left, level + 1))
               queue.append((node.right, level + 1))
       res = [sum(x) // len(x) for x in res]
       return res


   def main():
       root = TreeNode(12)
       root.left = TreeNode(7)
       root.right = TreeNode(1)
       root.left.left = TreeNode(9)
       root.left.right = TreeNode(2)
       root.right.left = TreeNode(10)
       root.right.right = TreeNode(5)
       print("Level averages are: " + str(find_level_averages(root)))


   main()

   # answer
   from collections import deque


   class TreeNode:
       def __init__(self, val):
           self.val = val
           self.left, self.right = None, None


   def find_level_averages(root):
       result = []
       if root is None:
           return result

       queue = deque()
       queue.append(root)
       while queue:
           levelSize = len(queue)
           levelSum = 0.0
           for _ in range(levelSize):
               currentNode = queue.popleft()
               # add the node's value to the running sum
               levelSum += currentNode.val
               # insert the children of current node to the queue
               if currentNode.left:
                   queue.append(currentNode.left)
               if currentNode.right:
                   queue.append(currentNode.right)

           # append the current level's average to the result array
           result.append(levelSum / levelSize)

       return result


   def main():
       root = TreeNode(12)
       root.left = TreeNode(7)
       root.right = TreeNode(1)
       root.left.left = TreeNode(9)
       root.left.right = TreeNode(2)
       root.right.left = TreeNode(10)
       root.right.right = TreeNode(5)
       print("Level averages are: " + str(find_level_averages(root)))


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(N), where ‘N’ is the total number of nodes in the tree.
   This is due to the fact that we traverse each node once.
   Space complexity
   The space complexity of the above algorithm will be O(N)O which is required for the queue.
   Since we can have a maximum of N/2 nodes at any level (this could happen only at the lowest level),
   therefore we will need O(N) space to store them in the queue.
   '''

Minimum Depth of a Binary Tree (easy)
-----------------------------------------
.. code:: python

   '''
   Problem Statement
   Find the minimum depth of a binary tree.
   The minimum depth is the number of nodes along the shortest path from the root node to the nearest leaf node.
   '''

   # mycode
   class TreeNode:
       def __init__(self, val):
           self.val = val
           self.left, self.right = None, None


   def find_minimum_depth(root):
       from collections import deque

       if not root:
           return 0

       queue = deque()
       queue.append(root)

       depth = 0

       while queue:
           depth += 1

           for i in range(len(queue)):
               current = queue.popleft()

               if current.left is None and current.right is None:
                   return depth
               if current.left:
                   queue.append(current.left)
               if current.right:
                   queue.append(current.right)


   def main():
       root = TreeNode(12)
       root.left = TreeNode(7)
       root.right = TreeNode(1)
       root.right.left = TreeNode(10)
       root.right.right = TreeNode(5)
       print("Tree Minimum Depth: " + str(find_minimum_depth(root)))
       root.left.left = TreeNode(9)
       root.right.left.left = TreeNode(11)
       print("Tree Minimum Depth: " + str(find_minimum_depth(root)))


   main()

   # answer
   class TreeNode:
       def __init__(self, val):
           self.val = val
           self.left, self.right = None, None


   def find_minimum_depth(root):
       from collections import deque
       if root is None:
           return 0

       queue = deque()
       queue.append(root)
       minimumTreeDepth = 0
       while queue:
           minimumTreeDepth += 1
           levelSize = len(queue)
           for _ in range(levelSize):
               currentNode = queue.popleft()

               # check if this is a leaf node
               if not currentNode.left and not currentNode.right:
                   return minimumTreeDepth

               # insert the children of current node in the queue
               if currentNode.left:
                   queue.append(currentNode.left)
               if currentNode.right:
                   queue.append(currentNode.right)


   def main():
       root = TreeNode(12)
       root.left = TreeNode(7)
       root.right = TreeNode(1)
       root.right.left = TreeNode(10)
       root.right.right = TreeNode(5)
       print("Tree Minimum Depth: " + str(find_minimum_depth(root)))
       root.left.left = TreeNode(9)
       root.right.left.left = TreeNode(11)
       print("Tree Minimum Depth: " + str(find_minimum_depth(root)))


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(N), where ‘N’ is the total number of nodes in the tree.
   This is due to the fact that we traverse each node once.
   Space complexity
   The space complexity of the above algorithm will be O(N)O which is required for the queue.
   Since we can have a maximum of N/2 nodes at any level (this could happen only at the lowest level),
   therefore we will need O(N) space to store them in the queue.
   '''


   '''
   Similar Problems
   Problem 1: Given a binary tree, find its maximum depth (or height).
   Solution: We will follow a similar approach. Instead of returning as soon as we find a leaf node,
   we will keep traversing for all the levels, incrementing maximumDepth each time we complete a level.
   Here is what the code will look like:
   '''

   from collections import deque


   class TreeNode:
       def __init__(self, val):
           self.val = val
           self.left, self.right = None, None


   def find_maximum_depth(root):
       if root is None:
           return 0

       queue = deque()
       queue.append(root)
       maximumTreeDepth = 0
       while queue:
           maximumTreeDepth += 1
           levelSize = len(queue)
           for _ in range(levelSize):
               currentNode = queue.popleft()

               # insert the children of current node in the queue
               if currentNode.left:
                   queue.append(currentNode.left)
               if currentNode.right:
                   queue.append(currentNode.right)

       return maximumTreeDepth


   def main():
       root = TreeNode(12)
       root.left = TreeNode(7)
       root.right = TreeNode(1)
       root.right.left = TreeNode(10)
       root.right.right = TreeNode(5)
       print("Tree Maximum Depth: " + str(find_maximum_depth(root)))
       root.left.left = TreeNode(9)
       root.right.left.left = TreeNode(11)
       print("Tree Maximum Depth: " + str(find_maximum_depth(root)))


   main()

Level Order Successor (easy)
-----------------------------------------
.. code:: python

   '''
   Problem Statement
   Given a binary tree and a node, find the level order successor of the given node in the tree.
   The level order successor is the node that appears right after the given node in the level order traversal.
   '''

   # mycode
   from collections import deque


   class TreeNode:
       def __init__(self, val):
           self.val = val
           self.left, self.right = None, None


   def find_successor(root, key):
       # TODO: Write your code here
       if not root:
           return None

       queue = deque()
       queue.append(root)

       flag = False
       while queue:

           for i in range(len(queue)):
               current = queue.popleft()
               if flag:
                   return current

               if current.val == key:
                   flag = True

               if current.left:
                   queue.append(current.left)
               if current.right:
                   queue.append(current.right)
       return None


   def main():
       root = TreeNode(12)
       root.left = TreeNode(7)
       root.right = TreeNode(1)
       root.left.left = TreeNode(9)
       root.right.left = TreeNode(10)
       root.right.right = TreeNode(5)
       result = find_successor(root, 12)
       if result:
           print(result.val)
       result = find_successor(root, 10)
       if result:
           print(result.val)


   main()

   # answer
   from collections import deque


   class TreeNode:
       def __init__(self, val):
           self.val = val
           self.left, self.right = None, None


   def find_successor(root, key):
       if root is None:
           return None

       queue = deque()
       queue.append(root)
       while queue:
           currentNode = queue.popleft()
           # insert the children of current node in the queue
           if currentNode.left:
               queue.append(currentNode.left)
           if currentNode.right:
               queue.append(currentNode.right)

           # break if we have found the key
           if currentNode.val == key:
               break

       return queue[0] if queue else None


   def main():
       root = TreeNode(12)
       root.left = TreeNode(7)
       root.right = TreeNode(1)
       root.left.left = TreeNode(9)
       root.right.left = TreeNode(10)
       root.right.right = TreeNode(5)
       result = find_successor(root, 12)
       if result:
           print(result.val)
       result = find_successor(root, 9)
       if result:
           print(result.val)


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(N), where ‘N’ is the total number of nodes in the tree.
   This is due to the fact that we traverse each node once.
   Space complexity
   The space complexity of the above algorithm will be O(N) which is required for the queue.
   Since we can have a maximum of N/2 nodes at any level (this could happen only at the lowest level),
   therefore we will need O(N) space to store them in the queue.
   '''

Connect Level Order Siblings (medium)
-----------------------------------------
.. code:: python

   '''
   Problem Statement
   Given a binary tree, connect each node with its level order successor.
   The last node of each level should point to a null node.
   '''

   # mycode
   from __future__ import print_function
   from collections import deque


   class TreeNode:
       def __init__(self, val):
           self.val = val
           self.left, self.right, self.next = None, None, None

       # level order traversal using 'next' pointer
       def print_level_order(self):
           nextLevelRoot = self
           while nextLevelRoot:
               current = nextLevelRoot
               nextLevelRoot = None
               while current:
                   print(str(current.val) + " ", end='')
                   if not nextLevelRoot:
                       if current.left:
                           nextLevelRoot = current.left
                       elif current.right:
                           nextLevelRoot = current.right
                   current = current.next
               print()


   def connect_level_order_siblings(root):
       # TODO: Write your code here
       if not root:
           return None

       queue = deque()
       queue.append(root)

       while queue:
           n = len(queue)
           previous = queue.popleft()
           if previous.left:
               queue.append(previous.left)
           if previous.right:
               queue.append(previous.right)

           for i in range(1, n):
               current = queue.popleft()
               previous.next = current

               if current.left:
                   queue.append(current.left)
               if current.right:
                   queue.append(current.right)

               previous = current
           previous.next = None


   def main():
       root = TreeNode(12)
       root.left = TreeNode(7)
       root.right = TreeNode(1)
       root.left.left = TreeNode(9)
       root.right.left = TreeNode(10)
       root.right.right = TreeNode(5)
       connect_level_order_siblings(root)

       print("Level order traversal using 'next' pointer: ")
       root.print_level_order()


   main()

   # answer
   from __future__ import print_function
   from collections import deque


   class TreeNode:
       def __init__(self, val):
           self.val = val
           self.left, self.right, self.next = None, None, None

       # level order traversal using 'next' pointer
       def print_level_order(self):
           nextLevelRoot = self
           while nextLevelRoot:
               current = nextLevelRoot
               nextLevelRoot = None
               while current:
                   print(str(current.val) + " ", end='')
                   if not nextLevelRoot:
                       if current.left:
                           nextLevelRoot = current.left
                       elif current.right:
                           nextLevelRoot = current.right
                   current = current.next
               print()


   def connect_level_order_siblings(root):
       if root is None:
           return

       queue = deque()
       queue.append(root)
       while queue:
           previousNode = None
           levelSize = len(queue)
           # connect all nodes of this level
           for _ in range(levelSize):
               currentNode = queue.popleft()

               if previousNode:
                   previousNode.next = currentNode
               previousNode = currentNode

               # insert the children of current node in the queue
               if currentNode.left:
                   queue.append(currentNode.left)
               if currentNode.right:
                   queue.append(currentNode.right)


   def main():
       root = TreeNode(12)
       root.left = TreeNode(7)
       root.right = TreeNode(1)
       root.left.left = TreeNode(9)
       root.right.left = TreeNode(10)
       root.right.right = TreeNode(5)
       connect_level_order_siblings(root)

       print("Level order traversal using 'next' pointer: ")
       root.print_level_order()


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(N)O, where ‘N’ is the total number of nodes in the tree.
   This is due to the fact that we traverse each node once.
   Space complexity
   The space complexity of the above algorithm will be O(N), which is required for the queue.
   Since we can have a maximum of N/2 nodes at any level (this could happen only at the lowest level),
   therefore we will need O(N) space to store them in the queue.
   '''

Problem Challenge 1 - Connect All Level Order Siblings (medium)
----------------------------------------------------------------
.. code:: python

   '''
   Problem Challenge 1
   Connect All Level Order Siblings (medium)
   Given a binary tree, connect each node with its level order successor.
   The last node of each level should point to the first node of the next level.
   '''

   # mycode
   from __future__ import print_function
   from collections import deque


   class TreeNode:
       def __init__(self, val):
           self.val = val
           self.left, self.right, self.next = None, None, None

       # tree traversal using 'next' pointer
       def print_tree(self):
           print("Traversal using 'next' pointer: ", end='')
           current = self
           while current:
               print(str(current.val) + " ", end='')
               current = current.next


   def connect_all_siblings(root):
       # TODO: Write your code here
       if not root:
           return None

       queue = deque()
       queue.append(root)

       previous = None
       while queue:
           for i in range(len(queue)):
               current = queue.popleft()

               if previous is None:
                   previous = current
               previous.next = current

               if current.left:
                   queue.append(current.left)
               if current.right:
                   queue.append(current.right)
               previous = current


   def main():
       root = TreeNode(12)
       root.left = TreeNode(7)
       root.right = TreeNode(1)
       root.left.left = TreeNode(9)
       root.right.left = TreeNode(10)
       root.right.right = TreeNode(5)
       connect_all_siblings(root)
       root.print_tree()


   main()

   # answer
   from __future__ import print_function
   from collections import deque


   class TreeNode:
       def __init__(self, val):
           self.val = val
           self.left, self.right, self.next = None, None, None

       # tree traversal using 'next' pointer
       def print_tree(self):
           print("Traversal using 'next' pointer: ", end='')
           current = self
           while current:
               print(str(current.val) + " ", end='')
               current = current.next


   def connect_all_siblings(root):
       if root is None:
           return

       queue = deque()
       queue.append(root)
       currentNode, previousNode = None, None
       while queue:
           currentNode = queue.popleft()
           if previousNode:
               previousNode.next = currentNode
           previousNode = currentNode

           # insert the children of current node in the queue
           if currentNode.left:
               queue.append(currentNode.left)
           if currentNode.right:
               queue.append(currentNode.right)


   def main():
       root = TreeNode(12)
       root.left = TreeNode(7)
       root.right = TreeNode(1)
       root.left.left = TreeNode(9)
       root.right.left = TreeNode(10)
       root.right.right = TreeNode(5)
       connect_all_siblings(root)
       root.print_tree()


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(N), where ‘N’ is the total number of nodes in the tree.
   This is due to the fact that we traverse each node once.
   Space complexity
   The space complexity of the above algorithm will be O(N) which is required for the queue.
   Since we can have a maximum of N/2 nodes at any level (this could happen only at the lowest level),
   therefore we will need O(N) space to store them in the queue.
   '''

Problem Challenge 2 - Right View of a Binary Tree (easy)
----------------------------------------------------------
.. code:: python

   '''
   Problem Challenge 2
   Right View of a Binary Tree (easy)
   Given a binary tree, return an array containing nodes in its right view.
   The right view of a binary tree is the set of nodes visible when the tree is seen from the right side.
   '''

   # mycode
   from __future__ import print_function
   from collections import deque


   class TreeNode:
       def __init__(self, val):
           self.val = val
           self.left, self.right = None, None


   def tree_right_view(root):
       result = []
       # TODO: Write your code here
       if not root:
           return result

       queue = deque()
       queue.append(root)

       while queue:
           for i in range(len(queue)):

               current = queue.popleft()

               if current.left:
                   queue.append(current.left)
               if current.right:
                   queue.append(current.right)

           result.append(current)

       return result


   def main():
       root = TreeNode(12)
       root.left = TreeNode(7)
       root.right = TreeNode(1)
       root.left.left = TreeNode(9)
       root.right.left = TreeNode(10)
       root.right.right = TreeNode(5)
       root.left.left.left = TreeNode(3)
       result = tree_right_view(root)
       print("Tree right view: ")
       for node in result:
           print(str(node.val) + " ", end='')


   main()

   # answer
   from __future__ import print_function
   from collections import deque


   class TreeNode:
       def __init__(self, val):
           self.val = val
           self.left, self.right = None, None


   def tree_right_view(root):
       result = []
       if root is None:
           return result

       queue = deque()
       queue.append(root)
       while queue:
           levelSize = len(queue)
           for i in range(0, levelSize):
               currentNode = queue.popleft()
               # if it is the last node of this level, add it to the result
               if i == levelSize - 1:
                   result.append(currentNode)
               # insert the children of current node in the queue
               if currentNode.left:
                   queue.append(currentNode.left)
               if currentNode.right:
                   queue.append(currentNode.right)

       return result


   def main():
       root = TreeNode(12)
       root.left = TreeNode(7)
       root.right = TreeNode(1)
       root.left.left = TreeNode(9)
       root.right.left = TreeNode(10)
       root.right.right = TreeNode(5)
       root.left.left.left = TreeNode(3)
       result = tree_right_view(root)
       print("Tree right view: ")
       for node in result:
           print(str(node.val) + " ", end='')


   main()


   '''
   Time complexity #
   The time complexity of the above algorithm is O(N), where ‘N’ is the total number of nodes in the tree.
   This is due to the fact that we traverse each node once.
   Space complexity
   The space complexity of the above algorithm will be O(N) as we need to return a list containing the level order traversal.
   We will also need O(N) space for the queue. Since we can have a maximum of N/2 nodes at any level
   (this could happen only at the lowest level), therefore we will need O(N) space to store them in the queue.
   '''


   '''
   Similar Questions #
   Problem 1: Given a binary tree, return an array containing nodes in its left view.
   The left view of a binary tree is the set of nodes visible when the tree is seen from the left side.
   Solution: We will be following a similar approach,
   but instead of appending the last element of each level we will be appending the first element of each level to the output array.
   '''
