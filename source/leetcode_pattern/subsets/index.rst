Subsets (easy)
----------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given a set with distinct elements, find all of its distinct subsets.
   Example 1:
   Input: [1, 3]
   Output: [], [1], [3], [1,3]
   Example 2:
   Input: [1, 5, 3]
   Output: [], [1], [5], [3], [1,5], [1,3], [5,3], [1,5,3]
   '''


   # mycode
   def find_subsets(nums):
       subsets = []
       subsets.append([])

       for currentNumber in nums:
           for i in range(len(subsets)):
               j = subsets[i].copy()
               j.append(currentNumber)
               subsets.append(j)

       return subsets


   def main():

       print("Here is the list of subsets: " + str(find_subsets([1, 3])))
       print("Here is the list of subsets: " + str(find_subsets([1, 5, 3])))


   main()


   # answer
   def find_subsets(nums):
       subsets = []
       # start by adding the empty subset
       subsets.append([])
       for currentNumber in nums:
           # we will take all existing subsets and insert the current number in them to create new subsets
           n = len(subsets)
           for i in range(n):
               # create a new subset from the existing subset and insert the current element to it
               set = subsets[i].copy()
               set.append(currentNumber)
               subsets.append(set)

       return subsets


   def main():

       print("Here is the list of subsets: " + str(find_subsets([1, 3])))
       print("Here is the list of subsets: " + str(find_subsets([1, 5, 3])))


   main()


   '''
   Time complexity
   Since, in each step, the number of subsets doubles as we add each element to all the existing subsets, the time complexity of the above algorithm is O(2^N),
   where ‘N’ is the total number of elements in the input set. This also means that, in the end, we will have a total of O(2^N) subsets.
   Space complexity
   All the additional space used by our algorithm is for the output list. Since we will have a total of O(2^N) subsets,
   the space complexity of our algorithm is also O(2^N).
   '''

Subsets With Duplicates (easy)
----------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given a set of numbers that might contain duplicates, find all of its distinct subsets.
   Example 1:
   Input: [1, 3, 3]
   Output: [], [1], [3], [1,3], [3,3], [1,3,3]
   Example 2:
   Input: [1, 5, 3, 3]
   Output: [], [1], [5], [3], [1,5], [1,3], [5,3], [1,5,3], [3,3], [1,3,3], [3,3,5], [1,5,3,3]
   '''


   # mycode
   def find_subsets(nums):
       subsets = []
       # TODO: Write your code here
       subsets.append([])

       start, end = 0, 0
       for i in range(len(nums)):
           start = 0
           if i > 0 and nums[i] == nums[i - 1]:
               start = end
           end = len(subsets)

           for j in range(start, end):
               set = subsets[j].copy()
               set.append(nums[i])
               subsets.append(set)

       return subsets


   def main():

       print("Here is the list of subsets: " + str(find_subsets([1, 3, 3])))
       print("Here is the list of subsets: " + str(find_subsets([1, 5, 3, 3])))


   main()


   # answer
   def find_subsets(nums):
       # sort the numbers to handle duplicates
       list.sort(nums)
       subsets = []
       subsets.append([])
       startIndex, endIndex = 0, 0
       for i in range(len(nums)):
           startIndex = 0
           # if current and the previous elements are same, create new subsets only from the subsets
           # added in the previous step
           if i > 0 and nums[i] == nums[i - 1]:
               startIndex = endIndex + 1
           endIndex = len(subsets) - 1
           for j in range(startIndex, endIndex + 1):
               # create a new subset from the existing subset and add the current element to it
               set = list(subsets[j])
               set.append(nums[i])
               subsets.append(set)
       return subsets


   def main():

       print("Here is the list of subsets: " + str(find_subsets([1, 3, 3])))
       print("Here is the list of subsets: " + str(find_subsets([1, 5, 3, 3])))


   main()


   '''
   Time complexity
   Since, in each step, the number of subsets could double (if not duplicate) as we add each element to all the existing subsets,
   the time complexity of the above algorithm is O(2^N), where ‘N’ is the total number of elements in the input set.
   This also means that, in the end, we will have a total of O(2^N) subsets at the most.
   Space complexity
   All the additional space used by our algorithm is for the output list. Since at most we will have a total of O(2^N) subsets,
   the space complexity of our algorithm is also O(2^N).
   '''

