## 73. 矩阵置0

### 题目描述

https://leetcode.cn/problems/set-matrix-zeroes/

### 标记数组法

使用两个标记数组，一个用于记录行是否存在0，一个用来记录列是否存在0。`注：`这是我看完题解之后才知道的

```java
class Solution {
    public void setZeroes(int[][] matrix) {
        int[] flag_row = new int[matrix.length];
        int[] flag_clo = new int[matrix[0].length]; 
        for(int i=0;i<matrix.length;i++){
            for(int j=0;j<matrix[0].length;j++){
                if(matrix[i][j]==0){
                    flag_row[i] = 1;
                    flag_clo[j] = 1;
                }
            }
        }
        for(int i=0;i<matrix.length;i++){
            if(flag_row[i]==1){
                for(int j=0;j<matrix[0].length;j++){
                    matrix[i][j] = 0;
                }
            }
        }
        for(int j=0;j<matrix[0].length;j++){
            if(flag_clo[j]==1){
                for(int i=0;i<matrix.length;i++){
                    matrix[i][j] = 0;
                }
            }
        }
    }
}
```

### 标记位法
因为题目要求`原地`，所以标记数组就不好用了。在方法一的基础上，我们使用原始矩阵的最后一行和最后一列来做每行每列的标记位。
但是需要避免最后一行或最后一列的0被覆盖，因此需要单独处理这两个部分，用两个标记位`flag_row`和`flag_clo`做记录。

时间复杂度：O(mn)，最多也就是完全遍历两次整个矩阵。

空间复杂度：O(1)，只用了常数位的辅助空间。

```java
class Solution {
    public void setZeroes(int[][] matrix) {
        int m = matrix.length-1;
        int q = matrix[m].length-1;
        boolean flag_row = false;
        boolean flag_clo = false;
        for(int n=0;n<matrix[0].length;n++){
            //如果最后一行有0，则flag_row置1
            if(matrix[m][n]==0){
                flag_row = true;
                break;
            }
        }
        for(int p=0;p<matrix.length;p++){
            //如果最后一列存在0，则flag_clo置1
            if(matrix[p][q]==0){
                flag_clo = true;
                break;
            }
        }
        //用矩阵的最后一行和最后一列标记行列是否该置0
        for(int i=0;i<matrix.length-1;i++){
            for(int j=0;j<matrix[0].length-1;j++){
                if(matrix[i][j]==0){
                    matrix[i][q] = 0;
                    matrix[m][j] = 0;
                }
            }
        }
        for(int i=0;i<matrix.length-1;i++){//根据行标记置0行
            if(matrix[i][q]==0){
                for(int j=0;j<matrix[0].length-1;j++){
                    matrix[i][j] = 0;
                }
            }
        }
        for(int i=0;i<matrix[0].length-1;i++){//根据列标记置0列
            if(matrix[m][i]==0){
                for(int j=0;j<matrix.length-1;j++){
                    matrix[j][i] = 0;
                }
            }
        }
        //根据之前的flag判断最后一行最后一列是否需要置0
        if(flag_row==true){
            for(int n=0;n<matrix[0].length;n++){
                matrix[m][n] = 0;
            }
        }
        if(flag_clo==true){
            for(int p=0;p<matrix.length;p++){
                matrix[p][q] = 0;
            }
        }
    }
}
```

### 写在最后
我的代码实在是不太优雅，就是能用而已，所以如果有哪位大佬愿意让它elegant一点，请踢我一jio。