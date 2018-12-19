# Problem 21: Merge Two Sorted Lists

## Description:

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

## Example:

```text
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```

## Key points & Thoughts:

用归并排序的思路就可以。

## Solution:

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    """
    @param l1: ListNode l1 is the head of the linked list
    @param l2: ListNode l2 is the head of the linked list
    @return: ListNode head of linked list
    """
    def mergeTwoLists(self, l1, l2):
        # write your code here
        result = ListNode(0)
        cur_1, cur_2, r = l1, l2, result
        while cur_1 and cur_2:
            if cur_1.val <= cur_2.val:
                r.next = cur_1
                while cur_1 and cur_1.val <= cur_2.val:
                    r = cur_1
                    cur_1 = cur_1.next
            else:
                r.next = cur_2
                while cur_2 and cur_2.val <= cur_1.val:
                    r = cur_2
                    cur_2 = cur_2.next
        
        if cur_1:
            r.next = cur_1
        if cur_2:
            r.next = cur_2
        
        return result.next
```

速度最快的，在两个列表中穿梭的版本

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def mergeTwoLists(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        if l1==None:
            return l2
        if l2==None:
            return l1
        if l1.val>l2.val:
            l1,l2=l2,l1
            
        p1,p2=l1,l2
        t=p1
        p1=p1.next
        while p1:
            if p1.val>p2.val:
                t.next=p2
                p2=p1
                t=t.next
                p1=t.next
            else:
                t=p1
                p1=p1.next
        t.next=p2
        
        return l1
                
```

