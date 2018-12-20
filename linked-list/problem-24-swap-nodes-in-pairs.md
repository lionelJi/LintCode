---
description: 简易版的reverse nodes in k-group，其实是一个意思。
---

# Problem 24: Swap Nodes in Pairs

## Description:

Given a linked list, swap every two adjacent nodes and return its head.

## Example:

```text
Given 1->2->3->4, you should return the list as 2->1->4->3.
```

**Note:**

* Your algorithm should use only constant extra space.
* You may **not** modify the values in the list's nodes, only nodes itself may be changed.

## Key points & Thoughts:

用之前学的一句话连续赋值逆序链表的方法试一下，思路和\#25题差不多。

是不是有更简单的做法呢。

leetcode上更快的解法：就是一直交换cur和cur.next，想法很直接。

## Solution:

My Solution:

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
    @return: a ListNode
    """
    def swapPairs(self, head):
        # write your code here
        dummy = ListNode(0)
        dummy.next = head
        
        head = dummy
        while head:
            head = self.reverse(head)
            
        return dummy.next
            
    def reverse(self, head):
        count = head.next
        for _ in range(2):
            if not count:
                return None
            count = count.next
        
        cur = new_head = head.next
        head.next = count
        while cur != count:
            head.next, cur.next, cur  = cur, head.next, cur.next
            
        return new_head
        
```

leetcode：

```python
class Solution:
    def swapPairs(self, a):
        if not a or not a.next:
            return a
        head = a.next
        curr = a
        prev = None
        while curr and curr.next:
            temp = curr.next
            curr.next = curr.next.next
            temp.next = curr
            if prev:
                prev.next = temp
            prev = curr
            curr = curr.next
        return head
```

