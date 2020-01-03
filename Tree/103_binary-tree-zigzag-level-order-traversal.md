# [103. 二叉树的锯齿形层次遍历] (https://leetcode-cn.com/problems/binary-tree-zigzag-level-order-traversal/)

#方法1：
利用两个栈。


```
class Solution {
public:
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        stack<TreeNode*> s1, s2;
        vector<vector<int>> res;
        vector<int> row;
        TreeNode *p;
        bool fromLeft = true;
        if(root)
            s1.push(root);
        else
            return res;
        while(!s1.empty() || !s2.empty()){
            row.clear();
           while(fromLeft && !s1.empty()){
                p = s1.top(); s1.pop();
               row.push_back(p->val);
                if(p->left)
                    s2.push(p->left);
                if(p->right)
                    s2.push(p->right);
            }
            while(!fromLeft && !s2.empty()){
                p = s2.top(); s2.pop();
                row.push_back(p->val);
                if(p->right)
                    s1.push(p->right);
                if(p->left)
                    s1.push(p->left);       
            }
            res.push_back(row);
            fromLeft = !fromLeft;
        }
        return res;
    }
};
```