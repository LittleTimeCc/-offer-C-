#### [剑指 Offer 06. 从尾到头打印链表](https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)

> 输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。



**示例 1：**

```
输入：head = [1,3,2]
输出：[2,3,1]
```

**限制：**

```
0 <= 链表长度 <= 10000
```



* ### 方法一：正序遍历，逆序返回


```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    vector<int> reversePrint(ListNode* head) {
        vector<int> res;
        while(head){
            res.push_back(head->val);
            head = head -> next;
        }
        reverse(res.begin(),res.end());
        return res;
    }
};
```



* ### 方法二：递归


```c++
class Solution {
public:
    vector<int> reversePrint(ListNode* head) {
        if(head == nullptr) return {};
        vector<int> res = reversePrint(head->next);
        res.push_back(head->val);
        return res;
    }
};
```

