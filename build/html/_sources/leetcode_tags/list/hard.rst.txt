=======
Hard
=======


23. Merge k Sorted Lists
------------------------------------------------------------

`23. Merge k Sorted Lists`_

.. code:: python

   class Solution:
       def mergeKLists(self, lists: List[ListNode]) -> ListNode:
           if not lists:
               return None
           if len(lists) == 1:
               return lists[0]
           mid = len(lists) // 2
           l1 = self.mergeKLists(lists[:mid])
           l2 = self.mergeKLists(lists[mid:])
           return self.merge(l1, l2)

       def merge(self, l1, l2):
           cur = dummy = ListNode(0)
           while l1 and l2:
               if l1.val > l2.val:
                   cur.next = l2
                   l2 = l2.next
               else:
                   cur.next = l1
                   l1 = l1.next
               cur = cur.next

           cur.next = l1 or l2
           return dummy.next

.. _23. Merge k Sorted Lists: https://leetcode.com/problems/merge-k-sorted-lists/


25. Reverse Nodes in k-Group
------------------------------------------------------------

`25. Reverse Nodes in k-Group`_

.. code:: python

   class Solution:
       def reverseKGroup(self, head: ListNode, k: int) -> ListNode:
           count, node = 0, head
           while node:
               count += 1
               node = node.next
           if k <= 1 or count < k:
               return head

           pre = nxt = None
           curr = head

           for _ in range(k):
               nxt = curr.next
               curr.next = pre
               pre = curr
               curr = nxt

           head.next = self.reverseKGroup(curr, k)
           return pre

.. _25. Reverse Nodes in k-Group: https://leetcode.com/problems/reverse-nodes-in-k-group/
