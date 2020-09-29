LinkedList Cycle (easy)
---------------------------------------
LeetCode：\ `141. Linked List Cycle`_

.. _141. Linked List Cycle: https://leetcode.com/problems/linked-list-cycle/

.. code:: python

   '''
   Problem Statement
   Given the head of a Singly LinkedList, write a function to determine if the LinkedList has a cycle in it or not.
   '''


   class Node:
       def __init__(self, value, next=None):
           self.value = value
           self.next = next


   def has_cycle(head):
       slow = fast = head
       while fast and fast.next:
           fast = fast.next.next
           slow = slow.next
           if fast == slow:
               return True
       return False


   def main():
       head = Node(1)
       head.next = Node(2)
       head.next.next = Node(3)
       head.next.next.next = Node(4)
       head.next.next.next.next = Node(5)
       head.next.next.next.next.next = Node(6)
       print("LinkedList has cycle: " + str(has_cycle(head)))

       head.next.next.next.next.next.next = head.next.next
       print("LinkedList has cycle: " + str(has_cycle(head)))

       head.next.next.next.next.next.next = head.next.next.next
       print("LinkedList has cycle: " + str(has_cycle(head)))


   main()


   '''
   Time Complexity
   As we have concluded above, once the slow pointer enters the cycle, the fast pointer will meet the slow pointer in the same loop.
   Therefore, the time complexity of our algorithm will be O(N) where ‘N’ is the total number of nodes in the LinkedList.
   Space Complexity #
   The algorithm runs in constant space O(1).
   '''


   '''
   Similar Problems
   Problem 1: Given the head of a LinkedList with a cycle, find the length of the cycle.
   Solution: We can use the above solution to find the cycle in the LinkedList.
   Once the fast and slow pointers meet, we can save the slow pointer and iterate the whole cycle with another pointer until we see the slow pointer again to find the length of the cycle.
   Here is what our algorithm will look like:
   '''


   class Node:
       def __init__(self, value, next=None):
           self.value = value
           self.next = next


   def find_cycle_length(head):
       slow = fast = head
       while fast and fast.next:
           fast = fast.next.next
           slow = slow.next
           if slow == fast:  # found the cycle
               return calculate_cycle_length(slow)

       return 0


   def calculate_cycle_length(slow):
       current = slow
       cycle_length = 0
       while True:
           current = current.next
           cycle_length += 1
           if current == slow:
               break
       return cycle_length


   def main():
       head = Node(1)
       head.next = Node(2)
       head.next.next = Node(3)
       head.next.next.next = Node(4)
       head.next.next.next.next = Node(5)
       head.next.next.next.next.next = Node(6)
       head.next.next.next.next.next.next = head.next.next
       print("LinkedList cycle length: " + str(find_cycle_length(head)))

       head.next.next.next.next.next.next = head.next.next.next
       print("LinkedList cycle length: " + str(find_cycle_length(head)))


   main()


   '''
   Time and Space Complexity:
   The above algorithm runs in O(N) time complexity and O(1) space complexity.
   '''

Start of LinkedList Cycle (medium)
---------------------------------------
LeetCode：\ `142. Linked List Cycle II`_

.. _142. Linked List Cycle II: https://leetcode.com/problems/linked-list-cycle-ii/

