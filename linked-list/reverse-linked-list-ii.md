# Problem 92: Reverse Linked List II

## Description:

Reverse a linked list from position _m_ to _n_. Do it in one-pass.

**Note:** 1 ≤ _m_ ≤ _n_ ≤ length of list.

## Example:

```text
Input: 1->2->3->4->5->NULL, m = 2, n = 4
Output: 1->4->3->2->5->NULL
```

## Key points & Thoughts:

学到了一个东西：

在python中是可以使用连续赋值的方式来一次为多个变量进行赋值的，比如：

a = b = c = 1 a, b, c = 1, 1, 1  这些都可以完成变量的赋值，但是就有一个问题了，比如：

a = 3 

a, b = 1, a 

### **如果按照正常的思维逻辑，先进行a = 1，在进行b = a，最后b应该等于1，但是这里b应该等于3，因为在连续赋值语句中等式右边其实都是局部变量，而不是真正的变量值本身，比如，上面例子中右边的a，在python解析的时候，只是把变量a的指向的变量3赋给b，而不是a=1之后a的结果，这一点刚开始学python的人可能容易误解，再举一个Leetcode里链表的例子理解就更深了。**

\*\*\*\*

**意思是： 连续赋值时把右边值原始的值赋给左边，而不会因为在前面改过了就赋值更高后的。**

假如要对一个链表进行翻转，就比如把1—&gt;2-&gt;3-&gt;4转化为4-&gt;3-&gt;2-&gt;1 1 对于这个问题很简单，只要反转指针就可以了，假如链表结构为：

class ListNode: def **init**\(self, x\): self.val = x self.next = None 1 2 3 4 我们可以用很简单的三行代码完成这个过程：

```python
def reverseList(self, head): 
    L = ListNode(float("-inf")) 
    while head: 
        L.next, head.next, head = head, L.next, head.next
    return L.next
```

我的方法也是用到九章讲过的，前面留一个节点好像warder一样。

leetcode上有用栈实现的方法，看起来很好懂。



## Solution:



我的做法：

```python
class Solution:
    def reverseBetween(self, head, m, n):
        """
        :type head: ListNode
        :type m: int
        :type n: int
        :rtype: ListNode
        """
        dummy = ListNode(0)
        dummy.next = head
        
        k = m
        warder = dummy
        # warder 是前面的节点， 
        while head and k>=2:
            warder = head
            head = head.next
            k -= 1
            
        prev = None       
        for _ in range(n - m + 1):
            temp = head.next
            head.next = prev
            prev = head
            head = temp
                        
        warder.next.next = head
        warder.next = prev
        return dummy.next
```

栈：

```python
class Solution(object):
    def reverseBetween(self, head, m, n):
        count, stack = 1, []
        dummy = prev = ListNode(0)
        prev.next = node = head
        while node and count < m:
            node = node.next
            prev = prev.next
            count += 1
        while node and count <= n:
            stack.append(node)
            node = node.next
            count += 1
        while stack:
            prev.next = stack.pop()
            prev = prev.next
        prev.next = node
        return dummy.next
```

