Single Number (easy)
-----------------------
.. code:: python

   '''
   Problem Statement
   In a non-empty array of integers, every number appears twice except for one, find that single number.
   Example 1:
   Input: 1, 4, 2, 1, 3, 2, 3
   Output: 4
   Example 2:
   Input: 7, 9, 7
   Output: 9
   '''


   # mycode
   def find_single_number(arr):
       # TODO: Write your code here
       s = 0

       for i in arr:
           s = s ^ i
       return s


   def main():
       arr = [1, 4, 2, 1, 3, 2, 3]
       print(find_single_number(arr))


   main()


   # answer
   def find_single_number(arr):
       num = 0
       for i in arr:
           num ^= i
       return num


   def main():
       arr = [1, 4, 2, 1, 3, 2, 3]
       print(find_single_number(arr))


   main()


   '''
   Time Complexity:
   Time complexity of this solution is O(n) as we iterate through all numbers of the input once.
   Space Complexity:
   The algorithm runs in constant space O(1).
   '''

Two Single Numbers (medium)
---------------------------
.. code:: python

   '''
   Problem Statement
   In a non-empty array of numbers, every number appears exactly twice except two numbers that appear only once. Find the two numbers that appear only once.
   Example 1:
   Input: [1, 4, 2, 1, 3, 5, 6, 2, 3, 5]
   Output: [4, 6]
   Example 2:
   Input: [2, 1, 3, 2]
   Output: [1, 3]
   '''


   # mycode
   def find_single_numbers(nums):
       # TODO: Write your code here
       sum = 0
       for num in nums:
           sum ^= num

       diff = 1
       while (diff & sum == 0):
           diff = diff << 1

       num1, num2 = 0, 0

       for num in nums:
           if num & diff == 0:
               num1 ^= num
           else:
               num2 ^= num

       return [num1, num2]


   def main():
       print('Single numbers are:' +
             str(find_single_numbers([1, 4, 2, 1, 3, 5, 6, 2, 3, 5])))
       print('Single numbers are:' + str(find_single_numbers([2, 1, 3, 2])))


   main()
   '''
   First for loop is to find num1 ^ num2. The first right one of num1^num2 marks the difference of the two numbers,
   and the third loop is to divide the array into two sets and find the single number respectively.
   '''


   # answer
   def find_single_numbers(nums):
       # get the XOR of the all the numbers
       n1xn2 = 0
       for num in nums:
           n1xn2 ^= num

       # get the rightmost bit that is '1'
       rightmost_set_bit = 1
       while (rightmost_set_bit & n1xn2) == 0:
           rightmost_set_bit = rightmost_set_bit << 1
       num1, num2 = 0, 0

       for num in nums:
           if (num & rightmost_set_bit) != 0:  # the bit is set
               num1 ^= num
           else:  # the bit is not set
               num2 ^= num

       return [num1, num2]


   def main():
       print('Single numbers are:' +
             str(find_single_numbers([1, 4, 2, 1, 3, 5, 6, 2, 3, 5])))
       print('Single numbers are:' + str(find_single_numbers([2, 1, 3, 2])))


   main()


   '''
   Time Complexity
   The time complexity of this solution is O(n) where ‘n’ is the number of elements in the input array.
   Space Complexity
   The algorithm runs in constant space O(1).
   '''