.. code:: python

   '''
   Problem Statement
   Given the head of a Singly LinkedList that contains a cycle, write a function to find the starting node of the cycle.
   '''

   # mycode
   class Node:
       def __init__(self, value, next=None):
           self.value = value
           self.next = next


   def find_cycle_start(head):
       if not head:
           return None

       fast = slow = head

       while fast and fast.next:
           fast = fast.next.next
           slow = slow.next
           if fast == slow:
               fast = head
               while fast and fast != slow:
                   fast = fast.next
                   slow = slow.next
               return fast
       return None


   def main():
       head = Node(1)
       head.next = Node(2)
       head.next.next = Node(3)
       head.next.next.next = Node(4)
       head.next.next.next.next = Node(5)
       head.next.next.next.next.next = Node(6)

       head.next.next.next.next.next.next = head.next.next
       print("LinkedList cycle start: " + str(find_cycle_start(head).value))

       head.next.next.next.next.next.next = head.next.next.next
       print("LinkedList cycle start: " + str(find_cycle_start(head).value))

       head.next.next.next.next.next.next = head
       print("LinkedList cycle start: " + str(find_cycle_start(head).value))


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
               print(temp.value, end='')
               temp = temp.next
           print()


   def find_cycle_start(head):
       cycle_length = 0
       # find the LinkedList cycle
       slow, fast = head, head
       while (fast is not None and fast.next is not None):
           fast = fast.next.next
           slow = slow.next
           if slow == fast:  # found the cycle
               cycle_length = calculate_cycle_length(slow)
               break
       return find_start(head, cycle_length)


   def calculate_cycle_length(slow):
       current = slow
       cycle_length = 0
       while True:
           current = current.next
           cycle_length += 1
           if current == slow:
               break
       return cycle_length


   def find_start(head, cycle_length):
       pointer1 = head
       pointer2 = head
       # move pointer2 ahead 'cycle_length' nodes
       while cycle_length > 0:
           pointer2 = pointer2.next
           cycle_length -= 1
       # increment both pointers until they meet at the start of the cycle
       while pointer1 != pointer2:
           pointer1 = pointer1.next
           pointer2 = pointer2.next
       return pointer1


   def main():
       head = Node(1)
       head.next = Node(2)
       head.next.next = Node(3)
       head.next.next.next = Node(4)
       head.next.next.next.next = Node(5)
       head.next.next.next.next.next = Node(6)

       head.next.next.next.next.next.next = head.next.next
       print("LinkedList cycle start: " + str(find_cycle_start(head).value))

       head.next.next.next.next.next.next = head.next.next.next
       print("LinkedList cycle start: " + str(find_cycle_start(head).value))

       head.next.next.next.next.next.next = head
       print("LinkedList cycle start: " + str(find_cycle_start(head).value))


   main()


   '''
   Time Complexity
   As we know, finding the cycle in a LinkedList with ‘N’ nodes and also finding the length of the cycle requires O(N).
   Also, as we saw in the above algorithm, we will need O(N) to find the start of the cycle.
   Therefore, the overall time complexity of our algorithm will be O(N).
   Space Complexity
   The algorithm runs in constant space O(1).
   '''

Happy Number (medium)
---------------------------------------
LeetCode：\ `202. Happy Number`_

.. _202. Happy Number: https://leetcode.com/problems/happy-number/

.. code:: python

   '''
   Problem Statement
   Any number will be called a happy number if,
   after repeatedly replacing it with a number equal to the sum of the square of all of its digits,
   leads us to number ‘1’. All other (not-happy) numbers will never reach ‘1’.
   Instead, they will be stuck in a cycle of numbers which does not include ‘1’.
   '''


   # mycode
   def find_happy_number(num):
       fast, slow = num, num
       while True:
           fast = square(square(fast))
           slow = square(slow)

           if fast == slow:
               break

       return slow == 1


   def square(num):
       square_num = 0
       while num > 0:
           square_num += (num % 10)**2
           num = num // 10
       return square_num


   def main():
       print(find_happy_number(23))
       print(find_happy_number(12))


   main()


   '''
   Time Complexity
   The time complexity of the algorithm is difficult to determine.
   However we know the fact that all unhappy numbers eventually get stuck in the cycle: 4 -> 16 -> 37 -> 58 -> 89 -> 145 -> 42 -> 20 -> 4
   This sequence behavior tells us two things:
   1. If the number N is less than or equal to 1000, then we reach the cycle or ‘1’ in at most 1001 steps.
   2. For N > 1000, suppose the number has ‘M’ digits and the next number is ‘N1’.
   From the above Wikipedia link, we know that the sum of the squares of the digits of ‘N’ is at most 9^2 M, or 81M
   (this will happen when all digits of ‘N’ are ‘9’).
   This means:
   1. N1 < 81M
   2. As we know M = log(N+1)
   3. Therefore: N1 < 81 * log(N+1) => N1 = O(logN)
   This concludes that the above algorithm will have a time complexity of O(logN).
   Space Complexity
   The algorithm runs in constant space O(1).
   '''

