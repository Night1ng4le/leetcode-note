## 350. 两个数组的交集II

### 题目描述

https://leetcode.cn/problems/intersection-of-two-arrays-ii/




### 双指针

**基本思路：**首先排序，在有序数组的基础上使用双指针。如果元素不等，较小元素对应的指针后移一位，如果相等，则两个一起后移。

> 一个问题：ArrayList转int[]
> 为什么会有这个问题？
> 因为`ArrayList`的`toArray`无法对`int`生效
> 为什么无法对`int`生效?
> 因为`int`不是对象，所以不是`object`的子类
> 所以比较好用的转换方法-> 遍历一下

**时间复杂度：**O(max(nlogn,mlogm,n+m))。


```java
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        Arrays.sort(nums1);
        Arrays.sort(nums2);
        int i = 0;
        int j = 0;
        ArrayList<Integer> res = new ArrayList<Integer>();
        while(i<nums1.length&&j<nums2.length){
            if(nums1[i]<nums2[j]) i++;
            else if(nums1[i]>nums2[j]) j++;
            else if(nums1[i]==nums2[j]){// 这里注意使用else，不然会出现数组越界
                res.add(nums1[i]);
                i++;
                j++;
                
            }
        }
        // ArrayList不能直接转int[]
        int[] result = new int[res.size()];
        for(int m=0;m<res.size();m++){
            result[m] = res.get(m);
        }
        return result;
    }
}
```

### 哈希表

等有空了补充这个。

### 思考题
1. 如果数组已经有序，则省去排序步骤，时间复杂度是O(m+n)
2. 如果nums1的大小比nums2小，将较小的数组使用哈希表计数，另一个数组找。
3. 如果内存不够，就还是先归并，再使用双指针。磁盘空间有限的情况下，归并排序是天然适合外部排序的算法（通常排序算算法都是针对内部排序的）。