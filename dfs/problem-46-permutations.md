# Problem 46: Permutations

## Description:

Given a collection of **distinct** integers, return all possible permutations.

## Example:

```text
Input: [1,2,3]
Output:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

## Solution:

```python
class Solution:
    def permute(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        results = []
        self.helper(nums, results, [], set())
        return results
        
    def helper(self, nums, results, permutation, visited):
        if len(permutation) == len(nums):
            results.append(permutation[:])
            return
        for i in nums:
            if i in visited:
                continue
            visited.add(i)
            permutation.append(i)
            self.helper(nums, results, permutation, visited)
            permutation.pop()
            visited.remove(i)
            
        
```

