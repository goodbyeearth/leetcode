# [160. intersection-of-two-linked-lists](https://leetcode-cn.com/problems/intersection-of-two-linked-lists/)

# 方法1
先遍历两个链表得到两个链表长度，让长的链表先走俩长度之差，再同时走。
```
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        int lenA=0, lenB=0;
        ListNode *p1=headA, *p2=headB;
        int diffLen;
        while(p1){
            lenA++;
            p1 = p1->next;
        }
        while(p2){
            lenB++;
            p2 = p2->next;
        }
        
        // p1 初始化为长的一支链表， p2 短
        if(lenA>=lenB){
            p1 = headA;
            p2 = headB;
            diffLen = lenA - lenB;
        }
        else{
            p1 = headB;
            p2 = headA;
            diffLen = lenB - lenA;
        }
        
        while(diffLen>0){
            p1 = p1->next;
            diffLen--;
        }
        while(p1){
            if(p1==p2)
                return p1;
            p1=p1->next; p2=p2->next;
        }
        return NULL;
    }
};
```

# 方法2
更快。
两个同时走，若遇到相同节点则返回 true；
若两个同时为空，则不相交。
若只有其中一个为空，将该指针置为**另一链表**的头结点，继续走。
继续重复以上操作。
（如果俩链表长度不等，则先走完的指针会先置为另一链表头结点，等到另一指针走完，该指针已走了俩长度之差的长度。此时，若俩链表有相交则必有俩指针在第二次遍历中必相遇。）
```
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode* ta = headA, * tb = headB;
        ListNode* tailA = NULL, * tailB = NULL;
        while(ta && tb){
            if(ta == tb) return ta;
            ta = ta->next;
            tb = tb->next;
            if(!ta && !tb) return NULL;
            if(!ta) ta = headB;
            if(!tb) tb = headA;
        }
        return NULL;
    }
};
```