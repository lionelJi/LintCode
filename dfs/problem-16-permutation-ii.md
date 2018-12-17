---
description: Medium & Basic.
---

# Problem 16: Permutation II

## Description:

Given a list of numbers with duplicate number in it. Find all **unique** permutations.

## Example:

For numbers `[1,2,2]` the unique permutations are:

```text
[
  [1,2,2],
  [2,1,2],
  [2,2,1]
]
```

## Key points & Thought:

需要去重复，对于\[1, 2, 2\]来说，先用第一个2和先用第二个2，会产生两个\[1, 2, 2\]导致重复。

所以需要加上判断，如果一个数和前面的数相等而且前面的数没有用过，就continue跳过这个数。

```python
if i > 0 and nums[i] == nums[i-1] and not visited[i-1]:
```

* 所以，对于\[1, 2, 2\]来说，第二个2在第一个2被visited之前，不能加进去，第二个2必须排在第一个2之后，这样就可以去掉重复

“前面的数用过了“， 可以使用一个map或者list存储很多True or False。

```python
visited = [False for i in range(len(nums))]
```

* 因为要比较和前面的数是否相等，所以需要对原list进行排序。

## Solution:

```python
class Solution:
    """
    @param: :  A list of integers
    @return: A list of unique permutations
    """

    def permuteUnique(self, nums):
        # write your code here
        results = []
        visited = [False for i in range(len(nums))]
        self.dfs(sorted(nums), results, [], visited)
        return results

    def dfs(self, nums, results, permutation, visited):
        if len(permutation) == len(nums):
            results.append(permutation[:])
            return
        
        for i in range(len(nums)):
            if visited[i]:
                continue
            if i > 0 and nums[i] == nums[i-1] and not visited[i-1]:
                continue
            permutation.append(nums[i])
            visited[i] = True
            self.dfs(nums, results, permutation, visited)
            visited[i] = False
            permutation.pop()

```

