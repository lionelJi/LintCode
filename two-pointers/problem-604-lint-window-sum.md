# Problem 604\(Lint\): Window Sum

## Description:

Given an array of n integers, and a moving window\(size k\), move the window at each iteration from the start of the array, find the `sum` of the element inside the window at each moving.  


## Example:

#### Example

For array `[1,2,7,8,5]`, moving window size k = `3`.  
1 + 2 + 7 = 10  
2 + 7 + 8 = 17  
7 + 8 + 5 = 20  
return `[10,17,20]`

## Key points & Thoughts:

慢指针指向window第一个位置。

快指针指向window后第一个位置。

不断的减去慢指针值，加上快指针的值，达到window向前移动的效果。

## Solution:

```python
class Solution:
    """
    @param nums: a list of integers.
    @param k: length of window.
    @return: the sum of the element inside the window at each moving.
    """
    def winSum(self, nums, k):
        # write your code here
        result = []
        if not nums or k > len(nums):
            return result
        left, right = 0, k
        # add the first value
        pre_sum = sum(nums[left:right])
        result.append(pre_sum)
        
        # moving forward, minus left value, add right value
        while right < len(nums):
            pre_sum -= nums[left]
            pre_sum += nums[right]
            result.append(pre_sum)
            right += 1
            left += 1
        
        return result
            
        
```

