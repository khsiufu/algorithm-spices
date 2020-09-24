Maximum Sum Subarray of Size K (easy)
--------------------------------------------------------------
.. code:: python

   '''
   Problem Statement：
   Given an array of positive numbers and a positive number ‘k’, find the maximum sum of any contiguous subarray of size ‘k’.

   Example 1:
   Input: [2, 1, 5, 1, 3, 2], k=3
   Output: 9
   Explanation: Subarray with maximum sum is [5, 1, 3].

   Example 2:
   Input: [2, 3, 4, 1, 5], k=2
   Output: 7
   Explanation: Subarray with maximum sum is [3, 4].
   '''


   # mycode
   def max_sub_array_of_size_k(k, arr):
       if not arr or not k:
           return 0
       max_sum = 0
       for start in range(len(arr) - k):
           window_sum = sum(arr[start:start + k])
           max_sum = max(max_sum, window_sum)
       return max_sum


   # answer
   def max_sub_array_of_size_k(k, arr):
       max_sum, window_sum = 0, 0
       window_start = 0

       for window_end in range(len(arr)):
           window_sum += arr[window_end]  # add the next element
           # slide the window, we don't need to slide if we've not hit the required window size of 'k'
           if window_end >= k - 1:
               max_sum = max(max_sum, window_sum)
               window_sum -= arr[window_start]  # subtract the element going out
               window_start += 1  # slide the window ahead
       return max_sum


   def main():
       print("Maximum sum of a subarray of size K: " +
             str(max_sub_array_of_size_k(3, [2, 1, 5, 1, 3, 2])))
       print("Maximum sum of a subarray of size K: " +
             str(max_sub_array_of_size_k(2, [2, 3, 4, 1, 5])))


   main()


   '''
   Time Complexity
   The time complexity of the above algorithm will be O(N).
   Space Complexity
   The algorithm runs in constant space O(1).
   '''

Smallest Subarray with a given sum (easy)
--------------------------------------------------------------
.. code:: python

   '''
   Problem Statement：
   Given an array of positive numbers and a positive number ‘S’, find the length of the smallest contiguous subarray whose sum is greater than or equal to ‘S’. Return 0, if no such subarray exists.

   Example 1:
   Input: [2, 1, 5, 2, 3, 2], S=7
   Output: 2
   Explanation: The smallest subarray with a sum great than or equal to '7' is [5, 2].

   Example 2:
   Input: [2, 1, 5, 2, 8], S=7
   Output: 1
   Explanation: The smallest subarray with a sum greater than or equal to '7' is [8].

   Example 3:
   Input: [3, 4, 1, 1, 6], S=8
   Output: 3
   Explanation: Smallest subarrays with a sum greater than or equal to '8' are [3, 4, 1] or [1, 1, 6].
   '''


   # mycode
   # mycode like bottom answer, so don't repeat write.


   # answer
   import math


   def smallest_subarray_with_given_sum(s, arr):
       window_sum = 0
       min_length = math.inf
       window_start = 0

       for window_end in range(0, len(arr)):
           window_sum += arr[window_end]  # add the next element
           # shrink the window as small as possible until the 'window_sum' is smaller than 's'
           while window_sum >= s:
               min_length = min(min_length, window_end - window_start + 1)
               window_sum -= arr[window_start]
               window_start += 1
       if min_length == math.inf:
           return 0
       return min_length


   def main():
       print("Smallest subarray length: " +
             str(smallest_subarray_with_given_sum(7, [2, 1, 5, 2, 3, 2])))
       print("Smallest subarray length: " +
             str(smallest_subarray_with_given_sum(7, [2, 1, 5, 2, 8])))
       print("Smallest subarray length: " +
             str(smallest_subarray_with_given_sum(8, [3, 4, 1, 1, 6])))


   main()


   '''
   Time Complexity
   The time complexity of the above algorithm will be O(N).
   The outer for loop runs for all elements and the inner while loop processes each element only once, therefore the time complexity of the algorithm will be O(N+N) which is asymptotically equivalent to O(N).
   Space Complexity
   The algorithm runs in constant space O(1).
   '''

