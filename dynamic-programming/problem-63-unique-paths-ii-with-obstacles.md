# Problem 63: Unique Paths II \(with obstacles\)

## Description:

A robot is located at the top-left corner of a _m_ x _n_ grid \(marked 'Start' in the diagram below\).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid \(marked 'Finish' in the diagram below\).

Now consider if some obstacles are added to the grids. How many unique paths would there be?

![](https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png)

An obstacle and empty space is marked as `1` and `0` respectively in the grid.

**Note:** _m_ and _n_ will be at most 100.

## Example:

**Example 1:**

```text
Input:
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
Output: 2
Explanation:
There is one obstacle in the middle of the 3x3 grid above.
There are two ways to reach the bottom-right corner:
1. Right -> Right -> Down -> Down
2. Down -> Down -> Right -> Right

```

## Key points and Thoughts:

初始化第0行和第0列的时候，只要遇到了obstacle=1的，接下来的所有位置都要置为0。

在多重循环用方程计算结果的时候，如果obstacle=1，要置为0，表示到这个位置的路径有0条。

## Solution:

在原障碍数组上直接更改：

```python
class Solution:
    """
    @param obstacleGrid: A list of lists of integers
    @return: An integer
    """

    def uniquePathsWithObstacles(self, obstacleGrid):
        # write your code here
        if not obstacleGrid or obstacleGrid[0][0]:
            return 0
        m, n = len(obstacleGrid), len(obstacleGrid[0])
        obstacleGrid[0][0] = 1

        for j in range(1, n):
            obstacleGrid[0][j] = int(not obstacleGrid[0][j] and obstacleGrid[0][j-1])

        for i in range(1, m):
            obstacleGrid[i][0] = int(not obstacleGrid[i][0] and obstacleGrid[i-1][0])

        for i in range(1, m):
            for j in range(1, n):
                if obstacleGrid[i][j]:
                    obstacleGrid[i][j] = 0
                else:
                    obstacleGrid[i][j] = obstacleGrid[i - 1][j] + obstacleGrid[i][j - 1]
        return obstacleGrid[m-1][n-1]
```

新建立一个数组进行更改：

```python
class Solution:
    """
    @param obstacleGrid: A list of lists of integers
    @return: An integer
    """

    def uniquePathsWithObstacles(self, obstacleGrid):
        # write your code here
        if not obstacleGrid:
            return None
        m, n = len(obstacleGrid), len(obstacleGrid[0])
        f = [[0] * n for _ in range(m)]

        for j in range(n):
            if obstacleGrid[0][j]:
                break
            f[0][j] = 1
        for i in range(m):
            if obstacleGrid[i][0]:
                break
            f[i][0] = 1
        for i in range(1, m):
            for j in range(1, n):
                if obstacleGrid[i][j]:
                    f[i][j] = 0
                else:
                    f[i][j] = f[i - 1][j] + f[i][j - 1]
        return f[-1][-1]
```

