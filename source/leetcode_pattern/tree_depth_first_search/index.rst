Binary Tree Path Sum (easy)
----------------------------------
.. code:: python

   '''
   Problem Statement
   Given a binary tree and a number ‘S’,
   find if the tree has a path from root-to-leaf such that the sum of all the node values of that path equals ‘S’.
   '''


   # mycode
   class TreeNode:
       def __init__(self, val, left=None, right=None):
           self.val = val
           self.left = left
           self.right = right


   def has_path(root, sum):
       # TODO: Write your code here
       if not root:
           return False

       if root.val == sum and root.left is None and root.right is None:
           return True

       return has_path(root.left, sum - root.val) or has_path(
           root.right, sum - root.val)


   def main():

       root = TreeNode(12)
       root.left = TreeNode(7)
       root.right = TreeNode(1)
       root.left.left = TreeNode(9)
       root.right.left = TreeNode(10)
       root.right.right = TreeNode(5)
       print("Tree has path: " + str(has_path(root, 23)))
       print("Tree has path: " + str(has_path(root, 16)))


   main()


   # answer
   class TreeNode:
       def __init__(self, val, left=None, right=None):
           self.val = val
           self.left = left
           self.right = right


   def has_path(root, sum):
       if root is None:
           return False

       # if the current node is a leaf and its value is equal to the sum, we've found a path
       if root.val == sum and root.left is None and root.right is None:
           return True

       # recursively call to traverse the left and right sub-tree
       # return true if any of the two recursive call return true
       return has_path(root.left, sum - root.val) or has_path(
           root.right, sum - root.val)


   def main():

       root = TreeNode(12)
       root.left = TreeNode(7)
       root.right = TreeNode(1)
       root.left.left = TreeNode(9)
       root.right.left = TreeNode(10)
       root.right.right = TreeNode(5)
       print("Tree has path: " + str(has_path(root, 23)))
       print("Tree has path: " + str(has_path(root, 16)))


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(N)O, where ‘N’ is the total number of nodes in the tree.
   This is due to the fact that we traverse each node once.
   Space complexity
   The space complexity of the above algorithm will be O(N) in the worst case.
   This space will be used to store the recursion stack.
   The worst case will happen when the given tree is a linked list (i.e., every node has only one child).
   '''

All Paths for a Sum (medium)
----------------------------------
.. code:: python

   '''
   Problem Statement
   Given a binary tree and a number ‘S’,
   find all paths from root-to-leaf such that the sum of all the node values of each path equals ‘S’.
   '''


   # mycode
   class TreeNode:
       def __init__(self, val, left=None, right=None):
           self.val = val
           self.left = left
           self.right = right


   def find_paths(root, sum):
       allPaths = []
       # TODO: Write your code here

       find_current_paths(root, sum, [], allPaths)
       return allPaths


   def find_current_paths(currentNode, sum, currentPath, allPaths):
       if not currentNode:
           return

       currentPath.append(currentNode.val)

       if currentNode.val == sum and currentNode.left is None and currentNode.right is None:
           allPaths.append(list(currentPath))
       else:
           find_current_paths(currentNode.left, sum - currentNode.val,
                              currentPath, allPaths)
           find_current_paths(currentNode.right, sum - currentNode.val,
                              currentPath, allPaths)

       del currentPath[-1]


   def main():

       root = TreeNode(12)
       root.left = TreeNode(7)
       root.right = TreeNode(1)
       root.left.left = TreeNode(4)
       root.right.left = TreeNode(10)
       root.right.right = TreeNode(5)
       sum = 23
       print("Tree paths with sum " + str(sum) + ": " +
             str(find_paths(root, sum)))


   main()


   # answer
   class TreeNode:
       def __init__(self, val, left=None, right=None):
           self.val = val
           self.left = left
           self.right = right


   def find_paths(root, sum):
       allPaths = []
       find_paths_recursive(root, sum, [], allPaths)
       return allPaths


   def find_paths_recursive(currentNode, sum, currentPath, allPaths):
       if currentNode is None:
           return

       # add the current node to the path
       currentPath.append(currentNode.val)

       # if the current node is a leaf and its value is equal to sum, save the current path
       if currentNode.val == sum and currentNode.left is None and currentNode.right is None:
           allPaths.append(list(currentPath))
       else:
           # traverse the left sub-tree
           find_paths_recursive(currentNode.left, sum - currentNode.val,
                                currentPath, allPaths)
           # traverse the right sub-tree
           find_paths_recursive(currentNode.right, sum - currentNode.val,
                                currentPath, allPaths)

       # remove the current node from the path to backtrack,
       # we need to remove the current node while we are going up the recursive call stack.
       del currentPath[-1]


   def main():

       root = TreeNode(12)
       root.left = TreeNode(7)
       root.right = TreeNode(1)
       root.left.left = TreeNode(4)
       root.right.left = TreeNode(10)
       root.right.right = TreeNode(5)
       sum = 23
       print("Tree paths with sum " + str(sum) + ": " +
             str(find_paths(root, sum)))


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(N^2), where ‘N’ is the total number of nodes in the tree.
   This is due to the fact that we traverse each node once (which will take O(N)),
   and for every leaf node we might have to store its path which will take O(N).
   We can calculate a tighter time complexity of O(NlogN) from the space complexity discussion below.
   Space complexity
   If we ignore the space required for the allPaths list,
   the space complexity of the above algorithm will be O(N) in the worst case.
   This space will be used to store the recursion stack.
   The worst case will happen when the given tree is a linked list (i.e., every node has only one child).
   How can we estimate the space used for the allPaths array? Take the example of the following balanced tree:
   Here we have seven nodes (i.e., N = 7). Since, for binary trees, there exists only one path to reach any leaf node,
   we can easily say that total root-to-leaf paths in a binary tree can’t be more than the number of leaves.
   As we know that there can’t be more than N/2N/2 leaves in a binary tree,
   therefore the maximum number of elements in allPaths will be O(N/2) = O(N).
   Now, each of these paths can have many nodes in them. For a balanced binary tree (like above),each leaf node will be at maximum depth.
   As we know that the depth (or height) of a balanced binary tree is O(logN)O(logN) we can say that, at the most,
   each path can have logNlogN nodes in it. This means that the total size of the allPaths list will be O(N*logN)O(N∗logN).
   If the tree is not balanced, we will still have the same worst-case space complexity.
   From the above discussion, we can conclude that the overall space complexity of our algorithm is O(N*logN).
   Also from the above discussion, since for each leaf node, in the worst case,
   we have to copy log(N) nodes to store its path, therefore the time complexity of our algorithm will also be O(N*logN).
   '''


   '''
   Similar Problems
   Problem 1: Given a binary tree, return all root-to-leaf paths.
   Solution: We can follow a similar approach. We just need to remove the “check for the path sum”.
   Problem 2: Given a binary tree, find the root-to-leaf path with the maximum sum.
   Solution: We need to find the path with the maximum sum. As we traverse all paths,
   we can keep track of the path with the maximum sum.
   '''

