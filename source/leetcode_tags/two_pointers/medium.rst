=======
Medium
=======


11. Container With Most Water
------------------------------------------------------------

`11. Container With Most Water`_

.. code:: python

   class Solution:
       def maxArea(self, height: List[int]) -> int:
           if len(height) < 2:
               return 0
           area, l, r = 0, 0, len(height) - 1
           while l < r:
               area = max(area, min(height[l], height[r]) * (r - l))
               if height[l] < height[r]:
                   l += 1
               else:
                   r -= 1
           return area

.. _11. Container With Most Water: https://leetcode.com/problems/container-with-most-water/


15. 3Sum
------------------------------------------------------------

`15. 3Sum`_

.. code:: python

   class Solution:
       def threeSum(self, nums: List[int]) -> List[List[int]]:
           res = []
           nums.sort()
           for i in range(len(nums) - 2):
               # pass duplicate
               if i > 0 and nums[i] == nums[i - 1]:
                   continue
               l, r = i + 1, len(nums) - 1
               while l < r:
                   s = nums[i] + nums[l] + nums[r]
                   if s < 0:
                       l += 1
                   elif s > 0:
                       r -= 1
                   else:
                       res.append((nums[i], nums[l], nums[r]))
                       # pass duplicate
                       while l < r and nums[l] == nums[l + 1]:
                           l += 1
                       while l < r and nums[i] == nums[i - 1]:
                           r -= 1
                       l += 1; r -= 1
           return res

.. _15. 3Sum: https://leetcode.com/problems/3sum/


16. 3Sum Closest
------------------------------------------------------------

`16. 3Sum Closest`_

.. code:: python

   class Solution:
       def threeSumClosest(self, nums: List[int], target: int) -> int:
           nums.sort()
           d = sys.maxsize
           res = 0
           for i in range(len(nums) - 2):
               l, r = i + 1, len(nums) - 1
               while l < r:
                   s = nums[i] + nums[l] + nums[r]
                   if s == target:
                       return s
                   diff = abs(s - target)
                   if diff < d:
                       d = diff
                       res = s
                   if s < target:
                       l += 1
                   else:
                       r -= 1
           return res

.. _16. 3Sum Closest: https://leetcode.com/problems/3sum-closest/


18. 4Sum
------------------------------------------------------------

`18. 4Sum`_

.. code:: python

   class Solution:
       def fourSum(self, nums: List[int], target: int) -> List[List[int]]:
           nums.sort()
           res = []
           self.findNSum(nums, target, 4, [], res)
           return res

       def findNSum(self, nums, target, N, path, res):
           if len(nums) < N or N < 2:
               return
           # solve 2-sum
           if N == 2:
               l, r = 0, len(nums) - 1
               while l < r:
                   if nums[l] + nums[r] == target:
                       res.append(path + [nums[l], nums[r]])
                       l += 1
                       r -= 1
                       while l < r and nums[l] == nums[l - 1]:
                           l += 1
                       while l < r and nums[r] == nums[r + 1]:
                           r -= 1
                   elif nums[l] + nums[r] < target:
                       l += 1
                   else:
                       r -= 1
           else:
               for i in range(0, len(nums) - N + 1):  # careful about range
                   if target < nums[i] * N or target > nums[-1] * N:  # take advantages of sorted list
                       break
                   if i == 0 or i > 0 and nums[i-1] != nums[i]:  # recursively reduce N
                       self.findNSum(nums[i+1:], target - nums[i], N - 1, path + [nums[i]], res)
           return

.. _18. 4Sum: https://leetcode.com/problems/4sum/


75. Sort Colors
------------------------------------------------------------

`75. Sort Colors`_

.. code:: python

   class Solution:
       def sortColors(self, nums: List[int]) -> None:
           l, r, zero = 0, len(nums) - 1, 0
           while l <= r:
               if nums[l] == 0:
                   nums[l], nums[zero] = nums[zero], nums[l]
                   l += 1; zero += 1
               elif nums[l] == 2:
                   nums[l], nums[r] = nums[r], nums[l]
                   r -= 1
               else:
                   l += 1

.. _75. Sort Colors: https://leetcode.com/problems/sort-colors/


287. Find the Duplicate Number
------------------------------------------------------------

`287. Find the Duplicate Number`_

.. code:: python

   class Solution:
       def findDuplicate(self, nums: List[int]) -> int:
           slow = fast = tail = 0

           while True:
               slow = nums[slow]
               fast = nums[nums[fast]]
               if slow == fast: break

           while True:
               slow = nums[slow]
               tail = nums[tail]
               if slow == tail: break

           return slow

.. _287. Find the Duplicate Number: https://leetcode.com/problems/find-the-duplicate-number/

