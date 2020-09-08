Topological Sort (medium)
-----------------------------------
.. code:: python

   '''
   Problem Statement
   Topological Sort of a directed graph (a graph with unidirectional edges) is a linear ordering of its vertices such that for every directed edge (U, V) from vertex U to vertex V, U comes before V in the ordering.
   Given a directed graph, find the topological ordering of its vertices.
   Example 1:
   Input: Vertices=4, Edges=[3, 2], [3, 0], [2, 0], [2, 1]
   Output: Following are the two valid topological sorts for the given graph:
   1) 3, 2, 0, 1
   2) 3, 2, 1, 0
   Example 2:
   Input: Vertices=5, Edges=[4, 2], [4, 3], [2, 0], [2, 1], [3, 1]
   Output: Following are all valid topological sorts for the given graph:
   1) 4, 2, 3, 0, 1
   2) 4, 3, 2, 0, 1
   3) 4, 3, 2, 1, 0
   4) 4, 2, 3, 1, 0
   5) 4, 2, 0, 3, 1
   Example 3:
   Input: Vertices=7, Edges=[6, 4], [6, 2], [5, 3], [5, 4], [3, 0], [3, 1], [3, 2], [4, 1]
   Output: Following are all valid topological sorts for the given graph:
   1) 5, 6, 3, 4, 0, 1, 2
   2) 6, 5, 3, 4, 0, 1, 2
   3) 5, 6, 4, 3, 0, 2, 1
   4) 6, 5, 4, 3, 0, 1, 2
   5) 5, 6, 3, 4, 0, 2, 1
   6) 5, 6, 3, 4, 1, 2, 0

   There are other valid topological ordering of the graph too.
   '''

   # mycode
   from collections import deque


   def topological_sort(vertices, edges):
       sortedOrder = []
       # TODO: Write your code here
       inDegree = {i: 0 for i in range(vertices)}
       graph = {i: [] for i in range(vertices)}

       for edge in edges:
           in_node, out_node = edge[0], edge[1]
           graph[in_node].append(out_node)
           inDegree[out_node] += 1

       sources = deque()
       for key in graph:
           if inDegree[key] == 0:
               sources.append(key)

       while sources:
           in_node = sources.popleft()
           sortedOrder.append(in_node)

           for i in graph[in_node]:
               inDegree[i] -= 1
               if inDegree[i] == 0:
                   sources.append(i)

       if len(sortedOrder) != vertices:
           return []

       return sortedOrder


   def main():
       print("Topological sort: " +
             str(topological_sort(4, [[3, 2], [3, 0], [2, 0], [2, 1]])))
       print("Topological sort: " +
             str(topological_sort(5, [[4, 2], [4, 3], [2, 0], [2, 1], [3, 1]])))
       print("Topological sort: " + str(
           topological_sort(7, [[6, 4], [6, 2], [5, 3], [5, 4], [3, 0], [3, 1],
                                [3, 2], [4, 1]])))


   main()

   # answer
   from collections import deque


   def topological_sort(vertices, edges):
       sortedOrder = []
       if vertices <= 0:
           return sortedOrder

       # a. Initialize the graph
       inDegree = {i: 0 for i in range(vertices)}  # count of incoming edges
       graph = {i: [] for i in range(vertices)}  # adjacency list graph

       # b. Build the graph
       for edge in edges:
           parent, child = edge[0], edge[1]
           graph[parent].append(child)  # put the child into it's parent's list
           inDegree[child] += 1  # increment child's inDegree

       # c. Find all sources i.e., all vertices with 0 in-degrees
       sources = deque()
       for key in inDegree:
           if inDegree[key] == 0:
               sources.append(key)

       # d. For each source, add it to the sortedOrder and subtract one from all of its children's in-degrees
       # if a child's in-degree becomes zero, add it to the sources queue
       while sources:
           vertex = sources.popleft()
           sortedOrder.append(vertex)
           for child in graph[
                   vertex]:  # get the node's children to decrement their in-degrees
               inDegree[child] -= 1
               if inDegree[child] == 0:
                   sources.append(child)

       # topological sort is not possible as the graph has a cycle
       if len(sortedOrder) != vertices:
           return []

       return sortedOrder


   def main():
       print("Topological sort: " +
             str(topological_sort(4, [[3, 2], [3, 0], [2, 0], [2, 1]])))
       print("Topological sort: " +
             str(topological_sort(5, [[4, 2], [4, 3], [2, 0], [2, 1], [3, 1]])))
       print("Topological sort: " + str(
           topological_sort(7, [[6, 4], [6, 2], [5, 3], [5, 4], [3, 0], [3, 1],
                                [3, 2], [4, 1]])))


   main()


   '''
   Time Complexity
   In step ‘d’, each vertex will become a source only once and each edge will be accessed and removed once.
   Therefore, the time complexity of the above algorithm will be O(V+E),
   where ‘V’ is the total number of vertices and ‘E’ is the total number of edges in the graph.
   Space Complexity
   The space complexity will be O(V+E), since we are storing all of the edges for each vertex in an adjacency list.
   '''
   '''
   Similar Problems
   Problem 1: Find if a given Directed Graph has a cycle in it or not.
   Solution: If we can’t determine the topological ordering of all the vertices of a directed graph, the graph has a cycle in it. This was also referred to in the above code:
       if (sortedOrder.size() != vertices) // topological sort is not possible as the graph has a cycle
         return new ArrayList<>();
   '''

