- [1. 两数之和](#1-两数之和)
- [167. 两数之和II输入有序数组](#167-两数之和-II-输入有序数组)

# n数之和

## 1 两数之和
**题目**：
<a href="https://leetcode-cn.com/problems/two-sum/" target="_blank">1. 两数之和</a>

```python
'''做减法看结果在不在字典里，不在就把放到字典里'''
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        hashtable = dict()
        for i, num in enumerate(nums):
            if target - num in hashtable:
                return [hashtable[target - num], i]
            hashtable[nums[i]] = i
        return []
```

## 167 两数之和 II 输入有序数组
**题目**：
<a href="https://leetcode-cn.com/problems/two-sum-ii-input-array-is-sorted/" target="_blank">167. 两数之和 II - 输入有序数组</a>

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        n = len(numbers)
        for i in range(n):
            low, high = i + 1, n - 1
            while low <= high:
                mid = (low + high) // 2
                if numbers[mid] == target - numbers[i]:
                    return [i + 1, mid + 1]
                elif numbers[mid] > target - numbers[i]:
                    high = mid - 1
                else:
                    low = mid + 1
        
        return [-1, -1]
```

**总结**：
因为有序数组，使用二分法外加两数之后标准的减法是否等于二分中间值做判断比较，大则往回走小则往前走。