Middle of the LinkedList (easy)
---------------------------------------
.. code:: python

   '''
   Problem Statement
   Given the head of a Singly LinkedList, write a method to return the middle node of the LinkedList.
   If the total number of nodes in the LinkedList is even, return the second middle node.
   Example 1:
   Input: 1 -> 2 -> 3 -> 4 -> 5 -> null
   Output: 3
   Example 2:
   Input: 1 -> 2 -> 3 -> 4 -> 5 -> 6 -> null
   Output: 4
   Example 3:
   Input: 1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7 -> null
   Output: 4
   '''


   class Node:
       def __init__(self, value, next=None):
           self.value = value
           self.next = next


   def find_middle_of_linked_list(head):
       # TODO: Write your code here
       slow, fast = head, head
       while fast is not None and fast.next is not None:
           fast = fast.next.next
           slow = slow.next
       return slow


   def main():
       head = Node(1)
       head.next = Node(2)
       head.next.next = Node(3)
       head.next.next.next = Node(4)
       head.next.next.next.next = Node(5)

       print("Middle Node: " + str(find_middle_of_linked_list(head).value))

       head.next.next.next.next.next = Node(6)
       print("Middle Node: " + str(find_middle_of_linked_list(head).value))

       head.next.next.next.next.next.next = Node(7)
       print("Middle Node: " + str(find_middle_of_linked_list(head).value))


   main()


   '''
   Time complexity
   The above algorithm will have a time complexity of O(N) where ‘N’ is the number of nodes in the LinkedList.
   Space complexity
   The algorithm runs in constant space O(1).
   '''

Problem Challenge 1 - Palindrome LinkedList (medium)
-----------------------------------------------------
.. code:: python

   '''
   Problem Challenge 1
   Palindrome LinkedList (medium)
   Given the head of a Singly LinkedList, write a method to check if the LinkedList is a palindrome or not.
   Your algorithm should use constant space and the input LinkedList should be in the original form once the algorithm is finished. The algorithm should have O(N)O(N) time complexity where ‘N’ is the number of nodes in the LinkedList.
   Example 1:
   Input: 2 -> 4 -> 6 -> 4 -> 2 -> null
   Output: true
   Example 2:
   Input: 2 -> 4 -> 6 -> 4 -> 2 -> 2 -> null
   Output: false
   '''


   # mycode
   class Node:
       def __init__(self, value, next=None):
           self.value = value
           self.next = next


   def is_palindromic_linked_list(head):
       # TODO: Write your code here
       slow, fast = head, head
       while fast is not None and fast.next is not None:
           slow = slow.next
           fast = fast.next.next

       end = reverse(slow)
       copy_end = end

       while head is not None and end is not None:

           if head.value != end.value:

               return False
           head = head.next
           end = end.next

       reverse(copy_end)

       return True


   def reverse(head):
       former, latter = None, head
       temp = None
       while latter:
           temp = latter
           latter = latter.next
           temp.next = former
           former = temp

       return temp


   def main():
       head = Node(2)
       head.next = Node(4)
       head.next.next = Node(6)
       head.next.next.next = Node(4)
       head.next.next.next.next = Node(2)

       print("Is palindrome: " + str(is_palindromic_linked_list(head)))

       head.next.next.next.next.next = Node(2)
       print("Is palindrome: " + str(is_palindromic_linked_list(head)))


   main()


   # answer
   class Node:
       def __init__(self, value, next=None):
           self.value = value
           self.next = next


   def is_palindromic_linked_list(head):
       if head is None or head.next is None:
           return True

       # find middle of the LinkedList
       slow, fast = head, head
       while (fast is not None and fast.next is not None):
           slow = slow.next
           fast = fast.next.next

       head_second_half = reverse(slow)  # reverse the second half
       # store the head of reversed part to revert back later
       copy_head_second_half = head_second_half

       # compare the first and the second half
       while (head is not None and head_second_half is not None):
           if head.value != head_second_half.value:
               break  # not a palindrome

           head = head.next
           head_second_half = head_second_half.next

       reverse(copy_head_second_half)  # revert the reverse of the second half

       if head is None or head_second_half is None:  # if both halves match
           return True

       return False


   def reverse(head):
       prev = None
       while (head is not None):
           next = head.next
           head.next = prev
           prev = head
           head = next
       return prev


   def main():
       head = Node(2)
       head.next = Node(4)
       head.next.next = Node(6)
       head.next.next.next = Node(4)
       head.next.next.next.next = Node(2)

       print("Is palindrome: " + str(is_palindromic_linked_list(head)))

       head.next.next.next.next.next = Node(2)
       print("Is palindrome: " + str(is_palindromic_linked_list(head)))


   main()


   '''
   Time complexity
   The above algorithm will have a time complexity of O(N) where ‘N’ is the number of nodes in the LinkedList.
   Space complexity
   The algorithm runs in constant space O(1).
   '''

