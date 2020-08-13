=========================
DFS
=========================


Check whether there is a path from \|start\| to \|target\| in graph G.

neighbor(x) returns the neighbors of x in G.

.. code:: python

   seen = set([start])

   def dfs(n):
       if n == target:
           return True
       for t in neighbor(n):
           if t in seen:
               continue
           seen.add(t)
           if dfs(t):
               return True
           seen.remove(t)  # back-tracking
       return False

   return dfs(start)
