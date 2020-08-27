=======
Hard
=======


4. Median of Two Sorted Arrays
------------------------------------------------------------

`4. Median of Two Sorted Arrays`_

.. code:: python

   class Solution:
       def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
           l = len(nums1) + len(nums2)
           if l % 2 == 0:
               return (self.getKth(nums1, nums2, l // 2) + self.getKth(nums1, nums2, l // 2 + 1)) * 0.5
           else:
               return self.getKth(nums1, nums2, l // 2 + 1)

       def getKth(self, A, B, k):
           # 保证 A 小于 B
           if len(A) > len(B):
               return self.getKth(B, A, k)
           if not A:
               return B[k-1]
           if k == 1:
               return min(A[0], B[0])

           pa = min(k // 2, len(A))
           pb = k - pa

           if A[pa - 1] <= B[pb - 1]:
               return self.getKth(A[pa:], B, pb)
           else:
               return self.getKth(A, B[pb:], pa)

.. _4. Median of Two Sorted Arrays: https://leetcode.com/problems/median-of-two-sorted-arrays/


154. Find Minimum in Rotated Sorted Array II
------------------------------------------------------------

`154. Find Minimum in Rotated Sorted Array II`_

.. code:: python

   class Solution:
       def findMin(self, nums: List[int]) -> int:
           l, r = 0, len(nums) - 1
           while l < r:
               m = l + (r - l) // 2
               if nums[m] > nums[r]:
                   l = m + 1
               elif nums[m] < nums[r]:
                   r = m
               else:
                   # nums[m] == nums[r]
                   r -= 1
           return nums[l]

.. _154. Find Minimum in Rotated Sorted Array II: https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/
