## 121. 买卖股票的最佳时机

- DS basic
- array
- DP

### 题目描述
https://leetcode.cn/problems/best-time-to-buy-and-sell-stock/

### 一个朴素的暴力算法

由于题目要求返回最大利润，根据题意，把每种情况的利润都填进二维表里。由于卖出时间>=买入时间，因此这里只需要填半张表。

> dp[i][j]表示以prices[i]买入，以price[j]卖出的利润。


随后遍历整张表，找出最大利润。

如果最大利润小于0，则返回0；反之返回最大利润

```java
class Solution {
    public int maxProfit(int[] prices) {
        int n = prices.length;
        int[][] dp = new int[n][n];

        // 根据题意，填好每种情况的最大利润
        for (int i=0; i<prices.length-1; i++) {
	        for (int j=i+1; j<prices.length; j++) {
                dp[i][j] = prices[j]-prices[i];
	        }
        }
        // 遍历最大值
        int max = -10000;
        for (int i=0; i<prices.length-1; i++) {
	        for (int j=i+1; j<prices.length; j++) {
                if(dp[i][j]>max){
                    max = dp[i][j];
                }
	        }
        }
        // 输出结果
        if(max<0){
            return 0;
        }
        return max;
    }
} 
```

这个朴素方法的结果是`超出内存限制`。（我都没想到我看到的居然不是超出时间限制orz，后来想了想毕竟这是一个时间复杂度O(n^2)，空间复杂度O(n^2)的方法

### 另一个朴素的暴力算法

感觉上一个方法是想用动态规划的思路但是失败了，所以我又回到了十分原始的双层循环。

```java
class Solution {
    public int maxProfit(int[] prices) {
        int maxprofit = -10000;
        for(int i=0;i<prices.length-1;i++){
            for(int j=i+1;j<prices.length;j++){
                if(maxprofit<prices[j]-prices[i]){
                    maxprofit = prices[j]-prices[i];
                }
            }
        }
        if(maxprofit<0){
            return 0;
        }
        return maxprofit;
    }
} 
```

很好，现在我又重新回到了`超出时间限制`这个问题。（仿佛有进展，但好像又不完全有进展。

### 动态规划
这道题跟之前的最大连续子序列的和有点像，也可以使用动态规划的方法写。
(事情进展到这一步，我已经完全想起来我为什么从来没有学会过动态规划了，因为！我不会定义子问题啊！)

（比葫芦画瓢ing~
根据53大佬的笔记可知，定义子问题要尽可能的控制变量，以便于发现子问题之间的联系。同时还要保证子问题的`无后效性`。
所以这里的子问题我猜应该是：在我确定第i天卖出股票的情况下，我应该在(0,i-1]哪一天买入。

> 换句话说，第i天的最大收益，取决于(0,i-1]天中的最低价格。

**确定子问题：**
dp[i]表示截止到第i天历史价格的最低点。

**状态转移方程：**
dp[i] = min(dp[i-1],nums[i])

**初始化**
dp[0] = prices[0]

**确定输出**
这里输出应该是全局最大化收益，需要维护一个maxprofit变量，确保收益持续最大。如果收益小于0，则输出0。

```java 
class Solution {
    private int min(int a, int b){
        return (a<b)?a:b;
    }
    public int maxProfit(int[] prices) {
        int maxprofit = -10000;
        int[] dp = new int[prices.length];
        dp[0] = prices[0];
        for(int i=1;i<prices.length;i++){
            dp[i] = min(dp[i-1],prices[i]);
            maxprofit = (prices[i]-dp[i]>maxprofit)?prices[i]-dp[i]:maxprofit;
        }
        if(maxprofit<0){
            return 0;
        }
        return maxprofit;
    }
}
```

终于！成功AC了！
这一题总结出来的点大概是，定义子问题的时候需要找到每个状态为截至时的变量，这样确定下来的问题似乎才具有无后效性。