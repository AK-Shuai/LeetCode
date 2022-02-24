**题目**：
<a href="https://leetcode-cn.com/problems/he-wei-sde-liang-ge-shu-zi-lcof/" target="_blank">剑指 Offer 57. 和为s的两个数字</a>


```python
# 纯纯手撸
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        hashtable = dict()
        for i,j in enumerate(nums):
            if target - j in hashtable:
                return [j, target - j]
            hashtable[nums[i]] = j
        return []
```

**总结**：
就是两数之和解法，可采用n数之和的套路