Longest Substring with K Distinct Characters (medium)
--------------------------------------------------------------
.. code:: python

   '''
   Problem Statement：
   Given a string, find the length of the longest substring in it with no more than K distinct characters.

   Example 1:
   Input: String="araaci", K=2
   Output: 4
   Explanation: The longest substring with no more than '2' distinct characters is "araa".

   Example 2:
   Input: String="araaci", K=1
   Output: 2
   Explanation: The longest substring with no more than '1' distinct characters is "aa".

   Example 3:
   Input: String="cbbebi", K=3
   Output: 5
   Explanation: The longest substrings with no more than '3' distinct characters are "cbbeb" & "bbebi".
   '''


   # mycode
   def longest_substring_with_k_distinct(str, k):
       from collections import defaultdict
       lookup = defaultdict(int)
       start, end = 0, 0
       max_len = 0

       while end < len(str):
           lookup[str[end]] += 1
           end += 1

           while len(lookup) > k:
               lookup[str[start]] -= 1
               if lookup[str[start]] == 0:
                   del lookup[str[start]]
               start += 1

           max_len = max(max_len, end - start)

       return max_len


   # answer
   def longest_substring_with_k_distinct(str, k):
       window_start = 0
       max_length = 0
       char_frequency = {}

       # in the following loop we'll try to extend the range [window_start, window_end]
       for window_end in range(len(str)):
           right_char = str[window_end]
           if right_char not in char_frequency:
               char_frequency[right_char] = 0
           char_frequency[right_char] += 1

           # shrink the sliding window, until we are left with 'k' distinct characters in the char_frequency
           while len(char_frequency) > k:
               left_char = str[window_start]
               char_frequency[left_char] -= 1
               if char_frequency[left_char] == 0:
                   del char_frequency[left_char]
               window_start += 1  # shrink the window
           # remember the maximum length so far
           max_length = max(max_length, window_end - window_start + 1)
       return max_length


   def main():
       print("Length of the longest substring: " +
             str(longest_substring_with_k_distinct("araaci", 2)))
       print("Length of the longest substring: " +
             str(longest_substring_with_k_distinct("araaci", 1)))
       print("Length of the longest substring: " +
             str(longest_substring_with_k_distinct("cbbebi", 3)))


   main()


   '''
   Time Complexity
   The time complexity of the above algorithm will be O(N) where ‘N’ is the number of characters in the input string.
   The outer for loop runs for all characters and the inner while loop processes each character only once, therefore the time complexity of the algorithm will be O(N+N) which is asymptotically equivalent to O(N).
   Space Complexity
   The space complexity of the algorithm is O(K), as we will be storing a maximum of ‘K+1’ characters in the HashMap.
   '''

Fruits into Baskets (medium)
--------------------------------------------------------------
.. code:: python

   '''
   Problem Statement：
   Given an array of characters where each character represents a fruit tree, you are given two baskets and your goal is to put maximum number of fruits in each basket. The only restriction is that each basket can have only one type of fruit.
   You can start with any tree, but once you have started you can’t skip a tree. You will pick one fruit from each tree until you cannot, i.e., you will stop when you have to pick from a third fruit type.
   Write a function to return the maximum number of fruits in both the baskets.

   Example 1:
   Input: Fruit=['A', 'B', 'C', 'A', 'C']
   Output: 3
   Explanation: We can put 2 'C' in one basket and one 'A' in the other from the subarray ['C', 'A', 'C']

   Example 2:
   Input: Fruit=['A', 'B', 'C', 'B', 'B', 'C']
   Output: 5
   Explanation: We can put 3 'B' in one basket and two 'C' in the other basket.
   This can be done if we start with the second letter: ['B', 'C', 'B', 'B', 'C']
   '''


   # mycode
   def fruits_into_baskets(fruits):
       from collections import defaultdict
       lookup = defaultdict(int)
       start, end = 0, 0
       max_len = 0

       while end < len(fruits):
           lookup[fruits[end]] += 1
           end += 1

           while len(lookup) > 2:
               lookup[fruits[start]] -= 1
               if lookup[fruits[start]] == 0:
                   del lookup[fruits[start]]
               start += 1

           max_len = max(max_len, end - start)

       return max_len


   # answer
   def fruits_into_baskets(fruits):
       window_start = 0
       max_length = 0
       fruit_frequency = {}

       # try to extend the range [window_start, window_end]
       for window_end in range(len(fruits)):
           right_fruit = fruits[window_end]
           if right_fruit not in fruit_frequency:
               fruit_frequency[right_fruit] = 0
           fruit_frequency[right_fruit] += 1

           # shrink the sliding window, until we are left with '2' fruits in the fruit frequency dictionary
           while len(fruit_frequency) > 2:
               left_fruit = fruits[window_start]
               fruit_frequency[left_fruit] -= 1
               if fruit_frequency[left_fruit] == 0:
                   del fruit_frequency[left_fruit]
               window_start += 1  # shrink the window
           max_length = max(max_length, window_end - window_start + 1)
       return max_length


   def main():
       print("Maximum number of fruits: " +
             str(fruits_into_baskets(['A', 'B', 'C', 'A', 'C'])))
       print("Maximum number of fruits: " +
             str(fruits_into_baskets(['A', 'B', 'C', 'B', 'B', 'C'])))


   main()


   '''
   Time Complexity
   The time complexity of the above algorithm will be O(N) where ‘N’ is the number of characters in the input array.
   The outer for loop runs for all characters and the inner while loop processes each character only once, therefore the time complexity of the algorithm will be O(N+N)which is asymptotically equivalent to O(N).
   Space Complexity
   The algorithm runs in constant space O(1) as there can be a maximum of three types of fruits stored in the frequency map.
   Similar Problems
   Problem 1: Longest Substring with at most 2 distinct characters
   Given a string, find the length of the longest substring in it with at most two distinct characters.
   Solution: This problem is exactly similar to our parent problem.
   '''

