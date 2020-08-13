=========================
BFS
=========================

Find the shortest path from \|start\| to \|target\| in a unweighted graph G.

neighbor(x) returns the neighbors of x in G.

.. code:: python

   q = deque([start])
   seen = set([start])
   steps = 0

   while q:
       size = len(q)
       for _ in range(size):
           n = q.popleft()
           if n == target:
               return steps
           for t in neighbor(n):
               if t in seen:
                   continue
               q.append(t)
               seen.add(t)
       steps += 1
   return -1  # not found
