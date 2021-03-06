# Problem 162: Find Peak Element

## Description:

There is an integer array which has the following features:

* The numbers in adjacent positions are different.
* A\[0\] &lt; A\[1\] && A\[A.length - 2\] &gt; A\[A.length - 1\].

We define a position P is a peak if:

```text
A[P] > A[P-1] && A[P] > A[P+1]
```

Find a peak element in this array. Return the index of the peak.

## Example:

Given `[1, 2, 1, 3, 4, 5, 7, 6]`

Return index `1` \(which is number 2\) or `6` \(which is number 7\)

## Solution:

根据mid的值和前后的大小关系调整start和end，mid小于前面的值的话，前面一定有峰，mid小于后面的值的话，后面一定有峰，找到一个即可。

```python
class Solution:
    """
    @param A: An integers array.
    @return: return any of peek positions.
    """
    def findPeak(self, A):
        # write your code here
        if not A:
            return -1
        start, end = 0, len(A) - 1
        
        while start + 1 < end:
            mid = start + (end - start) // 2
            if A[mid-1] > A[mid]:
                end = mid
            elif A[mid] < A[mid+1]:
                start = mid
            else:
                end = mid
                
        result = start if A[start] > A[end] else end
        return result

```

##  