Problem Challenge 2 - Rearrange a LinkedList (medium)
------------------------------------------------------
.. code:: python

   '''
   Problem Challenge 2
   Rearrange a LinkedList (medium)
   Given the head of a Singly LinkedList, write a method to modify the LinkedList such that the nodes from the second half of the LinkedList are inserted alternately to the nodes from the first half in reverse order. So if the LinkedList has nodes 1 -> 2 -> 3 -> 4 -> 5 -> 6 -> null, your method should return 1 -> 6 -> 2 -> 5 -> 3 -> 4 -> null.
   Your algorithm should not use any extra space and the input LinkedList should be modified in-place.
   Example 1:
   Input: 2 -> 4 -> 6 -> 8 -> 10 -> 12 -> null
   Output: 2 -> 12 -> 4 -> 10 -> 6 -> 8 -> null
   Example 2:
   Input: 2 -> 4 -> 6 -> 8 -> 10 -> null
   Output: 2 -> 10 -> 4 -> 8 -> 6 -> null
   '''

   # mycode
   from __future__ import print_function


   class Node:
       def __init__(self, value, next=None):
           self.value = value
           self.next = next

       def print_list(self):
           temp = self
           while temp is not None:
               print(str(temp.value) + " ", end='')
               temp = temp.next
           print()


   def reorder(head):
       # TODO: Write your code here
       slow, fast = head, head
       while fast is not None and fast.next is not None:
           slow = slow.next
           fast = fast.next.next

       end = reverse(slow)

       head_temp = head

       while end:

           temp = end
           end = end.next
           temp.next = head_temp.next
           head_temp.next = temp

           head_temp = head_temp.next.next
       head_temp.next = None

       return head


   def reverse(head):
       former, latter = None, head

       while latter:
           temp = latter
           latter = latter.next
           temp.next = former
           former = temp

       return temp


   def main():
       head = Node(2)
       head.next = Node(4)
       head.next.next = Node(6)
       head.next.next.next = Node(8)
       head.next.next.next.next = Node(10)
       head.next.next.next.next.next = Node(12)

       reorder(head)
       head.print_list()


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
               print(str(temp.value) + " ", end='')
               temp = temp.next
           print()


   def reorder(head):
       if head is None or head.next is None:
           return

       # find middle of the LinkedList
       slow, fast = head, head
       while fast is not None and fast.next is not None:
           slow = slow.next
           fast = fast.next.next

       # slow is now pointing to the middle node
       head_second_half = reverse(slow)  # reverse the second half
       head_first_half = head

       # rearrange to produce the LinkedList in the required order
       while head_first_half is not None and head_second_half is not None:
           temp = head_first_half.next
           head_first_half.next = head_second_half
           head_first_half = temp

           temp = head_second_half.next
           head_second_half.next = head_first_half
           head_second_half = temp

       # set the next of the last node to 'None'
       if head_first_half is not None:
           head_first_half.next = None


   def reverse(head):
       prev = None
       while head is not None:
           next = head.next
           head.next = prev
           prev = head
           head = next
       return prev


   def main():
       head = Node(2)
       head.next = Node(4)
       head.next.next = Node(6)
       head.next.next.next = Node(8)
       head.next.next.next.next = Node(10)
       head.next.next.next.next.next = Node(12)
       reorder(head)
       head.print_list()


   main()


   '''
   Time Complexity
   The above algorithm will have a time complexity of O(N) where ‘N’ is the number of nodes in the LinkedList.
   Space Complexity
   The algorithm runs in constant space O(1).
   '''

