# Problem 53: Maximum Subarray

## Description:

Given an integer array `nums`, find the contiguous subarray \(containing at least one number\) which has the largest sum and return its sum.

## Example:

**Example:**

```text
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

## Key points & Thoughts:

两种基本的思路：DP 和 pre\_sum

遍历整个list，不断累加num到pre\_sum，先更新max value，再更新min value，因为max value中减去的min value只能是之前的最小值，

DP：函数f是到这个index结尾的最大sum，f\[i\] = max\(0, f\[i-1\]\) + nums\[i\]，如果f\[i-1\]是负数，f\[i\]就不管前面的值，直接是本身就好，如果f\[i-1\]是正数，就加上现在的值。

## Solution:

pre\_sum:

```python
class Solution:
    def maxSubArray(self, nums):
        min_value, max_value = 0, float("-inf")
        pre_sum = 0
        for num in nums:
            pre_sum += num
            max_value = max(max_value, pre_sum - min_value)
            min_value = min(min_value, pre_sum)
        return max_value
```

DP:

```python
class Solution:
    def maxSubArray(self, nums):
        if len(nums) == 0:
            return 0
        f = [0 for _ in range(len(nums))]
        f[0] = nums[0]
        for i in range(1, len(nums)):
            f[i] = max(0, f[i-1]) + nums[i]
        return max(f)
```



