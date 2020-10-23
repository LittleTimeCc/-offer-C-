#### [剑指 Offer 40. 最小的k个数](https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/)

> 输入整数数组 `arr` ，找出其中最小的 `k` 个数。例如，输入4、5、1、6、2、7、3、8这8个数字，则最小的4个数字是1、2、3、4。
>



**示例 1：**

```
输入：arr = [3,2,1], k = 2
输出：[1,2] 或者 [2,1]
```

**示例 2：**

```
输入：arr = [0,1,2,1], k = 1
输出：[0]
```

**限制：**

```
0 <= k <= arr.length <= 10000
0 <= arr[i] <= 10000
```



* ### 方法一：优先级队列(小顶堆)


```c++
class Solution {
public:
    vector<int> getLeastNumbers(vector<int>& arr, int k) {
        vector<int> res;
        if(arr.size() == 0) return res;
        if(k == arr.size()) return arr;
        priority_queue<int,vector<int>,greater<int>> p; //小顶堆
        for(auto a : arr){
            p.push(a);
        }   
        while(k--){
            res.push_back(p.top());
            p.pop();
        }
        return res;
    }
};
```



* ### 方法二：计数排序


```c++
const int MAXN = 1e4 + 50;
int c[MAXN];
class Solution {
public:
    vector<int> getLeastNumbers(vector<int>& arr, int k) {
        vector<int> res;
        if(arr.size() == 0) return res;
        if(k == arr.size()) return arr;
        memset(c,0,sizeof(c));
        for(auto a : arr){
            c[a]++;
        }
        for(int i = 0;i < MAXN && k;i ++){
            if(c[i]){
                for(int j = 0; j < c[i] && k ; j++){
                    res.push_back(i);
                    k--;
                }
            }
        }
        return res;
    }
};
```



