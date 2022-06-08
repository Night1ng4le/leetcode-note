## 387. 字符串中第一个唯一的字符

### 题目描述


### 朴素双循环

需要注意的几个点：
- 注意区分break和continue的区别（对，没错，我就写错了
- 如果一个字符和前面出现过的已经重复了，但和后面的字符没重复。（不要认为它没重复过啊！！
- 边界情况需要认真考虑清楚（说的就是我自己orz

注： 今天忽然想用c++写，所以两个各写了一遍。

```c++
class Solution {
public:
    int firstUniqChar(string s) {
        int *repeat = new int[s.size()]();//每个元素初始化为0，这是一个标记数组，以确定后续是否有重复元素
        for(int i=0;i<s.size();i++){
            int j=i+1;
            while(j<s.size()){
                if(s[i]==s[j]){
                    repeat[i] = 1;
                    repeat[j] = 1;
                    break;
                }
                j++;
            }
            if(repeat[i]==1){
                continue;
            }else{
                return i;
            }
        }
        return -1;
    }
};
```

### 哈希表存储频数

```c++
class Solution{
    int firstUniqChar(string s){
        unordered_map<int, int> frequency;
        for(char ch:s){

        }
    }
}
```

### 哈希表
我的想法是，把其中一个字符串输入进哈希表，key是字符，value是字符出现次数。
``` C++
class Solution{
    int firstUniqChar(string s){
        unordered_map<int, int> position;
        for (int i = 0; i < s.size(); i++)
        {
            /* code */
            
        }
    }
}
```

### 队列