Tasks Scheduling (medium)
-----------------------------------
.. code:: python

   '''
   Problem Statement
   There are ‘N’ tasks, labeled from ‘0’ to ‘N-1’. Each task can have some prerequisite tasks which need to be completed before it can be scheduled. Given the number of tasks and a list of prerequisite pairs, find out if it is possible to schedule all the tasks.
   Example 1:
   Input: Tasks=3, Prerequisites=[0, 1], [1, 2]
   Output: true
   Explanation: To execute task '1', task '0' needs to finish first. Similarly, task '1' needs to finish
   before '2' can be scheduled. A possible sceduling of tasks is: [0, 1, 2]
   Example 2:
   Input: Tasks=3, Prerequisites=[0, 1], [1, 2], [2, 0]
   Output: false
   Explanation: The tasks have cyclic dependency, therefore they cannot be scheduled.
   Example 3:
   Input: Tasks=6, Prerequisites=[2, 5], [0, 5], [0, 4], [1, 4], [3, 2], [1, 3]
   Output: true
   Explanation: A possible scHeduling of tasks is: [0 1 4 3 2 5]
   '''

   # mycode
   from collections import deque


   def is_scheduling_possible(tasks, prerequisites):
       # TODO: Write your code here
       sortedOrder = []

       inDegree = {i: 0 for i in range(tasks)}
       graph = {i: [] for i in range(tasks)}

       for i in prerequisites:
           start, end = i[0], i[1]
           graph[start].append(end)
           inDegree[end] += 1

       sources = deque()
       for key in inDegree:
           if inDegree[key] == 0:
               sources.append(key)

       while sources:
           node = sources.popleft()
           sortedOrder.append(node)

           for i in graph[node]:
               inDegree[i] -= 1
               if inDegree[i] == 0:
                   sources.append(i)

       if len(sortedOrder) == tasks:
           return True
       return False


   def main():
       print("Is scheduling possible: " +
             str(is_scheduling_possible(3, [[0, 1], [1, 2]])))
       print("Is scheduling possible: " +
             str(is_scheduling_possible(3, [[0, 1], [1, 2], [2, 0]])))
       print("Is scheduling possible: " +
             str(is_scheduling_possible(6, [[0, 4], [1, 4], [3, 2], [1, 3]])))


   main()

   # answer
   from collections import deque

   def is_scheduling_possible(tasks, prerequisites):
       sortedOrder = []
       if tasks <= 0:
           return False

       # a. Initialize the graph
       inDegree = {i: 0 for i in range(tasks)}  # count of incoming edges
       graph = {i: [] for i in range(tasks)}  # adjacency list graph

       # b. Build the graph
       for prerequisite in prerequisites:
           parent, child = prerequisite[0], prerequisite[1]
           graph[parent].append(child)  # put the child into it's parent's list
           inDegree[child] += 1  # increment child's inDegree

       # c. Find all sources i.e., all vertices with 0 in-degrees
       sources = deque()
       for key in inDegree:
           if inDegree[key] == 0:
               sources.append(key)

       # d. For each source, add it to the sortedOrder and subtract one from all of its children's in-degrees
       # if a child's in-degree becomes zero, add it to the sources queue
       while sources:
           vertex = sources.popleft()
           sortedOrder.append(vertex)
           for child in graph[
                   vertex]:  # get the node's children to decrement their in-degrees
               inDegree[child] -= 1
               if inDegree[child] == 0:
                   sources.append(child)

       # if sortedOrder doesn't contain all tasks, there is a cyclic dependency between tasks, therefore, we
       # will not be able to schedule all tasks
       return len(sortedOrder) == tasks


   def main():
       print("Is scheduling possible: " +
             str(is_scheduling_possible(3, [[0, 1], [1, 2]])))
       print("Is scheduling possible: " +
             str(is_scheduling_possible(3, [[0, 1], [1, 2], [2, 0]])))
       print("Is scheduling possible: " +
             str(is_scheduling_possible(6, [[0, 4], [1, 4], [3, 2], [1, 3]])))


   main()


   '''
   Time complexity
   In step ‘d’, each task can become a source only once and each edge (prerequisite) will be accessed and removed once.
   Therefore, the time complexity of the above algorithm will be O(V+E),
   where ‘V’ is the total number of tasks and ‘E’ is the total number of prerequisites.
   Space complexity
   The space complexity will be O(V+E),
   since we are storing all of the prerequisites for each task in an adjacency list.
   '''


   '''
   Similar Problems
   Course Schedule: There are ‘N’ courses, labeled from ‘0’ to ‘N-1’.
   Each course can have some prerequisite courses which need to be completed before it can be taken.
   Given the number of courses and a list of prerequisite pairs,
   find if it is possible for a student to take all the courses.
   Solution: This problem is exactly similar to our parent problem.
   In this problem, we have courses instead of tasks.
   '''

