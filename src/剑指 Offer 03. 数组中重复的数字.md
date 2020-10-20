#### [剑指 Offer 03. 数组中重复的数字](https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/)

> 找出数组中重复的数字。
>
> 在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。



**示例 1：**

```
输入：
[2, 3, 1, 0, 2, 5, 3]
输出：2 或 3 
```

**限制：**

```
2 <= n <= 100000
```





* ### 方法一：排序

  * **时间:O(nlogn)  空间: O(1)**

```c++
class Solution {
public:
    int findRepeatNumber(vector<int>& nums) {
        int n = nums.size();
        sort(nums.begin(),nums.end());
        for(int i = 0; i < n - 1; i++){
            if(nums[i] == nums[i+1]){
                return nums[i];
            }
        }
        return -1;
    }
};
```



* ### 方法二：哈希

  * **时间：O(n)  空间:O(n)**

```c++
class Solution {
public:
    int findRepeatNumber(vector<int>& nums) {
        unordered_map<int,int> hash;
        for(auto n : nums){
            if(hash.find(n)!=hash.end()){
                return n;
            }
            hash[n] = 1;
        }
        return -1;
    }
};
```



* ### 方法三：原地交换

* **简要分析**

  * **时间：O(n) 空间:O(1)**
  * **因为数组元素的值的一定小于数组的大小，我们可以通过下标实现哈希的功能，将数组元素放到与自身值相等的下标处，如果出现重复返回重复数字**
  * **遍历中，第一次遇到数字 x 时，将其交换至索引 x 处；而当第二次遇到数字 x 时，一定有 nums[x] = x ，此时即可得到一组重复数字。**

![原地交换](img/原地交换.png)

* **算法流程：**
  * **遍历数组 nums ，若 nums[i] = i， 说明此数字已在对应索引位置，无需交换，因此跳过；**
  * **若 nums[nums[i]] = nums[i]： 代表索引 nums[i] 处和索引 i 处的元素值都为 nums[i] ，即找到一组重复值，返回此值 nums[i] ；**
  * **否则： 交换索引为 i 和 nums[i] 的元素值，将此数字交换至对应索引位置；**
  * **若遍历完尚未返回，则返回 -1 。**

```c++
class Solution {
public:
    int findRepeatNumber(vector<int>& nums) {
        int n = nums.size();
        for(int i = 0; i < n; i++){
            if(nums[i] == i){
                continue;
            }
            if(nums[nums[i]] == nums[i]){
                return nums[i];
            }
            std::swap(nums[nums[i]],nums[i]);
        }
        return -1;
    }
};
```