Sum of Path Numbers (medium)
----------------------------------
.. code:: python

   '''
   Problem Statement
   Given a binary tree where each node can only have a digit (0-9) value,
   each root-to-leaf path will represent a number. Find the total sum of all the numbers represented by all paths.
   '''


   # mycode
   class TreeNode:
       def __init__(self, val, left=None, right=None):
           self.val = val
           self.left = left
           self.right = right


   def find_sum_of_path_numbers(root):
       # TODO: Write your code here
       return find_root_to_leaf_path_numbers(root, 0)


   def find_root_to_leaf_path_numbers(currentNode, currentSum):
       if not currentNode:
           return 0

       currentSum = currentSum * 10 + currentNode.val

       if currentNode.left is None and currentNode.right is None:
           return currentSum
       else:
           return find_root_to_leaf_path_numbers(
               currentNode.left, currentSum) + find_root_to_leaf_path_numbers(
                   currentNode.right, currentSum)


   def main():
       root = TreeNode(1)
       root.left = TreeNode(0)
       root.right = TreeNode(1)
       root.left.left = TreeNode(1)
       root.right.left = TreeNode(6)
       root.right.right = TreeNode(5)
       print("Total Sum of Path Numbers: " + str(find_sum_of_path_numbers(root)))


   main()


   # answer
   class TreeNode:
       def __init__(self, val, left=None, right=None):
           self.val = val
           self.left = left
           self.right = right


   def find_sum_of_path_numbers(root):
       return find_root_to_leaf_path_numbers(root, 0)


   def find_root_to_leaf_path_numbers(currentNode, pathSum):
       if currentNode is None:
           return 0

       # calculate the path number of the current node
       pathSum = 10 * pathSum + currentNode.val

       # if the current node is a leaf, return the current path sum
       if currentNode.left is None and currentNode.right is None:
           return pathSum

       # traverse the left and the right sub-tree
       return find_root_to_leaf_path_numbers(
           currentNode.left, pathSum) + find_root_to_leaf_path_numbers(
               currentNode.right, pathSum)


   def main():
       root = TreeNode(1)
       root.left = TreeNode(0)
       root.right = TreeNode(1)
       root.left.left = TreeNode(1)
       root.right.left = TreeNode(6)
       root.right.right = TreeNode(5)
       print("Total Sum of Path Numbers: " + str(find_sum_of_path_numbers(root)))


   main()


   '''
   Time complexity #
   The time complexity of the above algorithm is O(N), where ‘N’ is the total number of nodes in the tree.
   This is due to the fact that we traverse each node once.
   Space complexity #
   The space complexity of the above algorithm will be O(N) in the worst case.
   This space will be used to store the recursion stack.
   The worst case will happen when the given tree is a linked list (i.e., every node has only one child).
   '''

