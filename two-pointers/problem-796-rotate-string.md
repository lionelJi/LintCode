# Problem 796: Rotate String

## Description:

We are given two strings, `A` and `B`.

A _shift on `A`_ consists of taking string `A` and moving the leftmost character to the rightmost position. For example, if `A = 'abcde'`, then it will be `'bcdea'` after one shift on `A`. Return `True` if and only if `A` can become `B` after some number of shifts on `A`.

## Example:

```text
Example 1:
Input: A = 'abcde', B = 'cdeab'
Output: true

Example 2:
Input: A = 'abcde', B = 'abced'
Output: false
```

**Note:**

* `A` and `B` will have length at most `100`.

## Key Points & Thought:

可以着重看一下下面的KMP算法

## Solution:

如果只return B in A + A

A = 'a', B = 'aa' 或者 A = 'aa', B = 'a' 这种情况会报错

```python
class Solution:
    def rotateString(self, A, B):
        """
        :type A: str
        :type B: str
        :rtype: bool
        """
        return len(B) == len(A) and B in A + A
        
```

