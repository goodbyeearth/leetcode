# [102. Binary Tree Level Order Traversal](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/)

# 思路
队列

```c++
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> res;
        if(root==NULL)
            return res;
        vector<int> row;
        queue<TreeNode*> q;
        TreeNode *node, *end_node;
        
        q.push(root);
        while(!q.empty()){
            end_node = q.back();
            while(true){
                node = q.front();q.pop();
                row.push_back(node->val);
    
                if(node->left){
                    q.push(node->left);
                }
                if(node->right){
                    q.push(node->right);
                }
                if(node==end_node)
                    break;
            }         
            res.push_back(row);
            row.clear();
        }
        return res;
    }
};
```

# 别人的答案：DFS
```c++
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> res;
        pre(root,0,res);
        return res;
    }
    void pre(TreeNode *root,int depth,vector<vector<int>> &res)
    {
        if(!root) return;
        if(depth>=res.size())   //说明需要增加一层
            res.push_back(vector<int>{});
        res[depth].push_back(root->val);
        pre(root->left,depth+1,res);
        pre(root->right,depth+1,res);
    }
};
```
作者：huang-fu-mai-yan
链接：https://leetcode-cn.com/problems/two-sum/solution/er-cha-shu-ceng-ci-bian-li-c-by-huang-fu-mai-yan/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。