Permutations (medium)
----------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given a set of distinct numbers, find all of its permutations.
   Permutation is defined as the re-arranging of the elements of the set. For example, {1, 2, 3} has the following six permutations:
   {1, 2, 3}
   {1, 3, 2}
   {2, 1, 3}
   {2, 3, 1}
   {3, 1, 2}
   {3, 2, 1}
   If a set has ‘n’ distinct elements it will have n!n! permutations.
   Example 1:
   Input: [1,3,5]
   Output: [1,3,5], [1,5,3], [3,1,5], [3,5,1], [5,1,3], [5,3,1]
   '''

   # mycode
   from collections import deque


   def find_permutations(nums):
       result = []
       # TODO: Write your code here
       currentPermutation = deque()
       currentPermutation.append([])

       for num in nums:
           for i in range(len(currentPermutation)):
               previousPermutation = currentPermutation.popleft()
               for j in range(len(previousPermutation) + 1):
                   newPermutation = previousPermutation.copy()
                   newPermutation.insert(j, num)

                   if len(newPermutation) == len(nums):
                       result.append(newPermutation)
                   else:
                       currentPermutation.append(newPermutation)

       return result


   def main():
       print("Here are all the permutations: " +
             str(find_permutations([1, 3, 5])))


   main()

   # answer
   from collections import deque


   def find_permutations(nums):
       numsLength = len(nums)
       result = []
       permutations = deque()
       permutations.append([])
       for currentNumber in nums:
           # we will take all existing permutations and add the current number to create new permutations
           n = len(permutations)
           for _ in range(n):
               oldPermutation = permutations.popleft()
               # create a new permutation by adding the current number at every position
               for j in range(len(oldPermutation) + 1):
                   newPermutation = list(oldPermutation)
                   newPermutation.insert(j, currentNumber)
                   if len(newPermutation) == numsLength:
                       result.append(newPermutation)
                   else:
                       permutations.append(newPermutation)

       return result


   def main():
       print("Here are all the permutations: " +
             str(find_permutations([1, 3, 5])))


   main()


   '''
   Time complexity
   We know that there are a total of N! permutations of a set with ‘N’ numbers.
   In the algorithm above, we are iterating through all of these permutations with the help of the two ‘for’ loops.
   In each iteration, we go through all the current permutations to insert a new number in them on line 17 (line 23 for C++ solution).
   To insert a number into a permutation of size ‘N’ will take O(N),
   which makes the overall time complexity of our algorithm O(N*N!).
   Space complexity
   All the additional space used by our algorithm is for the result list and the queue to store the intermediate permutations.
   If you see closely, at any time, we don’t have more than N! permutations between the result list and the queue.
   Therefore the overall space complexity to store N! permutations each containing NN elements will be O(N*N!).
   '''


   # recursive solution
   def generate_permutations(nums):
       result = []
       generate_permutations_recursive(nums, 0, [], result)
       return result


   def generate_permutations_recursive(nums, index, currentPermutation, result):
       if index == len(nums):
           result.append(currentPermutation)
       else:
           # create a new permutation by adding the current number at every position
           for i in range(len(currentPermutation) + 1):
               newPermutation = list(currentPermutation)
               newPermutation.insert(i, nums[index])
               generate_permutations_recursive(nums, index + 1, newPermutation,
                                               result)


   def main():
       print("Here are all the permutations: " +
             str(generate_permutations([1, 3, 5])))


   main()

String Permutations by changing case (medium)
----------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given a string, find all of its permutations preserving the character sequence but changing case.
   Example 1:
   Input: "ad52"
   Output: "ad52", "Ad52", "aD52", "AD52"
   Example 2:
   Input: "ab7c"
   Output: "ab7c", "Ab7c", "aB7c", "AB7c", "ab7C", "Ab7C", "aB7C", "AB7C"
   '''


   # mycode
   def find_letter_case_string_permutations(str):

       # TODO: Write your code here
       permutations = []
       permutations.append(str)

       for i in range(len(str)):
           if str[i].isalpha():
               for j in range(len(permutations)):
                   newPermutation = list(permutations[j])
                   newPermutation[i] = newPermutation[i].swapcase()
                   permutations.append(''.join(newPermutation))

       return permutations


   def main():
       print("String permutations are: " +
             str(find_letter_case_string_permutations("ad52")))
       print("String permutations are: " +
             str(find_letter_case_string_permutations("ab7c")))


   main()


   # answer
   def find_letter_case_string_permutations(str):
       permutations = []
       permutations.append(str)
       # process every character of the string one by one
       for i in range(len(str)):
           if str[i].isalpha():  # only process characters, skip digits
               # we will take all existing permutations and change the letter case appropriately
               n = len(permutations)
               for j in range(n):
                   chs = list(permutations[j])
                   # if the current character is in upper case, change it to lower case or vice versa
                   chs[i] = chs[i].swapcase()
                   permutations.append(''.join(chs))

       return permutations


   def main():
       print("String permutations are: " +
             str(find_letter_case_string_permutations("ad52")))
       print("String permutations are: " +
             str(find_letter_case_string_permutations("ab7c")))


   main()


   '''
   Time complexity
   Since we can have 2^N permutations at the most and while processing each permutation we convert it into a character array,
   the overall time complexity of the algorithm will be O(N*2^N).
   Space complexity
   All the additional space used by our algorithm is for the output list.
   Since we can have a total of O(2^N) permutations, the space complexity of our algorithm is O(N*2^N).
   '''

