### leetcode 25 k个一组翻转链表

给你一个链表，每 k 个节点一组进行翻转，请你返回翻转后的链表。

k 是一个正整数，它的值小于或等于链表的长度。

如果节点总数不是 k 的整数倍，那么请将最后剩余的节点保持原有顺序。

示例 :

给定这个链表：1->2->3->4->5

当 k = 2 时，应当返回: 2->1->4->3->5

当 k = 3 时，应当返回: 3->2->1->4->5

说明 :

你的算法只能使用常数的额外空间。
你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

题解

~~~python
"""
递归的方法，先数出k个节点，如果不够，直接return不翻转，如果够，拿出来做翻转，再连上后头节点递归的结果。
"""
class Solution:
    def reverseKGroup(self, head: ListNode, k: int) -> ListNode:
        p = head
        i = 1
        while p and i < k:
            p = p.next
            i += 1
        
        if not p:
            return head
        
        temp = p.next
        p.next = None
        
        newHead = self.reverse(head)
        newTemp = self.reverseKGroup(temp, k)
        head.next = newTemp  # head是翻转后的尾节点，正好连上新的头节点
        
        return newHead  # 返回的就是新的头节点
    
    def reverse(self, head):
        if not head or not head.next:
            return head
        
        res = self.reverse(head.next)
        head.next.next = head
        head.next = None
        return res
   
  	def reverse2(self, head):
  			pre, cur = None, head
        while cur:
          	next = cur.next
            cur.next = pre
            pre = cur
            cur = next
        return pre
~~~

