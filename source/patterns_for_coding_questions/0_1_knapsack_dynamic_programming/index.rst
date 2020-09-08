0/1 Knapsack (medium)
-------------------------------------
.. code:: python

   '''
   Introduction
   Given the weights and profits of ‘N’ items, we are asked to put these items in a knapsack which has a capacity ‘C’.
   The goal is to get the maximum profit out of the items in the knapsack.
   Each item can only be selected once, as we don’t have multiple quantities of any item.
   Let’s take the example of Merry, who wants to carry some fruits in the knapsack to get maximum profit.
       Here are the weights and profits of the fruits:
   Items: { Apple, Orange, Banana, Melon }
   Weights: { 2, 3, 1, 4 }
   Profits: { 4, 5, 3, 7 }
   Knapsack capacity: 5
   Let’s try to put various combinations of fruits in the knapsack, such that their total weight is not more than 5:
   Apple + Orange (total weight 5) => 9 profit
   Apple + Banana (total weight 3) => 7 profit
   Orange + Banana (total weight 4) => 8 profit
   Banana + Melon (total weight 5) => 10 profit
   This shows that Banana + Melon is the best combination as it gives us the maximum profit and the total weight does not exceed the capacity.
   '''


   # Basic Solution
   def solve_knapsack(profits, weights, capacity):
       return knapsack_recursive(profits, weights, capacity, 0)


   def knapsack_recursive(profits, weights, capacity, currentIndex):
       # base checks
       if capacity <= 0 or currentIndex >= len(profits):
           return 0

       # recursive call after choosing the element at the currentIndex
       # if the weight of the element at currentIndex exceeds the capacity, we  shouldn't process this
       profit1 = 0
       if weights[currentIndex] <= capacity:
           profit1 = profits[currentIndex] + knapsack_recursive(
               profits, weights, capacity - weights[currentIndex],
               currentIndex + 1)

       # recursive call after excluding the element at the currentIndex
       profit2 = knapsack_recursive(profits, weights, capacity, currentIndex + 1)

       return max(profit1, profit2)


   def main():
       print(solve_knapsack([1, 6, 10, 16], [1, 2, 3, 5], 7))
       print(solve_knapsack([1, 6, 10, 16], [1, 2, 3, 5], 6))


   main()


   '''
   Time and Space complexity
   The time complexity of the above algorithm is exponential O(2^n),
   where ‘n’ represents the total number of items. This can also be confirmed from the above recursion tree.
   As we can see, we will have a total of ‘31’ recursive calls – calculated through (2^n) + (2^n) - 1,
   which is asymptotically equivalent to O(2^n).
   The space complexity is O(n). This space will be used to store the recursion stack.
   Since the recursive algorithm works in a depth-first fashion,
   which means that we can’t have more than ‘n’ recursive calls on the call stack at any time.
   '''


   # Top-down Dynamic Programming with Memoization
   def solve_knapsack(profits, weights, capacity):
       # create a two dimensional array for Memoization, each element is initialized to '-1'
       dp = [[-1 for x in range(capacity + 1)] for y in range(len(profits))]
       return knapsack_recursive(dp, profits, weights, capacity, 0)


   def knapsack_recursive(dp, profits, weights, capacity, currentIndex):

       # base checks
       if capacity <= 0 or currentIndex >= len(profits):
           return 0

       # if we have already solved a similar problem, return the result from memory
       if dp[currentIndex][capacity] != -1:
           return dp[currentIndex][capacity]

       # recursive call after choosing the element at the currentIndex
       # if the weight of the element at currentIndex exceeds the capacity, we
       # shouldn't process this
       profit1 = 0
       if weights[currentIndex] <= capacity:
           profit1 = profits[currentIndex] + knapsack_recursive(
               dp, profits, weights, capacity - weights[currentIndex],
               currentIndex + 1)

       # recursive call after excluding the element at the currentIndex
       profit2 = knapsack_recursive(dp, profits, weights, capacity,
                                    currentIndex + 1)

       dp[currentIndex][capacity] = max(profit1, profit2)
       return dp[currentIndex][capacity]


   def main():
       print(solve_knapsack([1, 6, 10, 16], [1, 2, 3, 5], 7))
       print(solve_knapsack([1, 6, 10, 16], [1, 2, 3, 5], 6))


   main()


   '''
   Time and Space complexity
   Since our memorization array dp[profits.length][capacity+1] stores the results for all subproblems,
   we can conclude that we will not have more than N*C subproblems (where ‘N’ is the number of items and ‘C’ is the knapsack capacity).
   This means that our time complexity will be O(N*C).
   The above algorithm will use O(N*C) space for the memorization array.
   Other than that we will use O(N) space for the recursion call-stack.
   So the total space complexity will be O(N*C + N), which is asymptotically equivalent to O(N*C).
   '''


   # Bottom-up Dynamic Programming
   def solve_knapsack(profits, weights, capacity):
       # basic checks
       n = len(profits)
       if capacity <= 0 or n == 0 or len(weights) != n:
           return 0

       dp = [[0 for x in range(capacity + 1)] for y in range(n)]

       # populate the capacity = 0 columns, with '0' capacity we have '0' profit
       for i in range(0, n):
           dp[i][0] = 0

       # if we have only one weight, we will take it if it is not more than the capacity
       for c in range(0, capacity + 1):
           if weights[0] <= c:
               dp[0][c] = profits[0]

       # process all sub-arrays for all the capacities
       for i in range(1, n):
           for c in range(1, capacity + 1):
               profit1, profit2 = 0, 0
               # include the item, if it is not more than the capacity
               if weights[i] <= c:
                   profit1 = profits[i] + dp[i - 1][c - weights[i]]
               # exclude the item
               profit2 = dp[i - 1][c]
               # take maximum
               dp[i][c] = max(profit1, profit2)

       # maximum profit will be at the bottom-right corner.
       return dp[n - 1][capacity]


   def main():
       print(solve_knapsack([1, 6, 10, 16], [1, 2, 3, 5], 5))
       print(solve_knapsack([1, 6, 10, 16], [1, 2, 3, 5], 6))
       print(solve_knapsack([1, 6, 10, 16], [1, 2, 3, 5], 7))


   main()


   '''
   Time and Space complexity
   The above solution has the time and space complexity of O(N*C), where ‘N’ represents total items and ‘C’ is the maximum capacity.
   '''


   def solve_knapsack(profits, weights, capacity):
       # basic checks
       n = len(profits)
       if capacity <= 0 or n == 0 or len(weights) != n:
           return 0

       dp = [0 for x in range(capacity + 1)]

       # if we have only one weight, we will take it if it is not more than the capacity
       for c in range(0, capacity + 1):
           if weights[0] <= c:
               dp[c] = profits[0]

       # process all sub-arrays for all the capacities
       for i in range(1, n):
           for c in range(capacity, -1, -1):
               profit1, profit2 = 0, 0
               # include the item, if it is not more than the capacity
               if weights[i] <= c:
                   profit1 = profits[i] + dp[c - weights[i]]
               # exclude the item
               profit2 = dp[c]
               # take maximum
               dp[c] = max(profit1, profit2)

       return dp[capacity]


   def main():
       print("Total knapsack profit: " +
             str(solve_knapsack([1, 6, 10, 16], [1, 2, 3, 5], 7)))
       print("Total knapsack profit: " +
             str(solve_knapsack([1, 6, 10, 16], [1, 2, 3, 5], 6)))


   main()


   '''
   Time and Space complexity
   The above solution the has time and space complexity of O(N*S),
   where ‘N’ represents total numbers and ‘S’ is the total sum of all the numbers.
   '''

