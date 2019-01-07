# Problem 120: Triangle

## Description:

Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.

## Example:

Given the following triangle:

```text
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
```

The minimum path sum from top to bottom is 11 \(i.e., 2 + 3 + 5 + 1 = 11\).

## Key points & Thoughts:

几种解法：

开销 O\(2^n\):

* DFS - Traverse
* DFS - Divide and Conquer

开销 O\(n^2\):

* DFS - Divide & Conquer + Memorization
* DP

## Solution:

DFS - Traverse:

```python
class Solution:
    """
    @param triangle: a list of lists of integers
    @return: An integer, minimum path sum
    """
    min_path = float('inf')
    
    def minimumTotal(self, triangle):
        # write your code here
        self.traverse(triangle, 0, 0, 0)
        return Solution.min_path
        
        
    def traverse(self, tri, x, y, sum):
        # exit
        if x == len(tri):
            Solution.min_path = min(Solution.min_path, sum)
            return
        self.traverse(tri, x+1, y, sum + tri[x][y])
        self.traverse(tri, x+1, y+1, sum + tri[x][y])
        

```



DFS - Divide & Conquer:

```python
class Solution:
    """
    @param triangle: a list of lists of integers
    @return: An integer, minimum path sum
    """

    def minimumTotal(self, triangle):
        # write your code here
        return self.divide_conquer(triangle, 0, 0)
        
    def divide_conquer(self, tri, x, y):
        if x == len(tri):
            return 0
        return tri[x][y] + min(self.divide_conquer(tri, x+1, y),
                                self.divide_conquer(tri, x+1, y+1))
        

```



DFS - Divide & Conquer + Memorization:

```python
class Solution:
    """
    @param triangle: a list of lists of integers
    @return: An integer, minimum path sum
    """

    def minimumTotal(self, triangle):
        # write your code here
        min_value = [[float('inf')] * len(triangle[-1]) for i in range(len(triangle))]

        result = self.divide_conquer(triangle, 0, 0, min_value)
        return result

    def divide_conquer(self, tri, x, y, min_value):
        if x == len(tri):
            return 0
        if min_value[x][y] != float('inf'):
            # print('{0}   {1}  {2}'.format(x, y, min_value[x][y]))
            return min_value[x][y]

        min_value[x][y] = tri[x][y] + min(self.divide_conquer(tri, x + 1, y, min_value),
                                          self.divide_conquer(tri, x + 1, y + 1, min_value))
        return min_value[x][y]
```

