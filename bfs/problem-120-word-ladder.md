# Problem 120: Word Ladder

## Description:

Given two words \(_beginWord_ and _endWord_\), and a dictionary's word list, find the length of shortest transformation sequence from _beginWord_ to _endWord_, such that:

1. Only one letter can be changed at a time.
2. Each transformed word must exist in the word list. Note that _beginWord_ is _not_ a transformed word.

**Note:**

* Return 0 if there is no such transformation sequence.
* All words have the same length.
* All words contain only lowercase alphabetic characters.
* You may assume no duplicates in the word list.
* You may assume _beginWord_ and _endWord_ are non-empty and are not the same.

## Example:

**Example 1:**

```text
Input:
beginWord = "hit",
endWord = "cog",
wordList = ["hot","dot","dog","lot","log","cog"]

Output: 5

Explanation: As one shortest transformation is "hit" -> "hot" -> "dot" -> "dog" -> "cog",
return its length 5.
```

**Example 2:**

```text
Input:
beginWord = "hit"
endWord = "cog"
wordList = ["hot","dot","dog","lot","log"]

Output: 0

Explanation: The endWord "cog" is not in wordList, therefore no possible transformation.
```

## Key points & Thoughts:

使用基本的bfs，建立一个deque，把\(word, path\_length\)格式的tuple宽度优先存进去。

注意删掉所有遍历过的word，否则会反复横跳造成重复。

在leetcode上提交的时候因为给的参数wordList 的类型不是set而是list，导致一个很大的testcase在wordList里查找时超时，对于这种查找内容的东西，还是最好把list先化成set节省时间。

## Solution:

```python
from collections import deque

class Solution:
    def ladderLength(self, beginWord, endWord, wordList):
        """
        :type beginWord: str
        :type endWord: str
        :type wordList: List[str]
        :rtype: int
        """
        wordList = set(wordList)
        q = deque([(beginWord, 1)])
        if beginWord in wordList:
            wordList.remove(beginWord)
        if endWord not in wordList:
            return 0
        
        while q:
            curWord, curLen = q.popleft()
            if curWord == endWord:
                return curLen
            for i in range(len(curWord)):
                left, right = curWord[:i], curWord[i+1:]
                for ch in 'abcdefghijklmnopqrstuvwxyz':
                    if ch == curWord[i]:
                        continue
                    new_word = left + ch + right
                    if new_word in wordList:
                        q.append([new_word, curLen+1])
                        wordList.remove(new_word)
                        
        return 0
        
```