Complement of Base 10 Number (medium)
--------------------------------------
.. code:: python

   '''
   Problem Statement
   Every non-negative integer N has a binary representation, for example, 8 can be represented as “1000” in binary and 7 as “0111” in binary.
   The complement of a binary representation is the number in binary that we get when we change every 1 to a 0 and every 0 to a 1. For example, the binary complement of “1010” is “0101”.
   For a given positive number N in base-10, return the complement of its binary representation as a base-10 integer.
   Example 1:
   Input: 8
   Output: 7
   Explanation: 8 is 1000 in binary, its complement is 0111 in binary, which is 7 in base-10.
   Example 2:
   Input: 10
   Output: 5
   Explanation: 10 is 1010 in binary, its complement is 0101 in binary, which is 5 in base-10.
   '''


   # mycode
   def calculate_bitwise_complement(n):
       #TODO: Write your code here
       count, num = 0, n
       while num > 0:
           num = num >> 1
           count += 1
       s = 2**count - 1

       return n ^ s


   def main():
       print('Bitwise complement is: ' + str(calculate_bitwise_complement(8)))
       print('Bitwise complement is: ' + str(calculate_bitwise_complement(10)))


   main()


   # answer
   def calculate_bitwise_complement(num):
       # count number of total bits in 'num'
       bit_count, n = 0, num
       while n > 0:
           bit_count += 1
           n = n >> 1

       # for a number which is a complete power of '2' i.e., it can be written as pow(2, n), if we
       # subtract '1' from such a number, we get a number which has 'n' least significant bits set to '1'.
       # For example, '4' which is a complete power of '2', and '3' (which is one less than 4) has a binary
       # representation of '11' i.e., it has '2' least significant bits set to '1'
       all_bits_set = pow(2, bit_count) - 1

       # from the solution description: complement = number ^ all_bits_set
       return num ^ all_bits_set


   print('Bitwise complement is: ' + str(calculate_bitwise_complement(8)))
   print('Bitwise complement is: ' + str(calculate_bitwise_complement(10)))


   '''
   Time Complexity
   Time complexity of this solution is O(b)O where ‘b’ is the number of bits required to store the given number.
   Space Complexity
   Space complexity of this solution is O(1).
   '''

Problem Challenge 1
--------------------------
.. code:: python

   '''
   Problem Challenge 1
   Given a binary matrix representing an image, we want to flip the image horizontally, then invert it.
   To flip an image horizontally means that each row of the image is reversed. For example, flipping [0, 1, 1] horizontally results in [1, 1, 0].
   To invert an image means that each 0 is replaced by 1, and each 1 is replaced by 0. For example, inverting [1, 1, 0] results in [0, 0, 1].
   Example 1:
   Input: [
     [1,0,1],
     [1,1,1],
     [0,1,1]
   ]
   Output: [
     [0,1,0],
     [0,0,0],
     [0,0,1]
   ]
   Explanation: First reverse each row: [[1,0,1],[1,1,1],[1,1,0]]. Then, invert the image: [[0,1,0],[0,0,0],[0,0,1]]
   Example 2:
   Input: [
     [1,1,0,0],
     [1,0,0,1],
     [0,1,1,1],
     [1,0,1,0]
   ]
   Output: [
     [1,1,0,0],
     [0,1,1,0],
     [0,0,0,1],
     [1,0,1,0]
   ]
   Explanation: First reverse each row: [[0,0,1,1],[1,0,0,1],[1,1,1,0],[0,1,0,1]]. Then invert the image: [[1,1,0,0],[0,1,1,0],[0,0,0,1],[1,0,1,0]]
   '''


   # mycode
   def flip_and_invert_image(matrix):
       #TODO: Write your code here.

       for i in range(len(matrix)):
           start, end = 0, len(matrix[i]) - 1
           while start <= end:
               temp = matrix[i][end] ^ 1
               matrix[i][end] = matrix[i][start] ^ 1
               matrix[i][start] = temp
               end -= 1
               start += 1

       return matrix


   def main():
       print(flip_and_invert_image([[1, 0, 1], [1, 1, 1], [0, 1, 1]]))
       print(
           flip_and_invert_image([[1, 1, 0, 0], [1, 0, 0, 1], [0, 1, 1, 1],
                                  [1, 0, 1, 0]]))


   main()


   # answer
   def flip_an_invert_image(matrix):
       C = len(matrix)
       for row in matrix:
           for i in range((C + 1) // 2):
               row[i], row[C - i - 1] = row[C - i - 1] ^ 1, row[i] ^ 1

       return matrix


   def main():
       print(flip_an_invert_image([[1, 0, 1], [1, 1, 1], [0, 1, 1]]))
       print(
           flip_an_invert_image([[1, 1, 0, 0], [1, 0, 0, 1], [0, 1, 1, 1],
                                 [1, 0, 1, 0]]))


   main()


   '''
   Time Complexity
   The time complexity of this solution is O(n) as we iterate through all elements of the input.
   Space Complexity
   The space complexity of this solution is O(1).
   '''
