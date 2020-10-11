Reverse a LinkedList (easy)
------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given the head of a Singly LinkedList, reverse the LinkedList.
   Write a function to return the new head of the reversed LinkedList.
   '''

   # mycode
   class Node:
       def __init__(self, value, next=None):
           self.value = value
           self.next = next

       def print_list(self):
           temp = self
           while temp is not None:
               print(temp.value, end=" ")
               temp = temp.next
           print()


   def reverse(head):
       if not head:
           return None
       pre, cur = None, head
       while cur:
           nxt = cur.next
           cur.next = pre
           pre = cur
           cur = nxt
       return pre


   def main():
       head = Node(2)
       head.next = Node(4)
       head.next.next = Node(6)
       head.next.next.next = Node(8)
       head.next.next.next.next = Node(10)

       print("Nodes of original LinkedList are: ", end='')
       head.print_list()
       result = reverse(head)
       print("Nodes of reversed LinkedList are: ", end='')
       result.print_list()


   main()

   # answer
   from __future__ import print_function


   class Node:
       def __init__(self, value, next=None):
           self.value = value
           self.next = next

       def print_list(self):
           temp = self
           while temp is not None:
               print(temp.value, end=" ")
               temp = temp.next
           print()


   def reverse(head):
       previous, current, next = None, head, None
       while current is not None:
           next = current.next  # temporarily store the next node
           current.next = previous  # reverse the current node
           previous = current  # before we move to the next node, point previous to the current node
           current = next  # move on the next node
       return previous


   def main():
       head = Node(2)
       head.next = Node(4)
       head.next.next = Node(6)
       head.next.next.next = Node(8)
       head.next.next.next.next = Node(10)

       print("Nodes of original LinkedList are: ", end='')
       head.print_list()
       result = reverse(head)
       print("Nodes of reversed LinkedList are: ", end='')
       result.print_list()


   main()


   '''
   Time complexity
   The time complexity of our algorithm will be O(N) where ‘N’ is the total number of nodes in the LinkedList.
   Space complexity
   We only used constant space, therefore, the space complexity of our algorithm is O(1).
   '''

Reverse a Sub-list (medium)
------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given the head of a LinkedList and two positions ‘p’ and ‘q’, reverse the LinkedList from position ‘p’ to ‘q’.
   '''

   # mycode
   class Node:
       def __init__(self, value, next=None):
           self.value = value
           self.next = next

       def print_list(self):
           temp = self
           while temp is not None:
               print(temp.value, end=" ")
               temp = temp.next
           print()


   def reverse_sub_list(head, p, q):
       if p == q:
           return head

       pre = dummy = Node(0)
       dummy.next = head

       for _ in range(p - 1):
           pre = pre.next

       cur = pre.next
       # reverse the defined part
       node = None
       for _ in range(q - p + 1):
           nxt = cur.next
           cur.next = node
           node = cur
           cur = nxt
       # connect three parts
       pre.next.next = cur
       pre.next = node
       return dummy.next


   def main():
       head = Node(1)
       head.next = Node(2)
       head.next.next = Node(3)
       head.next.next.next = Node(4)
       head.next.next.next.next = Node(5)

       print("Nodes of original LinkedList are: ", end='')
       head.print_list()
       result = reverse_sub_list(head, 2, 4)
       print("Nodes of reversed LinkedList are: ", end='')
       result.print_list()


   main()


   '''
   Solution
   The problem follows the In-place Reversal of a LinkedList pattern.
   We can use a similar approach as discussed in Reverse a LinkedList. Here are the steps we need to follow:
   1. Skip the first p-1 nodes, to reach the node at position p.
   2. Remember the node at position p-1 to be used later to connect with the reversed sub-list.
   3. Next, reverse the nodes from p to q using the same approach discussed in Reverse a LinkedList.
   4. Connect the p-1 and q+1 nodes to the reversed sub-list.
   '''

   from __future__ import print_function


   class Node:
       def __init__(self, value, next=None):
           self.value = value
           self.next = next

       def print_list(self):
           temp = self
           while temp is not None:
               print(temp.value, end=" ")
               temp = temp.next
           print()


   def reverse_sub_list(head, p, q):
       if p == q:
           return head

       # after skipping 'p-1' nodes, current will point to 'p'th node
       current, previous = head, None
       i = 0
       while current is not None and i < p - 1:
           previous = current
           current = current.next
           i += 1

       # we are interested in three parts of the LinkedList, the part before index 'p',
       # the part between 'p' and 'q', and the part after index 'q'
       last_node_of_first_part = previous
       # after reversing the LinkedList 'current' will become the last node of the sub-list
       last_node_of_sub_list = current
       next = None  # will be used to temporarily store the next node

       i = 0
       # reverse nodes between 'p' and 'q'
       print(previous.value, current.value)
       while current is not None and i < q - p + 1:
           next = current.next
           current.next = previous
           previous = current
           current = next
           i += 1

       # connect with the first part
       if last_node_of_first_part is not None:
           # 'previous' is now the first node of the sub-list
           last_node_of_first_part.next = previous
       # this means p == 1 i.e., we are changing the first node (head) of the LinkedList
       else:
           head = previous

       # connect with the last part
       last_node_of_sub_list.next = current
       return head


   def main():
       head = Node(1)
       head.next = Node(2)
       head.next.next = Node(3)
       head.next.next.next = Node(4)
       head.next.next.next.next = Node(5)

       print("Nodes of original LinkedList are: ", end='')
       head.print_list()
       result = reverse_sub_list(head, 2, 4)
       print("Nodes of reversed LinkedList are: ", end='')
       result.print_list()


   main()


   '''
   Time complexity
   The time complexity of our algorithm will be O(N) where ‘N’ is the total number of nodes in the LinkedList.
   Space complexity
   We only used constant space, therefore, the space complexity of our algorithm is O(1).
   '''

