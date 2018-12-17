---
description: 'Given a list of numbers, return all possible permutations.'
---

# Problem 15: Permutation

## Example:

For nums = `[1,2,3]`, the permutations are:

```text
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

#### Challenge

Do it without recursion.

#### Notice

You can assume that there is no duplicate numbers in the list.

## Solution:

```python
class Solution:
    """
    @param: nums: A list of integers.
    @return: A list of permutations.
    """
    def permute(self, nums):
        # write your code here
        results = []
        self.dfs(nums, set(), [], results)
        return results
        
    def dfs(self, nums, visited, permutation, results):
        if len(permutation) == len(nums):
            results.append(permutation[:])
            return
        for i in range(len(nums)):
            if nums[i] in visited:
                continue
            visited.add(nums[i])
            permutation.append(nums[i])
            self.dfs(nums, visited, permutation, results)
            permutation.pop()
            visited.remove(nums[i])
```

