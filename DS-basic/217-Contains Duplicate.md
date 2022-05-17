### 217. 存在重复的元素

tags:
    - DS-basic
    - array
    - hash-table


#### 题目描述

https://leetcode.cn/problems/contains-duplicate/

数组中有相同元素则返回`true`，反之返回`false`

#### 朴素循环

设定初始flag为false，设置双层循环。因为每组数字只需要比较一次，所以内层循环每次都从i+1的位置开始。
时间复杂度是 $O(n^2)$

```
  i
  |
  v
 ---------------
| 1 | 2 | 4 | 1 |           
 ---------------
      ^
      |
     j=i+1
```


```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        boolean flag = false;
        for(int i=0;i<nums.length;i++){
            for(int j=i+1;j<nums.length;j++){
                if(nums[i]==nums[j]) flag = true;
            }
        }
        return flag;
    }
}
```

这个方法的结果是，超出时间限制。

#### 排序

- 排序（好像需要一些看见数组先排序的本能），时间复杂度O(NlogN)
- 遍历数组，比较相邻的两个元素是否重复，需要O(N)的时间
排序的时间复杂度是O(NlogN)

```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        Arrays.sort(nums);
        for(int i=0;i<nums.length-1;i++){
            if(nums[i]==nums[i+1]){
                return true;
            }
        }
        return false;
    }
}
```

#### 哈希表

寻找一组数据里的重复元素，哈希表是很好的选择。如果插入一个元素时发现该元素已经存在于哈希表中，则说明存在重复的元素。
> 哈希表适用的场景之一是快速查找
> key和value相同是set，不同是map

时间复杂度：O(N)，其中N为数组的长度。

```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        Set<Integer> hash_table = new HashSet<Integer>();
        for(int x:nums){
            if(!hash_table.add(x)){
                return true;
            }
        }
        return false;
    }
}
```