Problem Challenge 3 - Cycle in a Circular Array (hard)
---------------------------------------------------------
.. code:: python

   '''
   Problem Challenge 3
   Cycle in a Circular Array (hard)
   We are given an array containing positive and negative numbers. Suppose the array contains a number ‘M’ at a particular index.
   Now, if ‘M’ is positive we will move forward ‘M’ indices and if ‘M’ is negative move backwards ‘M’ indices. You should assume that the array is circular which means two things:
   If, while moving forward, we reach the end of the array, we will jump to the first element to continue the movement.
   If, while moving backward, we reach the beginning of the array, we will jump to the last element to continue the movement.
   Write a method to determine if the array has a cycle. The cycle should have more than one element and should follow one direction which means the cycle should not contain both forward and backward movements.
   Example 1:
   Input: [1, 2, -1, 2, 2]
   Output: true
   Explanation: The array has a cycle among indices: 0 -> 1 -> 3 -> 0
   Example 2:
   Input: [2, 2, -1, 2]
   Output: true
   Explanation: The array has a cycle among indices: 1 -> 3 -> 1
   Example 3:
   Input: [2, 1, -1, -2]
   Output: false
   Explanation: The array does not have any cycle.
   '''


   def circular_array_loop_exists(arr):
       for i in range(len(arr)):
           is_forward = arr[i] >= 0  # if we are moving forward or not
           slow, fast = i, i

           # if slow or fast becomes '-1' this means we can't find cycle for this number
           while True:
               # move one step for slow pointer
               slow = find_next_index(arr, is_forward, slow)
               # move one step for fast pointer
               fast = find_next_index(arr, is_forward, fast)
               if (fast != -1):
                   # move another step for fast pointer
                   fast = find_next_index(arr, is_forward, fast)
               if slow == -1 or fast == -1 or slow == fast:
                   break

           if slow != -1 and slow == fast:
               return True

       return False


   def find_next_index(arr, is_forward, current_index):
       direction = arr[current_index] >= 0

       if is_forward != direction:
           return -1  # change in direction, return -1

       next_index = (current_index + arr[current_index]) % len(arr)

       # one element cycle, return -1
       if next_index == current_index:
           next_index = -1

       return next_index


   def main():
       print(circular_array_loop_exists([1, 2, -1, 2, 2]))
       print(circular_array_loop_exists([2, 2, -1, 2]))
       print(circular_array_loop_exists([2, 1, -1, -2]))


   main()


   '''
   Time Complexity
   The above algorithm will have a time complexity of O(N^2) where ‘N’ is the number of elements in the array.
   This complexity is due to the fact that we are iterating all elements of the array and trying to find a cycle for each element.
   Space Complexity
   The algorithm runs in constant space O(1).
   An Alternate Approach
   In our algorithm, we don’t keep a record of all the numbers that have been evaluated for cycles.
   We know that all such numbers will not produce a cycle for any other instance as well.
   If we can remember all the numbers that have been visited, our algorithm will improve to O(N) as, then, each number will be evaluated for cycles only once.
   We can keep track of this by creating a separate array however the space complexity of our algorithm will increase to O(N).
   '''
