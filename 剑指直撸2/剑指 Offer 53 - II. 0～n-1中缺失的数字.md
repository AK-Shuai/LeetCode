**题目**：
<a href="https://leetcode-cn.com/problems/que-shi-de-shu-zi-lcof/" target="_blank">剑指 Offer 53 - II. 0～n-1中缺失的数字</a>

求和互减：
```python
class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        # 求和秒杀 虽然捡漏但是实在
        return sum(range(len(nums) + 1)) - sum(nums)
```

双指针：
```python
class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        i, j = 0, len(nums) - 1
        while i <= j:
            m = (i + j) // 2
            if nums[m] == m: i = m + 1 # 知识判断数组下标和数据值相等不
            else: j = m - 1 # 防止中位数大向下减
        return i
```