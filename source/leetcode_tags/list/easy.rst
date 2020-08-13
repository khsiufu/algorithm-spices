=======
Easy
=======


21. Merge Two Sorted Lists
------------------------------------------------------------

`21. Merge Two Sorted Lists`_

.. code:: python

   class Solution:
       def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
           tail = dummy = ListNode(0)
           while l1 and l2:
               if l1.val < l2.val:
                   tail.next = l1
                   l1 = l1.next
               else:
                   tail.next = l2
                   l2 = l2.next
               tail = tail.next

           tail.next = l1 or l2

           return dummy.next

.. _21. Merge Two Sorted Lists: https://leetcode.com/problems/merge-two-sorted-lists/


83. Remove Duplicates from Sorted List
------------------------------------------------------------

`83. Remove Duplicates from Sorted List`_

.. code:: python

   class Solution:
       def deleteDuplicates(self, head: ListNode) -> ListNode:
           if not head:
               return None
           cur = head
           while cur and cur.next:
               if cur.val == cur.next.val:
                   cur.next = cur.next.next
               else:
                   cur = cur.next
           return head

.. _83. Remove Duplicates from Sorted List: https://leetcode.com/problems/remove-duplicates-from-sorted-list/


141. Linked List Cycle
------------------------------------------------------------

`141. Linked List Cycle`_

.. code:: python

   class Solution:
       def hasCycle(self, head: ListNode) -> bool:
           if not head:
               return False
           fast = slow = head
           while fast and fast.next:
               fast = fast.next.next
               slow = slow.next
               if fast is slow:
                   return True
           return False

.. _141. Linked List Cycle: https://leetcode.com/problems/linked-list-cycle/


234. Palindrome Linked List
------------------------------------------------------------

`234. Palindrome Linked List`_

.. code:: python

   class Solution:
       def isPalindrome(self, head: ListNode) -> bool:
           if not head:
               return True

           fast = slow = head

           while fast.next and fast.next.next:
               fast = fast.next.next
               slow = slow.next

           p = head
           q = self.reverseList(slow.next)

           while q:
               if p.val != q.val:
                   return False
               p = p.next
               q = q.next

           return True

       def reverseList(self, head):
           if not head:
               return
           pre = None
           while head:
               nxt = head.next
               head.next = pre
               pre = head
               head = nxt
           return pre

.. _234. Palindrome Linked List: https://leetcode.com/problems/palindrome-linked-list/