Equal Subset Sum Partition (medium)
-------------------------------------
.. code:: python

   '''
   Problem Statement
   Given a set of positive numbers, find if we can partition it into two subsets such that the sum of elements in both subsets is equal.
   Example 1:
   Input: {1, 2, 3, 4}
   Output: True
   Explanation: The given set can be partitioned into two subsets with equal sum: {1, 4} & {2, 3}
   Example 2:
   Input: {1, 1, 3, 4, 7}
   Output: True
   Explanation: The given set can be partitioned into two subsets with equal sum: {1, 3, 4} & {1, 7}
   '''


   # my Top-down code
   def can_partition(num):
       # TODO: Write your code here
       s = sum(num)
       if s % 2 == 1:
           return False
       dp = [[False for x in range(int(s / 2) + 1)] for y in range(len(num))]
       return can_partition_recursive(dp, num, int(s / 2), 0)


   def can_partition_recursive(dp, num, sum, currentIndex):
       if sum == 0:
           return True
       if len(num) == 0 or currentIndex >= len(num):
           return False
       if dp[currentIndex][sum]:
           return dp[currentIndex][sum]
       if num[currentIndex] <= sum:
           if can_partition_recursive(dp, num, sum - num[currentIndex],
                                      currentIndex + 1):
               dp[currentIndex][sum] = True
               return dp[currentIndex][sum]

       dp[currentIndex][sum] = can_partition_recursive(dp, num, sum,
                                                       currentIndex + 1)
       return dp[currentIndex][sum]


   def main():
       print("Can partition: " + str(can_partition([1, 2, 3, 4])))
       print("Can partition: " + str(can_partition([1, 1, 3, 4, 7])))
       print("Can partition: " + str(can_partition([2, 3, 4, 6])))


   main()


   # my bottom-up code
   def can_partition(num):
       # TODO: Write your code here
       s = sum(num)
       if s % 2 == 1:
           return False
       dp = [[False for x in range(int(s / 2) + 1)] for y in range(len(num))]

       for i in range(len(num)):
           dp[i][0] = True

       for i in range(0, int(s / 2) + 1):
           if num[0] == i:
               dp[0][i] = True

       for i in range(1, len(num)):
           for n in range(1, int(s / 2) + 1):
               if num[i] <= n:
                   w1 = dp[i - 1][n - num[i]]
               w2 = dp[i - 1][n]
               dp[i][n] = w2 or w1

       return dp[len(num) - 1][int(s / 2)]


   def main():
       print("Can partition: " + str(can_partition([1, 2, 3, 4])))
       print("Can partition: " + str(can_partition([1, 1, 3, 4, 7])))
       print("Can partition: " + str(can_partition([2, 3, 4, 6])))


   main()


   # my bottom-up code with O(len(num)) space complexity
   def can_partition(num):
       # TODO: Write your code here
       s = sum(num)
       if s % 2 == 1:
           return False
       dp = [False for x in range(int(s / 2) + 1)]
       dp[0] = True

       for i in range(1, int(s / 2) + 1):
           if num[0] == i:
               dp[i] = True

       for i in range(1, len(num)):
           for n in range(int(s / 2), -1, -1):
               w1 = dp[n]
               if num[i] <= n:
                   w2 = dp[n - num[i]]
               dp[n] = w1 or w2

       return dp[int(s / 2)]


   def main():
       print("Can partition: " + str(can_partition([1, 2, 3, 4])))
       print("Can partition: " + str(can_partition([1, 1, 3, 4, 7])))
       print("Can partition: " + str(can_partition([2, 3, 4, 6])))


   main()


   # Basic Solution
   def can_partition(num):
       s = sum(num)
       # if 's' is a an odd number, we can't have two subsets with equal sum
       if s % 2 != 0:
           return False

       return can_partition_recursive(num, s / 2, 0)


   def can_partition_recursive(num, sum, currentIndex):
       # base check
       if sum == 0:
           return True

       n = len(num)
       if n == 0 or currentIndex >= n:
           return False

       # recursive call after choosing the number at the `currentIndex`
       # if the number at `currentIndex` exceeds the sum, we shouldn't process this
       if num[currentIndex] <= sum:
           if (can_partition_recursive(num, sum - num[currentIndex],
                                       currentIndex + 1)):
               return True

       # recursive call after excluding the number at the 'currentIndex'
       return can_partition_recursive(num, sum, currentIndex + 1)


   def main():
       print("Can partition: " + str(can_partition([1, 2, 3, 4])))
       print("Can partition: " + str(can_partition([1, 1, 3, 4, 7])))
       print("Can partition: " + str(can_partition([2, 3, 4, 6])))


   main()


   '''
   Time and Space complexity
   The time complexity of the above algorithm is exponential O(2^n), where ‘n’ represents the total number.
   The space complexity is O(n), which will be used to store the recursion stack.
   '''


   # Top-down Dynamic Programming with Memorization
   def can_partition(num):
       s = sum(num)

       # if 's' is a an odd number, we can't have two subsets with equal sum
       if s % 2 != 0:
           return False

       # initialize the 'dp' array, -1 for default, 1 for true and 0 for false
       dp = [[-1 for x in range(int(s / 2) + 1)] for y in range(len(num))]
       return True if can_partition_recursive(dp, num, int(s /
                                                           2), 0) == 1 else False


   def can_partition_recursive(dp, num, sum, currentIndex):
       # base check
       if sum == 0:
           return 1

       n = len(num)
       if n == 0 or currentIndex >= n:
           return 0

       # if we have not already processed a similar problem
       if dp[currentIndex][sum] == -1:
           # recursive call after choosing the number at the currentIndex
           # if the number at currentIndex exceeds the sum, we shouldn't process this
           if num[currentIndex] <= sum:
               if can_partition_recursive(dp, num, sum - num[currentIndex],
                                          currentIndex + 1) == 1:
                   dp[currentIndex][sum] = 1
                   return 1

           # recursive call after excluding the number at the currentIndex
           dp[currentIndex][sum] = can_partition_recursive(
               dp, num, sum, currentIndex + 1)

       return dp[currentIndex][sum]


   def main():
       print("Can partition: " + str(can_partition([1, 2, 3, 4])))
       print("Can partition: " + str(can_partition([1, 1, 3, 4, 7])))
       print("Can partition: " + str(can_partition([2, 3, 4, 6])))


   main()


   '''
   Time and Space complexity
   The above algorithm has the time and space complexity of O(N*S),
   where ‘N’ represents total numbers and ‘S’ is the total sum of all the numbers.
   '''


   # Bottom-up Dynamic Programming
   def can_partition(num):
       s = sum(num)

       # if 's' is a an odd number, we can't have two subsets with same total
       if s % 2 != 0:
           return False

       # we are trying to find a subset of given numbers that has a total sum of 's/2'.
       s = int(s / 2)

       n = len(num)
       dp = [[False for x in range(s + 1)] for y in range(n)]

       # populate the s=0 columns, as we can always for '0' sum with an empty set
       for i in range(0, n):
           dp[i][0] = True

       # with only one number, we can form a subset only when the required sum is
       # equal to its value
       for j in range(1, s + 1):
           dp[0][j] = num[0] == j

       # process all subsets for all sums
       for i in range(1, n):
           for j in range(1, s + 1):
               # if we can get the sum 'j' without the number at index 'i'
               if dp[i - 1][j]:
                   dp[i][j] = dp[i - 1][j]
               elif j >= num[
                       i]:  # else if we can find a subset to get the remaining sum
                   dp[i][j] = dp[i - 1][j - num[i]]

       # the bottom-right corner will have our answer.
       return dp[n - 1][s]


   def main():
       print("Can partition: " + str(can_partition([1, 2, 3, 4])))
       print("Can partition: " + str(can_partition([1, 1, 3, 4, 7])))
       print("Can partition: " + str(can_partition([2, 3, 4, 6])))


   main()


   '''
   Time and Space complexity
   The above solution the has time and space complexity of O(N*S),
   where ‘N’ represents total numbers and ‘S’ is the total sum of all the numbers.
   '''

