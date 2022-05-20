## 1. 两数之和

- DS basic
- array
- hash table

### 题目描述
https://leetcode.cn/problems/two-sum/

[这一题我居然是第一次写，震惊！(变相的说明了我真的很菜orz]

### 暴力循环
非常朴素的双层循环。因为这里是无序求和，所以两个数字的位置对结果没有影响。第二层循环从i+1的位置开始就可以了。

时间复杂度：O(N^2)，虽然数值上比两层都从0开始快了一点，但本质上并没有什么区别。

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] res = new int[2];
        for(int i=0;i<nums.length;i++){
            for(int j=i+1;j<nums.length;j++){
                if(nums[i]+nums[j]==target){
                    res[0] = i;
                    res[1] = j;
                }
            }
        }
        return res;
    }
}
```

更新一下输出的形式（我太菜了，我不会java），这种写法代码比较干净。
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        for(int i=0;i<nums.length;i++){
            for(int j=i+1;j<nums.length;j++){
                if(nums[i]+nums[j]==target){
                	return new int[]{i,j}; //就是这里
                }
            }
        }
    }
}
```

### 哈希表

一个一直听说，但是自己从来不会的解法。

这个方法把“两数之和”的问题，转化成了“两数之差”的问题。问题从寻找两个数，转化成了寻找一个数，所以可以考虑使用查找更快的哈希表。

- 方法一之所以慢，是因为需要花O(N)的时间去找target-nums[i];
- 根据哈希表的特点， 如果我们使用哈希表，就可以把搜索时间降到O(1);
- 根据题意，同一个元素在答案中不能反复出现，所以首先匹配哈希表中是否有target-nums[i]，然后插入nums[i]，避免元素跟自己匹配。

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer,Integer> hashtable = new HashMap<Integer,Integer>();
        for(int i=0;i<nums.length;i++){
            if(hashtable.containsKey(target-nums[i])){ // containsKey()这个方法是根据计算哈希值进行查找，containsValue()是通过遍历查找
                return new int[]{hashtable.get(target-nums[i]),i};
            }
            hashtable.put(nums[i],i);
        }
        return new int[0];
    }
}
```
