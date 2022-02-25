**题目**：
<a href="https://leetcode-cn.com/problems/shan-chu-lian-biao-de-jie-dian-lcof/" target="_blank">剑指 Offer 18. 删除链表的节点</a>


```python
class Solution:
    def deleteNode(self, head: ListNode, val: int) -> ListNode:
        head = ListNode(head)
        if head.val == val: return head.next # 如果头节点是的话直接返回

        pre, cur = head, head.next # 赋值第一部

        while cur and cur.val != val:
            pre, cur = cur, cur.next
        if cur: pre.next = cur.next
        return head
```

**帅解**：  
赋值第一步：  
<div align=center><img src="https://raw.githubusercontent.com/AK-Shuai/IMG/main/LeetCode/deleteNode_01.png" width="400"></div>



