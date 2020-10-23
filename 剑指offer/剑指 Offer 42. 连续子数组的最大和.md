#### [剑指 Offer 42. 连续子数组的最大和](https://leetcode-cn.com/problems/lian-xu-zi-shu-zu-de-zui-da-he-lcof/)

> 输入一个整型数组，数组中的一个或连续多个整数组成一个子数组。求所有子数组的和的最大值。
>
> 要求时间复杂度为O(n)。



**示例 1：**

```
输入: nums = [-2,1,-3,4,-1,2,1,-5,4]
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
```

**限制：**

```
1 <= arr.length <= 10^5
-100 <= arr[i] <= 100
```



* ### 方法：动态规划

  * **dp[i] 代表以元素 nums[i] 为结尾的连续子数组最大和。**

  * **若 dp[i−1]≤0 ，说明 dp[i−1] 对 dp[i] 产生负贡献，即 dp[i−1]+nums[i] 还不如 nums[i] 本身大。**

    - **当 dp[i−1]>0 时：执行 dp[i] = dp[i-1] + nums[i]；**
    - **当 dp[i−1]≤0 时：执行 dp[i] = nums[i] ；**

  *  **dp[i] = max(dp[i-1] + nums[i],nums[i]);**

    ![连续子数组的最大和](F:\LT找工作哈\博客&github\连续子数组的最大和.png)


```c++
const int N = 1e5 + 50;
int dp[N];
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int n = nums.size();
        dp[0] = nums[0];
        int res = dp[0];
        for(int i = 1;i < n; i++){
            dp[i] = max(dp[i-1] + nums[i],nums[i]);
            res = max(res,dp[i]);
        }
        return res;
    }
};
```


