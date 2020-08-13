=======
Easy
=======


28. Implement strStr()
-----------------------------------------------------------

`28. Implement strStr()`_

.. code:: python

   class Solution:
       def strStr(self, haystack: str, needle: str) -> int:
           L, n = len(needle), len(haystack)

           for start in range(n - L + 1):
               if haystack[start: start + L] == needle:
                   return start
           return -1

.. _28. Implement strStr(): https://leetcode.com/problems/implement-strstr/


88. Merge Sorted Array
-----------------------------------------------------------

`88. Merge Sorted Array`_

.. code:: python

   class Solution:
       def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
           i = m - 1
           j = n - 1
           k = m + n - 1
           while i >= 0 and j >= 0:
               if nums1[i] >= nums2[j]:
                   nums1[k] = nums1[i]
                   i -= 1
               else:
                   nums1[k] = nums2[j]
                   j -= 1
               k -= 1
           while j >= 0:
               nums1[k] = nums2[j]
               k -= 1
               j -= 1
           return

.. _88. Merge Sorted Array: https://leetcode.com/problems/merge-sorted-array/


167. Two Sum II - Input array is sorted
-----------------------------------------------------------

`167. Two Sum II - Input array is sorted`_

.. code:: python

   class Solution:
       def twoSum(self, numbers: List[int], target: int) -> List[int]:
           l, r = 0, len(numbers) - 1
           while l < r:
               if numbers[l] + numbers[r] == target:
                   return [l + 1, r + 1]
               elif numbers[l] + numbers[r] > target:
                   r -= 1
               else:
                   l += 1

.. _167. Two Sum II - Input array is sorted: https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/


344. Reverse String
-----------------------------------------------------------

`344. Reverse String`_

.. code:: python

   class Solution:
       def reverseString(self, s: List[str]) -> None:
           l, r = 0, len(s) - 1
           while l < r:
               s[l], s[r] = s[r], s[l]
               l += 1; r -= 1
           return

.. _344. Reverse String: https://leetcode.com/problems/reverse-string/


349. Intersection of Two Arrays
-----------------------------------------------------------

`349. Intersection of Two Arrays`_

.. code:: python

   class Solution:
       def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
           res = []
           nums1.sort()
           nums2.sort()
           i = j = 0
           while (i < len(nums1) and j < len(nums2)):
               if nums1[i] > nums2[j]:
                   j += 1
               elif nums1[i] < nums2[j]:
                   i += 1
               else:
                   if not (len(res) and nums1[i] == res[len(res)-1]):
                       res.append(nums1[i])
                   i += 1
                   j += 1

           return res

.. _349. Intersection of Two Arrays: https://leetcode.com/problems/intersection-of-two-arrays/
