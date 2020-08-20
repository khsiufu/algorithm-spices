=======
Hard
=======


212. Word Search II
------------------------------------------------------------

`212. Word Search II`_

.. code:: python

   class TrieNode():
       def __init__(self):
           self.children = collections.defaultdict(TrieNode)
           self.isWord = False

   class Trie():
       def __init__(self):
           self.root = TrieNode()

       def insert(self, word):
           node = self.root
           for w in word:
               node = node.children[w]
           node.isWord = True

       def search(self, word):
           node = self.root
           for w in word:
               node = node.children.get(w)
               if not node:
                   return False
           return node.isWord

   class Solution(object):
       def findWords(self, board, words):
           res = []
           trie = Trie()
           node = trie.root
           for w in words:
               trie.insert(w)
           for i in range(len(board)):
               for j in range(len(board[0])):
                   self.dfs(board, node, i, j, "", res)
           return res

       def dfs(self, board, node, i, j, path, res):
           if node.isWord:
               res.append(path)
               node.isWord = False
           if i < 0 or i >= len(board) or j < 0 or j >= len(board[0]):
               return
           tmp = board[i][j]
           node = node.children.get(tmp)
           if not node:
               return
           board[i][j] = "#"
           self.dfs(board, node, i+1, j, path+tmp, res)
           self.dfs(board, node, i-1, j, path+tmp, res)
           self.dfs(board, node, i, j-1, path+tmp, res)
           self.dfs(board, node, i, j+1, path+tmp, res)
           board[i][j] = tmp

.. _212. Word Search II: https://leetcode.com/problems/word-search-ii/


301. Remove Invalid Parentheses
------------------------------------------------------------

`301. Remove Invalid Parentheses`_

.. code:: python

   class Solution:
       def removeInvalidParentheses(self, s:str) -> List[str]:
           def isValid(s:str)->bool:
               cnt = 0
               for c in s:
                   if c == "(": cnt += 1
                   elif c == ")": cnt -= 1
                   if cnt < 0: return False  # 只用中途cnt出现了负值，你就要终止循环，已经出现非法字符了
               return cnt == 0

           # BFS
           level = {s}  # 用set避免重复
           while True:
               valid = list(filter(isValid, level))  # 所有合法字符都筛选出来
               if valid: return valid  # 如果当前valid是非空的，说明已经有合法的产生了
               # 下一层level
               next_level = set()
               for item in level:
                   for i in range(len(item)):
                       if item[i] in "()":  # 如果item[i]这个char是个括号就删了，如果不是括号就留着
                           next_level.add(item[:i]+item[i+1:])
               level = next_level

.. _301. Remove Invalid Parentheses: https://leetcode.com/problems/remove-invalid-parentheses/