Tasks Scheduling Order (medium)
-----------------------------------
.. code:: python

   '''
   Problem Statement
   There are ‘N’ tasks, labeled from ‘0’ to ‘N-1’. Each task can have some prerequisite tasks which need to be completed before it can be scheduled. Given the number of tasks and a list of prerequisite pairs, write a method to find the ordering of tasks we should pick to finish all tasks.
   Example 1:
   Input: Tasks=3, Prerequisites=[0, 1], [1, 2]
   Output: [0, 1, 2]
   Explanation: To execute task '1', task '0' needs to finish first. Similarly, task '1' needs to finish
   before '2' can be scheduled. A possible scheduling of tasks is: [0, 1, 2]
   Example 2:
   Input: Tasks=3, Prerequisites=[0, 1], [1, 2], [2, 0]
   Output: []
   Explanation: The tasks have cyclic dependency, therefore they cannot be scheduled.
   Example 3:
   Input: Tasks=6, Prerequisites=[2, 5], [0, 5], [0, 4], [1, 4], [3, 2], [1, 3]
   Output: [0 1 4 3 2 5]
   Explanation: A possible scheduling of tasks is: [0 1 4 3 2 5]
   '''

   # mycode
   from collections import deque


   def find_order(tasks, prerequisites):
       sortedOrder = []
       # TODO: Write your code here
       inDegree = {i: 0 for i in range(tasks)}
       graph = {i: [] for i in range(tasks)}

       for edge in prerequisites:
           in_node, out_node = edge[0], edge[1]
           graph[in_node].append(out_node)
           inDegree[out_node] += 1

       sources = deque()
       for key in graph:
           if inDegree[key] == 0:
               sources.append(key)

       while sources:
           in_node = sources.popleft()
           sortedOrder.append(in_node)

           for i in graph[in_node]:
               inDegree[i] -= 1
               if inDegree[i] == 0:
                   sources.append(i)

       if len(sortedOrder) != tasks:
           return []

       return sortedOrder


   def main():
       print("Is scheduling possible: " + str(find_order(3, [[0, 1], [1, 2]])))
       print("Is scheduling possible: " +
             str(find_order(3, [[0, 1], [1, 2], [2, 0]])))
       print("Is scheduling possible: " +
             str(find_order(6, [[2, 5], [0, 5], [0, 4], [1, 4], [3, 2], [1, 3]])))


   main()

   # answer
   from collections import deque


   def find_order(tasks, prerequisites):
       sortedOrder = []
       if tasks <= 0:
           return sortedOrder

       # a. Initialize the graph
       inDegree = {i: 0 for i in range(tasks)}  # count of incoming edges
       graph = {i: [] for i in range(tasks)}  # adjacency list graph

       # b. Build the graph
       for prerequisite in prerequisites:
           parent, child = prerequisite[0], prerequisite[1]
           graph[parent].append(child)  # put the child into it's parent's list
           inDegree[child] += 1  # increment child's inDegree

       # c. Find all sources i.e., all vertices with 0 in-degrees
       sources = deque()
       for key in inDegree:
           if inDegree[key] == 0:
               sources.append(key)

       # d. For each source, add it to the sortedOrder and subtract one from all of its children's in-degrees
       # if a child's in-degree becomes zero, add it to the sources queue
       while sources:
           vertex = sources.popleft()
           sortedOrder.append(vertex)
           for child in graph[
                   vertex]:  # get the node's children to decrement their in-degrees
               inDegree[child] -= 1
               if inDegree[child] == 0:
                   sources.append(child)

       # if sortedOrder doesn't contain all tasks, there is a cyclic dependency between tasks, therefore, we
       # will not be able to schedule all tasks
       if len(sortedOrder) != tasks:
           return []

       return sortedOrder


   def main():
       print("Is scheduling possible: " + str(find_order(3, [[0, 1], [1, 2]])))
       print("Is scheduling possible: " +
             str(find_order(3, [[0, 1], [1, 2], [2, 0]])))
       print("Is scheduling possible: " +
             str(find_order(6, [[2, 5], [0, 5], [0, 4], [1, 4], [3, 2], [1, 3]])))


   main()


   '''
   Time complexity
   In step ‘d’, each task can become a source only once and each edge (prerequisite) will be accessed and removed once.
   Therefore, the time complexity of the above algorithm will be O(V+E),
   where ‘V’ is the total number of tasks and ‘E’ is the total number of prerequisites.
   Space complexity
   The space complexity will be O(V+E), since we are storing all of the prerequisites for each task in an adjacency list.
   '''


   '''
   Similar Problems
   Course Schedule: There are ‘N’ courses, labeled from ‘0’ to ‘N-1’.
   Each course has some prerequisite courses which need to be completed before it can be taken.
   Given the number of courses and a list of prerequisite pairs,
   write a method to find the best ordering of the courses that a student can take in order to finish all courses.
   Solution: This problem is exactly similar to our parent problem. In this problem, we have courses instead of tasks.
   '''

