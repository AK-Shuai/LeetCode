**题目**：
<a href="https://leetcode.cn/problemsxuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/" target="_blank">剑指 Offer 11. 旋转数组的最小数字</a>


```java
class Solution {
    public int minArray(int[] numbers) {
        int j = numbers.length - 1;
        int i = 0;
        while (i < j){
            int m = (i+j) / 2;
            if(numbers[m] > numbers[i]){
                i = m + 1;
            }else if (numbers[m] < numbers[i]){
                j = m;
            }else{
                j--;
            }
            
        }
        return numbers[i];

    }
}
```