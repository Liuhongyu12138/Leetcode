### leetcode19 删除链表的倒数第N个节点

给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。

示例：

给定一个链表: **1->2->3->4->5**, 和 **n = 2**.

当删除了倒数第二个节点后，链表变为 **1->2->3->5**.
说明：

给定的 n 保证是有效的。

进阶：

你能尝试使用一趟扫描实现吗？

题解

~~~python
"""
	双指针简单题，两个指针扫描一趟，p先走n步，p和q同时走，当p走到结尾节点时，q走到距离p n个节点，也就是倒数第n+1个节点，令p的next指向p.next.next就可以删除第n个节点了。因为可能删除头节点，所以要维护一个虚拟头节点。
"""

class Solution:
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        dummy = ListNode(-1)
        dummy.next = head
        p, q = dummy, dummy
        while n:
            p = p.next
            n -= 1
        while p.next:
            p = p.next
            q = q.next
        q.next = q.next.next
        return dummy.next
~~~

