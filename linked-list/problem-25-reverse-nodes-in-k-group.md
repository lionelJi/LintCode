---
description: 这道题心态做炸了，链表的题以为自己能想清楚，还是要多做几道，别急躁了。
---

# Problem 25: Reverse Nodes in k-Group

## Description:

Given a linked list, reverse the nodes of a linked list _k_ at a time and return its modified list.

_k_ is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of _k_ then left-out nodes in the end should remain as it is.

## Example:

**Example:**

Given this linked list: `1->2->3->4->5`

For _k_ = 2, you should return: `2->1->4->3->5`

For _k_ = 3, you should return: `3->2->1->4->5`

**Note:**

* Only constant extra memory is allowed.
* You may not alter the values in the list's nodes, only nodes itself may be changed.

## Key points & Thoughts:

一团乱麻

理清楚思路：

逆序子函数里应该怎么实现：

传入这一组的前面一个节点head，用cur = head.next往后遍历k步看有没有，然后从cur开始逆序k步，这之后cur停在下一组的第一个元素上，prev停在这一组的最后一个元素上，可以当下一组的head：

对于testcase 1-&gt;2-&gt;3-&gt;4-&gt;5-&gt;6-&gt;7-&gt;None, k=3

第一组head应该在1之前： head -&gt; 1 -&gt; 2 -&gt; 3 -&gt; ...

 cur = head.next       prev = None         

for \_ in range\(k\): temp = cur.next  cur.next = prev  prev = cur  cur = temp

k=3次之后，cur位置是4，prev位置是3

这时候1，2，3的状态是   None &lt;- 1 &lt;- 2 &lt;- 3  4 

head.next仍然是1

逆序要想变成 head -&gt; 3 -&gt; 2 -&gt; 1 -&gt; 4 ....后需要几个步骤： 

1. 存下来下一组的头节点，即为这一组逆转后的最后一个节点，即为这一组没逆转后的第一个节点1

2. 让这一组逆转后的最后一个节点（逆转前第一个结点1）指向下一组第一个节点（结点4，现在由cur指向）

3.这一组的头从旧的第一个节点1转为指向新的第一个节点，由prev指向的3

把新的头节点1返回，作为head开始下一组 ... -&gt; 1 -&gt; 4 -&gt; 5 -&gt; 6 -&gt; 7 -&gt; None 的头节点

## Solution:

```python
"""
Definition of ListNode
class ListNode(object):
    def __init__(self, val, next=None):
        self.val = val
        self.next = next
"""

class Solution:
    """
    @param head: a ListNode
    @param k: An integer
    @return: a ListNode
    """
    def reverseKGroup(self, head, k):
        # write your code here
        dummy = ListNode(0)
        dummy.next = head
        
        head = dummy
        while head != None:
            # head 是每k个节点前面的一个节点，第一个head是dummy
            # 必须标记着每k个节点前面的那个节点，在逆转完k个之后把它和新的list连接上
            head = self.reverse(head, k)
            
        return dummy.next
            
        
    def reverse(self, head, k):
        cur = head.next
        for _ in range(k):
            # 从这一组的第一个元素开始检查了k步
            if not cur:
                return None
            cur = cur.next
            
        prev = None
        cur = head.next
        
        for _ in range(k):
            temp = cur.next
            cur.next = prev
            prev = cur
            cur = temp
            
        # head 置为每一组的前面一个结点
        # 下一组的前一个结点是这一组的第一个结点了：
        #  k = 3
        # head -> 1 -> 2 -> 3 -> 4
        # cur 现在在4，prev现在在3
        # head -> 3 -> 2 -> 1 -> 4    new_head = head.next = 1
        # 下一组是 new_head -> 4 -> ....
        new_head = head.next
        # 让 1 接上 4:
        # head.next:(1).next = 4
        head.next.next = cur
        head.next = prev
        
        return new_head
        
        

 

            
```

