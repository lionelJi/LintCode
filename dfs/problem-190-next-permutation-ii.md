---
description: 代码未完成
---

# Problem 190: Next Permutation II

## Description:

Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such arrangement is not possible, it must rearrange it as the lowest possible order \(ie, sorted in ascending order\).

## Example:

Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.

`1,2,3` → `1,3,2`

`3,2,1` → `1,2,3`

`1,1,5` → `1,5,1`  


## Key points & Thoughts:

一开始的想法是设置一个tag=false，permutation=input的时候tag=true，tag=true的时候return。

但是challenge里的要求是：

* The replacement must be in-place, do not allocate extra memory.

不知道是不是有好一点的方法。

！！！想法不对，replacement in-place 意思是不需要返回值，必须在原值上更改

思路完全不对。

看完leetcode解法：

* 找到第一个不是降序的位置
* 把i-1位置的数和后面降序序列里刚好比他大的数替换
* 将i-1后面的序列倒序

## Leetcode 解法：

**Algorithm**

First, we observe that for any given sequence that is in descending order, no next larger permutation is possible. For example, no next permutation is possible for the following array:

```text
[9, 5, 4, 3, 1]
```

We need to find the first pair of two successive numbers a\[i\]a\[i\] and a\[i-1\]a\[i−1\], from the right, which satisfy a\[i\] &gt; a\[i-1\]a\[i\]&gt;a\[i−1\]. Now, no rearrangements to the right of a\[i-1\]a\[i−1\] can create a larger permutation since that subarray consists of numbers in descending order. Thus, we need to rearrange the numbers to the right of a\[i-1\]a\[i−1\] including itself.

Now, what kind of rearrangement will produce the next larger number? We want to create the permutation just larger than the current one. Therefore, we need to replace the number a\[i-1\]a\[i−1\]with the number which is just larger than itself among the numbers lying to its right section, say a\[j\]a\[j\].

![ Next Permutation ](https://leetcode.com/media/original_images/31_nums_graph.png)

We swap the numbers a\[i-1\]a\[i−1\] and a\[j\]a\[j\]. We now have the correct number at index i-1i−1. But still the current permutation isn't the permutation that we are looking for. We need the smallest permutation that can be formed by using the numbers only to the right of a\[i-1\]a\[i−1\]. Therefore, we need to place those numbers in ascending order to get their smallest permutation.

But, recall that while scanning the numbers from the right, we simply kept decrementing the index until we found the pair a\[i\]a\[i\] and a\[i-1\]a\[i−1\] where, a\[i\] &gt; a\[i-1\]a\[i\]&gt;a\[i−1\]. Thus, all numbers to the right of a\[i-1\]a\[i−1\] were already sorted in descending order. Furthermore, swapping a\[i-1\]a\[i−1\] and a\[j\]a\[j\] didn't change that order. Therefore, we simply need to reverse the numbers following a\[i-1\]a\[i−1\] to get the next smallest lexicographic permutation.

The following animation will make things clearer:

![Next Permutation](https://leetcode.com/media/original_images/31_Next_Permutation.gif)

## Solution:

```python
class Solution:
    def nextPermutation(self, nums):
        """
        :type nums: List[int]
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        if not nums:
            return
        
        # 找到第一个不是降序的位置i-1
        i = len(nums) - 1
        while i-1 >= 0 and nums[i-1] >= nums[i]:
            i -= 1

        # 整个都是倒序的，下一个permutation就是正排序
        if not i:
            nums[:] = nums[::-1]
            return
        
        # 倒序，i-1位置和第一个比他大的数替换，替换后i位置上是正确的数字
        for j in range(len(nums)-1, i-1, -1):
            if nums[j] > nums[i-1]:
                nums[i-1], nums[j] = nums[j], nums[i-1]
                break
        # 将i位置往后逆序就好了
        nums[i:] = nums[i:][::-1]
        
            
        
```

