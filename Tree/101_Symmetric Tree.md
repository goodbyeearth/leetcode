# [101.Symmetric Tree](https://leetcode.com/problems/symmetric-tree/)

# 迭代
利用栈，对根的左子树做“中左右”的入栈顺序，对根的右子树做“中右左”的入栈顺序。
对比两个栈的出栈元素，如果不相等则return false；如果都不为空，则把其左右和右左共4个子节点入栈。

# C++
```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        if(root==NULL){
            return true;
        }
        stack<TreeNode*> s_l, s_r;
        s_l.push(root);
        s_r.push(root);
        while(!s_l.empty() && !s_r.empty()){
            TreeNode *n_l = s_l.top();
            TreeNode *n_r = s_r.top();
            s_l.pop();s_r.pop();
            if(n_l == nullptr && n_r == nullptr)    // 两个均为空
                continue;
            if(n_l == nullptr || n_r == nullptr)    // 一个为空一个不空
                return false;  
            if(n_l->val != n_r->val)              // 两个都不为空，且值不相等
                return false;       
            if(n_l != NULL){
                s_l.push(n_l->left);
                s_l.push(n_l->right);
            }
            if(n_r != NULL){
                s_r.push(n_r->right);
                s_r.push(n_r->left);
            }
        }
        if(!s_l.empty() || !s_r.empty()){
            return false;
        }
        return true;
    }   
};
```

# 递归
对根的左子树按“中左右”顺序进行递归遍历，对根的右子树按“中右左”顺序进行递归遍历。把两个子树的元素存放在数组中，对比两个数组是否完全一致。

# C++
```c++
class Solution {
public:
    vector<TreeNode*> v1, v2; 
    bool isSymmetric(TreeNode* root) {
        if(root==NULL){
            return true;
        }
        TreeNode *n_l, *n_r;
        root_left_right(root->left);
        root_right_left(root->right);
        if(v1.size() != v2.size())
            return false;
        for(int i=0;i<v1.size();i++){
            if(v1[i] == nullptr && v2[i]  == nullptr)    // 两个均为空
                continue;
            if(v1[i]  == nullptr || v2[i]  == nullptr)    // 一个为空一个不空
                return false;  
            if(v1[i]->val != v2[i]->val)              // 两个都不为空，且值不相等
                return false;       
        }
        return true; 
    }  
    
    void root_left_right(TreeNode* root){
        v1.push_back(root);
        if(root != nullptr){
            root_left_right(root->left);
            root_left_right(root->right);
        }        
    }
    
    void root_right_left(TreeNode* root){
        v2.push_back(root);
        if(root != nullptr){
            root_right_left(root->right);
            root_right_left(root->left);
        } 
    }
};
```

# 答案1
```c++
class Solution {
public:
    bool ismirror(TreeNode* left,TreeNode* right)
    {
        
        if(left==NULL&&right==NULL) return true;
        if(right==NULL||left==NULL) return false;
        
        return (left->val==right->val)&&ismirror(left->left,right->right)&&ismirror(left->right,right->left);
        
    }
    bool isSymmetric(TreeNode* root) {
        return ismirror(root,root);
    }
};
```
# 答案2
```c++
class Solution {
public:
    
    bool isSymmetric(TreeNode* root) {
         queue<TreeNode*> q;
        q.push(root);
        q.push(root);
        while (!q.empty())
        {
            TreeNode* t1 = q.front();
            q.pop();
            TreeNode* t2 = q.front();
            q.pop();
            if (t1 == NULL && t2 == NULL) continue;
            if (t1 == NULL || t2 == NULL) return false;
            if (t1->val != t2->val) return false;
            q.push(t1->left);
            q.push(t2->right);
            q.push(t1->right);
            q.push(t2->left);
        }
        return true;
    }
};
static const auto io_speed_up=[]{
    ios::sync_with_stdio(false);
    cin.tie();
    return 0;
}();
```