Balanced Parentheses (hard)
----------------------------------------------
.. code:: python

   '''
   Problem Statement
   For a given number ‘N’, write a function to generate all combination of ‘N’ pairs of balanced parentheses.
   Example 1:
   Input: N=2
   Output: (()), ()()
   Example 2:
   Input: N=3
   Output: ((())), (()()), (())(), ()(()), ()()()
   '''

   # mycode
   from collections import deque


   class ParenthesesString:
       def __init__(self, str, openCount, closeCount):
           self.str = str
           self.openCount = openCount
           self.closeCount = closeCount


   def generate_valid_parentheses(num):
       result = []
       # TODO: Write your code here
       queue = deque()
       queue.append(ParenthesesString('', 0, 0))

       while queue:
           ps = queue.popleft()

           if ps.openCount == num and ps.closeCount == num:
               result.append(ps.str)
           else:
               if ps.openCount > ps.closeCount:
                   queue.append(
                       ParenthesesString(ps.str + ')', ps.openCount,
                                         ps.closeCount + 1))
               if ps.openCount < num:
                   queue.append(
                       ParenthesesString(ps.str + '(', ps.openCount + 1,
                                         ps.closeCount))
       return result


   def main():
       print("All combinations of balanced parentheses are: " +
             str(generate_valid_parentheses(2)))
       print("All combinations of balanced parentheses are: " +
             str(generate_valid_parentheses(3)))


   main()

   # answer
   from collections import deque


   class ParenthesesString:
       def __init__(self, str, openCount, closeCount):
           self.str = str
           self.openCount = openCount
           self.closeCount = closeCount


   def generate_valid_parentheses(num):
       result = []
       queue = deque()
       queue.append(ParenthesesString("", 0, 0))
       while queue:
           ps = queue.popleft()
           # if we've reached the maximum number of open and close parentheses, add to the result
           if ps.openCount == num and ps.closeCount == num:
               result.append(ps.str)
           else:
               if ps.openCount < num:  # if we can add an open parentheses, add it
                   queue.append(
                       ParenthesesString(ps.str + "(", ps.openCount + 1,
                                         ps.closeCount))

               if ps.openCount > ps.closeCount:  # if we can add a close parentheses, add it
                   queue.append(
                       ParenthesesString(ps.str + ")", ps.openCount,
                                         ps.closeCount + 1))

       return result


   def main():
       print("All combinations of balanced parentheses are: " +
             str(generate_valid_parentheses(2)))
       print("All combinations of balanced parentheses are: " +
             str(generate_valid_parentheses(3)))


   main()