Subset Sum (medium)
-------------------------------------
.. code:: python

   '''
   Problem Statement
   Given a set of positive numbers, determine if a subset exists whose sum is equal to a given number ‘S’.
   Example 1:
   Input: {1, 2, 3, 7}, S=6
   Output: True
   The given set has a subset whose sum is '6': {1, 2, 3}
   Example 2:
   Input: {1, 2, 7, 1, 5}, S=10
   Output: True
   The given set has a subset whose sum is '10': {1, 2, 7}
   Example 3:
   Input: {1, 3, 4, 8}, S=6
   Output: False
   The given set does not have any subset whose sum is equal to '6'.
   '''


   def can_partition(num, sum):
       n = len(num)
       dp = [False for x in range(sum + 1)]

       # handle sum=0, as we can always have '0' sum with an empty set
       dp[0] = True

       # with only one number, we can have a subset only when the required sum is equal to its value
       for s in range(1, sum + 1):
           dp[s] = num[0] == s

       # process all subsets for all sums
       for i in range(1, n):
           for s in range(sum, -1, -1):
               # if dp[s]==true, this means we can get the sum 's' without num[i], hence we can move on to
               # the next number else we can include num[i] and see if we can find a subset to get the
               # remaining sum
               if not dp[s] and s >= num[i]:
                   dp[s] = dp[s - num[i]]

       return dp[sum]


   def main():
       print("Can partition: " + str(can_partition([1, 2, 3, 7], 6)))
       print("Can partition: " + str(can_partition([1, 2, 7, 1, 5], 10)))
       print("Can partition: " + str(can_partition([1, 3, 4, 8], 6)))


   main()


   '''
   Time and Space complexity
   The above solution has the time and space complexity of O(N*S), where ‘N’ represents total numbers and ‘S’ is the required sum.
   Challenge
   Can we improve our bottom-up DP solution even further? Can you find an algorithm that has O(S) space complexity?
   '''

