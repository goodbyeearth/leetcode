# [21.Merge Two Sorted Lists](https://leetcode-cn.com/problems/merge-two-sorted-lists/)

# 思路
略

```c++
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if(l1==nullptr)
            return l2;
        if(l2==nullptr)
            return l1;
        ListNode *l, *p, *p1, *p2;
        if(l1->val<=l2->val){
            l = l1;
            p = l1;
            p1 = l1->next;
            p2 = l2;
        }
        else{
            l = l2;
            p = l2;
            p1 = l1;
            p2 = l2->next;
        }
        while(p1!=nullptr && p2!=nullptr){
            if(p1->val <= p2->val){
                p->next = p1;
                p1 = p1->next;
            }
            else{
                p->next = p2;
                p2 = p2->next;
            }
            p = p->next;
        }
        if(p1 != nullptr)
            p->next = p1;
        if(p2 != nullptr)
            p->next = p2;
        return l;
    }
};
```

# 答案
递归。
```c++
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if(l1 == nullptr) return l2;
        if(l2 == nullptr) return l1;
        if(l1->val < l2->val){
            l1->next = mergeTwoLists(l1->next, l2);
            return l1;
        }
		else{
            l2->next = mergeTwoLists(l1, l2->next);
            return l2;
        }
    }
};

作者：zhengjingwei
链接：https://leetcode-cn.com/problems/two-sum/solution/he-bing-liang-ge-you-xu-lian-biao-cti-jie-8xing-by/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```