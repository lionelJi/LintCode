---
description: 稳定的排序算法，最好最坏情况都是O(nlogn)
---

# 归并排序Merge Sort

不要求在原数据上更改， 会有O\(n\)的空间开销：

```python
def MergeSort(nums):
    if len(nums) <= 1:
        return nums
    mid = len(nums) // 2
    left = MergeSort(nums[:mid])
    right = MergeSort(nums[mid:])
    return Merge(left, right)


def Merge(left, right):
    r, l = 0, 0
    result = []
    while l < len(left) and r < len(right):
        if left[l] < right[r]:
            result.append(left[l])
            l += 1
        else:
            result.append(right[r])
            r += 1
    result += list(left[l:])
    result += list(right[r:])
    return result
```

要求在原数据上更改：