Reverse every K-element Sub-list (medium)
------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given the head of a LinkedList and a number ‘k’, reverse every ‘k’ sized sub-list starting from the head.
   If, in the end, you are left with a sub-list with less than ‘k’ elements, reverse it too.
   '''

   # mycode
   class Node:
       def __init__(self, value, next=None):
           self.value = value
           self.next = next

       def print_list(self):
           temp = self
           while temp is not None:
               print(temp.value, end=" ")
               temp = temp.next
           print()


   def reverse_every_k_elements(head, k):
       count, cur = 0, head
       while cur:
           cur = cur.next
           count += 1

       # don't move
       if k <= 1:
           return head

       pre, cur = None, head
       # check
       if count < k:
           while cur:
               nxt = cur.next
               cur.next = pre
               pre = cur
               cur = nxt
           return pre

       for _ in range(k):
           nxt = cur.next
           cur.next = pre
           pre = cur
           cur = nxt

       head.next = reverse_every_k_elements(cur, k)

       return pre


   def main():
       head = Node(1)
       head.next = Node(2)
       head.next.next = Node(3)
       head.next.next.next = Node(4)
       head.next.next.next.next = Node(5)
       head.next.next.next.next.next = Node(6)
       head.next.next.next.next.next.next = Node(7)
       head.next.next.next.next.next.next.next = Node(8)

       print("Nodes of original LinkedList are: ", end='')
       head.print_list()
       result = reverse_every_k_elements(head, 3)
       print("Nodes of reversed LinkedList are: ", end='')
       result.print_list()


   main()

   # answer
   from __future__ import print_function


   class Node:
       def __init__(self, value, next=None):
           self.value = value
           self.next = next

       def print_list(self):
           temp = self
           while temp is not None:
               print(temp.value, end=" ")
               temp = temp.next
           print()


   def reverse_every_k_elements(head, k):
       if k <= 1 or head is None:
           return head

       current, previous = head, None
       while True:
           last_node_of_previous_part = previous
           # after reversing the LinkedList 'current' will become the last node of the sub-list
           last_node_of_sub_list = current
           next = None  # will be used to temporarily store the next node
           i = 0
           while current is not None and i < k:  # reverse 'k' nodes
               next = current.next
               current.next = previous
               previous = current
               current = next
               i += 1

           # connect with the previous part
           if last_node_of_previous_part is not None:
               last_node_of_previous_part.next = previous
           else:
               head = previous

           # connect with the next part
           last_node_of_sub_list.next = current

           if current is None:
               break
           previous = last_node_of_sub_list
       return head


   def main():
       head = Node(1)
       head.next = Node(2)
       head.next.next = Node(3)
       head.next.next.next = Node(4)
       head.next.next.next.next = Node(5)
       head.next.next.next.next.next = Node(6)
       head.next.next.next.next.next.next = Node(7)
       head.next.next.next.next.next.next.next = Node(8)

       print("Nodes of original LinkedList are: ", end='')
       head.print_list()
       result = reverse_every_k_elements(head, 3)
       print("Nodes of reversed LinkedList are: ", end='')
       result.print_list()


   main()


   '''
   Time complexity
   The time complexity of our algorithm will be O(N) where ‘N’ is the total number of nodes in the LinkedList.
   Space complexity
   We only used constant space, therefore, the space complexity of our algorithm is O(1).
   '''

Problem Challenge 1 - Reverse alternating K-element Sub-list (medium)
-----------------------------------------------------------------------
.. code:: python

   '''
   Problem Challenge 1
   Reverse alternating K-element Sub-list (medium)
   Given the head of a LinkedList and a number ‘k’, reverse every alternating ‘k’ sized sub-list starting from the head.
   If, in the end, you are left with a sub-list with less than ‘k’ elements, reverse it too.
   '''

   # mycode
   class Node:
       def __init__(self, value, next=None):
           self.value = value
           self.next = next

       def print_list(self):
           temp = self
           while temp is not None:
               print(temp.value, end=" ")
               temp = temp.next
           print()


   def reverse_alternate_k_elements(head, k):
       if k <= 1 or head is None:
           return head

       pre, cur = None, head

       while True:
           last_node_of_pre_part = pre
           last_node_of_sub_list = cur

           # reverse 'k' nodes
           i = 0
           while cur is not None and i < k:
               nxt = cur.next
               cur.next = pre
               pre = cur
               cur = nxt
               i += 1

           # connect with the previous part
           if last_node_of_pre_part is not None:
               last_node_of_pre_part.next = pre
           else:
               head = pre

           # connect with the next part
           last_node_of_sub_list.next = cur

           # skip 'k' nodes
           i = 0
           while cur is not None and i < k:
               pre = cur
               cur = cur.next
               i += 1

           if cur is None:
               break
       return head


   def main():
       head = Node(1)
       head.next = Node(2)
       head.next.next = Node(3)
       head.next.next.next = Node(4)
       head.next.next.next.next = Node(5)
       head.next.next.next.next.next = Node(6)
       head.next.next.next.next.next.next = Node(7)
       head.next.next.next.next.next.next.next = Node(8)

       print("Nodes of original LinkedList are: ", end='')
       head.print_list()
       result = reverse_alternate_k_elements(head, 2)
       print("Nodes of reversed LinkedList are: ", end='')
       result.print_list()


   main()

   # answer
   from __future__ import print_function


   class Node:
       def __init__(self, value, next=None):
           self.value = value
           self.next = next

       def print_list(self):
           temp = self
           while temp is not None:
               print(temp.value, end=" ")
               temp = temp.next
           print()


   def reverse_alternate_k_elements(head, k):
       if k <= 1 or head is None:
           return head

       current, previous = head, None
       while True:
           last_node_of_previous_part = previous
           # after reversing the LinkedList 'current' will become the last node of the sub-list
           last_node_of_sub_list = current
           next = None  # will be used to temporarily store the next node

           # reverse 'k' nodes
           i = 0
           while current is not None and i < k:
               next = current.next
               current.next = previous
               previous = current
               current = next
               i += 1

           # connect with the previous part
           if last_node_of_previous_part is not None:
               last_node_of_previous_part.next = previous
           else:
               head = previous

           # connect with the next part
           last_node_of_sub_list.next = current

           # skip 'k' nodes
           i = 0
           while current is not None and i < k:
               previous = current
               current = current.next
               i += 1

           if current is None:
               break
       return head


   def main():
       head = Node(1)
       head.next = Node(2)
       head.next.next = Node(3)
       head.next.next.next = Node(4)
       head.next.next.next.next = Node(5)
       head.next.next.next.next.next = Node(6)
       head.next.next.next.next.next.next = Node(7)
       head.next.next.next.next.next.next.next = Node(8)

       print("Nodes of original LinkedList are: ", end='')
       head.print_list()
       result = reverse_alternate_k_elements(head, 2)
       print("Nodes of reversed LinkedList are: ", end='')
       result.print_list()


   main()


   '''
   Time complexity
   The time complexity of our algorithm will be O(N) where ‘N’ is the total number of nodes in the LinkedList.
   Space complexity
   We only used constant space, therefore, the space complexity of our algorithm is O(1).
   '''

Problem Challenge 2 - Rotate a LinkedList (medium)
----------------------------------------------------
.. code:: python

   '''
   Problem Challenge 2
   Rotate a LinkedList (medium)
   Given the head of a Singly LinkedList and a number ‘k’, rotate the LinkedList to the right by ‘k’ nodes.
   '''

   # mycode
   class Node:
       def __init__(self, value, next=None):
           self.value = value
           self.next = next

       def print_list(self):
           temp = self
           while temp is not None:
               print(temp.value, end=" ")
               temp = temp.next
           print()


   def rotate(head, rotations):
       if not head or not head.next or rotations == 0:
           return head

       cur, count = head, 0
       while cur is not None:
           cur = cur.next
           count += 1

       rotations %= count

       if rotations == 0:
           return head

       fast = slow = head
       for _ in range(rotations):
           fast = fast.next

       while fast and fast.next:
           fast = fast.next
           slow = slow.next

       ret = slow.next
       slow.next = None
       fast.next = head
       return ret


   def main():
       head = Node(1)
       head.next = Node(2)
       head.next.next = Node(3)
       head.next.next.next = Node(4)
       head.next.next.next.next = Node(5)
       head.next.next.next.next.next = Node(6)

       print("Nodes of original LinkedList are: ", end='')
       head.print_list()
       result = rotate(head, 3)
       print("Nodes of rotated LinkedList are: ", end='')
       result.print_list()


   main()

   # answer
   from __future__ import print_function


   class Node:
       def __init__(self, value, next=None):
           self.value = value
           self.next = next

       def print_list(self):
           temp = self
           while temp is not None:
               print(temp.value, end=" ")
               temp = temp.next
           print()


   def rotate(head, rotations):
       if head is None or head.next is None or rotations <= 0:
           return head

       # find the length and the last node of the list
       last_node = head
       list_length = 1
       while last_node.next is not None:
           last_node = last_node.next
           list_length += 1

       last_node.next = head  # connect the last node with the head to make it a circular list
       rotations %= list_length  # no need to do rotations more than the length of the list
       skip_length = list_length - rotations
       last_node_of_rotated_list = head
       for i in range(skip_length - 1):
           last_node_of_rotated_list = last_node_of_rotated_list.next

       # 'last_node_of_rotated_list.next' is pointing to the sub-list of 'k' ending nodes
       head = last_node_of_rotated_list.next
       last_node_of_rotated_list.next = None
       return head


   def main():
       head = Node(1)
       head.next = Node(2)
       head.next.next = Node(3)
       head.next.next.next = Node(4)
       head.next.next.next.next = Node(5)
       head.next.next.next.next.next = Node(6)

       print("Nodes of original LinkedList are: ", end='')
       head.print_list()
       result = rotate(head, 3)
       print("Nodes of rotated LinkedList are: ", end='')
       result.print_list()


   main()


   '''
   Time complexity
   The time complexity of our algorithm will be O(N) where ‘N’ is the total number of nodes in the LinkedList.
   Space complexity
   We only used constant space, therefore, the space complexity of our algorithm is O(1).
   '''
