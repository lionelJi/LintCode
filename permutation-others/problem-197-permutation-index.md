# Problem 197: Permutation Index

## Description:

Given a permutation which contains no repeated number, find its index in all the permutations of these numbers, which are ordered in lexicographical order. The index begins at 1.

## Example:

Given \[1,2,4\], return 1.

## Key points & Thoughts:

很好用dfs给所有排列计数，但是dfs会找到所有情况，而我要做的是在找到和input相同的排列时就终止，这要怎么做呢。

用dfs的话会造成超时问题，需要想一个好的方案。

思路：

1.对于四位数：4213 = 4\*100+2\*100+1\*10+3

2.4个数的排列有4！种。当我们知道第一位数的时候，还有3！种方式，当知道第二位数时候还有2！种方式，当知道第三位数的时候还有1！种方式，前面三位数都确定的时候，最后一位也确定了。&lt;这里是按照高位到低位的顺序&gt;

3.对4个数的排列，各位的权值为：3！，2！，1！，0！。第一位之后的数小于第一位的个数是x，第二位之后的数小于第二位的个数是y，第三位之后的数小于第三的个数是z，第四位之后的数小于第四位的个数是w，则abcd排列所在的序列号:index = x\*3！+y\*2!+z\*1!,&lt;0!=0&gt;

在数的排列中，小数在前面，大数在后面，所以考虑该位数之后的数小于该位的数的个数，就这样。

4.例如 4213；x= 3，y = 1，z=0，index = 18+2=20

123；x = 0，y=0，index = 0

321；x= 2，y=1，index = 2\*2！+1\*1！ = 5

## Solution:

```python
class Solution:
    """
    @param A: An array of integers
    @return: A long integer
    """
    def permutationIndex(self, A):
        # write your code here
        result = 1
        factor = 1
        for i in range(len(A)-1, -1, -1):
            rank = 0
            for j in range(i+1, len(A)):
                if A[j] < A[i]:
                    rank += 1
            result += rank * factor
            factor *= len(A) - i
            
        return result

```

dfs版本：（会超时，不能用）

```python
class Solution:
    """
    @param A: An array of integers
    @return: A long integer
    """
    current_index = 0
    index = 0
    def permutationIndex(self, A):
        # write your code here
        self.helper(sorted(A), A, [], set())
        return self.index
        
    def helper(self, nums, current, permutation, visited):
        if len(permutation) == len(nums):
            self.current_index += 1
            print(permutation)
            print(self.current_index)
            if permutation == current:
                self.index = self.current_index
            return
        for i in nums:
            if i in visited:
                continue
            visited.add(i)
            permutation.append(i)
            self.helper(nums, current, permutation, visited)
            permutation.pop()
            visited.remove(i)
```

