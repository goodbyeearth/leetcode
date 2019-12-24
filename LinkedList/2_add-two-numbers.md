# [2. add-two-numbers](https://leetcode-cn.com/problems/add-two-numbers/)

# 方法1：


```
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode *p1=l1, *p2=l2;
        ListNode *res, *p3;
        p3 = res = new ListNode(0);
        int v1, v2, v3;
        int carry = 0;   // 进位
        bool first=true;
        while(p1 || p2 || carry){
            // p1, p2 四种组合情况
            if(!p1 && p2){
                v1 = 0;
                v2 = p2->val;
            }
            else if(p1 && !p2){
                 v1 = p1->val;
                v2 = 0;
            }
            else if(p1 &&p2){
                v1 = p1->val;
                v2 = p2->val;
            }
            else{
                v1 = 0;
                v2 = 0;
            }
            // 考虑进位
            v3 = v1 + v2 + carry;
            if(v3>=10){
                carry = 1;
                v3 = v3 - 10;
            }
            else{
                carry = 0;
            }
            
            if(first){
                p3->val = v3;
                first = false;
            }
            else{
                ListNode *p=new ListNode(v3);
                p3->next  = p;
                p3 = p3->next; 
            }
            if(p1)
                p1 = p1->next; 
            if(p2)
                p2 = p2->next; 
        }
        return res;
    }
};
```