Unique Generalized Abbreviations (hard)
----------------------------------------------
.. code:: python

   '''
   Problem Statement
   Given a word, write a function to generate all of its unique generalized abbreviations.
   Generalized abbreviation of a word can be generated by replacing each substring of the word by the count of characters in the substring. Take the example of “ab” which has four substrings: “”, “a”, “b”, and “ab”. After replacing these substrings in the actual word by the count of characters we get all the generalized abbreviations: “ab”, “1b”, “a1”, and “2”.
   Example 1:
   Input: "BAT"
   Output: "BAT", "BA1", "B1T", "B2", "1AT", "1A1", "2T", "3"
   Example 2:
   Input: "code"
   Output: "code", "cod1", "co1e", "co2", "c1de", "c1d1", "c2e", "c3", "1ode", "1od1", "1o1e", "1o2",
   "2de", "2d1", "3e", "4"
   '''


   # mycode
   def generate_generalized_abbreviation(word):
       result = []
       # TODO: Write your code here
       generate_abbreviation_recursive(word, list(), 0, 0, result)
       return result


   def generate_abbreviation_recursive(word, abWord, start, count, result):
       if start == len(word):
           if count != 0:
               abWord.append(str(count))
           result.append(''.join(abWord))
       else:
           generate_abbreviation_recursive(word, list(abWord), start + 1,
                                           count + 1, result)

           newword = list(abWord)
           if count != 0:
               newword.append(str(count))
           newword.append(word[start])
           generate_abbreviation_recursive(word, newword, start + 1, 0, result)


   def main():
       print("Generalized abbreviation are: " +
             str(generate_generalized_abbreviation("BAT")))
       print("Generalized abbreviation are: " +
             str(generate_generalized_abbreviation("code")))


   main()

   # answer
   from collections import deque


   class AbbreviatedWord:
       def __init__(self, str, start, count):
           self.str = str
           self.start = start
           self.count = count


   def generate_generalized_abbreviation(word):
       wordLen = len(word)
       result = []
       queue = deque()
       queue.append(AbbreviatedWord(list(), 0, 0))
       while queue:
           abWord = queue.popleft()
           if abWord.start == wordLen:
               if abWord.count != 0:
                   abWord.str.append(str(abWord.count))
               result.append(''.join(abWord.str))
           else:
               # continue abbreviating by incrementing the current abbreviation count
               queue.append(
                   AbbreviatedWord(list(abWord.str), abWord.start + 1,
                                   abWord.count + 1))

               # restart abbreviating, append the count and the current character to the string
               if abWord.count != 0:
                   abWord.str.append(str(abWord.count))

               newWord = list(abWord.str)
               newWord.append(word[abWord.start])
               queue.append(AbbreviatedWord(newWord, abWord.start + 1, 0))

       return result


   def main():
       print("Generalized abbreviation are: " +
             str(generate_generalized_abbreviation("BAT")))
       print("Generalized abbreviation are: " +
             str(generate_generalized_abbreviation("code")))


   main()


   '''
   Time complexity
   Since we had two options for each character, we will have a maximum of 2^N combinations.
   If you see the visual representation of Example-1 closely you will realize that it is equivalent to a binary tree,
   where each node has two children. This means that we will have 2^N leaf nodes and 2^N-1 intermediate nodes,
   so the total number of elements pushed to the queue will be 2^N + 2^N-1, which is asymptotically equivalent to O(2^N).
   While processing each element, we do need to concatenate the current string with a character.
   This operation will take O(N), so the overall time complexity of our algorithm will be O(N*2^N).
   Space complexity
   All the additional space used by our algorithm is for the output list.
   Since we can’t have more than O(2^N) combinations, the space complexity of our algorithm is O(N*2^N).
   '''


   # Recursive Solution
   def generate_generalized_abbreviation(word):
       result = []
       generate_abbreviation_recursive(word, list(), 0, 0, result)
       return result


   def generate_abbreviation_recursive(word, abWord, start, count, result):

       if start == len(word):
           if count != 0:
               abWord.append(str(count))
           result.append(''.join(abWord))
       else:
           # continue abbreviating by incrementing the current abbreviation count
           generate_abbreviation_recursive(word, list(abWord), start + 1,
                                           count + 1, result)

           # restart abbreviating, append the count and the current character to the string
           if count != 0:
               abWord.append(str(count))
           newWord = list(abWord)
           newWord.append(word[start])
           generate_abbreviation_recursive(word, newWord, start + 1, 0, result)


   def main():
       print("Generalized abbreviation are: " +
             str(generate_generalized_abbreviation("BAT")))
       print("Generalized abbreviation are: " +
             str(generate_generalized_abbreviation("code")))


   main()

