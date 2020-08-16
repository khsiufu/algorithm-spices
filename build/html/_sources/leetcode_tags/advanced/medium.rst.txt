=======
Medium
=======


208. Implement Trie (Prefix Tree)
------------------------------------------------------

`208. Implement Trie (Prefix Tree)`_

.. code:: python

   class Trie:

       def __init__(self):
           self.root = {}
           self.word_end = -1


       def insert(self, word: str) -> None:
           curNode = self.root
           for c in word:
               if c not in curNode:
                   curNode[c] = {}
               curNode = curNode[c]
           curNode[self.word_end] = True


       def search(self, word: str) -> bool:
           curNode = self.root
           for c in word:
               if c not in curNode:
                   return False
               curNode = curNode[c]
           if self.word_end not in curNode:
               return False
           return True


       def startsWith(self, prefix: str) -> bool:
           curNode = self.root
           for c in prefix:
               if c not in curNode:
                   return False
               curNode = curNode[c]
           return True


   # Your Trie object will be instantiated and called as such:
   # obj = Trie()
   # obj.insert(word)
   # param_2 = obj.search(word)
   # param_3 = obj.startsWith(prefix)

.. _208. Implement Trie (Prefix Tree): https://leetcode.com/problems/implement-trie-prefix-tree/
