# Problem 74: Search a 2D Matrix

## Description:

Write an efficient algorithm that searches for a value in an _m_ x _n_ matrix. This matrix has the following properties:

* Integers in each row are sorted from left to right.
* The first integer of each row is greater than the last integer of the previous row.

## Example:

**Example 1:**

```text
Input:
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 3
Output: true
```

**Example 2:**

```text
Input:
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 13
Output: false
```

## Solution:

两次二分查找。

```python
class Solution(object):
    def searchMatrix(self, matrix, target):
        """
        :type matrix: List[List[int]]
        :type target: int
        :rtype: bool
        """
        if not matrix or not matrix[0]:
            return False
        y1, y2, x1, x2 = 0, len(matrix)-1, 0, len(matrix[0])-1
        
        while y1 + 1 < y2:
            mid = y1 + (y2 - y1) // 2
            if matrix[mid][0] <= target:
                y1 = mid
            else:
                y2 = mid
        # 找到可能存在的行坐标
        y = y1 if matrix[y2][0] > target else y2
        
        while x1 + 1 < x2:
            mid = x1 + (x2 - x1) // 2
            if matrix[y][mid] <= target:
                x1 = mid
            else:
                x2 = mid
        return True if matrix[y][x1] == target or matrix[y][x2] == target else False
        
```

