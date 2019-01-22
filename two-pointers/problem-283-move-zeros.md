# Problem 283: Move Zeros

## Description:

Given an array `nums`, write a function to move all `0`'s to the end of it while maintaining the relative order of the non-zero elements.

把所有0都挪到列表尾。

## Example:

Given `nums = [0, 1, 0, 3, 12]`, after calling your function, `nums` should be `[1, 3, 12, 0, 0]`.

## Key Points & Thoughts:

指针都应该指向什么：慢指针指向第一个0值位置，快指针从慢指针位置开始遍历寻找非0值。

## Solution:

```python
class Solution:
    """
    @param nums: an integer array
    @return: nothing
    """
    def moveZeroes(self, nums):
        # write your code here
        if not nums:
            return []
        # left pointer should be position of the first zero
        index = 0
        while index < len(nums) and nums[index] != 0:
            index += 1
        
        # when right pointer find non-zero value, exchange them
        for i in range(index + 1, len(nums)):
            if nums[i] != 0:
                nums[i], nums[index] = nums[index], nums[i]
                index += 1
        
        return nums
            
```

