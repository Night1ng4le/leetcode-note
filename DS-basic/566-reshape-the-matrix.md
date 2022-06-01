## 566. 重塑矩阵

### 题目描述

https://leetcode.cn/problems/reshape-the-matrix/

### 中间数组

因为我不会直接从一个m\*n的矩阵转换成一个r\*c的矩阵。所以首先排成一个一维数组，然后再转换成我想要的形状。
- 先判断能不能转换
- 如果能，flatten
- 把flatten之后的数组转换成我想要的


```java
class Solution {
    public int[][] matrixReshape(int[][] mat, int r, int c) {
        int x = mat.length*mat[0].length;
        if(x!=r*c){
            return mat;
        }
        int[] temp = new int[x];
        int i = 0;
        for(int j=0;j<mat.length;j++){ // 遍历所有元素
            for(int m=0;m<mat[0].length;m++){
                temp[i] = mat[j][m];
                i++;
            }
        }
        i=0;
        int[][] res = new int[r][c];
        for(int p=0;p<r;p++){
            for(int q=0;q<c;q++){ //遍历所有元素
                res[p][q] = temp[i];
                i++;
            }
        }
        return res;
    }
}
```