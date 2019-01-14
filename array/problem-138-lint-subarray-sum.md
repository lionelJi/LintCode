# Problem 138\(Lint\): Subarray Sum

## Description:

Given an integer array, find a subarray where the sum of numbers is **zero**. Your code should return the index of the first number and the index of the last number.

## Example:

#### Example

Given `[-3, 1, 2, -3, 4]`, return `[0, 2]` or `[1, 3]`.

## Key points & Thoughts:

这样n方时间复杂度的算法有的test case会超时，肯定不行了。

```python
def subarraySum(self, nums):
    # write your code here
    for i in range(len(nums)):
        for j in range(i, len(nums)):
            if sum(nums[i:j+1]) == 0:
                print('i: %d, j: %d' % (i, j))
                return [i, j]
```

要用动态规划存之前的结果吗？如果是这样的话，需要有一个二维数组存储很多中间值，还有什么方法么

一个字典初始化为{0: -1}，设置一个sum参数，从头到位遍历数组，每一个sum和对应的坐标都存到一个字典里，以\[-3, 1, 2, -3, 4\]为例，存到字典里的第一个值应该是{0: -1, -3 : 0}，然后是{0: -1, -3 : 0, -2 : 1}，如果某一个sum已经在之前的字典key里了，比如某一刻sum又等于-3了，说明从上一个sum为-3的index到现在这个index，中间的值加起来为0，返回就好了，这样时间复杂度是n而不是n方了。

## Solution:

```python
class Solution:
    """
    @param nums: A list of integers
    @return: A list of integers includes the index of the first number and the index of the last number
    """
    def subarraySum(self, nums):
        # write your code here
        pre_sum = 0
        pre_hash = {0: -1}
        for i, num in enumerate(nums):
            pre_sum += num
            if pre_sum in pre_hash:
                return pre_hash[pre_sum] + 1, i
            pre_hash[pre_sum] = i
        return -1, -1
```