No-repeat Substring (hard)
--------------------------------------------------------------
.. code:: python

   '''
   Problem Statement：
   Given a string, find the length of the longest substring which has no repeating characters.

   Example 1:
   Input: String="aabccbb"
   Output: 3
   Explanation: The longest substring without any repeating characters is "abc".

   Example 2:
   Input: String="abbbb"
   Output: 2
   Explanation: The longest substring without any repeating characters is "ab".

   Example 3:
   Input: String="abccde"
   Output: 3
   Explanation: Longest substrings without any repeating characters are "abc" & "cde".
   '''


   # mycode
   def non_repeat_substring(str):
       from collections import defaultdict
       lookup = defaultdict(int)
       start, end = 0, 0
       counter = 0
       max_len = 0

       while end < len(str):
           if lookup[str[end]] > 0:
               counter += 1
           lookup[str[end]] += 1
           end += 1
           while counter > 0:
               if lookup[str[start]] > 1:
                   counter -= 1
               lookup[str[start]] -= 1
               start += 1
           max_len = max(max_len, end - start)
       return max_len


   # answer
   def non_repeat_substring(str):
       window_start = 0
       max_length = 0
       char_index_map = {}

       # try to extend the range [windowStart, windowEnd]
       for window_end in range(len(str)):
           right_char = str[window_end]
           # if the map already contains the 'right_char', shrink the window from the beginning so that
           # we have only one occurrence of 'right_char'
           if right_char in char_index_map:
               # this is tricky; in the current window, we will not have any 'right_char' after its previous index
               # and if 'window_start' is already ahead of the last index of 'right_char', we'll keep 'window_start'
               window_start = max(window_start, char_index_map[right_char] + 1)
           # insert the 'right_char' into the map
           char_index_map[right_char] = window_end
           # remember the maximum length so far
           max_length = max(max_length, window_end - window_start + 1)
       return max_length


   def main():
       print("Length of the longest substring: " +
             str(non_repeat_substring("aabccbb")))
       print("Length of the longest substring: " +
             str(non_repeat_substring("abbbb")))
       print("Length of the longest substring: " +
             str(non_repeat_substring("abccde")))


   main()


   '''
   Time Complexity
   The time complexity of the above algorithm will be O(N) where ‘N’ is the number of characters in the input string.
   Space Complexity
   The space complexity of the algorithm will be O(K) where KK is the number of distinct characters in the input string.
   This also means K<=N, because in the worst case, the whole string might not have any repeating character so the entire string will be added to the HashMap.
   Having said that, since we can expect a fixed set of characters in the input string (e.g., 26 for English letters), we can say that the algorithm runs in fixed space O(1); in this case, we can use a fixed-size array instead of the HashMap.
   '''

