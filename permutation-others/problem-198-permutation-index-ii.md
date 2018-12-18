# Problem 198: Permutation Index II

## Description:

Given a permutation which may contain repeated numbers, find its index in all the permutations of these numbers, which are ordered in lexicographical order. The index begins at 1.

和\#197相比，数据可能有重复了。

## Example:

Given the permutation `[1, 4, 2, 2]`, return `3`.

## Key points & Thoughts:

与上一题的不同之处时会有重复的数。那么，只要在发现是重复数的那一位用`rank * fact`的结果除以重复的次数`dup`再加入index就可以了。当然，每个重复数的dup都要阶乘，例如有3个2，4个8，`dup`就是`3! * 4! = 144`。`index`是所有previous排列的次数和，返回下一次`index+1`。

## Solution:

```python
class Solution:
    """
    @param A: An array of integers
    @return: A long integer
    """
    def permutationIndexII(self, A):
        # write your code here
        if A is None or len(A) == 0:
            return 0
            
        result, factor, multi_fact = 1, 1, 1
        counter = {}
        for i in range(len(A) - 1, -1, -1):
            if A[i] not in counter:
                counter[A[i]] = 0
            counter[A[i]] += 1
            multi_fact *= counter[A[i]]
            rank = 0
            for j in range(i+1, len(A)):
                if A[i] > A[j]:
                    rank += 1
            
            result += rank * factor // multi_fact
            factor *= len(A) - i
            
        return result
```

