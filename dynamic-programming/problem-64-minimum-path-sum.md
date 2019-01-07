# Problem 64: Minimum Path Sum

## Description:

Given a **m x n** grid filled with non-negative numbers, find a path from top left to bottom right which **minimizes** the sum of all numbers along its path.

## Example:

```text
Input
[[1,3,1],[1,5,1],[4,2,1]]

Output:
7
```

## Key points & Thoughts:

初始化一个二位动态规划时，要去初始化第零行和第零列。

## Solution:

```python
class Solution:
    """
    @param grid: a list of lists of integers
    @return: An integer, minimizes the sum of all numbers along its path
    """
    def minPathSum(self, grid):
        # write your code here
        # State: minimum path length from (0, 0) to (i, j)
        if not grid:
            return None
        m, n = len(grid), len(grid[0])
        f = [[0] * n for _ in range(m)]
        f[0][0] = grid[0][0]
        
        # Initialize
        for i in range(1, m):
            f[i][0] = grid[i][0] + f[i-1][0]
        for j in range(1, n):
            f[0][j] = grid[0][j] + f[0][j-1]
        
        # Function
        for i in range(1, m):
            for j in range(1, n):
                f[i][j] = grid[i][j] + min(f[i-1][j], f[i][j-1])
        
        return f[-1][-1]
        
```



