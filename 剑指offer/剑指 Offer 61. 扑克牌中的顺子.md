#### [剑指 Offer 61. 扑克牌中的顺子](https://leetcode-cn.com/problems/bu-ke-pai-zhong-de-shun-zi-lcof/)

> 从扑克牌中随机抽5张牌，判断是不是一个顺子，即这5张牌是不是连续的。2～10为数字本身，A为1，J为11，Q为12，K为13，而大、小王为 0 ，可以看成任意数字。A 不能视为 14。



**示例 1：**

```
输入: [1,2,3,4,5]
输出: True
```

**示例 2：**

```
输入: [0,0,1,2,5]
输出: True
```

**限制：**

```
数组长度为 5 

数组的数取值为 [0, 13] .
```

* **解题思路：** **排序 + 遍历**

  * **除大小王外，所有牌 无重复 ；**

  * **设此 5 张牌中最大的牌为 $ max $ ，最小的牌为 $ min $（大小王除外），则需满足：**
    $$
    max - min < 5
    $$
  
* **因而，可将问题转化为：此 5 张牌是否满足以上两个条件？**
  
* **先对数组排序;**

* **判别重复： 排序数组中的相同元素位置相邻，因此可通过遍历数组，判断$  nums[i] == nums[i + 1]   $是否成立来判重。**

* **获取最大 / 最小的牌： 排序后，数组末位元素  $ nums[4] $  为最大牌；元素 $    nums[joker]    $ 为最小牌，其中 $     joker    $ 为大小王的数量。**


```c++
class Solution {
public:
    bool isStraight(vector<int>& nums) {
        int joker = 0;
        sort(nums.begin(),nums.end());
        for(int i = 0;i < 4; i++){
            if(nums[i] == 0) joker++;
            else if(nums[i] == nums[i+1]) return false;
        }
        return nums[4] - nums[joker] < 5;
    }
};
```


