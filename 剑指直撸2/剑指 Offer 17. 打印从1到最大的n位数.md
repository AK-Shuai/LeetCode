**题目**：
<a href="https://leetcode-cn.com/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/" target="_blank">剑指 Offer 17. 打印从1到最大的n位数</a>


```python
class Solution:
    def printNumbers(self, n: int) -> List[int]:
        m, h = 1, []
        for i in range(n): # 循环求出打印最大数
            m *= 10
        
        for j in range(1, m):
            h.append(j) # 有最大数循环最佳数组就可以
        return h
```

**帅解**：   
<a href="https://leetcode-cn.com/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/solution/jian-zhi-offer-17-da-yin-cong-1dao-zui-d-yrhg/" target="_blank">本人题解</a>
