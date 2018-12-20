# Problem 297: Serialize and Deserialize Binary Tree

## Description:

Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

## Example:

```text
You may serialize the following tree:

    1
   / \
  2   3
     / \
    4   5

as "[1,2,3,null,null,4,5]"
```

## Key points and Thoughts:

我的做法：

可以用bfs把树状结构化成列表，记得因为叶子结点的左子树右子树虽然为空，但也会加进列表中，所以要在最后把列表后面的None值都删掉。

在从列表生成树状结构的时候，用一个queue存已经建立好的节点，用isLeftChild变量和一个queue的下标index确定是哪个节点的孩子。

## Solution:

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Codec:

    def serialize(self, root):
        """Encodes a tree to a single string.
        
        :type root: TreeNode
        :rtype: str
        """
        res = []
        def helper(root):
            if not root:
                res.append("#")
            else:
                res.append(str(root.val))
                helper(root.left)
                helper(root.right)
        helper(root)
        return " ".join(res)
        

    def deserialize(self, data):
        """Decodes your encoded data to tree.
        
        :type data: str
        :rtype: TreeNode
        """
        def helper():
            val = next(vals)
            if val != "#":
                res = TreeNode(int(val))
                res.left = helper()
                res.right = helper()
                return res
        
        vals = iter(data.split())
        return helper()

# Your Codec object will be instantiated and called as such:
# codec = Codec()
# codec.deserialize(codec.serialize(root))
```

```python
"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left, self.right = None, None
"""


class Solution:
    """
    @param root: An object of TreeNode, denote the root of the binary tree.
    This method will be invoked first, you should design your own algorithm 
    to serialize a binary tree which denote by a root node to a string which
    can be easily deserialized by your own "deserialize" method later.
    """
    def serialize(self, root):
        # write your code here
        data = []
        queue = [root]
        while queue:
            cur = queue.pop(0)
            cur_val = None if not cur else cur.val
            data = data + [cur_val]
            if cur:
                queue = queue + [cur.left] + [cur.right]
        while data and not data[-1]:
            data.pop()
        return data

    """
    @param data: A string serialized by your serialize method.
    This method will be invoked second, the argument data is what exactly
    you serialized at method "serialize", that means the data is not given by
    system, it's given by your own serialize method. So the format of data is
    designed by yourself, and deserialize it here as you serialize it in 
    "serialize" method.
    """

    def deserialize(self, data):
        if not data:
            return None
        root = TreeNode(data[0])
        queue, index, isLeftChild = [root], 0, True
        for i in range(1, len(data)):
            if data[i] is not None:
                node = TreeNode(data[i])
                if isLeftChild:
                    queue[index].left = node
                else:
                    queue[index].right = node
                queue.append(node)
            if not isLeftChild:
                index += 1
            isLeftChild = not isLeftChild
        return root

```

