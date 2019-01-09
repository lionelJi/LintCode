# Problem 349: Intersection of Two Arrays

## Description:

Given two arrays, write a function to compute their intersection.

## Example:

**Example 1:**

```text
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2]
```

**Example 2:**

```text
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [9,4]
```

## Solution:

Three different algorithms:

\#1: HashSet --- Time: O\(n + m\)    Space: O\(min{m,n}\)

```python
class Solution:
    """
    @param nums1: an integer array
    @param nums2: an integer array
    @return: an integer array
    """
    def intersection(self, nums1, nums2):
        # write your code here
        result = set()
        if len(nums1) > len(nums2):
            nums1, nums2 = nums2, nums1
        nums1 = set(nums1)
        for element in nums2:
            if element in nums1:
                result.add(element)
        return list(result)
```

\#2: Binary Search --- Time: O\(nlogn + mlogn\)    Space: O\(1\)

```python
class Solution:
    """
    @param nums1: an integer array
    @param nums2: an integer array
    @return: an integer array
    """
    def intersection(self, nums1, nums2):
        # write your code here
        result = set()
        if not nums1:
            return []
        nums1 = sorted(nums1)
        for element in nums2:
            start, end = 0, len(nums1) - 1
            while start + 1 < end:
                mid = start + (end - start) // 2
                if nums1[mid] >= element:
                    end = mid
                else:
                    start = mid
            if nums1[start] == element or nums1[end] == element:
                result.add(element)
        return list(result)
```

\#3: Quick Sort + Merge --- Time: O\(nlogn + mlogm + n + m\)     Space: O\(1\)

```python
class Solution:
    """
    @param nums1: an integer array
    @param nums2: an integer array
    @return: an integer array
    """
    def intersection(self, nums1, nums2):
        # write your code here
        result = set()
        nums1, nums2 = sorted(nums1), sorted(nums2)
        len_1, len_2, i, j = len(nums1), len(nums2), 0, 0
        while i < len_1 and j < len_2:
            if nums1[i] < nums2[j]:
                i += 1
            elif nums2[j] < nums1[i]:
                j += 1
            else:
                result.add(nums1[i])
                i += 1
                j += 1
        return list(result)
```



