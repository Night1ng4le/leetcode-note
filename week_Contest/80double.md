## 80. 双周赛

### 第一题（easy） - 强密码检验器II

**题目描述：** https://leetcode.cn/contest/biweekly-contest-80/problems/strong-password-checker-ii/

**思路：** 模拟

```java
class Solution {
    public boolean strongPasswordCheckerII(String password) {
        if(password.length()<8){
            return false;
        }
        int upper = 0, lower = 0, num = 0, special = 0;
        String spe = "!@#$%^&*()-+";
        for(int i=0;i<password.length();i++){
            char c = password.charAt(i);
            if(c>='A'&&c<='Z'){
                upper++;
            }
            if(c>='a'&&c<='z'){
                lower++;
            }
            if(c>='0'&&c<='9'){
                num++;
            }
            if(spe.contains(spe.valueOf(c))){
                special++;
            }
        }
        if(upper<1||lower<1||num<1||special<1){
            return false;
        }
        for(int i=1;i<password.length();i++){
            if(password.charAt(i) == password.charAt(i-1)){
                return false;
            }
        }
        return true;
    }
}
```

### 第二题（Medium） - 咒语和药水的成功对数

**题目：**

**思路：**一开始想的是暴力的思路（毕竟最好想），但是时间不允许。

然后看见数组必然想到排序嘛，排序+二分是一个极好的思路。咒语的顺序不能改变，所以对药水进行排序。对于一个有序数组二分是最常见的检索方法，时间复杂度直接变为O(max(mlogm,n))，其中mlogm是归并排序的时间。

```java
//我先尝试一下暴力的思路
class Solution {
    public int[] successfulPairs(int[] spells, int[] potions, long success) {
        int n = spells.length;
        int m = potions.length;
        int[] pairs = new int[n];
        
        
        for(int i=0;i<spells.length;i++){
        	for(int j=0;j<potions.length;j++){
        		//这里注意数据类型转换
                Long long_spell = Long.valueOf(spells[i]);
                Long long_potions = Long.valueOf(potions[j]);
        		if(long_spell*long_potions>=success){
        			pairs[i]++;
        		}
        	}
        }
        return pairs;
    }
}
```

其实有一个不太一样的思路，就是先对药水从强到弱排序，第一个不成功的直接continue到下一个咒语的循环，算是对暴力的一点点优化？

```java
//二分法的思路
class Solution {
    public int[] successfulPairs(int[] spells, int[] potions, long success) {
        int n = spells.length;
        int m = potions.length;
        int[] pairs = new int[n];
        
        Arrays.sort(potions);
        
        for(int i=0;i<spells.length;i++){
            int left = 0, right = m - 1;
            int mid;
            Long long_spell = Long.valueOf(spells[i]);
        	while(left<=right){
                mid = (left+right)/2;
                Long long_potions = Long.valueOf(potions[mid]);
        		if(long_spell*long_potions>=success){
                    pairs[i] += right - mid + 1;
                    right = mid-1;
        		}
                if(long_spell*long_potions<success){
                    left = mid+1;
                }
            }
                
                
        }
        return pairs;
    }
}
```

### 第三题（Hard） - 


### 第四题（Hard） - 统计得分小于 K 的子数组数目