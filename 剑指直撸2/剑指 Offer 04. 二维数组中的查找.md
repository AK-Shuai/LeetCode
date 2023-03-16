**题目**：
<a href="https://leetcode.cn/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/" target="_blank">剑指 Offer 04. 二维数组中的查找</a>


```java
class Solution {
    public boolean findNumberIn2DArray(int[][] matrix, int target) {
        // 获取二维里单个数组最大长度
        int i = matrix.length - 1;
        int j = 0;
        // 停止条件必须是 二维数组单数组指向必须大于0 二维数组的单数组必须在长度内
        while(i >= 0 && j < matrix[0].length){
            // 头节点如果大 向上查找
            if(matrix[i][j] > target){
                i--;
            // 如果小在二维数组内的小数组往后找
            }else if (matrix[i][j] < target){
                j++;
            }else{
                return true;
            }
        }
        return false;
    }
}
```


倒着查，上下左右的查找，