Longest Substring with Same Letters after Replacement (hard)
--------------------------------------------------------------
.. code:: python

   '''
   Problem Statement：
   Given a string with lowercase letters only, if you are allowed to replace no more than ‘k’ letters with any letter, find the length of the longest substring having the same letters after replacement.

   Example 1:
   Input: String="aabccbb", k=2
   Output: 5
   Explanation: Replace the two 'c' with 'b' to have a longest repeating substring "bbbbb".

   Example 2:
   Input: String="abbcb", k=1
   Output: 4
   Explanation: Replace the 'c' with 'b' to have a longest repeating substring "bbbb".

   Example 3:
   Input: String="abccde", k=1
   Output: 3
   Explanation: Replace the 'b' or 'd' with 'c' to have the longest repeating substring "ccc".
   '''


   # mycode
   def length_of_longest_substring(str, k):
       from collections import defaultdict
       max_len, max_freq, lookup = 0, 0, defaultdict(int)
       start, end = 0, 0

       while end < len(str):
           lookup[str[end]] += 1
           max_freq = max(max_freq, lookup[str[end]])
           end += 1
           if end - start - max_freq > k:
               lookup[str[start]] -= 1
               start += 1
           max_len = max(max_len, end - start)
       return max_len


   # answer
   def length_of_longest_substring(str, k):
       window_start, max_length, max_repeat_letter_count = 0, 0, 0
       frequency_map = {}

       # Try to extend the range [window_start, window_end]
       for window_end in range(len(str)):
           right_char = str[window_end]
           if right_char not in frequency_map:
               frequency_map[right_char] = 0
           frequency_map[right_char] += 1
           max_repeat_letter_count = max(max_repeat_letter_count,
                                         frequency_map[right_char])

           # Current window size is from window_start to window_end, overall we have a letter which is
           # repeating 'max_repeat_letter_count' times, this means we can have a window which has one letter
           # repeating 'max_repeat_letter_count' times and the remaining letters we should replace.
           # if the remaining letters are more than 'k', it is the time to shrink the window as we
           # are not allowed to replace more than 'k' letters
           if (window_end - window_start + 1 - max_repeat_letter_count) > k:
               left_char = str[window_start]
               frequency_map[left_char] -= 1
               window_start += 1

           max_length = max(max_length, window_end - window_start + 1)
       return max_length


   def main():
       print(length_of_longest_substring("aabccbb", 2))
       print(length_of_longest_substring("abbcb", 1))
       print(length_of_longest_substring("abccde", 1))


   main()


   '''
   Time Complexity
   The time complexity of the above algorithm will be O(N) where ‘N’ is the number of letters in the input string.
   Space Complexity
   As we are expecting only the lower case letters in the input string, we can conclude that the space complexity will be O(26), to store each letter’s frequency in the HashMap, which is asymptotically equal to O(1).
   '''

Longest Subarray with Ones after Replacement (hard)
--------------------------------------------------------------
.. code:: python

   '''
   Problem Statement：
   Given an array containing 0s and 1s, if you are allowed to replace no more than ‘k’ 0s with 1s, find the length of the longest contiguous subarray having all 1s.

   Example 1:
   Input: Array=[0, 1, 1, 0, 0, 0, 1, 1, 0, 1, 1], k=2
   Output: 6
   Explanation: Replace the '0' at index 5 and 8 to have the longest contiguous subarray of 1s having length 6.

   Example 2:
   Input: Array=[0, 1, 0, 0, 1, 1, 0, 1, 1, 0, 0, 1, 1], k=3
   Output: 9
   Explanation: Replace the '0' at index 6, 9, and 10 to have the longest contiguous subarray of 1s having length 9.
   '''


   # mycode
   def length_of_longest_substring(arr, k):
       max_len, start, end = 0, 0, 0
       max_ones_count = 0

       while end < len(arr):
           if arr[end] == 1:
               max_ones_count += 1

           end += 1

           if end - start - max_ones_count > k:
               if arr[start] == 1:
                   max_ones_count -= 1
               start += 1

           max_len = max(max_len, end - start)
       return max_len


   # answer
   def length_of_longest_substring(arr, k):
       window_start, max_length, max_ones_count = 0, 0, 0

       # Try to extend the range [window_start, window_end]
       for window_end in range(len(arr)):
           if arr[window_end] == 1:
               max_ones_count += 1

           # Current window size is from window_start to window_end, overall we have a maximum of 1s
           # repeating 'max_ones_count' times, this means we can have a window with 'max_ones_count' 1s
           # and the remaining are 0s which should replace with 1s.
           # now, if the remaining 1s are more than 'k', it is the time to shrink the window as we
           # are not allowed to replace more than 'k' 0s
           if (window_end - window_start + 1 - max_ones_count) > k:
               if arr[window_start] == 1:
                   max_ones_count -= 1
               window_start += 1

           max_length = max(max_length, window_end - window_start + 1)
       return max_length


   def main():
       print(length_of_longest_substring([0, 1, 1, 0, 0, 0, 1, 1, 0, 1, 1], 2))
       print(length_of_longest_substring([0, 1, 0, 0, 1, 1, 0, 1, 1, 0, 0, 1, 1], 3))


   main()


   '''
   Time Complexity
   The time complexity of the above algorithm will be O(N) where ‘N’ is the count of numbers in the input array.
   Space Complexity
   The algorithm runs in constant space O(1).
   '''

