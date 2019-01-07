# Problem 148: Sort List

## Description:

Sort a linked list in _O_\(_n_ log _n_\) time using constant space complexity.

## Example:

**Example 1:**

```text
Input: 4->2->1->3
Output: 1->2->3->4
```

**Example 2:**

```text
Input: -1->5->3->4->0
Output: -1->0->3->4->5
```

## Key point & Thoughts:

回顾一下归并排序的写法：（分治思想）

```python
def MergeSort(nums):
    if len(nums) <= 1:
        return nums
    mid = len(nums) // 2
    left = MergeSort(nums[:mid])
    right = MergeSort(nums[mid:])
    return Merge(left, right)


def Merge(left, right):
    r, l = 0, 0
    result = []
    while l < len(left) and r < len(right):
        if left[l] < right[r]:
            result.append(left[l])
            l += 1
        else:
            result.append(right[r])
            r += 1
    result += list(left[l:])
    result += list(right[r:])
    return result
```

链表有什么不一样？ 

* 没法直接找到middle position，需要用快慢指针实现 while fast and fast.next:
* slow.next需要置空为None。
* 不用创造新的一个链表挨个存下来，直接穿针引线就可以。
* 把两个链表中第一个节点值较小的作为返回值，把另一个链表加到这上面就可以了。

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
    @return: You should return the head of the sorted linked list, using constant space complexity.
    """
    def sortList(self, head):
        # write your code here
        if not head or not head.next:
            return head
        
        # devide into two parts
        slow, fast = head, head.next
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
        second = slow.next
        slow.next = None
        
        l = self.sortList(head)
        r = self.sortList(second)
        return self.merge(l, r)
        
    def merge(self, l, r):
        if not l or not r:
            return l or r
        if l.val > r.val:
            l, r = r, l
        # get the return node 'head'
        head = prev = l
        # now head is minimum value
        l = l.next
        while l and r:
            if l.val < r.val:
                l = l.next
            else:
                n = prev.next
                prev.next = r
                temp = r.next
                r.next = n
                r = temp
            prev = prev.next
        prev.next = l or r
        return head
        
```



