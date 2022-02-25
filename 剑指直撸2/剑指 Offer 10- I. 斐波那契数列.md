**题目**：
<a href="https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof/" target="_blank">剑指 Offer 10- I. 斐波那契数列</a>


```python
class Solution:
    def fib(self, n: int) -> int:
        a ,b = 0, 1
        for _ in range(n):
            a, b = b, a+b
        return a % 1000000007
```