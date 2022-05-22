## 118. 杨辉三角

### 题目描述

https://leetcode.cn/problems/pascals-triangle/

### 动态规划
其实这一题我没看出来是动态规划，题目给的提示思路是是动态规划。

首先观察一下杨辉三角
```
# 以numRows = 5为例子：
-----------------

    1 
   1  1
  1  2  1
 1  3  3  1
1  4  6  4  1
-----------------
```
可以看出每行的元素数目=行数，且每行第1个及最后一个元素数值均为1。

**定义子问题**
dp[i][j] 表示第i行第j个元素

**状态转移方程**
dp[i][j] = dp[i-1][j-1]+dp[i-1][j]

**初始化输入**
dp[i][0] = 1

```java
class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> trangle = new ArrayList<>();
        int[][] dp = new int[numRows+1][numRows+1];
        for(int i=1;i<=numRows;i++){
            List<Integer> row = new ArrayList<>();
            dp[i][0] = 1;
            dp[i][numRows] = 1;
            row.add(dp[i][0]);
            for(int j=1; j<i; j++){
                dp[i][j] = dp[i-1][j-1]+dp[i-1][j];
                row.add(dp[i][j]);
            }
            trangle.add(row);
        }
        return trangle;
    }
}
```

大概是我还没完全理解动态规划，还需要再反复理解一段时间。