All Tasks Scheduling Orders (hard)
-----------------------------------
.. code:: python

   '''
   Problem Statement
   There are ‘N’ tasks, labeled from ‘0’ to ‘N-1’.
   Each task can have some prerequisite tasks which need to be completed before it can be scheduled.
   Given the number of tasks and a list of prerequisite pairs,
   write a method to print all possible ordering of tasks meeting all prerequisites.
   Example 1:
   Input: Tasks=3, Prerequisites=[0, 1], [1, 2]
   Output: [0, 1, 2]
   Explanation: There is only possible ordering of the tasks.
   Example 2:
   Input: Tasks=4, Prerequisites=[3, 2], [3, 0], [2, 0], [2, 1]
   Output:
   1) [3, 2, 0, 1]
   2) [3, 2, 1, 0]
   Explanation: There are two possible orderings of the tasks meeting all prerequisites.
   Example 3:
   Input: Tasks=6, Prerequisites=[2, 5], [0, 5], [0, 4], [1, 4], [3, 2], [1, 3]
   Output:
   1) [0, 1, 4, 3, 2, 5]
   2) [0, 1, 3, 4, 2, 5]
   3) [0, 1, 3, 2, 4, 5]
   4) [0, 1, 3, 2, 5, 4]
   5) [1, 0, 3, 4, 2, 5]
   6) [1, 0, 3, 2, 4, 5]
   7) [1, 0, 3, 2, 5, 4]
   8) [1, 0, 4, 3, 2, 5]
   9) [1, 3, 0, 2, 4, 5]
   10) [1, 3, 0, 2, 5, 4]
   11) [1, 3, 0, 4, 2, 5]
   12) [1, 3, 2, 0, 5, 4]
   13) [1, 3, 2, 0, 4, 5]
   '''

   # mycode
   from collections import deque


   def print_orders(tasks, prerequisites):
       # TODO: Write your code here
       sortedOrder = []

       inDegree = {i: 0 for i in range(tasks)}
       graph = {i: [] for i in range(tasks)}

       for prerequisite in prerequisites:
           start, end = prerequisite[0], prerequisite[1]
           graph[start].append(end)
           inDegree[end] += 1

       sources = deque()
       for key in inDegree:
           if inDegree[key] == 0:
               sources.append(key)

       print_all_topological_sorts(graph, inDegree, sources, sortedOrder)


   def print_all_topological_sorts(graph, inDegree, sources, sortedOrder):
       if sources:
           for vertex in sources:
               sortedOrder.append(vertex)
               next_sources = sources.copy()
               next_sources.remove(vertex)

               for i in graph[vertex]:
                   inDegree[i] -= 1
                   if inDegree[i] == 0:
                       next_sources.append(i)

               print_all_topological_sorts(graph, inDegree, next_sources,
                                           sortedOrder)

               sortedOrder.remove(vertex)
               for i in graph[vertex]:
                   inDegree[i] += 1

       if len(sortedOrder) == len(inDegree):
           print(sortedOrder)


   def main():
       print("Task Orders: ")
       print_orders(3, [[0, 1], [1, 2]])

       print("Task Orders: ")
       print_orders(4, [[3, 2], [3, 0], [2, 0], [2, 1]])

       print("Task Orders: ")
       print_orders(6, [[2, 5], [0, 5], [0, 4], [1, 4], [3, 2], [1, 3]])


   main()

   # answer
   from collections import deque


   def print_orders(tasks, prerequisites):
       sortedOrder = []
       if tasks <= 0:
           return False

       # a. Initialize the graph
       inDegree = {i: 0 for i in range(tasks)}  # count of incoming edges
       graph = {i: [] for i in range(tasks)}  # adjacency list graph

       # b. Build the graph
       for prerequisite in prerequisites:
           parent, child = prerequisite[0], prerequisite[1]
           graph[parent].append(child)  # put the child into it's parent's list
           inDegree[child] += 1  # increment child's inDegree

       # c. Find all sources i.e., all vertices with 0 in-degrees
       sources = deque()
       for key in inDegree:
           if inDegree[key] == 0:
               sources.append(key)

       print_all_topological_sorts(graph, inDegree, sources, sortedOrder)


   def print_all_topological_sorts(graph, inDegree, sources, sortedOrder):
       if sources:
           for vertex in sources:
               sortedOrder.append(vertex)
               sourcesForNextCall = deque(sources)  # make a copy of sources
               # only remove the current source, all other sources should remain in the queue for the next call
               sourcesForNextCall.remove(vertex)
               # get the node's children to decrement their in-degrees
               for child in graph[vertex]:
                   inDegree[child] -= 1
                   if inDegree[child] == 0:
                       sourcesForNextCall.append(child)

               # recursive call to print other orderings from the remaining (and new) sources
               print_all_topological_sorts(graph, inDegree, sourcesForNextCall,
                                           sortedOrder)

               # backtrack, remove the vertex from the sorted order and put all of its children back to consider
               # the next source instead of the current vertex
               sortedOrder.remove(vertex)
               for child in graph[vertex]:
                   inDegree[child] += 1

       # if sortedOrder doesn't contain all tasks, either we've a cyclic dependency between tasks, or
       # we have not processed all the tasks in this recursive call
       if len(sortedOrder) == len(inDegree):
           print(sortedOrder)


   def main():
       print("Task Orders: ")
       print_orders(3, [[0, 1], [1, 2]])

       print("Task Orders: ")
       print_orders(4, [[3, 2], [3, 0], [2, 0], [2, 1]])

       print("Task Orders: ")
       print_orders(6, [[2, 5], [0, 5], [0, 4], [1, 4], [3, 2], [1, 3]])


   main()


   '''
   Time and Space Complexity
   If we don’t have any prerequisites, all combinations of the tasks can represent a topological ordering.
   As we know, that there can be N! combinations for ‘N’ numbers,
   therefore the time and space complexity of our algorithm will be O(V! * E)
   where ‘V’ is the total number of tasks and ‘E’ is the total prerequisites.
   We need the ‘E’ part because in each recursive call, at max, we remove (and add back) all the edges.
   '''


