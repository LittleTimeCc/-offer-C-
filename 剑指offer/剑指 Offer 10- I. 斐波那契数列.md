#### [剑指 Offer 10- I. 斐波那契数列](https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof/)

> 写一个函数，输入 `n` ，求斐波那契（Fibonacci）数列的第 `n` 项。斐波那契数列的定义如下：
>
> F(0) = 0,   F(1) = 1
> F(N) = F(N - 1) + F(N - 2), 其中 N > 1.
> 斐波那契数列由 0 和 1 开始，之后的斐波那契数就是由之前的两数相加而得出。
>
> 答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。



**示例 1：**

```
输入：n = 2
输出：1
```

**示例 2：**

```
输入：n = 5
输出：5
```

**限制：**

```
0 <= n <= 100
```



* ### 方法一：动态规划


```c++
const int N = 105;
const int MOD = 1e9 + 7;
class Solution {
public:
    int fib(int n) {
        if(n == 0) return 0;
        if(n == 1) return 1;
        int dp[N];
        dp[0] = 0;
        dp[1] = 1;
        for(int i = 2;i <= n;i++){
            dp[i] = (dp[i-1] + dp[i-2]) % MOD;
        }
        return dp[n];
    }
};
```



* ### 方法二：动态规划 + 滚动数组

  * **滚动数组思想： dp[i] = dp[i-1]+dp[i-2]，每一个数都只和它的前两个状态有关，所以实际上只需要开一个大小为3的数组，通过不断的迭代，只保留与当前决策有用的状态，而之前的无用信息全部舍去。**

```c++
const int MOD = 1e9 + 7;
class Solution {
public:
    int fib(int n) {
        if(n == 0) return 0;
        if(n == 1) return 1;
        int dp[3];
        dp[0] = 0;
        dp[1] = 1;
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
	int fib(int n) {
		Ma A;
	    A.a[0][0] = 0;
	    A.a[0][1] = A.a[1][0] = A.a[1][1] = 1;
	    Ma F;
	    F.a[0][0] = 0;
        F.a[1][0] = 1;
        F.a[0][1] = F.a[1][1] = 0;
	    Ma res = (A^n)*F;
	    return res.a[0][0];
	}
};
```
