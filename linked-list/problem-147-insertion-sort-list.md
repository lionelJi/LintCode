# Problem 147: Insertion Sort List

## Description:



Sort a linked list using insertion sort.

![](https://upload.wikimedia.org/wikipedia/commons/0/0f/Insertion-sort-example-300px.gif)  
A graphical example of insertion sort. The partial sorted list \(black\) initially contains only the first element in the list.  
With each iteration one element \(red\) is removed from the input data and inserted in-place into the sorted list  
 

**Algorithm of Insertion Sort:**

1. Insertion sort iterates, consuming one input element each repetition, and growing a sorted output list.
2. At each iteration, insertion sort removes one element from the input data, finds the location it belongs within the sorted list, and inserts it there.
3. It repeats until no input elements remain.

## Solution:

这道题在插入位置上可以节省一部分时间：

* start如果比要插入的数小，继续往后查找就好
* start如果比插入的数大，start回到dummy，从头找插入的位置

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def insertionSortList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        start = dummy = ListNode(0)
        cur = dummy.next = head
        
        while cur and cur.next:
            if cur.val < cur.next.val:
                cur = cur.next
                continue
            if start.next.val > cur.next.val:
                start = dummy
            while start.next.val < cur.next.val:
                start = start.next
            temp = cur.next
            cur.next = temp.next
            temp.next = start.next
            start.next = temp
        
        return dummy.next
```

