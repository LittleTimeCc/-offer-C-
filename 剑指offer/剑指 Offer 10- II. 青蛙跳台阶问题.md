#### [剑指 Offer 10- II. 青蛙跳台阶问题](https://leetcode-cn.com/problems/qing-wa-tiao-tai-jie-wen-ti-lcof/)

> 一只青蛙一次可以跳上1级台阶，也可以跳上2级台阶。求该青蛙跳上一个 n 级的台阶总共有多少种跳法。
>
> 答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。



**示例 1：**

```
输入：n = 2
输出：2
```

**示例 2：**

```
输入：n = 7
输出：21
```

**示例 3：**

```
输入：n = 0
输出：1
```

**限制：**

```
0 <= n <= 100
```



* ### 方法一：动态规划


```c++
const int N = 105;
const int MOD = 1e9 +7;
class Solution {
public:
    int numWays(int n) {
        if(n <= 1){
            return 1;
        }
        int dp[N];
        dp[0] = dp[1] = 1;
        for(int i = 2;i <= n;i++){
            dp[i] = (dp[i-1] + dp[i-2]) % 1000000007;
        }
        return dp[n];
    }
};
```



* ### 方法二：动态规划 + 滚动数组

  * **滚动数组思想： dp[i] = dp[i-1]+dp[i-2]，每一个数都只和它的前两个状态有关，所以实际上只需要开一个大小为3的数组，通过不断的迭代，只保留与当前决策有用的状态，而之前的无用信息全部舍去。**

```c++
const int MOD = 1e9 +7;
class Solution {
public:
    int numWays(int n) {
        if(n <= 1){
            return 1;
        }
        int dp[3];
        dp[0] = dp[1] = 1;
        for(int i = 2;i <= n;i++){
            dp[2] = (dp[1] + dp[0]) % MOD;
            dp[0] = dp[1];
            dp[1] = dp[2];
        }
        return dp[2];
    }
};
```



* ### 方法三：矩阵快速幂

  $$
  \begin{bmatrix}
  0&1\\
  1&1\\
  \end{bmatrix}
  
  \begin{bmatrix}    
  F_0&0\\
  F_1&0\\
  \end{bmatrix}
  =
  \begin{bmatrix}
  F_1&0\\
  F_0 + F_1&0\\
  \end{bmatrix}
  \\
  \\
  
  \begin{matrix}  
  \\
  F_0 + F_1 = F_2
  \end{matrix}
  $$
  
  
  $$
  \begin{bmatrix}
  0&1\\
  1&1\\
  \end{bmatrix}^n
  
  \begin{bmatrix}    
  F_0&0\\
  F_1&0\\
  \end{bmatrix}
  =
  \begin{bmatrix}
  F_{n-1}&0\\
  F_{n-2} + F_{n-1}&0\\
  \end{bmatrix}
  \\
  \\
  
  \begin{matrix}  
  \\
  F_{n-1} + F_{n-2} = F_n
  \end{matrix}
  $$
  
  
  **如上的递推的矩阵可知，只需要计算矩阵的n次幂即可得到数列的第n项，因此问题转换为矩阵的n次幂。**


```c++
const int M = 2;
typedef long long LL;
const int MOD = 1e9 + 7;
struct Ma{
    LL a[M][M];
    Ma(){
        memset(a,0,sizeof(a));
    }
    void Unit(){
        a[0][0] = a[1][1] = 1;
        a[0][1] = a[1][0] = 0;
    }
    Ma operator*(const Ma& C) const{
        Ma res;
        for(int i = 0; i < M; i++){
            for(int j = 0; j < M;j++){
                for(int k = 0; k< M; k++){
                    res.a[i][j] += (a[i][k] * C.a[k][j]) % MOD;
                    res.a[i][j] %= MOD;
                }
            }
        }
        return res;
    }
    Ma operator^(int n) const{
        Ma res; res.Unit(); //res设置为单位矩阵
        Ma A = *this;
        while(n){
            if(n&0x1) res = res*A;
            A=A*A;
            n >>= 1;
        }
        return res;
    }
};
class Solution {
public:
	int numWays(int n) {
        if(n <= 1) return 1;
		Ma A;
	    A.a[0][0] = 0;
	    A.a[0][1] = A.a[1][0] = A.a[1][1] = 1;
	    Ma F;
	    F.a[0][0] = 1;
        F.a[1][0] = 1;
        F.a[0][1] = F.a[1][1] = 0;
	    Ma res = (A^n)*F;
	    return res.a[0][0];
	}
};
```



