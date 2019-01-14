# Problem 88: Merge sorted array

## Description:

Given two sorted integer arrays _nums1_ and _nums2_, merge _nums2_ into _nums1_ as one sorted array.

**Note:**

* The number of elements initialized in _nums1_ and _nums2_ are _m_ and _n_respectively.
* You may assume that _nums1_ has enough space \(size that is greater or equal to _m_ + _n_\) to hold additional elements from _nums2_.

## Example:

**Example:**

```text
Input:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

Output: [1,2,2,3,5,6]
```

## Solution:

因为列表里的元素是升序的，而且A中的empty在列表尾端，所以合并时从两个列表末尾不断选较大的数加到A的尾端。空的值都在列表尾，所以要跳出merge要从列表头开始的固定思路。

```python
class Solution:
    """
    @param: A: sorted integer array A which has m elements, but size of A is m+n
    @param: m: An integer
    @param: B: sorted integer array B which has n elements
    @param: n: An integer
    @return: nothing
    """
    def mergeSortedArray(self, A, m, B, n):
        # write your code here
        i, m, n = len(A) - 1, m-1, n-1
        while m >= 0 and n >= 0:
            if A[m] >= B[n]:
                A[i] = A[m]
                m -= 1
            else:
                A[i] = B[n]
                n -= 1
            i -= 1
        if m < 0:
            A[:i+1] = B[:i+1]
```