Path With Given Sequence (medium)
----------------------------------
.. code:: python

   '''
   Problem Statement
   Given a binary tree and a number sequence, find if the sequence is present as a root-to-leaf path in the given tree.
   '''


   # mycode
   class TreeNode:
       def __init__(self, val, left=None, right=None):
           self.val = val
           self.left = left
           self.right = right


   def find_path(root, sequence):
       # TODO: Write your code here

       return find_current_path(root, sequence)


   def find_current_path(currentNode, sequence):

       if not currentNode:
           return False

       if currentNode.val != sequence[0]:
           return False
       else:
           if currentNode.left is None and currentNode.right is None:
               return True
           else:
               del sequence[0]
               return find_current_path(currentNode.left,
                                        sequence) or find_current_path(
                                            currentNode.right, sequence)


   def main():

       root = TreeNode(1)
       root.left = TreeNode(0)
       root.right = TreeNode(1)
       root.left.left = TreeNode(1)
       root.right.left = TreeNode(6)
       root.right.right = TreeNode(5)

       print("Tree has path sequence: " + str(find_path(root, [1, 0, 7])))
       print("Tree has path sequence: " + str(find_path(root, [1, 1, 6])))


   main()


   # answer
   class TreeNode:
       def __init__(self, val, left=None, right=None):
           self.val = val
           self.left = left
           self.right = right


   def find_path(root, sequence):
       if not root:
           return len(sequence) == 0

       return find_path_recursive(root, sequence, 0)


   def find_path_recursive(currentNode, sequence, sequenceIndex):

       if currentNode is None:
           return False

       seqLen = len(sequence)
       if sequenceIndex >= seqLen or currentNode.val != sequence[sequenceIndex]:
           return False

       # if the current node is a leaf, add it is the end of the sequence, we have found a path!
       if currentNode.left is None and currentNode.right is None and sequenceIndex == seqLen - 1:
           return True

       # recursively call to traverse the left and right sub-tree
       # return true if any of the two recursive call return true
       return find_path_recursive(currentNode.left, sequence, sequenceIndex + 1) or \
              find_path_recursive(currentNode.right, sequence, sequenceIndex + 1)


   def main():

       root = TreeNode(1)
       root.left = TreeNode(0)
       root.right = TreeNode(1)
       root.left.left = TreeNode(1)
       root.right.left = TreeNode(6)
       root.right.right = TreeNode(5)

       print("Tree has path sequence: " + str(find_path(root, [1, 0, 7])))
       print("Tree has path sequence: " + str(find_path(root, [1, 1, 6])))


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(N), where ‘N’ is the total number of nodes in the tree.
   This is due to the fact that we traverse each node once.
   Space complexity
   The space complexity of the above algorithm will be O(N) in the worst case.
   This space will be used to store the recursion stack.
   The worst case will happen when the given tree is a linked list (i.e., every node has only one child).
   '''

Count Paths for a Sum (medium)
----------------------------------
.. code:: python

   '''
   Problem Statement
   Given a binary tree and a number ‘S’,
   find all paths in the tree such that the sum of all the node values of each path equals ‘S’.
   Please note that the paths can start or end at any node but all paths must follow direction from parent to child (top to bottom).
   '''


   # mycode
   class TreeNode:
       def __init__(self, val, left=None, right=None):
           self.val = val
           self.left = left
           self.right = right


   def count_paths(root, S):
       # TODO: Write your code here
       return find_current_count(root, S, 0)


   def find_current_count(currentNode, S, count):
       if not currentNode:
           return 0

       if currentNode.val == S:
           count += 1

       return count + find_current_count(
           currentNode.left, S, count) + find_current_count(
               currentNode.right, S, count) + find_current_count(
                   currentNode.left,
                   S - currentNode.val, count) + find_current_count(
                       currentNode.right, S - currentNode.val, count)


   def main():
       root = TreeNode(1)
       root.left = TreeNode(7)
       root.right = TreeNode(9)
       root.left.left = TreeNode(6)
       root.left.right = TreeNode(5)
       root.right.left = TreeNode(2)
       root.right.right = TreeNode(3)
       print("Tree has paths: " + str(count_paths(root, 12)))


   main()


   # answer
   class TreeNode:
       def __init__(self, val, left=None, right=None):
           self.val = val
           self.left = left
           self.right = right


   def count_paths(root, S):
       return count_paths_recursive(root, S, [])


   def count_paths_recursive(currentNode, S, currentPath):
       if currentNode is None:
           return 0

       # add the current node to the path
       currentPath.append(currentNode.val)
       pathCount, pathSum = 0, 0
       # find the sums of all sub-paths in the current path list
       for i in range(len(currentPath) - 1, -1, -1):
           pathSum += currentPath[i]
           # if the sum of any sub-path is equal to 'S' we increment our path count.
           if pathSum == S:
               pathCount += 1

       # traverse the left sub-tree
       pathCount += count_paths_recursive(currentNode.left, S, currentPath)
       # traverse the right sub-tree
       pathCount += count_paths_recursive(currentNode.right, S, currentPath)

       # remove the current node from the path to backtrack
       # we need to remove the current node while we are going up the recursive call stack
       del currentPath[-1]

       return pathCount


   def main():
       root = TreeNode(12)
       root.left = TreeNode(7)
       root.right = TreeNode(1)
       root.left.left = TreeNode(4)
       root.right.left = TreeNode(10)
       root.right.right = TreeNode(5)
       print("Tree has paths: " + str(count_paths(root, 11)))


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(N^2) in the worst case, where ‘N’ is the total number of nodes in the tree.
   This is due to the fact that we traverse each node once, but for every node, we iterate the current path.
   The current path, in the worst case, can be O(N) (in the case of a skewed tree).
   But, if the tree is balanced, then the current path will be equal to the height of the tree, i.e., O(logN).
   So the best case of our algorithm will be O(NlogN).
   Space complexity
   The space complexity of the above algorithm will be O(N). This space will be used to store the recursion stack.
   The worst case will happen when the given tree is a linked list (i.e., every node has only one child).
   We also need O(N) space for storing the currentPath in the worst case.
   Overall space complexity of our algorithm is O(N).
   '''

