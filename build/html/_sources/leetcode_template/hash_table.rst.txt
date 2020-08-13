=========================
Hash Table
=========================


.. code:: python

   class ListNode:
       def __init__(self, key, value):
           self.key = key
           self.value = value
           self.next = None

   class MyHashMap:
       def __init__(self):
           self.size = 1000
           self.hash_table = [None] * self.size

       def put(self, key, value):
           index = key % self.size
           if self.hash_table[index] is None:
               self.hash_table[index] = ListNode(key, value)
           else:
               curr_node = self.hash_table[index]
               while True:
                   if curr_node.key == key:
                       curr_node.value = value
                       print("null")
                       return
                   if curr_node.next is None:
                       break
                   curr_node = curr_node.next
               curr_node.next = ListNode(key, value)

       def get(self, key):
           index = key % self.size
           curr_node = self.hash_table[index]
           while curr_node:
               if curr_node.key == key:
                   print(curr_node.value)
                   return curr_node.value
               else:
                   curr_node = curr_node.next
           print(-1)
           return -1

       def remove(self, key):
           index = key % self.size
           curr_node = prev_node = self.hash_table[index]

           if not curr_node:
               print("null")
               return

           if curr_node.key == key:
               self.hash_table[index] = curr_node.next
           else:
               curr_node = curr_node.next

               while curr_node:
                   if curr_node.key == key:
                       prev_node.next = curr_node.next
                       break
                   else:
                       prev_node, curr_node = prev_node.next, curr_node.next

   obj = MyHashMap()
   obj.put(1, 2)
   obj.put(2, 2)
   obj.get(1)
   obj.get(3)
   obj.put(2, 1)
   obj.get(2)
   obj.remove(2)
   obj.get(2)
