**题目**：
<a href="https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/" target="_blank">剑指 Offer 22. 链表中倒数第k个节点</a>


```python
class Solution:
    def getKthFromEnd(self, head: ListNode, k: int) -> ListNode:
        head = ListNode(head)

        per, cur = head, head # 获取两个指针
        for _ in range(k): # 一个指针先走k步
            per = per.next

        while per: # 俩指针同时走，先走k步指针如果走完，后走指针就到达了倒数位置，输出即可
           per, cur = per.next, cur.next
        return head
```
