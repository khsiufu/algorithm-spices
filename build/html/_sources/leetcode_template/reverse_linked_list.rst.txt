=========================
Reverse Linked List
=========================


.. code:: python

   class ListNode:
       def __init__(self, x):
           self.value = x
           self.next = None

   def reverse_link(head):
       if not head:
           return
       pre, nxt, curr = None, None, head

       while curr:
           nxt = curr.next
           curr.next = pre
           pre = curr
           curr = nxt
       return pre

   def create_link(nums):
       dummy = ListNode(0)
       curr = dummy
       for i in nums:
           curr.next = ListNode(i)
           curr = curr.next
       return dummy.next

   def print_link(head):
       curr = head
       while curr:
           print(curr.value)
           curr = curr.next

   if __name__ == '__main__':
       head = create_link([1, 2, 5, 10, 4])
       head = reverse_link(head)
       print_link(head)
