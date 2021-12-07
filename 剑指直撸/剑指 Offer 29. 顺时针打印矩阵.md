**题目**：
<a href="https://leetcode-cn.com/problems/shun-shi-zhen-da-yin-ju-zhen-lcof/" target="_blank">剑指 Offer 29. 顺时针打印矩阵</a>


```python
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        res = []
        while matrix:
            res += matrix.pop(0)
            matrix = list(zip(*matrix))[::-1]
        return res

        """
        1 2 3
        4 5 6
        7 8 9
        matrix.pop(0)

        4 5 6
        7 8 9
        matrix = list(zip(*matrix))[::-1]

        6 9
        5 8
        4 7
        matrix.pop(0)

        5 8
        4 7
        matrix = list(zip(*matrix))[::-1]

        8 7
        5 4
        matrix.pop(0)

        5 4
        matrix = list(zip(*matrix))[::-1]

        4
        5
        matrix.pop(0)

        5
        matrix = list(zip(*matrix))[::-1]

        5
        matrix.pop(0)

        done!

        """
```