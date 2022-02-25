**题目**：
<a href="https://leetcode-cn.com/problems/er-jin-zhi-zhong-1de-ge-shu-lcof/" target="_blank">剑指 Offer 15. 二进制中1的个数</a>


```python
class Solution:
    def hammingWeight(self, n: int) -> int:
        res = 0
        while n:
            res += n & 1 # 取出二进制最右位数字加上
            n >>= 1 # 二进制右移一位
        return res
```