Problem Challenge 1 - Tree Diameter (medium)
---------------------------------------------
.. code:: python

   '''
   Problem Challenge 1
   Tree Diameter (medium)
   Given a binary tree, find the length of its diameter.
   The diameter of a tree is the number of nodes on the longest path between any two leaf nodes.
   The diameter of a tree may or may not pass through the root.
   Note: You can always assume that there are at least two leaf nodes in the given tree.
   '''


   # mycode
   class TreeNode:
       def __init__(self, val, left=None, right=None):
           self.val = val
           self.left = left
           self.right = right


   class TreeDiameter:
       def __init__(self):
           self.treeDiameter = 0

       def find_diameter(self, root):
           # TODO: Write your code here
           def depth(currentNode):
               if not currentNode:
                   return 0

               left = depth(currentNode.left)
               right = depth(currentNode.right)

               self.treeDiameter = max(self.treeDiameter, left + right + 1)
               return 1 + max(left, right)

           depth(root)
           return self.treeDiameter


   def main():
       treeDiameter = TreeDiameter()
       root = TreeNode(1)
       root.left = TreeNode(2)
       root.right = TreeNode(3)
       root.left.left = TreeNode(4)
       root.right.left = TreeNode(5)
       root.right.right = TreeNode(6)
       print("Tree Diameter: " + str(treeDiameter.find_diameter(root)))
       root.left.left = None
       root.right.left.left = TreeNode(7)
       root.right.left.right = TreeNode(8)
       root.right.right.left = TreeNode(9)
       root.right.left.right.left = TreeNode(10)
       root.right.right.left.left = TreeNode(11)
       print("Tree Diameter: " + str(treeDiameter.find_diameter(root)))


   main()


   # answer
   class TreeNode:
       def __init__(self, val, left=None, right=None):
           self.val = val
           self.left = left
           self.right = right


   class TreeDiameter:
       def __init__(self):
           self.treeDiameter = 0

       def find_diameter(self, root):
           self.calculate_height(root)
           return self.treeDiameter

       def calculate_height(self, currentNode):
           if currentNode is None:
               return 0

           leftTreeHeight = self.calculate_height(currentNode.left)
           rightTreeHeight = self.calculate_height(currentNode.right)

           # diameter at the current node will be equal to the height of left subtree +
           # the height of right sub-trees + '1' for the current node
           diameter = leftTreeHeight + rightTreeHeight + 1

           # update the global tree diameter
           self.treeDiameter = max(self.treeDiameter, diameter)

           # height of the current node will be equal to the maximum of the hights of
           # left or right subtrees plus '1' for the current node
           return max(leftTreeHeight, rightTreeHeight) + 1


   def main():
       treeDiameter = TreeDiameter()
       root = TreeNode(1)
       root.left = TreeNode(2)
       root.right = TreeNode(3)
       root.left.left = TreeNode(4)
       root.right.left = TreeNode(5)
       root.right.right = TreeNode(6)
       print("Tree Diameter: " + str(treeDiameter.find_diameter(root)))
       root.left.left = None
       root.right.left.left = TreeNode(7)
       root.right.left.right = TreeNode(8)
       root.right.right.left = TreeNode(9)
       root.right.left.right.left = TreeNode(10)
       root.right.right.left.left = TreeNode(11)
       print("Tree Diameter: " + str(treeDiameter.find_diameter(root)))


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(N)O(N), where ‘N’ is the total number of nodes in the tree.
   This is due to the fact that we traverse each node once.
   Space complexity
   The space complexity of the above algorithm will be O(N) in the worst case.
   This space will be used to store the recursion stack.
   The worst case will happen when the given tree is a linked list (i.e., every node has only one child).
   '''

Problem Challenge 2 - Path with Maximum Sum (hard)
---------------------------------------------------
.. code:: python

   '''
   Problem Challenge 2
   Path with Maximum Sum (hard)
   Find the path with the maximum sum in a given binary tree. Write a function that returns the maximum sum.
   A path can be defined as a sequence of nodes between any two nodes and doesn’t necessarily pass through the root.
   '''

   # mycode
   import math


   class TreeNode:
       def __init__(self, val, left=None, right=None):
           self.val = val
           self.left = left
           self.right = right


   class MaximumPathSum:
       def find_maximum_path_sum(self, root):
           # TODO: Write your code here
           self.globalMaximum = -math.inf
           self.find_maximum_path_sum_recursive(root)
           return self.globalMaximum

       def find_maximum_path_sum_recursive(self, currentNode):
           if not currentNode:
               return 0

           maximumLeft = max(
               0, self.find_maximum_path_sum_recursive(currentNode.left))
           maximumRight = max(
               0, self.find_maximum_path_sum_recursive(currentNode.right))

           self.globalMaximum = max(self.globalMaximum,
                                    maximumLeft + currentNode.val + maximumRight)

           return max(maximumLeft, maximumRight) + currentNode.val


   def main():
       maximumPathSum = MaximumPathSum()
       root = TreeNode(1)
       root.left = TreeNode(2)
       root.right = TreeNode(3)

       print("Maximum Path Sum: " +
             str(maximumPathSum.find_maximum_path_sum(root)))
       root.left.left = TreeNode(1)
       root.left.right = TreeNode(3)
       root.right.left = TreeNode(5)
       root.right.right = TreeNode(6)
       root.right.left.left = TreeNode(7)
       root.right.left.right = TreeNode(8)
       root.right.right.left = TreeNode(9)
       print("Maximum Path Sum: " +
             str(maximumPathSum.find_maximum_path_sum(root)))

       root = TreeNode(-1)
       root.left = TreeNode(-3)
       print("Maximum Path Sum: " +
             str(maximumPathSum.find_maximum_path_sum(root)))


   main()

   # answer
   import math


   class TreeNode:
       def __init__(self, val, left=None, right=None):
           self.val = val
           self.left = left
           self.right = right


   class MaximumPathSum:
       def find_maximum_path_sum(self, root):
           self.globalMaximumSum = -math.inf
           self.find_maximum_path_sum_recursive(root)
           return self.globalMaximumSum

       def find_maximum_path_sum_recursive(self, currentNode):
           if currentNode is None:
               return 0

           maxPathSumFromLeft = self.find_maximum_path_sum_recursive(
               currentNode.left)
           maxPathSumFromRight = self.find_maximum_path_sum_recursive(
               currentNode.right)

           # ignore paths with negative sums, since we need to find the maximum sum we should
           # ignore any path which has an overall negative sum.
           maxPathSumFromLeft = max(maxPathSumFromLeft, 0)
           maxPathSumFromRight = max(maxPathSumFromRight, 0)

           # maximum path sum at the current node will be equal to the sum from the left subtree +
           # the sum from right subtree + val of current node
           localMaximumSum = maxPathSumFromLeft + maxPathSumFromRight + currentNode.val

           # update the global maximum sum
           self.globalMaximumSum = max(self.globalMaximumSum, localMaximumSum)

           # maximum sum of any path from the current node will be equal to the maximum of
           # the sums from left or right subtrees plus the value of the current node
           return max(maxPathSumFromLeft, maxPathSumFromRight) + currentNode.val


   def main():
       maximumPathSum = MaximumPathSum()
       root = TreeNode(1)
       root.left = TreeNode(2)
       root.right = TreeNode(3)

       print("Maximum Path Sum: " +
             str(maximumPathSum.find_maximum_path_sum(root)))
       root.left.left = TreeNode(1)
       root.left.right = TreeNode(3)
       root.right.left = TreeNode(5)
       root.right.right = TreeNode(6)
       root.right.left.left = TreeNode(7)
       root.right.left.right = TreeNode(8)
       root.right.right.left = TreeNode(9)
       print("Maximum Path Sum: " +
             str(maximumPathSum.find_maximum_path_sum(root)))

       root = TreeNode(-1)
       root.left = TreeNode(-3)
       print("Maximum Path Sum: " +
             str(maximumPathSum.find_maximum_path_sum(root)))


   main()


   '''
   Time complexity
   The time complexity of the above algorithm is O(N), where ‘N’ is the total number of nodes in the tree.
   This is due to the fact that we traverse each node once.
   Space complexity
   The space complexity of the above algorithm will be O(N) in the worst case.
   This space will be used to store the recursion stack.
   The worst case will happen when the given tree is a linked list (i.e., every node has only one child).
   '''
