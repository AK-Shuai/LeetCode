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


```java
// 用HashSet 如果插入false就退出
class Solution {
    public int findRepeatNumber(int[] nums) {
        Set<Integer> set = new HashSet<Integer>();
        int a = -1;
        for(int num:nums){
            if(!set.add(num)){
                a = num;
                break;
            }
        }
        return a;
    }
}
```