Alien Dictionary (hard)
-----------------------------------
.. code:: python

   '''
   Problem Statement
   There is a dictionary containing words from an alien language for which we don’t know the ordering of the characters. Write a method to find the correct order of characters in the alien language.
   Example 1:
   Input: Words: ["ba", "bc", "ac", "cab"]
   Output: bac
   Explanation: Given that the words are sorted lexicographically by the rules of the alien language, so
   from the given words we can conclude the following ordering among its characters:

   1. From "ba" and "bc", we can conclude that 'a' comes before 'c'.
   2. From "bc" and "ac", we can conclude that 'b' comes before 'a'

   From the above two points, we can conclude that the correct character order is: "bac"
   Example 2:
   Input: Words: ["cab", "aaa", "aab"]
   Output: cab
   Explanation: From the given words we can conclude the following ordering among its characters:

   1. From "cab" and "aaa", we can conclude that 'c' comes before 'a'.
   2. From "aaa" and "aab", we can conclude that 'a' comes before 'b'

   From the above two points, we can conclude that the correct character order is: "cab"
   Example 3:
   Input: Words: ["ywx", "wz", "xww", "xz", "zyy", "zwz"]
   Output: ywxz
   Explanation: From the given words we can conclude the following ordering among its characters:

   1. From "ywx" and "wz", we can conclude that 'y' comes before 'w'.
   2. From "wz" and "xww", we can conclude that 'w' comes before 'x'.
   3. From "xww" and "xz", we can conclude that 'w' comes before 'z'
   4. From "xz" and "zyy", we can conclude that 'x' comes before 'z'
   5. From "zyy" and "zwz", we can conclude that 'y' comes before 'w'

   From the above five points, we can conclude that the correct character order is: "ywxz"
   '''

   # mycode
   from collections import deque


   def find_order(words):
       # TODO: Write your code here
       inDegree = {}
       graph = {}
       for word in words:
           for char in word:
               inDegree[char] = 0
               graph[char] = []

       for i in range(len(words) - 1):
           word1, word2 = words[i], words[i + 1]
           for j in range(min(len(word1), len(word2))):
               if word1[j] != word2[j]:
                   inDegree[word2[j]] += 1
                   graph[word1[j]].append(word2[j])
                   break

       sources = deque()
       for key in inDegree:
           if inDegree[key] == 0:
               sources.append(key)

       sortedOrder = []
       while sources:
           vertex = sources.popleft()
           sortedOrder.append(vertex)

           for i in graph[vertex]:
               inDegree[i] -= 1
               if inDegree[i] == 0:
                   sources.append(i)

       return "".join(sortedOrder)


   def main():
       print("Character order: " + find_order(["ba", "bc", "ac", "cab"]))
       print("Character order: " + find_order(["cab", "aaa", "aab"]))
       print("Character order: " +
             find_order(["ywx", "wz", "xww", "xz", "zyy", "zwz"]))


   main()

   # answer
   from collections import deque


   def find_order(words):
       if len(words) == 0:
           return ""

       # a. Initialize the graph
       inDegree = {}  # count of incoming edges
       graph = {}  # adjacency list graph
       for word in words:
           for character in word:
               inDegree[character] = 0
               graph[character] = []

       # b. Build the graph
       for i in range(0, len(words) - 1):
           # find ordering of characters from adjacent words
           w1, w2 = words[i], words[i + 1]
           for j in range(0, min(len(w1), len(w2))):
               parent, child = w1[j], w2[j]
               if parent != child:  # if the two characters are different
                   # put the child into it's parent's list
                   graph[parent].append(child)
                   inDegree[child] += 1  # increment child's inDegree
                   break  # only the first different character between the two words will help us find the order

       # c. Find all sources i.e., all vertices with 0 in-degrees
       sources = deque()
       for key in inDegree:
           if inDegree[key] == 0:
               sources.append(key)

       # d. For each source, add it to the sortedOrder and subtract one from all of its children's in-degrees
       # if a child's in-degree becomes zero, add it to the sources queue
       sortedOrder = []
       while sources:
           vertex = sources.popleft()
           sortedOrder.append(vertex)
           for child in graph[
                   vertex]:  # get the node's children to decrement their in-degrees
               inDegree[child] -= 1
               if inDegree[child] == 0:
                   sources.append(child)

       # if sortedOrder doesn't contain all characters, there is a cyclic dependency between characters, therefore, we
       # will not be able to find the correct ordering of the characters
       if len(sortedOrder) != len(inDegree):
           return ""

       return ''.join(sortedOrder)


   def main():
       print("Character order: " + find_order(["ba", "bc", "ac", "cab"]))
       print("Character order: " + find_order(["cab", "aaa", "aab"]))
       print("Character order: " +
             find_order(["ywx", "wz", "xww", "xz", "zyy", "zwz"]))


   main()


   '''
   Time complexity
   In step ‘d’, each task can become a source only once and each edge (a rule) will be accessed and removed once.
   Therefore, the time complexity of the above algorithm will be O(V+E),
   where ‘V’ is the total number of different characters and ‘E’ is the total number of the rules in the alien language.
   Since, at most, each pair of words can give us one rule, therefore,
   we can conclude that the upper bound for the rules is O(N) where ‘N’ is the number of words in the input.
   So, we can say that the time complexity of our algorithm is O(V+N).
   Space complexity
   The space complexity will be O(V+N), since we are storing all of the rules for each character in an adjacency list.
   '''

