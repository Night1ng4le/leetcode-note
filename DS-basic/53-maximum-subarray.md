## 53. 最大子数组和

- array
- divide & conquer
- DP(Dynamic Programming)

### 题目描述


### 1.动态规划

这是一道经典的动态规划问题。注意题目描述中的`连续`。题目只要求返回结果，不要求输出最大连续子数组是哪一个，这样的问题通常可以使用动态规划解决。

> 动态规划要求问题具有`无后效性`
> 求解问题的步骤一般分为：
>	1. 定义一个状态，这是一个最优解的结构特征
>	2. 进行状态递推，得到递推公式
>	3. 进行初始化
>	4. 返回结果

**定义状态（子问题）**
dp[i]：表示以nums[i]结尾的连续子数组的最大的和

**状态转移方程（描述子问题之间的联系）**
状态转移方程[1]:

dp[i] = dp[i−1]+nums[i], if dp[i−1]>0
dp[i] = nums[i], if dp[i−1]<=0

我们讨论dp[i-1]的结果
- 如果dp[i-1]<=0，则另起炉灶，max = nums[i]
- 如果dp[i-1]>0，则max = dp[i-1] + nums[i]

状态转移方程[2]:
dp[i] = max{nums[i],dp[i-1]+nums[i]}

这个比较容易理解，比较加上nums[i]和nums[i]哪个大，记录下数值较大的结果。

**确定初始值**
根据题意，初始值即为只有一个元素的时候，所以dp[0] = nums[0]

**输出**
note：这里的输出不应该是最后一个状态的结果，而应该是`全局所有状态的最大值`。
我们需要在所有最优子问题中求解全局最优。 

时间复杂度：O(N)

```java
// 这里用的是状态转移方程2
class Solution {
    private int max(int a, int b){
    	// return max number
        int max = 0;
        if(a>b){
            max = a;
        }else{
            max = b;
        }
        return max;
    }
    public int maxSubArray(int[] nums) {
    	// initialize
        int[] dp = new int[nums.length];
        dp[0] = nums[0];
        // state change
        for(int i=1;i<nums.length;i++){
            dp[i] = max(nums[i],dp[i-1]+nums[i]);
        }

        // output 
        int result = dp[0];
        for(int i=1;i<dp.length;i++){
            if(dp[i]>result){
                result = dp[i];
            }
        }
        return result;
    }
}
```

`无后效性`：动态规划要求已经求解的子问题不受后续阶段的影响。换言之，动态规划对状态空间的遍历构成一张有向无环图，遍历就是该有向无环图的一个拓扑序。有向无环图中`节点`对应问题中的`状态`，`边`对应状态之间的`转移`，转移的选取就是动态规划中的`决策`。 


### 分治法
和最大的子数组一定会出现