Problem Challenge 1 - Permutation in a String (hard)
--------------------------------------------------------------
.. code:: python

   '''
   Problem Challenge 1：
   Permutation in a String (hard)
   Given a string and a pattern, find out if the string contains any permutation of the pattern.
   Permutation is defined as the re-arranging of the characters of the string. For example, “abc” has the following six permutations:
   abc
   acb
   bac
   bca
   cab
   cba
   If a string has ‘n’ distinct characters it will have n!n! permutations.

   Example 1:
   Input: String="oidbcaf", Pattern="abc"
   Output: true
   Explanation: The string contains "bca" which is a permutation of the given pattern.

   Example 2:
   Input: String="odicf", Pattern="dc"
   Output: false
   Explanation: No permutation of the pattern is present in the given string as a substring.

   Example 3:
   Input: String="bcdxabcdy", Pattern="bcdyabcdx"
   Output: true
   Explanation: Both the string and the pattern are a permutation of each other.

   Example 4:
   Input: String="aaacb", Pattern="abc"
   Output: true
   Explanation: The string contains "acb" which is a permutation of the given pattern.
   '''

   # mycode
   def find_permutation(str, pattern):
       from collections import Counter
       lookup = Counter(pattern)

       window_start, matched = 0, 0

       for window_end in range(len(str)):
           right_char = str[window_end]
           if right_char in lookup:
               lookup[right_char] -= 1
               if lookup[right_char] == 0:
                   matched += 1

           if matched == len(lookup):
               return True

           if window_end >= len(pattern) - 1:
               left_char = str[window_start]
               window_start += 1
               if left_char in lookup:
                   if lookup[left_char] == 0:
                       matched -= 1
                   lookup[left_char] += 1
       return False


   # answer
   def find_permutation(str, pattern):
       window_start, matched = 0, 0
       char_frequency = {}

       for chr in pattern:
           if chr not in char_frequency:
               char_frequency[chr] = 0
           char_frequency[chr] += 1

       # our goal is to match all the characters from the 'char_frequency' with the current window
       # try to extend the range [window_start, window_end]
       for window_end in range(len(str)):
           right_char = str[window_end]
           if right_char in char_frequency:
               # decrement the frequency of matched character
               char_frequency[right_char] -= 1
               if char_frequency[right_char] == 0:
                   matched += 1

           if matched == len(char_frequency):
               return True

           # shrink the window by one character
           if window_end >= len(pattern) - 1:
               left_char = str[window_start]
               window_start += 1
               if left_char in char_frequency:
                   if char_frequency[left_char] == 0:
                       matched -= 1
                   char_frequency[left_char] += 1

       return False


   def main():
       print('Permutation exist: ' + str(find_permutation("oidbcaf", "abc")))
       print('Permutation exist: ' + str(find_permutation("odicf", "dc")))
       print('Permutation exist: ' +
             str(find_permutation("bcdxabcdy", "bcdyabcdx")))
       print('Permutation exist: ' + str(find_permutation("aaacb", "abc")))


   main()


   '''
   Time Complexity
   The time complexity of the above algorithm will be O(N + M) where ‘N’ and ‘M’ are the number of characters in the input string and the pattern respectively.

   Space Complexity
   The space complexity of the algorithm is O(M) since in the worst case,
   the whole pattern can have distinct characters which will go into the HashMap.
   '''

