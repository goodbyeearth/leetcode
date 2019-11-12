# [234.Palindrome Linked List](https://leetcode-cn.com/problems/palindrome-linked-list/)

# 思路
先转置前半条链表，然后对两半链条按顺序遍历，对比各自的元素。

```c++
class Solution {
public:
    bool isPalindrome(ListNode* head) {
        ListNode *p=head, *head1, *head2;
        int len=0;
        if(head==nullptr || head->next==nullptr)
            return true;
        while(p!=nullptr){
            len++;
            p = p->next;
        }
        p = head;
        ListNode *q=nullptr, *next_p;
        for(int i=0;i<len/2;i++){
            next_p = p->next;
            p->next = q;
            q = p;
            p = next_p;
        }
        head1 = q;
        head2 = p;
        if(len%2==1)
            head2 = head2->next;
        while(head1!=nullptr){
            if(head1->val!=head2->val)
                return false;
            head1 = head1->next;
            head2 = head2->next;
        }
        return true;
    }
};
```