# Problem 34: N-Queens II

## Description:

Now, instead outputting board configurations, return the total number of distinct solutions.

## Example:

For n=4, there are 2 distinct solutions.

## Key points & Thoughts:

什么不一样？

不需要得到具体在那个地方，不需要打印出棋盘，只要知道有几种结果就行。

一共几种结果存成一个变量result，permutation长度等于n时，就把result加一。

同样需要判断对角线和横竖线。

试一下吧。

## Solution:

```python
class Solution:
    """
    @param n: The number of queens.
    @return: The total number of distinct solutions.
    """
    result = 0
    def totalNQueens(self, n):
        # write your code here
        self.helper(n, [])
        return self.result
        
    def helper(self, n, positions):
        if len(positions) == n:
            print(positions)
            self.result += 1
            return
        for i in range(n):
            if i in positions or self.diagonal(i, positions):
                continue
            positions.append(i)
            self.helper(n, positions)
            positions.pop()
            
    def diagonal(self, i, positions):
        for x, y in enumerate(positions):
            if x - y == len(positions) - i or x + y == len(positions) + i:
                return True
        return False
            

```

