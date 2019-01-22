# Problem 26: Remove Duplicates

## Description:

Given a sorted array _nums_, remove the duplicates [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) such that each element appear only _once_ and return the new length.

Do not allocate extra space for another array, you must do this by **modifying the input array** [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) with O\(1\) extra memory.

## Example:

**Example 1:**

```text
Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.

It doesn't matter what you leave beyond the returned length.
```

**Example 2:**

```text
Given nums = [0,0,1,1,1,2,2,3,3,4],

Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.

It doesn't matter what values are set beyond the returned length.
```

## Key points  & Thoughts:

慢指针指向最后一个不重复的数。

快指针遍历慢指针后面，找到第一个和慢指针值不想等的数换到它后面。

如果给的数组是无序的，则需要先排序。

也可以用hashset做，但有额外的空间开销。

## Solution:

```python
class Solution:
    def removeDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        # 慢指针应该是最后一个不重复的数字
        # 快指针应该去找第一个和慢指针不同的值，换到慢指针后面
        if not nums:
            return 0
        index = 0
        
        for i in range(index + 1, len(nums)):
            if nums[i] != nums[index]:
                index += 1
                nums[index], nums[i] = nums[i], nums[index]
                
        return index + 1
```

