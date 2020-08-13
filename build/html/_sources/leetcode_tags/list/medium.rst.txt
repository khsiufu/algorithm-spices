=======
Medium
=======


2. Add Two Numbers
------------------------------------------------------------

`2. Add Two Numbers`_

.. code:: python

   class Solution:
       def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
           tail = dummy = ListNode(0)
           carry = 0
           while l1 or l2 or carry:
               if l1:
                   carry += l1.val
                   l1 = l1.next
               if l2:
                   carry += l2.val
                   l2 = l2.next
               tail.next = ListNode(carry % 10)
               carry //= 10
               tail = tail.next
           return dummy.next

.. _2. Add Two Numbers: https://leetcode.com/problems/add-two-numbers/


19. Remove Nth Node From End of List
------------------------------------------------------------

`19. Remove Nth Node From End of List`_

.. code:: python

   class Solution:
       def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
           if not head:
               return None
           dummy = ListNode(0)
           dummy.next = head
           slow = fast = dummy
           for _ in range(n):
               fast = fast.next

           while fast and fast.next:
               fast = fast.next
               slow = slow.next
           slow.next = slow.next.next
           return dummy.next

.. _19. Remove Nth Node From End of List: https://leetcode.com/problems/remove-nth-node-from-end-of-list/


24. Swap Nodes in Pairs
------------------------------------------------------------

`24. Swap Nodes in Pairs`_

.. code:: python

   class Solution:
       def swapPairs(self, head: ListNode) -> ListNode:
           if not head or not head.next:
               return head
           second = head.next
           pre = ListNode(0)
           while head and head.next:
               nxt = head.next
               head.next = nxt.next
               nxt.next = head
               pre.next = nxt
               head = head.next
               pre = nxt.next
           return second
           """
           0 - > 1 -> 2 -> 3 -> 4
           pre   h    nxt
           0 - > 2 - > 1 -> 3   4
           pre   nxt   h
           """

.. _24. Swap Nodes in Pairs: https://leetcode.com/problems/swap-nodes-in-pairs/


61. Rotate List
------------------------------------------------------------

`61. Rotate List`_

.. code:: python

   class Solution:
       def rotateRight(self, head: ListNode, k: int) -> ListNode:
           if not head or not head.next or k == 0:
               return head
           cur, count = head, 0
           while cur:
               count += 1
               cur = cur.next

           k %= count
           if k == 0:
               return head

           fast = slow = head
           for _ in range(k):
               fast = fast.next
           while fast and fast.next:
               fast = fast.next
               slow = slow.next
           ret = slow.next
           fast.next = head
           slow.next = None
           return ret

.. _61. Rotate List: https://leetcode.com/problems/rotate-list/


82. Remove Duplicates from Sorted List II
------------------------------------------------------------

`82. Remove Duplicates from Sorted List II`_

.. code:: python

   class Solution:
       def deleteDuplicates(self, head: ListNode) -> ListNode:
           if not head:
               return None
           dummy = pre = ListNode(0)
           dummy.next = head
           while head and head.next:
               if head.val == head.next.val:
                   while head and head.next and head.val == head.next.val:
                       head = head.next
                   # pass number
                   head = head.next
                   pre.next = head
               else:
                   pre = pre.next
                   head = head.next
           return dummy.next

.. _82. Remove Duplicates from Sorted List II: https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/


92. Reverse Linked List II
------------------------------------------------------------

`92. Reverse Linked List II`_

.. code:: python

   class Solution:
       def reverseBetween(self, head: ListNode, m: int, n: int) -> ListNode:
           if m == n:
               return head

           dummy = ListNode(0)
           dummy.next = head
           pre = dummy

           for i in range(m - 1):
               pre = pre.next

           # reverse the [m, n] nodes
           reverse = nxt = None
           cur = pre.next
           for i in range(n - m + 1):
               nxt = cur.next
               cur.next = reverse
               reverse = cur
               cur = nxt

           pre.next.next = cur
           pre.next = reverse

           return dummy.next

.. _92. Reverse Linked List II: https://leetcode.com/problems/reverse-linked-list-ii/


142. Linked List Cycle II
------------------------------------------------------------

`142. Linked List Cycle II`_

.. code:: python

   class Solution:
       def detectCycle(self, head: ListNode) -> ListNode:
           if not head:
               return None
           fast = slow = head
           while fast and fast.next:
               fast = fast.next.next
               slow = slow.next
               if fast is slow:
                   fast = head
                   while fast and fast != slow:
                       fast = fast.next
                       slow = slow.next
                   return fast
           return None

.. _142. Linked List Cycle II: https://leetcode.com/problems/linked-list-cycle-ii/


143. Reorder List
------------------------------------------------------------

`143. Reorder List`_

.. code:: python

   class Solution:
       def reorderList(self, head: ListNode) -> None:
           if not head:
               return

           # find the mid point
           slow = fast = head
           while fast and fast.next:
               slow = slow.next
               fast = fast.next.next

           # reverse the second half in-place
           pre, node = None, slow
           while node:
               pre, node.next, node = node, pre, node.next

           # Merge in-place; Note: the last node of "first" and "second" are the same
           first, second = head, pre
           while second.next:
               first.next, first = second, first.next
               second.next, second = first, second.next
           return

.. _143. Reorder List: https://leetcode.com/problems/reorder-list/


148. Sort List
------------------------------------------------------------

`148. Sort List`_

.. code:: python

   class Solution:
       def sortList(self, head: ListNode) -> ListNode:
           if not head or not head.next:
               return head

           slow = fast = head
           while fast.next and fast.next.next:
               slow, fast = slow.next, fast.next.next

           fast = slow
           slow = slow.next
           fast.next = None

           l1 = self.sortList(head)
           l2 = self.sortList(slow)

           return self.merge(l1, l2)

       def merge(self, l1, l2):
           tail = dummy = ListNode(0)
           while l1 and l2:
               if l1.val >= l2.val:
                   tail.next = l2
                   l2 = l2.next
               else:
                   tail.next = l1
                   l1 = l1.next
               tail = tail.next

           tail.next = l1 or l2
           return dummy.next

.. _148. Sort List: https://leetcode.com/problems/sort-list/
