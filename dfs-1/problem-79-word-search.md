# Problem 79: Word Search

## Description:

Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

## Example:

```text
board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

Given word = "ABCCED", return true.
Given word = "SEE", return true.
Given word = "ABCB", return false.
```

## Key points & Thoughts:

比较类似灌水法，可以用dfs实现，在主函数里找到第一个字符，然后截取 input\[1: \] 进行dfs递归。

还是老问题，一定要注意回头，一开始写完的版本没有加visited集合，导致 "ABCB" 这样走几步回头的字符串也可以返回True。

Word Search 1 还可以，加油做一下Word Search 2。

## Solution:

```python
class Solution:
    direction = [(0, -1), (-1, 0), (0, 1), (1, 0)]
    result = False

    def exist(self, board, word):
        """
        :type board: List[List[str]]
        :type word: str
        :rtype: bool
        """
        for i in range(len(board)):
            for j in range(len(board[0])):
                if board[i][j] == word[0]:
                    self.dfs(board, word[1:], i, j, set())

        return self.result

    def dfs(self, board, word, row, col, visited):
        visited.add((row, col))
        if self.result:
            return
        if len(word) == 0:
            self.result = True
            return
        for (row_d, col_d) in self.direction:
            new_r, new_c = row + row_d, col + col_d
            if (new_r, new_c) in visited:
                continue
            if self.is_valid(board, new_r, new_c) and board[new_r][new_c] == word[0]:
                self.dfs(board, word[1:], new_r, new_c, visited)
                visited.remove((new_r, new_c))

    def is_valid(self, board, row, col):
        return 0 <= row < len(board) and 0 <= col < len(board[0])
```