Minimum Subset Sum Difference (hard)
-------------------------------------
.. code:: python

   '''
   Problem Statement
   Given a set of positive numbers, partition the set into two subsets with minimum difference between their subset sums.
   Example 1:
   Input: {1, 2, 3, 9}
   Output: 3
   Explanation: We can partition the given set into two subsets where minimum absolute difference
   between the sum of numbers is '3'. Following are the two subsets: {1, 2, 3} & {9}.
   Example 2:
   Input: {1, 2, 7, 1, 5}
   Output: 0
   Explanation: We can partition the given set into two subsets where minimum absolute difference
   between the sum of number is '0'. Following are the two subsets: {1, 2, 5} & {7, 1}.
   Example 3:
   Input: {1, 3, 100, 4}
   Output: 92
   Explanation: We can partition the given set into two subsets where minimum absolute difference
   between the sum of numbers is '92'. Here are the two subsets: {1, 3, 4} & {100}.
   '''


   # Basic Solution
   def can_partition(num):
       return can_partition_recursive(num, 0, 0, 0)


   def can_partition_recursive(num, currentIndex, sum1, sum2):
       # base check
       if currentIndex == len(num):
           return abs(sum1 - sum2)

       # recursive call after including the number at the currentIndex in the first set
       diff1 = can_partition_recursive(num, currentIndex + 1,
                                       sum1 + num[currentIndex], sum2)

       # recursive call after including the number at the currentIndex in the second set
       diff2 = can_partition_recursive(num, currentIndex + 1, sum1,
                                       sum2 + num[currentIndex])

       return min(diff1, diff2)


   def main():
       print("Can partition: " + str(can_partition([1, 2, 3, 9])))
       print("Can partition: " + str(can_partition([1, 2, 7, 1, 5])))
       print("Can partition: " + str(can_partition([1, 3, 100, 4])))


   main()


   # Top-down Dynamic Programming with Memoization
   def can_partition(num):
       s = sum(num)
       dp = [[-1 for x in range(s + 1)] for y in range(len(num))]
       return can_partition_recursive(dp, num, 0, 0, 0)


   def can_partition_recursive(dp, num, currentIndex, sum1, sum2):
       # base check
       if currentIndex == len(num):
           return abs(sum1 - sum2)

       # check if we have not already processed similar problem
       if dp[currentIndex][sum1] == -1:
           # recursive call after including the number at the currentIndex in the first set
           diff1 = can_partition_recursive(dp, num, currentIndex + 1,
                                           sum1 + num[currentIndex], sum2)

           # recursive call after including the number at the currentIndex in the second set
           diff2 = can_partition_recursive(dp, num, currentIndex + 1, sum1,
                                           sum2 + num[currentIndex])

           dp[currentIndex][sum1] = min(diff1, diff2)

       return dp[currentIndex][sum1]


   def main():
       print("Can partition: " + str(can_partition([1, 2, 3, 9])))
       print("Can partition: " + str(can_partition([1, 2, 7, 1, 5])))
       print("Can partition: " + str(can_partition([1, 3, 100, 4])))


   main()


   # Bottom-up Dynamic Programming
   def can_partition(num):
       s = sum(num)
       n = len(num)
       dp = [[False for x in range(int(s / 2) + 1)] for y in range(n)]

       # populate the s=0 columns, as we can always form '0' sum with an empty set
       for i in range(0, n):
           dp[i][0] = True

       # with only one number, we can form a subset only when the required sum is equal to that number
       for j in range(0, int(s / 2) + 1):
           dp[0][j] = num[0] == j

       # process all subsets for all sums
       for i in range(1, n):
           for j in range(1, int(s / 2) + 1):
               # if we can get the sum 's' without the number at index 'i'
               if dp[i - 1][j]:
                   dp[i][j] = dp[i - 1][j]
               elif j >= num[i]:
                   # else include the number and see if we can find a subset to get the remaining sum
                   dp[i][j] = dp[i - 1][j - num[i]]

       sum1 = 0
       # find the largest index in the last row which is true
       for i in range(int(s / 2), -1, -1):
           if dp[n - 1][i]:
               sum1 = i
               break

       sum2 = s - sum1
       return abs(sum2 - sum1)


   def main():
       print("Can partition: " + str(can_partition([1, 2, 3, 9])))
       print("Can partition: " + str(can_partition([1, 2, 7, 1, 5])))
       print("Can partition: " + str(can_partition([1, 3, 100, 4])))


   main()


   '''
   Time and Space complexity
   The above solution has the time and space complexity of O(N*S),
   where ‘N’ represents total numbers and ‘S’ is the total sum of all the numbers.
   '''