Problem Challenge 1 - Evaluate Expression (hard)
-------------------------------------------------
.. code:: python

   '''
   Problem Challenge 1
   Evaluate Expression (hard)
   Given an expression containing digits and operations (+, -, *),
   find all possible ways in which the expression can be evaluated by grouping the numbers and operators using parentheses.
   Example 1:
   Input: "1+2*3"
   Output: 7, 9
   Explanation: 1+(2*3) => 7 and (1+2)*3 => 9
   Example 2:
   Input: "2*3-4-5"
   Output: 8, -12, 7, -7, -3
   Explanation: 2*(3-(4-5)) => 8, 2*(3-4-5) => -12, 2*3-(4-5) => 7, 2*(3-4)-5 => -7, (2*3)-4-5 => -3
   '''


   # mycode
   def diff_ways_to_evaluate_expression(input):
       result = []
       # TODO: Write your code here

       if '+' not in input and '-' not in input and '*' not in input:
           result.append(input)
       else:
           for i in range(len(input)):
               if not input[i].isdigit():
                   left = diff_ways_to_evaluate_expression(input[0:i])
                   right = diff_ways_to_evaluate_expression(input[i + 1:])

                   for j in left:
                       for k in right:
                           if input[i] == '+':
                               result.append(int(j) + int(k))
                           if input[i] == '*':
                               result.append(int(j) * int(k))
                           if input[i] == '-':
                               result.append(int(j) - int(k))
       return result


   def main():
       print("Expression evaluations: " +
             str(diff_ways_to_evaluate_expression("1+2*3")))

       print("Expression evaluations: " +
             str(diff_ways_to_evaluate_expression("2*3-4-5")))


   main()


   # answer
   def diff_ways_to_evaluate_expression(input):
       return diff_ways_to_evaluate_expression_rec({}, input)


   def diff_ways_to_evaluate_expression_rec(map, input):
       if input in map:
           return map[input]

       result = []
       # base case: if the input string is a number, parse and return it.
       if '+' not in input and '-' not in input and '*' not in input:
           result.append(int(input))
       else:
           for i in range(0, len(input)):
               char = input[i]
               if not char.isdigit():
                   # break the equation here into two parts and make recursively calls
                   leftParts = diff_ways_to_evaluate_expression_rec(
                       map, input[0:i])
                   rightParts = diff_ways_to_evaluate_expression_rec(
                       map, input[i + 1:])
                   for part1 in leftParts:
                       for part2 in rightParts:
                           if char == '+':
                               result.append(part1 + part2)
                           elif char == '-':
                               result.append(part1 - part2)
                           elif char == '*':
                               result.append(part1 * part2)

       map[input] = result
       return result


   def main():
       print("Expression evaluations: " +
             str(diff_ways_to_evaluate_expression("1+2*3")))

       print("Expression evaluations: " +
             str(diff_ways_to_evaluate_expression("2*3-4-5")))


   main()


   '''
   Time complexity
   The time complexity of this algorithm will be exponential and will be similar to Balanced Parentheses.
   Estimated time complexity will be O(N*2^N) but the actual time complexity ( O(4^n/\sqrt{n}) ) is bounded by the Catalan number and is beyond the scope of a coding interview.
   Space complexity
   The space complexity of this algorithm will also be exponential, estimated at O(2^N) though the actual will be ( O(4^n/\sqrt{n})).
   Memoized version
   The problem has overlapping subproblems,
   as our recursive calls can be evaluating the same sub-expression multiple times.
   To resolve this, we can use memoization and store the intermediate results in a HashMap.
   In each function call, we can check our map to see if we have already evaluated this sub-expression before.
   '''

