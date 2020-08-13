=========================
Sliding Window
=========================


面试常见题型。无意间发现国内版力扣，有人归类滑动窗口，写的不错。\ `链结`_

题目参考：LeetCode 3. Combinations

::

   Given a string, find the length of the longest substring without repeating characters.
   Example 1:
   Input: "abcabcbb"
   Output: 3
   Explanation: The answer is "abc", with the length of 3.

   Example 2:
   Input: "bbbbb"
   Output: 1
   Explanation: The answer is "b", with the length of 1.

   Example 3:
   Input: "pwwkew"
   Output: 3
   Explanation: The answer is "wke", with the length of 3.
               Note that the answer must be a substring, "pwke" is a subsequence and not a substring.


.. code:: python

   class Solution:
       def lengthOfLongestSubstring(self, s: str) -> int:
           from collections import defaultdict
           lookup = defaultdict(int)
           res, start, end = 0, 0, 0
           counter = 0
           max_len = 0

           while end < len(s):
               if lookup[s[end]] > 0:  # 如果大于0，代表查找表里面已经有该数字，counter += 1
                   counter += 1
               lookup[s[end]] += 1
               end += 1
               while counter > 0:  # counter > 0，表示查找表已经出现重复数字
                   if lookup[s[start]] > 1:  # 大于1就是多出来数字
                       counter -= 1
                   lookup[s[start]] -= 1
                   start += 1
               max_len = max(max_len, end - start)
           return max_len

题目参考： LeetCode 76. Minimum Window Substring

::

   Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).

   Example:
   Input: S = "ADOBECODEBANC", T = "ABC"
   Output: "BANC"

   Note:
   - If there is no such window in S that covers all characters in T, return the empty string "".
   - If there is such window, you are guaranteed that there will always be only one unique minimum window in S.


.. code:: python

   class Solution:
       def minWindow(self, s: str, t: str) -> str:
           from collections import defaultdict
           lookup = defaultdict(int)
           # 统计各字符需要的数量
           for c in t:
               lookup[c] += 1
           # 左指针 ＆ 右指针 & 答案
           start, end, res = 0, 0, ''
           # 记录t的数量
           counter = len(t)
           # 记录最短长度，初始化inf
           min_len = float('inf')

           while end < len(s):
               if lookup[s[end]] > 0:  # 如果此位置数在查找表，总数减1
                   counter -= 1
               lookup[s[end]] -= 1  # end往右移并把所有数记录在查找表
               end += 1
               while counter == 0:  # 已经找到包含t的滑动窗口
                   if min_len > end - start:
                       min_len = end - start
                       res = s[start:end]
                   if lookup[s[start]] == 0:  # 上面已经记录res，start开始往右移，如果等于0表示此字符为t里面字符
                       counter += 1
                   lookup[s[start]] += 1
                   start += 1
           return res

.. _链结: https://leetcode-cn.com/problems/minimum-window-substring/solution/hua-dong-chuang-kou-by-powcai-2/