Problem Challenge 2 - String Anagrams (hard)
--------------------------------------------------------------
.. code:: python

   '''
   Problem Challenge 2：
   String Anagrams (hard)
   Given a string and a pattern, find all anagrams of the pattern in the given string.
   Anagram is actually a Permutation of a string. For example, “abc” has the following six anagrams:
   abc
   acb
   bac
   bca
   cab
   cba
   Write a function to return a list of starting indices of the anagrams of the pattern in the given string.

   Example 1:
   Input: String="ppqp", Pattern="pq"
   Output: [1, 2]
   Explanation: The two anagrams of the pattern in the given string are "pq" and "qp".

   Example 2:
   Input: String="abbcabc", Pattern="abc"
   Output: [2, 3, 4]
   Explanation: The three anagrams of the pattern in the given string are "bca", "cab", and "abc".
   '''


   # mycode
   def find_string_anagrams(str, pattern):
       len_s, len_p = len(str), len(pattern)
       vs, vp = [0] * 26, [0] * 26
       res = []

       for chr in pattern:
           vp[ord(chr) - ord('a')] += 1

       for i in range(len_s):
           if i >= len_p:
               vs[ord(str[i - len_p]) - ord('a')] -= 1
           vs[ord(str[i]) - ord('a')] += 1
           if vs == vp:
               res.append(i + 1 - len_p)
       return res


   # answer
   def find_string_anagrams(str, pattern):
       window_start, matched = 0, 0
       char_frequency = {}

       for chr in pattern:
           if chr not in char_frequency:
               char_frequency[chr] = 0
           char_frequency[chr] += 1

       result_indices = []
       # Our goal is to match all the characters from the 'char_frequency' with the current window
       # try to extend the range [window_start, window_end]
       for window_end in range(len(str)):
           right_char = str[window_end]
           if right_char in char_frequency:
               # Decrement the frequency of matched character
               char_frequency[right_char] -= 1
               if char_frequency[right_char] == 0:
                   matched += 1

           if matched == len(char_frequency):  # Have we found an anagram?
               result_indices.append(window_start)

           # Shrink the sliding window
           if window_end >= len(pattern) - 1:
               left_char = str[window_start]
               window_start += 1
               if left_char in char_frequency:
                   if char_frequency[left_char] == 0:
                       matched -= 1  # Before putting the character back, decrement the matched count
                   char_frequency[left_char] += 1  # Put the character back

       return result_indices


   def main():
       print(find_string_anagrams("ppqp", "pq"))
       print(find_string_anagrams("abbcabc", "abc"))


   main()


   '''
   Time Complexity
   The time complexity of the above algorithm will be O(N + M) where ‘N’ and ‘M’ are the number of characters in the input string and the pattern respectively.
   Space Complexity
   The space complexity of the algorithm is O(M) since in the worst case, the whole pattern can have distinct characters which will go into the HashMap.
   In the worst case, we also need O(N) space for the result list, this will happen when the pattern has only one character and the string contains only that character.
   '''

Problem Challenge 3 - Smallest Window containing Substring (hard)
------------------------------------------------------------------
.. code:: python

   '''
   Problem Challenge 3：
   Smallest Window containing Substring (hard)
   Given a string and a pattern, find the smallest substring in the given string which has all the characters of the given pattern.

   Example 1:
   Input: String="aabdec", Pattern="abc"
   Output: "abdec"
   Explanation: The smallest substring having all characters of the pattern is "abdec"

   Example 2:
   Input: String="abdabca", Pattern="abc"
   Output: "abc"
   Explanation: The smallest substring having all characters of the pattern is "abc".

   Example 3:
   Input: String="adcad", Pattern="abc"
   Output: ""
   Explanation: No substring in the given string has all characters of the pattern.
   '''


   # mycode
   def find_substring(str, pattern):
       from collections import Counter
       lookup = Counter(pattern)

       window_start, matched, substr_start = 0, 0, 0
       min_len = len(str) + 1

       for winow_end in range(len(str)):
           right_char = str[winow_end]
           if right_char in lookup:
               lookup[right_char] -= 1
               if lookup[right_char] == 0:
                   matched += 1

           while matched == len(lookup):
               if min_len > winow_end - window_start + 1:
                   min_len = winow_end - window_start + 1
                   substr_start = window_start

               left_char = str[window_start]
               window_start += 1
               if left_char in lookup:
                   if lookup[left_char] == 0:
                       matched -= 1
                   lookup[left_char] += 1

       if min_len > len(str):
           return ""
       return str[substr_start: substr_start + min_len]


   # answer
   def find_substring(str, pattern):
       window_start, matched, substr_start = 0, 0, 0
       min_length = len(str) + 1
       char_frequency = {}

       for chr in pattern:
           if chr not in char_frequency:
               char_frequency[chr] = 0
           char_frequency[chr] += 1

       # try to extend the range [window_start, window_end]
       for window_end in range(len(str)):
           right_char = str[window_end]
           if right_char in char_frequency:
               char_frequency[right_char] -= 1
               if char_frequency[
                       right_char] >= 0:  # Count every matching of a character
                   matched += 1

           # Shrink the window if we can, finish as soon as we remove a matched character
           while matched == len(pattern):
               if min_length > window_end - window_start + 1:
                   min_length = window_end - window_start + 1
                   substr_start = window_start

               left_char = str[window_start]
               window_start += 1
               if left_char in char_frequency:
                   # Note that we could have redundant matching characters, therefore we'll decrement the
                   # matched count only when a useful occurrence of a matched character is going out of the window
                   if char_frequency[left_char] == 0:
                       matched -= 1
                   char_frequency[left_char] += 1

       if min_length > len(str):
           return ""
       return str[substr_start:substr_start + min_length]


   def main():
       print(find_substring("aabdec", "abc"))
       print(find_substring("abdabca", "abc"))
       print(find_substring("adcad", "abc"))


   main()


   '''
   Time Complexity
   The time complexity of the above algorithm will be O(N + M) where ‘N’ and ‘M’ are the number of characters in the input string and the pattern respectively.
   Space Complexity
   The space complexity of the algorithm is O(M) since in the worst case, the whole pattern can have distinct characters which will go into the HashMap.
   In the worst case, we also need O(N) space for the resulting substring, which will happen when the input string is a permutation of the pattern.
   '''

