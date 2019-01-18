# Problem 4: Median of two Sorted Array

## Description:

There are two sorted arrays **nums1** and **nums2** of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O\(log \(m+n\)\).

You may assume **nums1** and **nums2** cannot be both empty.

## Example:

**Example 1:**

```text
nums1 = [1, 3]
nums2 = [2]

The median is 2.0
```

**Example 2:**

```text
nums1 = [1, 2]
nums2 = [3, 4]

The median is (2 + 3)/2 = 2.5
```

## Key points & Solution:

函数化的思维：实现一个从两个有序列表中找第k大的值的函数

如果两个列表长度和加起来是奇数，就调用找第len/2 + 1大的值。

如果两个列表长度加起来是偶数，就调用找（第\(len/2\) + 第\(len/2 + 1\)\) / 2。

实现那个函数有几个出口条件

* A列表空了（或者index大于len）
* B列表空了（或者index大于len）
* k 值为1了

## Solution:

```python
import sys
class Solution:
    """
    @param: A: An integer array
    @param: B: An integer array
    @return: a double whose format is *.5 or *.0
    """
    def findMedianSortedArrays(self, A, B):
        # write your code here
        size = len(A) + len(B)
        if size % 2 == 0:
            return (self.findKthLargest(A, 0, B, 0, size//2) + self.findKthLargest(A, 0, B, 0, size//2 + 1)) / 2
        
        return self.findKthLargest(A, 0, B, 0, size//2 + 1)
        
        
    def findKthLargest(self, A, A_start, B, B_start, k):
        if A_start >= len(A):
            return B[B_start + k - 1]
        if B_start >= len(B):
            return A[A_start + k - 1]
        if k == 1:
            return min(A[A_start], B[B_start])

        A_key = A[A_start + k//2 - 1] if (A_start + k//2) <= len(A) else sys.maxsize
        B_key = B[B_start + k//2 - 1] if (B_start + k//2) <= len(B) else sys.maxsize
        
        if A_key > B_key:
            return self.findKthLargest(A, A_start, B, B_start + k//2, k - k//2)
        else:
            return self.findKthLargest(A, A_start + k//2, B, B_start, k - k//2)            
```

