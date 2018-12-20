# Problem 511\(Lint\): Swap Two Nodes in Linked List

## Description:

Given a linked list and two values v1 and v2. Swap the two nodes in the linked list with values v1 and v2. It's guaranteed there is no duplicate values in the linked list. If v1 or v2 does not exist in the given linked list, do nothing.

## Example:

Given `1->2->3->4->null` and v1 = `2`, v2 = `4`.

Return `1->4->3->2->null`.

## Key points & Solution:

首先要找到两个val对应的node，和两个previous的node，在交换两个node的next和两个previous的next时，发现连续赋值真的好棒啊，因为赋值没有先后顺序，所以一句话就能实现出来。

其实找两个node时还可以简化，只需要一个prev和一个cur往前走，如果val等于v1或者v2就把对应的prev1和cur1赋值给当前就行，不需要调用程序，会就行先不改了。

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
    @param v1: An integer
    @param v2: An integer
    @return: a new head of singly-linked list
    """
    def swapNodes(self, head, v1, v2):
        # write your code here
        dummy = ListNode(0)
        dummy.next = head
        
        prev1 = prev2 = dummy
        cur1 = cur2 = dummy.next
        prev1, cur1 = self.get_Node(prev1, cur1, v1)
        prev2, cur2 = self.get_Node(prev2, cur2, v2)
        
        if not cur1 or not cur2:
            return dummy.next
        
        prev1.next, prev2.next = cur2, cur1
        cur1.next, cur2.next = cur2.next, cur1.next
        return dummy.next
    
    def get_Node(self, prev, cur, value):
        while cur:
            if cur.val == value:
                break
            prev = prev.next
            cur = cur.next
        return prev, cur
        

```

