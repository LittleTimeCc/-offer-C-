#### [剑指 Offer 09. 用两个栈实现队列](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/)

> 用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )
>



**示例 1：**

```
输入：
["CQueue","appendTail","deleteHead","deleteHead"]
[[],[3],[],[]]
输出：[null,null,3,-1]
```

**示例 2：**

```
输入：
["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
[[],[],[5],[2],[],[]]
输出：[null,-1,null,null,5,2]
```

**提示：**

```
1 <= values <= 10000
最多会对 appendTail、deleteHead 进行 10000 次调用
```



* ### 思路：

  * **维护一个用来进队列的栈s1，一个用来出队列的栈s2;**
  * **进栈只需直接压入s1栈(即放到队列末尾);**
  * **出栈时，如果s2栈为空，将s1栈一个一个出栈压入s2栈，由此实现栈的元素反转，即后进s1的元素压入s2的栈底，先进s1的元素压入s2的栈顶;**
  * **当s1中的元素全部压入s2栈后，则s2栈顶即为第一个进入队列的元素，此时直接弹出s2栈顶元素即可;**
  * **如果s1栈和s2栈都是空的，则说明队列为空，直接返回-1;**
  * **出栈时，如果s2栈不为空，则无需考虑s1栈，直接将s2栈顶元素出栈即可。**


```c++
class CQueue {
public:
    CQueue() {

    }
    
    void appendTail(int value) {
        s1.push(value);
    }
    
    int deleteHead() {
        int res = -1;
        if(!s2.empty()){
            res = s2.top();
            s2.pop();
        }else{
            if(s1.empty()) return res;
            else{
                while(!s1.empty()){
                    s2.push(s1.top());
                    s1.pop();
                }
                res = s2.top();
                s2.pop();
            }
           
        }
        return res;
    }
private:
    stack<int> s1,s2;
};

/**
 * Your CQueue object will be instantiated and called as such:
 * CQueue* obj = new CQueue();
 * obj->appendTail(value);
 * int param_2 = obj->deleteHead();
 */
```