Problem Challenge 2 - Structurally Unique Binary Search Trees (hard)
---------------------------------------------------------------------
.. code:: python

   '''
   Problem Challenge 2
   Structurally Unique Binary Search Trees (hard)
   Given a number ‘n’, write a function to return all structurally unique Binary Search Trees (BST) that can store values 1 to ‘n’?
   Example 1:
   Input: 2
   Output: List containing root nodes of all structurally unique BSTs.
   Explanation: Here are the 2 structurally unique BSTs storing all numbers from 1 to 2:
   Example 2:
   Input: 3
   Output: List containing root nodes of all structurally unique BSTs.
   Explanation: Here are the 5 structurally unique BSTs storing all numbers from 1 to 3:
   '''


   class TreeNode:
       def __init__(self, val):
           self.val = val
           self.left = None
           self.right = None


   def find_unique_trees(n):

       # TODO: Write your code here
       if n < 1:
           return []
       return find_unique_trees_recursive(1, n)


   def find_unique_trees_recursive(start, end):
       result = []
       if start > end:
           return [None]
       for i in range(start, end + 1):
           left = find_unique_trees_recursive(start, i - 1)
           right = find_unique_trees_recursive(i + 1, end)

           for j in left:
               for k in right:
                   root = TreeNode(i)
                   root.left = j
                   root.right = k
                   result.append(root)

       return result


   def main():
       print("Total trees: " + str(len(find_unique_trees(2))))
       print("Total trees: " + str(len(find_unique_trees(3))))


   main()


   # answer
   class TreeNode:
       def __init__(self, val):
           self.val = val
           self.left = None
           self.right = None


   def find_unique_trees(n):
       if n <= 0:
           return []
       return findUnique_trees_recursive(1, n)


   def findUnique_trees_recursive(start, end):
       result = []
       # base condition, return 'None' for an empty sub-tree
       # consider n = 1, in this case we will have start = end = 1, this means we should have only one tree
       # we will have two recursive calls, findUniqueTreesRecursive(1, 0) & (2, 1)
       # both of these should return 'None' for the left and the right child
       if start > end:
           result.append(None)
           return result

       for i in range(start, end + 1):
           # making 'i' the root of the tree
           leftSubtrees = findUnique_trees_recursive(start, i - 1)
           rightSubtrees = findUnique_trees_recursive(i + 1, end)
           for leftTree in leftSubtrees:
               for rightTree in rightSubtrees:
                   root = TreeNode(i)
                   root.left = leftTree
                   root.right = rightTree
                   result.append(root)

       return result


   def main():
       print("Total trees: " + str(len(find_unique_trees(2))))
       print("Total trees: " + str(len(find_unique_trees(3))))


   main()


   '''
   Time complexity
   The time complexity of this algorithm will be exponential and will be similar to Balanced Parentheses.
   Estimated time complexity will be O(n*2^n) but the actual time complexity ( O(4^n/\sqrt{n})) is bounded
   by the Catalan number and is beyond the scope of a coding interview. See more details here.
   Space complexity
   The space complexity of this algorithm will be exponential too, estimated at O(2^n),
   but the actual will be ( O(4^n/\sqrt{n})).
   Memoized version
   Since our algorithm has overlapping subproblems, can we use memoization to improve it?
   We could, but every time we return the result of a subproblem from the cache,
   we have to clone the result list because these trees will be used as the left or right child of a tree.
   This cloning is equivalent to reconstructing the trees, therefore,
   the overall time complexity of the memoized algorithm will also be the same.
   '''

Problem Challenge 3 - Count of Structurally Unique Binary Search Trees (hard)
------------------------------------------------------------------------------
.. code:: python

   '''
   Problem Challenge 3
   Count of Structurally Unique Binary Search Trees (hard)
   Given a number ‘n’, write a function to return the count of structurally unique Binary Search Trees (BST) that can store values 1 to ‘n’.
   Example 1:
   Input: 2
   Output: 2
   Explanation: As we saw in the previous problem, there are 2 unique BSTs storing numbers from 1-2.
   Example 2:
   Input: 3
   Output: 5
   Explanation: There will be 5 unique BSTs that can store numbers from 1 to 5.
   '''


   # mycode
   class TreeNode:
       def __init__(self, val):
           self.val = val
           self.left = None
           self.right = None


   def count_trees(n):
       if n < 0:
           return -1
       if n <= 1:
           return 1

       count = 0
       for i in range(1, n + 1):
           left = count_trees(i - 1)
           right = count_trees(n - i)
           count += left * right
       return count


   def main():
       print("Total trees: " + str(count_trees(2)))
       print("Total trees: " + str(count_trees(3)))


   main()


   # answer
   class TreeNode:
       def __init__(self, val):
           self.val = val
           self.left = None
           self.right = None


   def count_trees(n):
       return count_trees_rec({}, n)


   def count_trees_rec(map, n):
       if n in map:
           return map[n]

       if n <= 1:
           return 1
       count = 0
       for i in range(1, n + 1):
           # making 'i' the root of the tree
           countOfLeftSubtrees = count_trees_rec(map, i - 1)
           countOfRightSubtrees = count_trees_rec(map, n - i)
           count += (countOfLeftSubtrees * countOfRightSubtrees)

       map[n] = count
       return count


   def main():
       print("Total trees: " + str(count_trees(2)))
       print("Total trees: " + str(count_trees(3)))


   main()


   '''
   Time complexity #
   The time complexity of this algorithm will be exponential and will be similar to Balanced Parentheses.
   Estimated time complexity will be O(n*2^n) but the actual time complexity ( O(4^n/\sqrt{n}))
   is bounded by the Catalan number and is beyond the scope of a coding interview.
   Space complexity
   The space complexity of this algorithm will be exponential too, estimated O(2^n) but the actual will be (O(4^n/\sqrt{n}).
   Memorized version
   Our algorithm has overlapping subproblems as our recursive call will be evaluating the same sub-expression multiple times.
   To resolve this, we can use memorization and store the intermediate results in a HashMap.
   In each function call, we can check our map to see if we have already evaluated this sub-expression before.
   '''

