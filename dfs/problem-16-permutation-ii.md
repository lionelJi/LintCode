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

所以需要加上判断，如果一个数和前面的数相等而且前面的数用过了，就continue跳过这个数。

“前面的数用过了“， 可以使用一个map或者list存储很多True or False。

## Solution:

```python

```

##  