Problem Challenge 1 - Count of Subset Sum (hard)
------------------------------------------------
.. code:: python

   '''
   Problem Challenge 1
   Count of Subset Sum (hard)
   Given a set of positive numbers, find the total number of subsets whose sum is equal to a given number ‘S’.
   Example 1: #
   Input: {1, 1, 2, 3}, S=4
   Output: 3
   The given set has '3' subsets whose sum is '4': {1, 1, 2}, {1, 3}, {1, 3}
   Note that we have two similar sets {1, 3}, because we have two '1' in our input.
   Example 2: #
   Input: {1, 2, 7, 1, 5}, S=9
   Output: 3
   The given set has '3' subsets whose sum is '9': {2, 7}, {1, 7, 1}, {1, 2, 1, 5}
   '''


   def count_subsets(num, sum):
       #TODO: Write - Your - Code
       dp = [[0 for i in range(sum + 1)] for j in range(len(num))]

       for i in range(len(num)):
           dp[i][0] = 1

       for i in range(sum + 1):
           if i == num[0]:
               dp[0][i] = 1

       for i in range(1, len(num)):
           for j in range(1, sum + 1):
               dp[i][j] += dp[i - 1][j]
               if num[i] <= j:
                   dp[i][j] += dp[i - 1][j - num[i]]

       return dp[len(num) - 1][sum]


   def main():
       print("Total number of subsets " + str(count_subsets([1, 1, 2, 3], 4)))
       print("Total number of subsets: " + str(count_subsets([1, 2, 7, 1, 5], 9)))


   main()


   # Basic Solution
   def count_subsets(num, sum):
       return count_subsets_recursive(num, sum, 0)


   def count_subsets_recursive(num, sum, currentIndex):
       # base checks
       if sum == 0:
           return 1
       n = len(num)
       if n == 0 or currentIndex >= n:
           return 0

       # recursive call after selecting the number at the currentIndex
       # if the number at currentIndex exceeds the sum, we shouldn't process this
       sum1 = 0
       if num[currentIndex] <= sum:
           sum1 = count_subsets_recursive(num, sum - num[currentIndex],
                                          currentIndex + 1)

       # recursive call after excluding the number at the currentIndex
       sum2 = count_subsets_recursive(num, sum, currentIndex + 1)

       return sum1 + sum2


   def main():
       print("Total number of subsets " + str(count_subsets([1, 1, 2, 3], 4)))
       print("Total number of subsets: " + str(count_subsets([1, 2, 7, 1, 5], 9)))


   main()


   # Top-down Dynamic Programming with Memorization
   def count_subsets(num, sum):
       # create a two dimensional array for Memoization, each element is initialized to '-1'
       dp = [[-1 for x in range(sum + 1)] for y in range(len(num))]
       return count_subsets_recursive(dp, num, sum, 0)


   def count_subsets_recursive(dp, num, sum, currentIndex):
       # base checks
       if sum == 0:
           return 1

       n = len(num)
       if n == 0 or currentIndex >= n:
           return 0

       # check if we have not already processed a similar problem
       if dp[currentIndex][sum] == -1:
           # recursive call after choosing the number at the currentIndex
           # if the number at currentIndex exceeds the sum, we shouldn't process this
           sum1 = 0
           if num[currentIndex] <= sum:
               sum1 = count_subsets_recursive(dp, num, sum - num[currentIndex],
                                              currentIndex + 1)

           # recursive call after excluding the number at the currentIndex
           sum2 = count_subsets_recursive(dp, num, sum, currentIndex + 1)

           dp[currentIndex][sum] = sum1 + sum2

       return dp[currentIndex][sum]


   def main():
       print("Total number of subsets " + str(count_subsets([1, 1, 2, 3], 4)))
       print("Total number of subsets: " + str(count_subsets([1, 2, 7, 1, 5], 9)))


   main()


   '''
   Time and Space complexity
   The above solution has the time and space complexity of O(N*S),
   where ‘N’ represents total numbers and ‘S’ is the desired sum.
   Challenge
   Can we improve our bottom-up DP solution even further? Can you find an algorithm that has O(S) space complexity?
   '''


   # Bottom-up Dynamic Programming
   def count_subsets(num, sum):
       n = len(num)
       dp = [[-1 for x in range(sum + 1)] for y in range(n)]

       # populate the sum = 0 columns, as we will always have an empty set for zero sum
       for i in range(0, n):
           dp[i][0] = 1

       # with only one number, we can form a subset only when the required sum is
       # equal to its value
       for s in range(1, sum + 1):
           dp[0][s] = 1 if num[0] == s else 0

       # process all subsets for all sums
       for i in range(1, n):
           for s in range(1, sum + 1):
               # exclude the number
               dp[i][s] = dp[i - 1][s]
               # include the number, if it does not exceed the sum
               if s >= num[i]:
                   dp[i][s] += dp[i - 1][s - num[i]]

       # the bottom-right corner will have our answer.
       return dp[n - 1][sum]


   def main():
       print("Total number of subsets " + str(count_subsets([1, 1, 2, 3], 4)))
       print("Total number of subsets: " + str(count_subsets([1, 2, 7, 1, 5], 9)))


   main()


   def count_subsets(num, sum):
       n = len(num)
       dp = [0 for x in range(sum + 1)]
       dp[0] = 1

       # with only one number, we can form a subset only when the required sum is equal to the number
       for s in range(1, sum + 1):
           dp[s] = 1 if num[0] == s else 0

       # process all subsets for all sums
       for i in range(1, n):
           for s in range(sum, -1, -1):
               if s >= num[i]:
                   dp[s] += dp[s - num[i]]

       return dp[sum]


   def main():
       print("Total number of subsets " + str(count_subsets([1, 1, 2, 3], 4)))
       print("Total number of subsets: " + str(count_subsets([1, 2, 7, 1, 5], 9)))


   main()