Problem Challenge 1 - Reconstructing a Sequence (hard)
-------------------------------------------------------
.. code:: python

   '''
   Problem Challenge 1
   Reconstructing a Sequence (hard)
   Given a sequence originalSeq and an array of sequences,
   write a method to find if originalSeq can be uniquely reconstructed from the array of sequences.
   Unique reconstruction means that we need to find if originalSeq is the only sequence
   such that all sequences in the array are subsequences of it.
   Example 1:
   Input: originalSeq: [1, 2, 3, 4], seqs: [[1, 2], [2, 3], [3, 4]]
   Output: true
   Explanation: The sequences [1, 2], [2, 3], and [3, 4] can uniquely reconstruct
   [1, 2, 3, 4], in other words, all the given sequences uniquely define the order of numbers
   in the 'originalSeq'.
   Example 2:
   Input: originalSeq: [1, 2, 3, 4], seqs: [[1, 2], [2, 3], [2, 4]]
   Output: false
   Explanation: The sequences [1, 2], [2, 3], and [2, 4] cannot uniquely reconstruct
   [1, 2, 3, 4]. There are two possible sequences we can construct from the given sequences:
   1) [1, 2, 3, 4]
   2) [1, 2, 4, 3]
   Example 3:
   Input: originalSeq: [3, 1, 4, 2, 5], seqs: [[3, 1, 5], [1, 4, 2, 5]]
   Output: true
   Explanation: The sequences [3, 1, 5] and [1, 4, 2, 5] can uniquely reconstruct
   [3, 1, 4, 2, 5].
   '''

   # mycode
   from collections import deque


   def can_construct(originalSeq, sequences):
       # TODO: Write your code here
       inDegree = {}
       graph = {}

       for sequence in sequences:
           for i in sequence:
               inDegree[i] = 0
               graph[i] = []

       for sequence in sequences:
           for i in range(1, len(sequence)):
               start, end = sequence[i - 1], sequence[i]
               inDegree[end] += 1
               graph[start].append(end)

       if len(inDegree) != len(originalSeq):
           return False

       sources = deque()
       for key in inDegree:
           if inDegree[key] == 0:
               sources.append(key)

       sortedOrder = []
       while sources:
           if len(sources) != 1:
               return False
           if originalSeq[len(sortedOrder)] != sources[0]:
               return False
           vertex = sources.popleft()
           sortedOrder.append(vertex)
           for i in graph[vertex]:
               inDegree[i] -= 1
               if inDegree[i] == 0:
                   sources.append(i)

       return len(sortedOrder) == len(originalSeq)


   def main():
       print("Can construct: " +
             str(can_construct([1, 2, 3, 4], [[1, 2], [2, 3], [3, 4]])))
       print("Can construct: " +
             str(can_construct([1, 2, 3, 4], [[1, 2], [2, 3], [2, 4]])))
       print("Can construct: " +
             str(can_construct([3, 1, 4, 2, 5], [[3, 1, 5], [1, 4, 2, 5]])))


   main()

   # answer
   from collections import deque


   def can_construct(originalSeq, sequences):
       sortedOrder = []
       if len(originalSeq) <= 0:
           return False

       # a. Initialize the graph
       inDegree = {}  # count of incoming edges
       graph = {}  # adjacency list graph
       for sequence in sequences:
           for num in sequence:
               inDegree[num] = 0
               graph[num] = []

       # b. Build the graph
       for sequence in sequences:
           for i in range(1, len(sequence)):
               parent, child = sequence[i - 1], sequence[i]
               graph[parent].append(child)
               inDegree[child] += 1

       # if we don't have ordering rules for all the numbers we'll not able to uniquely construct the sequence
       if len(inDegree) != len(originalSeq):
           return False

       # c. Find all sources i.e., all vertices with 0 in-degrees
       sources = deque()
       for key in inDegree:
           if inDegree[key] == 0:
               sources.append(key)

       # d. For each source, add it to the sortedOrder and subtract one from all of its children's in-degrees
       # if a child's in-degree becomes zero, add it to the sources queue
       while sources:
           if len(sources) > 1:
               return False  # more than one sources mean, there is more than one way to reconstruct the sequence
           if originalSeq[len(sortedOrder)] != sources[0]:
               # the next source(or number) is different from the original sequence
               return False

           vertex = sources.popleft()
           sortedOrder.append(vertex)
           for child in graph[
                   vertex]:  # get the node's children to decrement their in-degrees
               inDegree[child] -= 1
               if inDegree[child] == 0:
                   sources.append(child)

       # if sortedOrder's size is not equal to original sequence's size, there is no unique way to construct
       return len(sortedOrder) == len(originalSeq)


   def main():
       print("Can construct: " +
             str(can_construct([1, 2, 3, 4], [[1, 2], [2, 3], [3, 4]])))
       print("Can construct: " +
             str(can_construct([1, 2, 3, 4], [[1, 2], [2, 3], [2, 4]])))
       print("Can construct: " +
             str(can_construct([3, 1, 4, 2, 5], [[3, 1, 5], [1, 4, 2, 5]])))


   main()


   '''
   Time complexity
   In step ‘d’, each number can become a source only once and each edge (a rule) will be accessed and removed once.
   Therefore, the time complexity of the above algorithm will be O(V+E),
   where ‘V’ is the count of distinct numbers and ‘E’ is the total number of the rules. Since, at most,
   each pair of numbers can give us one rule, we can conclude that the upper bound for the rules is O(N) where ‘N’ is the count of numbers in all sequences.
   So, we can say that the time complexity of our algorithm is O(V+N).
   Space complexity
   The space complexity will be O(V+N), since we are storing all of the rules for each number in an adjacency list.
   '''

