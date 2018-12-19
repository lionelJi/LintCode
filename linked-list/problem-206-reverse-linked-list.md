# Problem 206: Reverse Linked List

## Description:

Reverse a singly linked list.

## Example:

```text
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
```

## Key points & Thoughts:

有iteratively 和 recursively两种方法，都写一下。

## Solution:

```python
class Solution:
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        prev = None
        while head != None:
            temp = head.next
            head.next = prev
            prev = head
            head = temp
        return prev
```

```python
class Solution:
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        # not head.next 是要返回一开始最末端的结点，也就是新的头节点
        # not head 是处理输入是null这样的情况。
        if not head or not head.next:
            return head
        new_head = self.reverseList(head.next)
        head.next.next = head
        head.next = None
        return new_head
```

