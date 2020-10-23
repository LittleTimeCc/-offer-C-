#### [剑指 Offer 03. 数组中重复的数字](https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/)

> 在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。
>
> 

**示例 1：**

```
现有矩阵 matrix 如下：

[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
给定 target = 5，返回 true。

给定 target = 20，返回 false。
```

**限制：**

```
0 <= n <= 1000

0 <= m <= 1000
```



* **从右上角开始走，利用这个顺序关系可以在`O(m+n)`的复杂度下解决这个题： (row是行,col是列)**
  - **如果当前位置元素比target小，则row++**
  - **如果当前位置元素比target大，则col--**
  - **如果相等，返回true**
  - **如果越界了还没找到，说明不存在，返回false**

```c++
class Solution {
public:
    bool findNumberIn2DArray(vector<vector<int>>& matrix, int target) {
        if(matrix.size()==0)    
            return false;
        int i = 0, j = matrix[0].size() - 1;  //i是行  j是列
        while(i < matrix.size() && j >= 0)
        {
            if(matrix[i][j] == target) 
                return true;
            else if(matrix[i][j] > target) 
                j--;
            else
                i++;
        }

        return false;
    }
};
```