Problem Challenge 4 - Words Concatenation (hard)
------------------------------------------------------------------
.. code:: python

   '''
   Problem Challenge 4：
   Words Concatenation (hard)
   Given a string and a list of words, find all the starting indices of substrings in the given string that are a concatenation of all the given words exactly once without any overlapping of words. It is given that all words are of the same length.

   Example 1:
   Input: String="catfoxcat", Words=["cat", "fox"]
   Output: [0, 3]
   Explanation: The two substring containing both the words are "catfox" & "foxcat".

   Example 2:
   Input: String="catcatfoxfox", Words=["cat", "fox"]
   Output: [3]
   Explanation: The only substring containing both the words is "catfox".
   '''


   # mycode
   def find_word_concatenation(str, words):
       result_indices = []
       word_count = len(words)
       word_len = len(words[0])

       for i in range(len(str) - word_count * word_len + 1):
           cnt = 0
           curr = str[i:i + word_count * word_len]

           for j in range(word_count):
               if words[j] not in curr:
                   break
               else:
                   cnt += 1

           if cnt == word_count:
               result_indices.append(i)

       return result_indices


   # answer
   def find_word_concatenation(str, words):
       if len(words) == 0 or len(words[0]) == 0:
           return []

       word_frequency = {}

       for word in words:
           if word not in word_frequency:
               word_frequency[word] = 0
               word_frequency[word] += 1

       result_indices = []
       words_count = len(words)
       word_length = len(words[0])

       for i in range((len(str) - words_count * word_length) + 1):
           words_seen = {}
           for j in range(0, words_count):
               next_word_index = i + j * word_length
               # Get the next word from the string
               word = str[next_word_index:next_word_index + word_length]
               if word not in word_frequency:  # Break if we don't need this word
                   break

               # Add the word to the 'words_seen' map
               if word not in words_seen:
                   words_seen[word] = 0
               words_seen[word] += 1

               # No need to process further if the word has higher frequency than required
               if words_seen[word] > word_frequency.get(word, 0):
                   break

               if j + 1 == words_count:  # Store index if we have found all the words
                   result_indices.append(i)

       return result_indices


   def main():
       print(find_word_concatenation("catfoxcat", ["cat", "fox"]))
       print(find_word_concatenation("catcatfoxfox", ["cat", "fox"]))


   main()


   '''
   Time Complexity
   The time complexity of the above algorithm will be O(N * M * Len) where ‘N’ is the number of characters in the given string,
   ‘M’ is the total number of words, and ‘Len’ is the length of a word.
   Space Complexity
   The space complexity of the algorithm is O(M) since at most, we will be storing all the words in the two HashMaps.
   In the worst case, we also need O(N) space for the resulting list. So, the overall space complexity of the algorithm will be O(M+N).
   '''