Problem Challenge 2 - Target Sum (hard)
---------------------------------------
.. code:: python

   '''
   Problem Challenge 2
   Target Sum (hard)
   You are given a set of positive numbers and a target sum ‘S’. Each number should be assigned either a ‘+’ or ‘-’ sign.
   We need to find the total ways to assign symbols to make the sum of the numbers equal to the target ‘S’.
   Example 1:
   Input: {1, 1, 2, 3}, S=1
   Output: 3
   Explanation: The given set has '3' ways to make a sum of '1': {+1-1-2+3} & {-1+1-2+3} & {+1+1+2-3}
   Example 2:
   Input: {1, 2, 7, 1}, S=9
   Output: 2
   Explanation: The given set has '2' ways to make a sum of '9': {+1+2+7-1} & {-1+2+7+1}
   '''


   # mycode
   def find_target_subsets(num, s):
       dp = [[0 for x in range(2 * sum(num) + 1)] for y in range(len(num))]
       len_s = sum(num) - s

       for i in range(2 * sum(num) + 1):
           if i - len_s == num[0]:
               dp[0][i] = 1
           if i - len_s == -num[0]:
               dp[0][i] = 1

       for i in range(1, len(num)):
           for j in range(1, 2 * sum(num) + 1):
               if j - num[i] >= 0:
                   dp[i][j] += dp[i - 1][j - num[i]]
               if j + num[i] <= 2 * sum(num):
                   dp[i][j] += dp[i - 1][j + num[i]]
       return dp[len(num) - 1][s + len_s]


   # answer
   def find_target_subsets(num, s):
       totalSum = sum(num)

       # if 's + totalSum' is odd, we can't find a subset with sum equal to '(s + totalSum) / 2'
       if totalSum < s or (s + totalSum) % 2 == 1:
           return 0

       return count_subsets(num, (s + totalSum) // 2)


   # this function is exactly similar to what we have in 'Count of Subset Sum' problem.
   def count_subsets(num, s):
       n = len(num)
       dp = [[0 for x in range(s + 1)] for y in range(n)]

       # populate the sum = 0 columns, as we will always have an empty set for zero sum
       for i in range(0, n):
           dp[i][0] = 1

       # with only one number, we can form a subset only when the required sum is
       # equal to the number
       for s in range(1, s + 1):
           dp[0][s] = 1 if num[0] == s else 0

       # process all subsets for all sums
       for i in range(1, n):
           for s in range(1, s + 1):
               dp[i][s] = dp[i - 1][s]
               if s >= num[i]:
                   dp[i][s] += dp[i - 1][s - num[i]]

       # the bottom-right corner will have our answer.
       return dp[n - 1][s]


   def main():
       print("Total ways: " + str(find_target_subsets([1, 1, 2, 3], 1)))
       print("Total ways: " + str(find_target_subsets([1, 2, 7, 1], 9)))


   main()


   '''
   Time and Space complexity
   The above solution has time and space complexity of O(N*S), where ‘N’ represents total numbers and ‘S’ is the desired sum.
   We can further improve the solution to use only O(S) space.
   '''


   def find_target_subsets(num, s):
       totalSum = sum(num)

       # if 's + totalSum' is odd, we can't find a subset with sum equal to '(s +totalSum) / 2'
       if totalSum < s or (s + totalSum) % 2 == 1:
           return 0

       return count_subsets(num, (s + totalSum) // 2)


   # this function is exactly similar to what we have in 'Count of Subset Sum' problem
   def count_subsets(num, sum):
       n = len(num)
       dp = [0 for x in range(sum + 1)]
       dp[0] = 1

       # with only one number, we can form a subset only when the required sum is equal to the number
       for s in range(1, sum + 1):
           dp[s] = 1 if num[0] == s else 0

       # process all subsets for all sums
       for i in range(1, n):
           for s in range(sum, -1, -1):
               if s >= num[i]:
                   dp[s] += dp[s - num[i]]

       return dp[sum]


   def main():
       print("Total ways: " + str(find_target_subsets([1, 1, 2, 3], 1)))
       print("Total ways: " + str(find_target_subsets([1, 2, 7, 1], 9)))


   main()
