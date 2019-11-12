# [206.Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)

# 方法1：迭代
头插入法。

# C++
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
    ListNode* reverseList(ListNode* head) {
        if(!head)
            return NULL;
        ListNode *p=head->next, *q;
        head->next = NULL;
        while(p){
            q = p->next;
            p->next = head;
            head = p;
            p = q;
        }
        return head;
    }
};
```

# 方法2：递归
递归：翻转第二个节点以后的子链，返回翻转后的tail,将tail的next指向第一个节点，把第一个节点的next置空，返回该节点。

# C++
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
    ListNode* reverseList(ListNode* head) {
        if(!head || !head->next)
            return head;
        ListNode* tail = head;
        while(tail->next){
            tail = tail->next;
        }
        ListNode *r_tail = reverse(head);
        return tail;
    }
    ListNode* reverse(ListNode* head){      
        if(!head->next){      // 只剩一个元素
            return head;
        }
        ListNode *subListHead = head->next;
        ListNode *r_subListTail;   // 翻转后的子链的尾
        r_subListTail = reverse(subListHead);
        r_subListTail->next = head;
        head->next=NULL;
        return head;
    }
};
```

# 别人的答案

## 思路
遍历链表，cur为变量当前结点，pre为其前驱结点，r后其后继结点。让cur结点的next域指向pre结点，
注意到一旦调整指针指向后，cur的后继结点就会断开，为此需要用r来指向原cur的后继节点。

## C++
```c++
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode *pre = nullptr, *cur = head, *r = nullptr;
        while (cur != nullptr) {
            r = cur->next;
            cur->next = pre;
            pre = cur;
            cur = r;
        }
        return pre;
    }
};