Problem Challenge 2 - Minimum Height Trees (hard)
--------------------------------------------------
.. code:: python

   '''
   Problem Challenge 2
   Minimum Height Trees (hard)
   We are given an undirected graph that has characteristics of a k-ary tree. In such a graph, we can choose any node as the root to make a k-ary tree. The root (or the tree) with the minimum height will be called Minimum Height Tree (MHT). There can be multiple MHTs for a graph. In this problem, we need to find all those roots which give us MHTs. Write a method to find all MHTs of the given graph and return a list of their roots.
   Example 1:
   Input: vertices: 5, Edges: [[0, 1], [1, 2], [1, 3], [2, 4]]
   Output:[1, 2]
   Explanation: Choosing '1' or '2' as roots give us MHTs. In the below diagram, we can see that the
   height of the trees with roots '1' or '2' is three which is minimum.
   '''

   # mycode
   from collections import deque


   def find_trees(nodes, edges):
       # TODO: Write your code here
       inDegree = {i: 0 for i in range(nodes)}
       graph = {i: [] for i in range(nodes)}

       for edge in edges:
           i, j = edge[0], edge[1]
           inDegree[i] += 1
           inDegree[j] += 1
           graph[i].append(j)
           graph[j].append(i)

       leaves = deque()
       for key in inDegree:
           if inDegree[key] == 1:
               leaves.append(key)

       totalSize = nodes
       while totalSize > 2:
           leafSize = len(leaves)
           totalSize -= leafSize
           for i in range(leafSize):
               vertex = leaves.popleft()
               for i in graph[vertex]:
                   inDegree[i] -= 1
                   if inDegree[i] == 1:
                       leaves.append(i)

       return leaves


   def main():
       print("Roots of MHTs: " +
             str(find_trees(5, [[0, 1], [1, 2], [1, 3], [2, 4]])))
       print("Roots of MHTs: " + str(find_trees(4, [[0, 1], [0, 2], [2, 3]])))
       print("Roots of MHTs: " + str(find_trees(4, [[1, 2], [1, 3]])))


   main()

   # answer
   from collections import deque


   def find_trees(nodes, edges):
       if nodes <= 0:
           return []

       # with only one node, since its in-degrees will be 0, therefore, we need to handle it separately
       if nodes == 1:
           return [0]

       # a. Initialize the graph
       inDegree = {i: 0 for i in range(nodes)}  # count of incoming edges
       graph = {i: [] for i in range(nodes)}  # adjacency list graph

       # b. Build the graph
       for edge in edges:
           n1, n2 = edge[0], edge[1]
           # since this is an undirected graph, therefore, add a link for both the nodes
           graph[n1].append(n2)
           graph[n2].append(n1)
           # increment the in-degrees of both the nodes
           inDegree[n1] += 1
           inDegree[n2] += 1

       # c. Find all leaves i.e., all nodes with 0 in-degrees
       leaves = deque()
       for key in inDegree:
           if inDegree[key] == 1:
               leaves.append(key)

       # d. Remove leaves level by level and subtract each leave's children's in-degrees.
       # Repeat this until we are left with 1 or 2 nodes, which will be our answer.
       # Any node that has already been a leaf cannot be the root of a minimum height tree, because
       # its adjacent non-leaf node will always be a better candidate.
       totalNodes = nodes
       while totalNodes > 2:
           leavesSize = len(leaves)
           totalNodes -= leavesSize
           for i in range(0, leavesSize):
               vertex = leaves.popleft()
               # get the node's children to decrement their in-degrees
               for child in graph[vertex]:
                   inDegree[child] -= 1
                   if inDegree[child] == 1:
                       leaves.append(child)

       return list(leaves)


   def main():
       print("Roots of MHTs: " +
             str(find_trees(5, [[0, 1], [1, 2], [1, 3], [2, 4]])))
       print("Roots of MHTs: " + str(find_trees(4, [[0, 1], [0, 2], [2, 3]])))
       print("Roots of MHTs: " + str(find_trees(4, [[1, 2], [1, 3]])))


   main()


   '''
   Time complexity
   In step ‘d’, each node can become a source only once and each edge will be accessed and removed once.
   Therefore, the time complexity of the above algorithm will be O(V+E),
   where ‘V’ is the total nodes and ‘E’ is the total number of the edges.
   Space complexity
   The space complexity will be O(V+E), since we are storing all of the edges for each node in an adjacency list.
   '''
