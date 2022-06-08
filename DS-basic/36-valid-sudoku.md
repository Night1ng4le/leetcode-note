## 36. 有效的数独

### 题目描述


### 一个大佬的思路

这一题有想到行列要用哈希表，但是属于我卡在了同一个格子有没有重复数字。所以参考了一个大佬的思路：

由于board中的整数限定在1到9的范围内，因此可以分别建立哈希表来存储任一个数在相应维度上是否出现过。维度有3个：所在的行，所在的列，所在的box，注意box的下标也是从左往右、从上往下的。

遍历到每个数的时候，例如boar[i][j]，我们判断其是否满足三个条件：

    在第 i 个行中是否出现过
    在第 j 个列中是否出现过
    在第 j/3 + (i/3)*3个box中是否出现过.

[liujin-4](https://leetcode.cn/problems/valid-sudoku/solution/36-jiu-an-zhao-cong-zuo-wang-you-cong-shang-wang-x/)

同一排的三个box，数字的位置只跟纵坐标有关
```
 -----------
| 0 | 1 | 2 |
 -----------
| 3 | 4 | 5 |
 -----------
| 6 | 7 | 8 |
 -----------


数字所在的格子分布如上图所示。每一行的三个box都是box[0], box[1],box[2];区分不同行的box就需要借助一个3的倍数。原理跟j/3差不多，也就是(i/3)*3。
```

```c++
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        int row[9][9] = {0};
		int clo[9][9] = {0};
		int box[9][9] = {0};
		for (int i=0; i<9; i++)
		{
			for (int j=0; j<9; j++){
				if(board[i][j]=='.') continue;
				int curNumber = board[i][j]-'1'; //这里-1是因为数组下标是0-8，数独数字是0-9.为了便于记录，所以这里直接-1，跟数组下标一一对应。
				if(row[i][curNumber]) return false;
				if(clo[j][curNumber]) return false;
				if(box[j/3+(i/3)*3][curNumber]) return false;

				//如果都没出现过
				row[i][curNumber] = 1;
				clo[j][curNumber] = 1;
				box[j/3+(i/3)*3][curNumber] = 1;
			}
		}
		return true;
    }
};

```


