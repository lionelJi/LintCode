# Problem 212: Word Search II

## Description:

Given a 2D board and a list of words from the dictionary, find all words in the board.

Each word must be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

## Example:

```text
Input: 
words = ["oath","pea","eat","rain"] and board =
[
  ['o','a','a','n'],
  ['e','t','a','e'],
  ['i','h','k','r'],
  ['i','f','l','v']
]

Output: ["eat","oath"]
```

## Key points & Thoughts:

看上去像是一直调用word search 1就可以，不知道对不对，写写看。

写完了，道理是这么个道理，但是极端的testcase会超时，当检查 'aaaaaaab' 不在board里的时候，还是会检查 'aaaaaaac'， 这会浪费很多时间。

可不可以只要找不到的就加到一个set中。

题目中提到了使用Trie.

## Solution:

leetcode上的用trie实现的方法，学习一下，有点酷：



```text
    def buildTrie(self, words):
        trie = {}
        for word in words:
            cur = trie
            for char in word:
                cur = cur.setdefault(char, {})
            cur['word'] = word
        return trie


s = Solution()
trie = s.buildTrie({"dog", "dad", "dgdg", "can", "again"})

print(trie)
```

建立一个这样的trie可以把这几个单词存成这样的字典格式：

{'a': {'g': {'a': {'i': {'n': {'word': 'again'}}}}}, 'd': {'o': {'g': {'word': 'dog'}}, 'a': {'d': {'word': 'dad'}}, 'g': {'d': {'g': {'word': 'dgdg'}}}}, 'c': {'a': {'n': {'word': 'can'}}}}

一层一层的。

访问的时候可以一层一层剥开，如果访问到key是 'word' 了，说明找到了这个单词。

这个解法还运用了把用过的字符替换成‘\#‘的方法防止回头，也可以借鉴一下。

```python
class Solution(object):
    def findWords(self, board, words):
        """
        :type board: List[List[str]]
        :type words: List[str]
        :rtype: List[str]
        """
        # Backtracking + Trie
        trie = self.buildTrie(words)
        self.res = []
        for i in range(len(board)):
            for j in range(len(board[0])):
                self.dfs(board, i, j, trie)
        return self.res
    
    def dfs(self, board, i, j, trie):
        # found one
        if trie.get('word'):
            self.res.append(trie['word'])
            # de-duplicate
            trie['word'] = None
        if i<0 or i>=len(board) or j<0 or j>=len(board[0]) or board[i][j] not in trie:
            return
        c, board[i][j] = board[i][j], '#'
        self.dfs(board, i-1, j, trie[c])
        self.dfs(board, i+1, j, trie[c])
        self.dfs(board, i, j-1, trie[c])
        self.dfs(board, i, j+1, trie[c])
        board[i][j] = c
    
    def buildTrie(self, words):
        trie = {}
        for word in words:
            cur = trie
            for char in word:
                cur = cur.setdefault(char, {})
            cur['word'] = word
        return trie
```



 



看到了一个把所有前缀都存下来，然后遍历棋盘上所有字符，每个为开始进行dfs的方法，照着写了一遍，有点巧妙，但是性能可能不是那么好。

每次都看现在新链接的字符串cur在不在前缀集合里，不在的话就直接返回。

```python
class Solution:
    """
    @param board: A list of lists of character
    @param words: A list of string
    @return: A list of string
    """
    directions = [[0,1], [1,0], [-1,0], [0,-1]]

    def wordSearchII(self, board, words):

        result = []

        if not board or not board[0] or not words:
            return result

        # dic_prefix init
        dic_prefix = set()
        for w in words:
            for i in range(len(w)):
                dic_prefix.add(w[:i+1])

        # loop
        row, col = len(board), len(board[0])
        for r in range(len(board)):
            for c in range(len(board[0])):
                self.dfs(r, c, board, words, board[r][c], dic_prefix, set(), result)
        return result

    def dfs(self, row, col, board, words, cur, dic_prefix, visited, result):
        visited.add((row, col))
        if cur not in dic_prefix:
            return
        if cur in words and cur not in result:
            result.append(cur)
        for (row_d, col_d) in self.directions:
            new_r, new_c = row + row_d, col + col_d
            if (0 <= new_r < len(board) and 0 <= new_c < len(board[0])) and (new_r, new_c) not in visited:
                self.dfs(new_r, new_c, board, words, cur + board[new_r][new_c], dic_prefix, visited, result)
                visited.remove((new_r,new_c))
```

