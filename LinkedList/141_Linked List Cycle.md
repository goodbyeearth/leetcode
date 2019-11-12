# [141.Linked List Cycle](https://leetcode-cn.com/problems/linked-list-cycle/)
# 思路一
每次迭代慢指针移动一步，快指针移动两步。如果快指针触碰到 NULL 或者慢指针和快指针相等（慢被快追上，快指针比慢指针速度快一步，若有环则比追上并相等）。
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
    bool hasCycle(ListNode *head) {
        if(head==NULL || head->next==NULL)
            return false;
        ListNode *fast=head->next, *slow=head;   // fast 不设为 head 防止第一步认为 fast==slow
        while(fast!=NULL && fast->next!=NULL && fast!=slow){
            fast = fast->next->next;
            slow = slow->next;
        }
        if(fast==NULL || fast->next==NULL)
            return false;
        else
            return true;
    }
};
```
复杂度分析

时间复杂度：O(n)，让我们将 n 设为链表中结点的总数。为了分析时间复杂度，我们分别考虑下面两种情况。

链表中不存在环：
快指针将会首先到达尾部，其时间取决于列表的长度，也就是 O(n)。

链表中存在环：
我们将慢指针的移动过程划分为两个阶段：非环部分与环形部分：

慢指针在走完非环部分阶段后将进入环形部分：此时，快指针已经进入环中 迭代次数 = 非环部分长度 = N迭代次数 = 非环部分长度 = N

两个指针都在环形区域中：考虑两个在环形赛道上的运动员 - 快跑者每次移动两步而慢跑者每次只移动一步。其速度的差值为 1，因此需要经过 二者之间距离/速度差值次循环后，
快跑者可以追上慢跑者。这个距离几乎就是 "环形部分长度 K" 且速度差值为 1，我们得出这样的结论 迭代次数 = 近似于 "环形部分长度 K".

因此，在最糟糕的情形下，时间复杂度为 O(N+K)，也就是 O(n)。

空间复杂度：O(1)，我们只使用了慢指针和快指针两个结点，所以空间复杂度为 O(1)O(1)。


# 思路二
利用 set。
```c++
class Solution {
public:
    bool hasCycle(ListNode *head) {
        set<ListNode*> s;
        ListNode *p = head;
        while(p!=NULL && s.find(p)==s.end()){
            s.insert(p);
            p = p->next;
        }
        if(p==NULL)
            return false;
        else
            return true;
    }
};
```
复杂度分析

时间复杂度：O(n)，对于含有 n 个元素的链表，我们访问每个元素最多一次。添加一个结点到哈希表中只需要花费 O(1) 的时间。

空间复杂度：O(n)，空间取决于添加到哈希表中的元素数目，最多可以添加 n 个元素。

