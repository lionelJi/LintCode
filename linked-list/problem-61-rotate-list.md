# Problem 61: Rotate List

## Description:

Given a linked list, rotate the list to the right by _k_ places, where _k_ is non-negative.  


## Example:

**Example 1:**

```text
Input: 1->2->3->4->5->NULL, k = 2
Output: 4->5->1->2->3->NULL
Explanation:
rotate 1 steps to the right: 5->1->2->3->4->NULL
rotate 2 steps to the right: 4->5->1->2->3->NULL
```

**Example 2:**

```text
Input: 0->1->2->NULL, k = 4
Output: 2->0->1->NULL
Explanation:
rotate 1 steps to the right: 2->0->1->NULL
rotate 2 steps to the right: 1->2->0->NULL
rotate 3 steps to the right: 0->1->2->NULL
rotate 4 steps to the right: 2->0->1->NULL
```

## Key point & Thoughts:

我的想法：

需要计算整个链表长度，然后找到倒数第k个数，然后将其断开。

计算链表长度时就可以把最后一个节点和头节点相连。

testcase里有k比链表长度大很多的情况，所以要用k对链表长度取余数。

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
    @param head: the List
    @param k: rotate to the right k places
    @return: the list after rotation
    """
    def rotateRight(self, head, k):
        # write your code here
        
        len, count = 1, head
        if not head:
            return head
        while count.next:
            len += 1
            count = count.next
        count.next = head
        k = k % len
        # Find new head position
        prev = head
        for _ in range(2*len - k - 1):
            prev = prev.next
        new_head = prev.next
        prev.next = None
    
        return new_head
```

