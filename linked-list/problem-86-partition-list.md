# Problem 86: Partition List

## Description:

Given a linked list and a value _x_, partition it such that all nodes less than _x_come before nodes greater than or equal to _x_.

You should preserve the original relative order of the nodes in each of the two partitions.

## Example:

```text
Input: head = 1->4->3->2->5->2, x = 3
Output: 1->2->2->4->3->5
```

## Key points & Thoughts:

一开始的想法是新建一个头节点，把所有小于x的节点都取下来连在新的头节点上，最后把这个链表和剩下的大于x的原链表相连。

但更简单的想法是，新建两个头节点，分别存放大于和小于的所有节点，最后拼接在一起。

## Solution:

```python
class Solution:
    def partition(self, head, x):
        """
        :type head: ListNode
        :type x: int
        :rtype: ListNode
        """
        l = ListNode(0)
        g = ListNode(0)
        l_new, g_new = l, g
        
        while head:
            if head.val < x:
                l_new.next = head
                l_new = l_new.next
            else:
                g_new.next = head
                g_new = g_new.next
            head = head.next
        g_new.next = None
        l_new.next = g.next
        return l.next
```

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def partition(self, head, x):
        """
        :type head: ListNode
        :type x: int
        :rtype: ListNode
        """
        dummy = ListNode(0)
        dummy.next = head
        start = ListNode(0)
        cur = start
        
        prev = dummy
        while head:
            if head.val < x:
                prev.next = head.next
                cur.next = head
                cur = head
            else:
                prev = head
            head = head.next
        cur.next = dummy.next
        return start.next
        
```

