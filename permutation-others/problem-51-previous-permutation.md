# Problem 51: Previous Permutation

## Description:

Given a list of integers, which denote a permutation.

Find the previous permutation in ascending order.

## Example:

For `[1,3,2,3]`, the previous permutation is `[1,2,3,3]`

For `[1,2,3,4]`, the previous permutation is `[4,3,2,1]`

## Key points & Thoughts:

和next permutation思路一样：

对于序列5 4 2 3 6，正确的前一个序列应该是5 3 6 4 2。

从右向左找到第一个nums\[i\] &lt; nums\[i-1\]的地方。

把i-1位置的和从右向左第一个比i-1位置小的互换，这是i-1位置是正确的数字，i位置到结尾仍然是一个升序序列。变成了5 3 2 4 6。

将i-1之后的逆序，变为i-1起始的最大值就可以了，结果是5 4 6 4 2。

## Solution:

```python
class Solution:
    """
    @param: nums: A list of integers
    @return: A list of integers that's previous permuation
    """
    def previousPermuation(self, nums):
        # write your code here
        if nums is None or len(nums) == 0:
            return []
            
        i = len(nums) - 1
        while i >= 1 and nums[i] >= nums[i-1]:
            i -= 1
        
        if not i:
            return nums[::-1]
        
        for j in range(len(nums)-1, i-1, -1):
            if nums[j] < nums[i-1]:
                nums[j], nums[i-1] = nums[i-1], nums[j]
                break
        return nums[:i] + nums[i:][::-1]
        
        
```

