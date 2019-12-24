# [328. odd-even-linked-list](https://leetcode-cn.com/problems/odd-even-linked-list/)

# 方法1
螺旋。。
```
class Solution {
public:
    ListNode* oddEvenList(ListNode* head) {
        ListNode *head1, *head2;
        if(!head)
            return head;
        head1 = head;
        head2 = head->next;
        ListNode *p1=head1, *p2=head2, *pre_p1;
        while(p1 && p2){
            p1->next = p2->next;
            pre_p1 = p1;
            p1 = p1->next;
            if(p1){
                p2->next = p1->next;
                p2 = p2->next;
            }
        }
        if(!p1)  // 取奇链表最后一个非空节点
            p1 = pre_p1;
        p1->next = head2;
        return head1;
    }
};
```