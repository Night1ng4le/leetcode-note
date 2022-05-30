## 88. 合并两个有序数组

### 题目描述

https://leetcode.cn/problems/merge-sorted-array/

### 双指针

总的来说思路跟归并排序差不多，需要注意几个问题：
- 数组下标不要越界
- 因为这里没有新建第三个数组，所以排序需要从后往前排，避免覆盖前面的数字

```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int i = m-1;
        int j = n-1;
        int k = m+n-1;
        while(k>=0){
            if(i<0&&j>=0){
                nums1[k--] = nums2[j--];
            }
            if(j<0&&i>=0){
                nums1[k--] = nums1[i--];
            }
            if(i>=0&&j>=0){
                if(nums1[i]<nums2[j]){
                    nums1[k--] = nums2[j--];
                }else{
                    nums1[k--] = nums1[i--];
                }
            }
        }
    }
}
```