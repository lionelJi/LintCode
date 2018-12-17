# Problem 33: N-Queens

## Description:

The n-queens puzzle is the problem of placing n queens on an `n×n` chessboard such that no two queens attack each other.

Given an integer `n`, return all distinct solutions to the n-queens puzzle.

Each solution contains a distinct board configuration of the n-queens' placement, where `'Q'` and `'.'`both indicate a queen and an empty space respectively.

## Example:

There exist two distinct solutions to the 4-queens puzzle:

```text
[
  // Solution 1
  [".Q..",
   "...Q",
   "Q...",
   "..Q."
  ],
  // Solution 2
  ["..Q.",
   "Q...",
   "...Q",
   ".Q.."
  ]
]
```

## Key points & Thoughts:

最主要的思路就是为棋盘建立一个合适的表示结构，用一个长度为n的列表表示棋子在第N行的列序号，通过的列序号的筛选，用dfs获得所有可能的位置结果。

位置冲突的表示很重要：

* 所有皇后不能在同一列上，所以list中不能有重复数字。
* 所有皇后不能再同一斜线上，所以list中的数字和其坐标有一定的限制条件：
  * 正对角线： x2 - x1 = y2 - y1
  * 反对角线:    x2 - x1 = y1 - y2

## Solution:

```python
class Solution:
    """
    @param: n: The number of queens
    @return: All distinct solutions
    """

    def solveNQueens(self, n):
        # write your code here
        if n is None:
            return None
        pos = []
        self.get_pos(n, [], pos, set())
        results = self.draw_board(pos, n)
        return results

    def get_pos(self, n, perm, position, visited):
        if len(perm) == n:
            position.append(perm[:])
            return
        for i in range(n):
            if i in visited:
                continue
            if perm and self.is_diagonal(i, perm):
                continue
            perm.append(i)
            visited.add(i)
            self.get_pos(n, perm, position, visited)
            visited.remove(i)
            perm.pop()

    def is_diagonal(self, i, perm):
        for x, y in enumerate(perm):
            if (len(perm) - x) == (i - y) or (x + y) == (len(perm) + i):
                return True
        return False

    def draw_board(self, pos, n):
        results = []
        for ans in pos:
            result = []
            for i in ans:
                result.append('.' * i + 'Q' + '.' * (n - i - 1))
            results.append(result)
        return results
```

