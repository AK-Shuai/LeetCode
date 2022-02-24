- [1. 两数之和](#1-两数之和)
- [167. 两数之和II输入有序数组](#167-两数之和-II-输入有序数组)
- [15. 三数之和](#15-三数之和)
- [18. 四数之和](#18-四数之和)
- [454. 四数相加 II](#454-四数相加-II)
- [n数之和方法总结](#n数之和方法总结)

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

## 15 三数之和

**题目**：
<a href="https://leetcode-cn.com/problems/3sum/" target="_blank">15. 三数之和</a>

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        n = len(nums)
        nums.sort()
        ans = list()
        
        # 枚举 a
        for first in range(n):
            # 需要和上一次枚举的数不相同
            if first > 0 and nums[first] == nums[first - 1]:
                continue
            # c 对应的指针初始指向数组的最右端
            third = n - 1
            target = -nums[first]
            # 枚举 b
            for second in range(first + 1, n):
                # 需要和上一次枚举的数不相同
                if second > first + 1 and nums[second] == nums[second - 1]:
                    continue
                # 需要保证 b 的指针在 c 的指针的左侧
                while second < third and nums[second] + nums[third] > target:
                    third -= 1
                # 如果指针重合，随着 b 后续的增加
                # 就不会有满足 a+b+c=0 并且 b<c 的 c 了，可以退出循环
                if second == third:
                    break
                if nums[second] + nums[third] == target:
                    ans.append([nums[first], nums[second], nums[third]])
        
        return ans
```

**参考**：  
1. <a href="https://leetcode-cn.com/problems/3sum/solution/man-hua-jue-bu-wu-ren-zi-di-xiang-kuai-su-kan-dong/" target="_blank">漫画理解</a>

## 18 四数之和

**题目**：
<a href="https://leetcode-cn.com/problems/4sum/" target="_blank">18. 四数之和
</a>

```python
class Solution:
    def fourSum(self, nums: List[int], target: int) -> List[List[int]]:
        quadruplets = list() # 定义一个返回值
        if not nums or len(nums) < 4:
            return quadruplets
        
        nums.sort()
        length = len(nums)
        # 定义4个指针i,j,left,right  i从0开始遍历,j从i+1开始遍历,留下left和right作为双指针
        for i in range(length - 3):
            if i > 0 and nums[i] == nums[i - 1]: # 当i的值与前面的值相等时忽略
                continue
            # 获取当前最小值,如果最小值比目标值大,说明后面越来越大的值根本没戏
            if nums[i] + nums[i + 1] + nums[i + 2] + nums[i + 3] > target:
                break # 这里使用的break,直接退出此次循环,因为后面的数只会更大
            # 获取当前最大值,如果最大值比目标值小,说明后面越来越小的值根本没戏,忽略
            if nums[i] + nums[length - 3] + nums[length - 2] + nums[length - 1] < target:
                continue # 这里使用continue,继续下一次循环,因为下一次循环有更大的数
            # 第二层循环j,初始值指向i+1
            for j in range(i + 1, length - 2):
                if j > i + 1 and nums[j] == nums[j - 1]: # 当j的值与前面的值相等时忽略
                    continue
                if nums[i] + nums[j] + nums[j + 1] + nums[j + 2] > target:
                    break
                if nums[i] + nums[j] + nums[length - 2] + nums[length - 1] < target:
                    continue
                left, right = j + 1, length - 1
                # 双指针遍历,如果等于目标值,left++并去重,right--并去重,当当前和大于目标值时right--,当当前和小于目标值时left++
                while left < right:
                    total = nums[i] + nums[j] + nums[left] + nums[right]
                    if total == target:
                        quadruplets.append([nums[i], nums[j], nums[left], nums[right]])
                        left += 1 # left先+1之后,和它前面的left-1进行比较,若后+1,则和它后面的left+1进行比较
                        while left < right and nums[left] == nums[left - 1]:
                            left += 1
                        right -= 1
                        while left < right and nums[right] == nums[right + 1]:
                            right -= 1   
                    elif total < target:
                        left += 1
                    else:
                        right -= 1
        
        return quadruplets
```

## 454 四数相加 II

**题目**：
<a href="https://leetcode-cn.com/problems/4sum-ii/" target="_blank">454. 四数相加 II
</a>

```python
class Solution:
    def fourSumCount(self, A: List[int], B: List[int], C: List[int], D: List[int]) -> int:
        # Counter类是dict()子类, 用于计数可哈希对象
        # 它是一个集合,元素像字典键(key)一样存储,它们的计数存储为值
        countAB = collections.Counter(u + v for u in A for v in B)
        ans = 0
        for u in C:
            for v in D:
                if -u - v in countAB:
                    ans += countAB[-u - v]
        return ans
```

**参考**：  
1. <a href="https://leetcode-cn.com/problems/4sum-ii/solution/si-wei-dao-tu-zheng-li-xiang-jie-counter-nw0f/" target="_blank">454题的优化解详情
</a>

## n数之和方法总结
对于两数之和, 看它是否是有序的, 如果是无序的就使用 哈希表 的方法, 如果是有序的, 就可以使用 双指针 的方法.

对于一个数组上的三数之和/四数之和等, 无论数组是否有序, 都排序后使用 双指针 的方法.

对于多个数组之和的情况, 首先对它们进行分组来实现降维操作, 一般来说都是分为两个相等的小组, 之后再使用 哈希表 的方法.

情况比较多, 大家要根据具体情况判断具体哪个方法更好, 时间/空间复杂度更低, 选择最优秀的算法.
