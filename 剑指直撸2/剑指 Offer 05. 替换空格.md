**题目**：
<a href="https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/" target="_blank">剑指 Offer 05. 替换空格</a>


```python
'''数组解，如果不能使用新数组就只能用双指针'''
class Solution:
    def replaceSpace(self, s: str) -> str:
        res = []
        for a in s:
            if a == ' ':
                res.append('%20')
            else:
                res.append(a)
        return "".join(res)
```

1. 先统计空格，每有一个则拓展两个空格，因为%20占用3个位置
2. 左指针，右指针分别等于原始字符串的末尾，拓展后的末尾，当左没有到头时持续往左
3. 如果不是空格，直接替换。是空格，替换为%20，右边指针分别向左移动1和3个位置

```python
class Solution:
    def replaceSpace(self, s: str) -> str:
        counter = s.count(' ')
        
        res = list(s)
        # 每碰到一个空格就多拓展两个格子，1 + 2 = 3个位置存’%20‘
        res.extend([' '] * counter * 2)
        
        # 原始字符串的末尾，拓展后的末尾
        left, right = len(s) - 1, len(res) - 1
        
        while left >= 0:
            if res[left] != ' ':
                res[right] = res[left]
                right -= 1
            else:
                # [right - 2, right), 左闭右开
                res[right - 2: right + 1] = '%20'
                right -= 3
            left -= 1
        return ''.join(res)
```