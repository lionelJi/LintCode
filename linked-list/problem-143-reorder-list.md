# Problem 143: Reorder List

## Description:

Given a singly linked list _L_: _L_0→_L_1→…→_Ln_-1→_L_n,  
reorder it to: _L_0→_Ln_→_L_1→_Ln_-1→_L_2→_Ln_-2→…

You may **not** modify the values in the list's nodes, only nodes itself may be changed.

## Example:

**Example 1:**

```text
Given 1->2->3->4, reorder it to 1->4->2->3.
```

**Example 2:**

```text
Given 1->2->3->4->5, reorder it to 1->5->2->4->3.
```

## Key points & Thoughts:

第一时间的想法是，可以用快慢指针找到中间的节点，然后头一个中间一个，挨个串联起来。

少想了一个东西，如果given是 1-&gt;2-&gt;3-&gt;4-&gt;5-&gt;6-&gt;None，结果应该是 1-&gt;6-&gt;2-&gt;5-&gt;3-&gt;4-&gt;None, 所以找到中间节点之后是不是还要把之后的链表逆序，再穿插，感觉有点麻烦。可能用递归会好一些。

找到点感觉了。

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
    @param head: The head of linked list.
    @return: nothing
    """
    def reorderList(self, head):
        # write your code here
        dummy = ListNode(0)
        dummy.next = head
        slow = fast = dummy
        while fast:
            if fast.next and slow.next:
                slow = slow.next
                fast = fast.next.next
            else:
                break
        # Reverse all after mid node.
        cur = slow.next
        slow.next = None
        while cur:
            slow.next, cur.next, cur = cur, slow.next, cur.next
            
        cur1, cur2 = dummy.next, slow.next
        while cur1 and cur1 != slow:
            cur1.next, cur2.next, slow.next, cur1, cur2 = cur2, cur1.next, \
                         cur2.next, cur1.next, cur2.next
        return head
```

