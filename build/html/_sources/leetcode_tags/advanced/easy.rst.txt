=======
Easy
=======


225. Implement Stack using Queues
------------------------------------------------------

`225. Implement Stack using Queues`_

.. code:: python

   class MyStack:

       def __init__(self):
           self.queue = collections.deque([])

       def push(self, x: int) -> None:
           self.queue.append(x)

       def pop(self) -> int:
           return self.queue.pop()

       def top(self) -> int:
           return self.queue[-1]

       def empty(self) -> bool:
           return len(self.queue) == 0

   # Your MyStack object will be instantiated and called as such:
   # obj = MyStack()
   # obj.push(x)
   # param_2 = obj.pop()
   # param_3 = obj.top()
   # param_4 = obj.empty()

.. _225. Implement Stack using Queues: https://leetcode.com/problems/implement-stack-using-queues/


232. Implement Queue using Stacks
------------------------------------------------------

`232. Implement Queue using Stacks`_

.. code:: python

   class MyQueue:

       def __init__(self):
           self.inStack, self.outStack = [], []

       def push(self, x: int) -> None:
           self.inStack.append(x)

       def pop(self) -> int:
           self.move()
           return self.outStack.pop()

       def peek(self) -> int:
           self.move()
           return self.outStack[-1]

       def empty(self) -> bool:
           return not self.inStack and not self.outStack

       def move(self):
           if not self.outStack:
               while self.inStack:
                   self.outStack.append(self.inStack.pop())

.. _232. Implement Queue using Stacks: https://leetcode.com/problems/implement-queue-using-stacks/
