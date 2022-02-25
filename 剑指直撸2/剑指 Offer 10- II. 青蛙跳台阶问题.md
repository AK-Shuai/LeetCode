**题目**：
<a href="https://leetcode-cn.com/problems/qing-wa-tiao-tai-jie-wen-ti-lcof/" target="_blank">剑指 Offer 10- II. 青蛙跳台阶问题</a>


```python
class Solution:
    def numWays(self, n: int) -> int:
        a ,b = 1, 1
        for _ in range(n):
            a, b = b, a+b
        return a % 1000000007
```