**题目**：
<a href="https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/" target="_blank">剑指 Offer 03. 数组中重复的数字</a>

```python
'''手撸解法：拿个哈希表如果值出现2就退出'''
class Solution:
    def findRepeatNumber(self, nums: List[int]) -> int:
        hashmap = {}

        for end in range(len(nums)):
            hashmap[nums[end]] = hashmap.get(nums[end], 0) +1

            if hashmap[nums[end]] > 1:
                return nums[end]
        
        return 0
```