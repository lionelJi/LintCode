# Problem 215: Kth Largest Element

## Description:

Find the **k**th largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

## Example:

**Example 1:**

```text
Input: [3,2,1,5,6,4] and k = 2
Output: 5
```

**Example 2:**

```text
Input: [3,2,3,1,2,4,5,5,6] and k = 4
Output: 4
```

## Key points & Thoughts:

This [textbook algorthm](https://en.wikipedia.org/wiki/Quickselect) has \mathcal{O}\(N\)O\(N\) average time complexity. Like quicksort, it was developed by Tony Hoare, and is also known as _Hoare's selection algorithm_.

The approach is basically the same as for quicksort. For simplicity let's notice that `k`th largest element is the same as `N - k`th smallest element, hence one could implement `k`th smallest algorithm for this problem.

First one chooses a pivot, and defines its position in a sorted array in a linear time. This could be done with the help of _partition algorithm_.

> To implement partition one moves along an array, compares each element with a pivot, and moves all elements smaller than pivot to the left of the pivot.

As an output we have an array where pivot is on its perfect position in the ascending sorted array, all elements on the left of the pivot are smaller than pivot, and all elements on the right of the pivot are larger or equal to pivot.

Hence the array is now split into two parts. If that would be a quicksort algorithm, one would proceed recursively to use quicksort for the both parts that would result in \mathcal{O}\(N \log\(N\)\)O\(Nlog\(N\)\) time complexity. Here there is no need to deal with both parts since now one knows in which part to search for `N - k`th smallest element, and that reduces average time complexity to \mathcal{O}\(N\)O\(N\).

Finally the overall algorithm is quite straightforward :

* Choose a random pivot.
* Use a partition algorithm to place the pivot into its perfect position `pos` in the sorted array, move smaller elements to the left of pivot, and larger or equal ones - to the right.
* Compare `pos` and `N - k` to choose the side of array to proceed recursively.

> ! Please notice that this algorithm works well even for arrays with duplicates.

![quickselect](https://leetcode.com/problems/kth-largest-element-in-an-array/Figures/215/215_quickselect.png)

## Solution:

```python
from random import randrange
class Solution(object):
    def findKthLargest(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        if len(nums) == 1:
            return nums[0]
        nums, pivot = self.partition(nums, randrange(len(nums)))
        
        # the pivot is in its final sorted position
        if pivot == k - 1:
            return nums[pivot]
        # go left
        elif pivot > k - 1:
            return self.findKthLargest(nums[:pivot], k)
        # go right
        else:
            return self.findKthLargest(nums[pivot+1:], k-pivot-1)
        
    def partition(self, nums, pivot=0):
        i = 0
        
        # 1. move pivot to first
        if pivot != 0:
            nums[0], nums[pivot] = nums[pivot], nums[0]
            
        # 2. move all larger elements to the left
        for j in range(1, len(nums)):
            if nums[j] > nums[0]:
                nums[j], nums[i+1] = nums[i+1], nums[j]
                i += 1
                
        # 3. move pivot to its final place
        nums[0], nums[i] = nums[i], nums[0]
        
        return nums, i
        
```

