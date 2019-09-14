给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。

**你不能只是单纯的改变节点内部的值**，而是需要实际的进行节点交换。

 

示例:

~~~
给定 1->2->3->4, 你应该返回 2->1->4->3.
~~~



题解1

~~~python
"""
	迭代的做法：很好想，首先头节点要改变，所以需要一个dummy。
	让p永远指向待处理节点的前一个节点。
	p=dummy，只要dummy.next and dummy.next.next, 需要交换，分别赋值给a和b。
	然后就是把当前这个区间调换位置，p.next = b, a.next = b.next b.next = a p=a顺序不能乱！
"""
class Solution:
    def swapPairs(self, head: ListNode) -> ListNode:
        dummy = ListNode(-1)
        dummy.next = head
        
        p = dummy
        while p.next and p.next.next:
            a, b = p.next, p.next.next
            p.next = b
            a.next = b.next
            b.next = a
            p = a
        
        return dummy.next
~~~



题解2

~~~python
"""
	递归大法好！递归的本质：需要思考最小操作。
	三个点：	1.返回值：交换完成的子链表。（能不能直接返回题目需要的结果：能）
				   2.调用单元（最小操作）：设需要交换的两个点为head和next，head连接后面交换
				   完成的子链表，next连接head，完成交换。
				   3.终止条件，head为空或者next为空，无法继续交换。
"""

class Solution:
    def swapPairs(self, head: ListNode) -> ListNode:
        if not head or not head.next:
            return head
        
        res = head.next
        head.next = self.swapPairs(head.next.next)
        res.next = head
        
        return res
~~~

