# Problem 10: String Permutation II

## Description:

Given a string, find all permutations of it without duplicates.

## Example:

Given `"abb"`, return `["abb", "bab", "bba"]`.

Given `"aabb"`, return `["aabb", "abab", "baba", "bbaa", "abba", "baab"]`.  


## Key points and Thought:

和第16题permutation去重复思路完全一样。

对字符串‘bab‘进行sorted会返回一个列表\['a', 'b', 'b'\]，而不是字符串.

去重复的策略完全一样：

```python
if i != 0 and str[i] == str[i-1] and not visited[i-1]:
```

因为传递的参数permutation是一个字符串，所以传递时可以用 permutation + str\[i\]， 而不用先append到list中再pop出来。这种传值也导致把每个permutation加入到result中的时候不需要deep copy。

## Solution:

```python
class Solution:
    """
    @param str: A string
    @return: all permutations
    """
    def stringPermutation2(self, str):
        # write your code here
        result = []
        visited = [False for i in range(len(str))]
        self.helper(sorted(str), result, '', visited)
        return result
        
    def helper(self, str, result, permutation, visited):
        if len(permutation) == len(str):
            result.append(permutation)
            return
        for i in range(len(str)):
            if visited[i]:
                continue
            if i != 0 and str[i] == str[i-1] and not visited[i-1]:
                continue
            visited[i] = True
            self.helper(str, result, permutation + str[i], visited)
            visited[i] = False
            
```



